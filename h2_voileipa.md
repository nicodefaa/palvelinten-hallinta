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

<img width="632" height="221" alt="kuva" src="https://github.com/user-attachments/assets/d0ad6bb3-d6d1-47dc-9cba-f84915a5cc63" />

*Julkinen avain on turvallista jakaa, mutta peitin sen itse kuvasta koska olen vainoharhainen* 😅



*En aluksi muistanut lisätä omaa käyttäjääni sudoless-ryhmään, jolloin tuli seuraava virhe:*

<img width="896" height="490" alt="kuva" src="https://github.com/user-attachments/assets/2f2ac577-16e7-4063-862c-7c098492b783" />
