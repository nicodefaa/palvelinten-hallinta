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

Jos vain pientä osaa ominaisuuksista käytetään käytännössä, onko järkevää DSL:n sisältää oletuksena satoja muita joita käytetään vain erittäin harvoin? Onko niitä joskus ennen tarvittu enemmän?

Lähde: [Configuration Management of Distributed Systems over Unreliable and Hostile Networks. Karvinen, Tero 2024.](https://westminsterresearch.westminster.ac.uk/item/w7vvz/configuration-management-of-distributed-systems-over-unreliable-and-hostile-networks)


## a) Räpylä / Daemonin asennus käsin

## b) Automaatti / Daemonin asennus Ansiblella

## c) Asetus / Asetustiedoston muuttaminen

## d) Paikka remonttiin / Asetusten rikkominen, ja korjaus Ansiblella

## e) Idempotetti
