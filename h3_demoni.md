# h3 Demoni

## Apachen asennus Ansiblella

- Käytetään *package*-komentoa asentamaan apache2 "sudo apt-get install apache2"
- Käytetään *file*-komentoa kopioimaan ja hallitsemaan asetustiedostoja "sudoedit /etc/apache2/..."
- Käytetään *service*-komentoa (uudelleen)käynnistämään palvelu "sudo systemctl restart apache2"
- Luodaan rooli apache2 ja jaetaan se kolmeen osaan: *files*, *handlers* ja *tasks*.
