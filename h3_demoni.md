# h3 Demoni (Daemon)

## Apachen asennus Ansiblella

- Käytetään **package**-moduulia asentamaan apache2. Komento: *sudo apt-get install apache2*
- Käytetään **file**-moduulia kopioimaan ja hallitsemaan asetustiedostoja. Komento: *sudoedit /etc/apache2/...*
- Käytetään **service**-moduulia (uudelleen)käynnistämään palvelu. Komento: *sudo systemctl restart apache2*
- Luodaan rooli apache2 ja jaetaan se kolmeen osaan:
  - **files**: valmiit konfiguraatiotiedostot, esim *files/example.com.conf*
  - **handlers**: palvelun uudelleenkäynnistys pyydettäessä
  - **tasks**: päätoimintojen suoritus, asentaa apachen, kopio conf-tiedoston palvelimelle ja luo linkin sites-enabled-hakemistoon¨
- Lopputuloksena Apache näyttää uudelleenkäynnistyksen jälkeen localhost web-sivun.

Lähde: [Apache installed with Ansible - quick notes](https://terokarvinen.com/apache-ansible/)

## Handlerien suoritus ja notify

- Handlerin tehtävät suoritetaan ainoastaan jos niille annetaan ilmoitus/notifointi (notify)
- Tämä mahdollistaa ominaisuuden jossa palvelu voidaan uudelleenkäynnistää automaattisesti vain tilanteissa joissa on tehty muutoksia
- Jos muutoksia ei tapahtu suorituksessa, ei myöskään uudelleenkäynnistystä tapahdu
- Yksi tehtävä (task) voi määrätä useampaa handleria suoriutumaan
- Handlerit suoritetaan siinä järjestyksessä jossa ne ovat listattu handlers-osiossa (handlers/main.yml), ei tasks-osion notify-listan järjestyksessä

Lähde: [Handlers: running operations on change](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html)

## Ansible-doc service

- Johdanto: Service-moduuli hallitsee palveluita etäkoneilla. Tämä toimii välittäjänä taustalla toimivalle palvelunhallintamoduulille, ja kaikki moduulit eivät välttämättä tue samoja argumentteja.
- **enabled**: määrittää käynnistyykö palvelu systeemin käynnistyksen yhteydessä. boolean-arvo eli *true/false*. Vähintään toinen, *state*- tai *enabled*-määritys vaaditaan aina.
- **name**: palvelun nimi johon tehtävä kohdistetaan
- **state**: palvelun "tila", joka määrittää mitä palvelulle tehdään. *started/stopped* ovat idempotentteja, eli tekevät toiminnon vain jos ei ole jo tosi. *restarted* käynnistää aina uudelleen riippumatta nykytilasta. *reloaded* on kevyempi vaihtoehto restartille, jossa ladataan uudelleen vain asetukset (ei välttämättä ole vaihtoehto kaikissa palveluissa). Vähintään toinen, *state*- tai *enabled*-määritys vaaditaan aina.
- **EXAMPLES**:
<img width="366" height="311" alt="kuva" src="https://github.com/user-attachments/assets/ccabb803-b8bd-4591-9a99-8a99ad5ecad7" />

Esimerkkejä ansible-doc service -sivulta
1. käynnistää palvelun jos ei ole jo käynnissä.
2. pysäyttää palvelun jos on käynnissä.
3. uudelleenkäynnistää palvelun aina jos käynnissä, käynnistää jos ei ole käynnissä.
4. lataa palvelun asetukset aina uudelleen
5. laittaa palvelun päälle niin, että se käynnistyy systeemin yhteydessä, mutta ei vaikuta tämän hetkiseen päälläoloon.

Lähde: [ansible.builtin.service module – Manage services](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/service_module.html) + *ansible-doc service* -komento

### Omia mietteitä
Paljon uusia termejä joiden osuvat suomennokset alkavat olla haastavia keksiä, mutta tuntuu myös että suomentamalla ohjeet oppii samalla sisäistämään asian paremmin.
Onko oikeasti väliä käytetäänkö "sudo apt-get update" vai "sudo apt update", kun molemmat tekevät päällisin puolin saman asian?

## a) Apassi - Apache2:n asennus manuaalisesti

<img width="601" height="174" alt="kuva" src="https://github.com/user-attachments/assets/581aad95-a4e0-4f04-b277-16b102d2c5a8" />

*Apachen asennus "sudo apt install apache2" ja statuksen tarkistus "systemctl status apache2". On päällä ja enabloitu.*

<img width="577" height="71" alt="kuva" src="https://github.com/user-attachments/assets/65fe3a27-2be9-4ca5-8c7f-7675327d448b" />

*"echo "teksti" > tiedostopolku" komentoformaatti nopeampi vaihtoehto microlle simppeliin testitekstiin.*

<img width="560" height="141" alt="kuva" src="https://github.com/user-attachments/assets/43203951-509b-4bdc-abc7-1cb55d939a5d" />

*Apachen conf-asetustiedoston luonti.*

<img width="676" height="264" alt="kuva" src="https://github.com/user-attachments/assets/a4333322-839a-4173-be92-34493efbb968" />

*"a2ensite"-komento ottaa sivuston käyttöön eli tekee kohdetiedostoon symbolisen linkin /etc/apache2/sites-available -hakemistoon. "a2disssite" poistaa sivuston käytöstä eli poistaa symbolisen linkin kohdetiedostoon sites-enabled -hakemistosta.*



## b) Moottorix - Nginx:n asennus manuaalisesti

## c) Automoottorix - Nginx: asennus Ansiblella

## d) Vapaaehtoinen bonus
