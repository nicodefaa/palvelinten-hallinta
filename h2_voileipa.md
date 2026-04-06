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


### a)

<img width="632" height="221" alt="kuva" src="https://github.com/user-attachments/assets/d0ad6bb3-d6d1-47dc-9cba-f84915a5cc63" />

*Julkinen avain on turvallista jakaa, mutta peitin sen itse kuvasta koska foliohattu* 😅

### b)

<img width="430" height="142" alt="kuva" src="https://github.com/user-attachments/assets/765b4d9d-38be-44e1-bdde-bb8be1abfde9" />

*Tehtävässä a luotu antero kirjautuu suoraan ilman salasanaa*

### c)

<img width="168" height="116" alt="kuva" src="https://github.com/user-attachments/assets/96c82798-2ed4-439a-b20c-ef2596daa35b" />



<img width="278" height="141" alt="kuva" src="https://github.com/user-attachments/assets/1ea4af7e-eed0-4618-a0e3-53c4287b145d" />

*roles/package/tasks/main.yml*

<img width="289" height="216" alt="kuva" src="https://github.com/user-attachments/assets/c95989d3-3dc9-4079-b872-0f4d98a7707e" />

*Ansiblen hakemistopuu tässä vaiheessa*

