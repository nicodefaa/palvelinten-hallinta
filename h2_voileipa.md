# h2 Voileipä

## Salasanattoman sudo-käyttäjän luonti

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

<img width="437" height="55" alt="kuva" src="https://github.com/user-attachments/assets/ab9bf261-993c-4638-8111-285652e1f9bd" />
<img width="632" height="221" alt="kuva" src="https://github.com/user-attachments/assets/d0ad6bb3-d6d1-47dc-9cba-f84915a5cc63" />

