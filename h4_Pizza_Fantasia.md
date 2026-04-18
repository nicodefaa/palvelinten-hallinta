# h4 Pizza Fantasia

## Tiivistelmät:

## 4.12.1 Size and Complexity of Some DSLs (112. Ominaisuuksien määrä.)
- **Salt DSL**:ssä n. **510 state-funktiota**, joiden dokumentaatio sisältää yli 75000 sanaa. Ohjausrakenteet(if,else) tehdään käyttäen Jinja2-mallipohjaa YAML-koodin kirjoittamiseen, joka taas muunnetaan Python-rakenteeksi suorittamista varten.
- **Puppet DSL**:ssä n. **113 funktiota**, ja käyttää niihin omia konsepteja, kuten virtuaalisia resursseja (virtual resources), tavallisten ohjelmointirakenteiden sijaan.

## 4.12.2 Use of DSL Functions in Case Configuration (112-115. Mitä oikeasti käytetään.)
- Vaikka DSL-kielissä on paljon funktioita, niin käytännössä niistä käytetään yleensä vain pientä osaa, kuten *package-file-service*-malli damoenien asennukseen ja konfigurointiin, ja *package-file*-malli client-ohjelmiin.
- Mozilla-esimerkissä yleisimmmät funktiot, joita käytetään ovat *file*, *package*, *exec* ja *service*, yhteensä n. 38% kaikista käytetyistä komennoista. Ohjausrakenteista(control structures) käytetyimmät ovat *cae* ja *if*, yhteensä 23%.

## 4.12.3.1 Dependencies Between Main Functions (115-117. Tärkeimmät rakennuspalikat.)
- Yleisimmät funktiot ovat *package-file-serivce*, *user*, *group* ja *exec*.
- Konfiguraatiot perustuvat usein muutamaan perusmalliin, kuten *package-file-service* daemoneille, *package-file* sovelluksille (app), *user-group* käyttäjähallintaan (user management), ja *file-directory-symlink* tiedostojen hallintaan (file manipulation).
- Suurin osa funktioista kutsuu järjestelmän natiiveja komentoja, kuten *apt-get*.
- Systeemi tulee pyrkiä olemaan *idempotentti*, eli muutoksia tehdään suorittaessa vain silloin, jos ehdot eivät jo täyty. Jos järjestelmä on jo halutussa tilassa, voidaan hallintatyökalua ajaa uudelleen ilman, että se muuttaa mitään.
- Kaksi yleisintä funktiota: *file*, joka on helppo tehdä idempotentiksi, ja *exec*, joka vaihtelee kutsuttavan ohjelman mukaan.

Jos vain pientä osaa ominaisuuksista käytetään käytännössä, onko järkevää DSL:n sisältää oletuksena satoja muita joita käytetään vain erittäin harvoin? Onko niitä joskus ennen tarvittu enemmän?

