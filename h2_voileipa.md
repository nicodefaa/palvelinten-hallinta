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

- Lopuksi testataan: *ssh antero@localhost* -> *sudo -k* -> sudo echo "testi" -> Ei kysy salasanaa komentoa varten

---
