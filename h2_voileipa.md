# h2 Voileipä

## Salasanattoman sudo-käyttäjän luonti (manuaalisesti)

- Luodaan uusi käyttäjä komenolla: *sudo adduser antero*
- Luodaan uusi ryhmä komennolla: *sudo groupadd sudoless*
- Lisätään uusi käyttäjä uuteen ryhmään komennolla: *sudo adduser antero sudoless*
- Luodaan uusi tiedosto sudo-asetuksille: *sudo visudo /etc/sudoers.d/sudoless*
- Lisätään sinne: *%sudoless ALL = (ALL) NOPASSWD: ALL*

Rivin selitys:

%sudoless = tämä ryhmä

ALL = kaikki koneet

(ALL) = voi toimia kaikkina käyttäjinä

NOPASSWD = ei kysy salasanaa

ALL = saa suorittaa kaikkia komentoja

- Lopuksi testataan: *ssh antero@localhost* -> *sudo -k* -> sudo echo "testi" -> Ei kysy salasanaa komentoa varten 👌

Lähde: [Sudo without password](https://terokarvinen.com/passwordless-sudo/)

---

## Salasanaton sudo-käyttäjä Ansiblella

- Lisätään uusi rooli ja sen alle oma */tasks/main.yml*
- Lisätään sinne ryhmän luonti, käyttäjän luonti, SSH-avaimen lisäys ja NOPASSWD-asetus
- Lisätään uusi rooli myös *site.yml*:n listaan
- Tarkempi rakenne tehtävän a screenshotissa alla

Lähde: [Passwordless Sudo with Ansible](https://terokarvinen.com/passwordless-sudo-with-ansible/)

## Ansible-doc 
### ansible-doc copy
content - kirjoittaa tekstisisällön tiedostoon
dest - kohdetiedosto ja -polku johon kopioidaan
src - lähdetiedosto joka kopioidaan
owner & group - ryhmä ja omistaja joka tulee olemaan kohteella
mode - oikeudet jotka tulee olemaan kohteella, esim 0600 tai 0744

### ansible-doc apt
name - paketin nimi, voi olla useampia
state - "tila" asennettu/poistettu (present/absent)
update_cache - ajaa komennon "apt-get update" eli päivittää "pakettivaraston"

### ansible-doc file
path - tiedostopolku muokattavaan tiedostoon
recurse - "true" asettaa asetukset myös alikansioihin
src - käytetään liittämään linkki johonkin tiedostoon
state - vaihtoehtoina esim absent, joka poistaa ja directory joka luo kansion
owner, group, mode - omistaja, ryhmä ja oikeudet

### ansible-doc user
name - käyttäjänimi
create_home - "true" luo käyttäjälle kotihakemiston (yleensä oletus), "false" ei luo
comment - vapaa kuvaus
groups - ryhmä(t) joihin luotava käyttäjä tulee kuulumaan
shell - komentotulkki (esim. /bin/bash)
state - present/absent luo tai poistaa
system - järjestelmäkäyttäjän luontia varten

## ansible-doc authorized_key
user - käyttäjä jolle SSH-avain lisätään
key - SSH-avain joka lisätään (julkinen avain)

### a) Sudoless tunnus ansiblella

<img width="632" height="221" alt="kuva" src="https://github.com/user-attachments/assets/d0ad6bb3-d6d1-47dc-9cba-f84915a5cc63" />

*Julkinen avain on turvallista jakaa, mutta peitin sen itse kuvasta koska foliohattu* 😅

### b) Anteron salasanaton SSH kirjautuminen

<img width="430" height="142" alt="kuva" src="https://github.com/user-attachments/assets/765b4d9d-38be-44e1-bdde-bb8be1abfde9" />

*Tehtävässä a luotu antero kirjautuu suoraan ilman salasanaa*

### c) Pakettien asennus

<img width="278" height="141" alt="kuva" src="https://github.com/user-attachments/assets/1ea4af7e-eed0-4618-a0e3-53c4287b145d" />

*roles/package/tasks/main.yml asetettu asentamaan 3 pakettia. update_cache: yes = apt-get update*

<img width="168" height="116" alt="kuva" src="https://github.com/user-attachments/assets/96c82798-2ed4-439a-b20c-ef2596daa35b" />

*roolin suoritus lisätty site.yml*

<img width="289" height="216" alt="kuva" src="https://github.com/user-attachments/assets/c95989d3-3dc9-4079-b872-0f4d98a7707e" />

*Ansiblen hakemistopuu tässä vaiheessa*

### d) tiedoston luonti

<img width="315" height="157" alt="kuva" src="https://github.com/user-attachments/assets/7b2497c9-aeaa-4d9c-b688-1b4ab69d02b3" />

*/roles/file/tasks/main.yml*

*| = mahdollistaa useamman rivin kirjoittamisen tiedostoon (kokeilin ilman ja lopputuloksena kaikki teksti oli samalla rivillä)*

*0600 = - rw- --- --- (jaoteltu selkeyden vuoksi) = omistajalla luku- (r/4) ja kirjoitus- (w/2) oikeudet, ryhmällä ja muilla ei mitään*

<img width="310" height="105" alt="kuva" src="https://github.com/user-attachments/assets/72dc0987-219e-430f-a62c-dbc92cec8490" />

*roolin suoritus lisätty site.yml playbookiin*

### e) Jotain muuta - palvelun käynnistys (service)

<img width="332" height="89" alt="kuva" src="https://github.com/user-attachments/assets/755b4e9b-911d-46b8-8761-2f04b51f61e2" />

*roles/service/tasks/main.yml sisältö. Lisäsin "- service" site.yml playbookiin samaan tapaan kuin muut aikaisemmissa tehtävissä*

<img width="578" height="262" alt="kuva" src="https://github.com/user-attachments/assets/bce42b1c-6dd3-4f2f-8107-a370bea05e57" />

*Poistin cron-palvelun käytöstä playbookin suorituksen testaamista varten*

<img width="638" height="173" alt="kuva" src="https://github.com/user-attachments/assets/d3a132aa-f3a2-4810-91c0-91a40bcfab6f" />

*Playbookin suorituksen jälkeen cron-palvelu meni takaisin päälle. Tämän jälkeen playbookin uudessa suorituksessa tuloksena ok=9 changed=0, koska kaikki ehdot olivat jo toteutettuna.*