Lähde: [Configuration Management of Distributed Systems over Unreliable and Hostile Networks. Karvinen, Tero 2024.](https://westminsterresearch.westminster.ac.uk/item/w7vvz/configuration-management-of-distributed-systems-over-unreliable-and-hostile-networks)


## a) Räpylä / Daemonin asennus käsin

Valitsin tähän tehtävään **rsyslog**-daemonin, joka 

Aloitin asentamalla rsyslog:in komennoilla *sudo apt update* ja *sudo apt install rsyslog*.

<img width="699" height="281" alt="kuva" src="https://github.com/user-attachments/assets/dfcbd8da-9f71-4a94-bf49-4870c5338c9b" />

rsyslogin status. Käynnissä ja enabloituna

<img width="784" height="145" alt="kuva" src="https://github.com/user-attachments/assets/ce12de09-c523-47b9-98a2-0ec2eb378886" />

Suoritin testin, jossa kirjoitin logiin oman lisäyksen komennolla logger **"rsyslog testi"**, ja tämän jälkeen printtasin login viimeiset 3 riviä komennolla **tail -n 3 /var/log/syslog**. tail printtaa oletuksena tiedoston viimeiset 10 riviä, ja -n parametrillä voidaan valita oma haluttu määrä rivejä.

<img width="589" height="57" alt="kuva" src="https://github.com/user-attachments/assets/e5573937-4490-4bc3-8074-6b28f673a1df" />

Tein muutoksen konfiguraatioon kuvassa näkyvin komennoin. `*.* /var/log/test.log` **test.conf**-tiedostossa kertoo rsyslogille, että kaikki logiviestit tulee viedä **test.log**-tiedostoon.

<img width="674" height="66" alt="kuva" src="https://github.com/user-attachments/assets/5a783e9c-6073-45f9-a359-dae85601485b" />

Tämän jälkeen tekemäni uusi testisyöte tallentui **test.log**-tiedostoon (kaikkien muiden automaattisten logiviestien ohella).

## b) Automaatti / Daemonin asennus Ansiblella

<img width="656" height="458" alt="kuva" src="https://github.com/user-attachments/assets/0d9e57c6-0a38-457c-ac9c-5f401d48f980" />

Loin rsyslogille omat task- ja handlers-hakemistot, sekä task:n alle main.yml tiedoston johon kirjoitin yllä kuvassa näkyvän tekstin. Toiminto asentaa rsyslogin, tarkistaa että se on käynnissä ja enabloituna, sekä luo konfiguraatio-tiedoston uutta logitiedostoa varten samaan tapaan kuin tein manuaalisesti tehtävässä a. Lopuksi kutsutaan vielä handleria käynnistämään rsyslog uudelleen mikäli muutoksia tehdään.

<img width="687" height="115" alt="kuva" src="https://github.com/user-attachments/assets/cd082832-5539-4dc1-93f5-b72e7a6705d7" />

Handler, joka uudelleenkäynnistää rsyslog:in kutsuttaessa.

<img width="196" height="219" alt="kuva" src="https://github.com/user-attachments/assets/957cc9d2-abbf-424d-99a3-3f31ff0ba1bb" />

Lopuksi vielä rsyslog-roolin lisäys site.yml-playbookiin, jotta se ajetaan. Kommentoin muut roolit ulos testin ajaksi, jotta suoritus on hieman nopeampaa ja tekstiä tulee ruudulle vähemmän. shift + alt + ylä/alanuoli = multicursor.

<img width="632" height="374" alt="kuva" src="https://github.com/user-attachments/assets/3b143189-9b04-41c2-8588-ecf72231a353" />

Playbook ajoi ilman virheitä (=hyvä), mutta muutoksia ei vielä tullut, koska olin ne jo tehnyt manuaalisesti tehtävässä a. (Jatkuu alla tehtävässä c.)

## c) Asetus / Asetustiedoston muuttaminen

<img width="505" height="275" alt="kuva" src="https://github.com/user-attachments/assets/e7b9124b-437e-48fa-a689-4f1c506b4c8d" />

Muunsin roles/rsyslog/tasks/main.yml -tiedoston content-kohtaa, niin että se ohjaa ainoastaan user-facilityn ("luokan") lokiviestit test.log-tiedostoon.

<img width="1024" height="342" alt="kuva" src="https://github.com/user-attachments/assets/888800c5-128b-4cc2-9340-639aed72df42" />

Tällä kertaa playbookia ajaessa sain error-viestin, jossa kerrottiin että kutsuttavaa "restart syslog" handleria ei löydy. Tässä kohtaa tajusin heti, että virhe johtui typosta (r puuttui), sillä kutsuttavan handlerin ja itse handlerin nimen tulee olla täysin identtiset. Korjasin virheen roles/syslog/tasks/main.yml -tiedostosta, jonka jälkeen playbook ajoi ilman virheitä.

<img width="622" height="58" alt="kuva" src="https://github.com/user-attachments/assets/31dad703-0d65-46eb-bad3-9afc73208862" />

Muutokset kuitenkin tehtiin vaikka ansible ei virheen takia siitä antanutkaan lopullista ilmoitusta (koska seuraavassa ajossa tuli edelleen ok=4, changed=0), joten jouduin vielä muuttamaan manuaalisesti test.conf-tiedoston ajoa edeltävään tilaan.

<img width="1144" height="223" alt="kuva" src="https://github.com/user-attachments/assets/324f5387-6b9d-41f2-9779-5d8025d0101c" />

Tämän jälkeen playbookia ajaessa tuli changed=2, eli conf-tiedoston muutos ja restart. (Ja seuraavassa taas changed=0 eli on idempotentti)

<img width="614" height="98" alt="kuva" src="https://github.com/user-attachments/assets/a6035d65-565a-48ab-a393-b2f0d2fc2974" />

*test.conf-tiedoston sisältö muuttui ansiblen toimesta.*

## d) Paikka remonttiin / Asetusten rikkominen, ja korjaus Ansiblella

## e) Idempotetti
