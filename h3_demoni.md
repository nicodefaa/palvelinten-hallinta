# h3 Demoni (Daemon)

## Apachen asennus Ansiblella

- Käytetään **package**-mallia asentamaan apache2. Komento: *sudo apt-get install apache2*
- Käytetään **file**-mallia kopioimaan ja hallitsemaan asetustiedostoja. Komento: *sudoedit /etc/apache2/...*
- Käytetään **service**-mallia (uudelleen)käynnistämään palvelu. Komento: *sudo systemctl restart apache2*
- Luodaan rooli apache2 ja jaetaan se kolmeen osaan:
  - **files**: valmiit konfiguraatiotiedostot, esim *files/example.com.conf*
  - **handlers**: palvelun uudelleenkäynnistys
  - **tasks**: päätoimintojen suoritus, asentaa apachen, kopio conf-tiedoston palvelimelle ja luo linkin sites-enabled-hakemistoon¨
- Lopputuloksena Apache näyttää uudelleenkäynnistyksen jälkeen http://localhost web-sivun.

Lähde: (Apache installed with Ansible - quick notes)[https://terokarvinen.com/apache-ansible/]

## Handlerien suoritus ja notify

- Handlerin tehtävät suoritetaan ainoastaan jos niille annetaan ilmoitus (notify)
- Tämä mahdollistaa ominaisuuden jossa palvelu voidaan uudelleenkäynnistää automaattisesti vain tilanteissa joissa on tehty muutoksia
- Jos muutoksia ei tapahtu suorituksessa, ei myöskään uudelleenkäynnistystä tapahdu

Lähde: (Handlers: running operations on change)[https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html]
