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

*rsyslogin status. Käynnissä ja enabloituna*

<img width="784" height="145" alt="kuva" src="https://github.com/user-attachments/assets/ce12de09-c523-47b9-98a2-0ec2eb378886" />

*Suoritin testin, jossa kirjoitin logiin oman lisäyksen komennolla logger **"rsyslog testi"**, ja tämän jälkeen printtasin login viimeiset 3 riviä komennolla **tail -n 3 /var/log/syslog**. tail printtaa oletuksena tiedoston viimeiset 10 riviä, ja -n parametrillä voidaan valita oma haluttu määrä rivejä.*

<img width="589" height="57" alt="kuva" src="https://github.com/user-attachments/assets/e5573937-4490-4bc3-8074-6b28f673a1df" />

*Tein muutoksen konfiguraatioon kuvassa näkyvin komennoin. `*.* /var/log/test.log` **test.conf**-tiedostossa kertoo rsyslogille, että kaikki logiviestit tulee viedä **test.log**-tiedostoon.*

<img width="674" height="66" alt="kuva" src="https://github.com/user-attachments/assets/5a783e9c-6073-45f9-a359-dae85601485b" />

*Tämän jälkeen uusi testisyöte tallentui **test.log**-tiedostoon (kaikkien muiden automaattisten logiviestien ohella).*


## b) Automaatti / Daemonin asennus Ansiblella

## c) Asetus / Asetustiedoston muuttaminen

## d) Paikka remonttiin / Asetusten rikkominen, ja korjaus Ansiblella

## e) Idempotetti
