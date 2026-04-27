# h5 Gitar Hero

## x) Tiivistelmä: 1.3 Getting Started - What is Git?

- Git tallentaa projektin tilan snapshotteina jokaisen commitin yhteydessä.
- Lähes kaikki Git:in toiminnot toimivat paikallisesti ilman verkkoa.
- **Commit** tallentaa projektin tilan paikallisesti ja **Push** vie projektin verkon yli valittuun online repositoryyn.
- Vanhaa dataa ei yleensä poisteta, vaan muutettu data lisätään vanhan päälle, jonka ansiosta kertaalleen commitattu data on turvallisesti tallessa.
- Muuttamatonta tiedostoa ei tallennetta uudelleen, vaan lisätään vain viittaus vanhaan versioon.

Lähde: Chacon & Straub 2014.

### git add --all && git commit; git pull && git push -komennon selitys:

`git add --all` = lisää kaikki muutokset staging-alueelle.
`&&` = suorittaa seuraavan komennon, jos edellinen onnistui.
`git commit` = tallentaa staging-alueella olevat muutokset paikallisesti.
`;` = suorittaa seuraavan komennon riippumatta siitä, onnistuiko edellinen.
`git pull` = hakee muutokset online reposta ja yhdistää ne paikalliseen versioon.
`git push` = vie paikalliset commitatut muutokset online repoon.

Lähde: Git.

## a) Online --- GitHub varaston luonti

Loin tehtävää varten uuden repon tänne githubiin ja nimesin sen "sunshine":ksi vaatimuksen mukaan.

Pistin päälle option, joka loi repoon README-tiedoston, sekä valitsin lisenssiksi GPL-3.0:n, joka loi lisäksi LICENSE-tiedoston.

<img width="630" height="571" alt="kuva" src="https://github.com/user-attachments/assets/3a61d9a6-8c09-4605-8b70-0ce36d012d19" />

*Repon luonti*
<br>

## b) Dolly --- Repon kloonaus ja testimuutoksia

Kloonasin äsken tekemäni sunshine-repon käyttämällä komentoa `git clone [repon URL]`.

Kloonauksen jälkeen kotihakemistoon tuli hakemisto "sunshine", ja sisältä löytyivät kopioituna GitHubissakin näkyvät **LICENSE** ja **README.md**.

<img width="1065" height="223" alt="kuva" src="https://github.com/user-attachments/assets/21e8c69a-f162-41a8-8ca9-1ac3b5dfd66a" />

*Kloonattu repo kotihakemistossa*
<br>

Seuraavana tein pari muutosta; 

ensin lisäsin README.md-tiedostoon uuden kommentin, ja sitten loin vielä kokonaan uuden tekstitiedoston:

<img width="700" height="208" alt="kuva" src="https://github.com/user-attachments/assets/059ac968-3b61-4cdb-943e-93fd42553f0b" />

*Muutosten teko Debianissa*
<br>

Käytin komentoa `git add --all` lisäämään kaikki muutokset staging-alueelle valmiiksi commit:ia varten.

Käytin komentoa `git commit -m "viesti"` committaamaan muutokset. Tämä ensimmäinen commit keskeytyi ja tuli pyyntö lisätä konfiguraatioon käyttäjänimi ja sähköposti.

<img width="1106" height="293" alt="kuva" src="https://github.com/user-attachments/assets/5553da9d-f1dc-454c-9ac0-6355f11bc3a3" />

*add ja ensimmäinen commit yritys*
<br>

Lisäsin pyydetyt tiedot annetuilla komennoilla `git config --global user.name` \ `user.email`, jonka jälkeen tein commitin uudelleen:

<img width="1104" height="131" alt="kuva" src="https://github.com/user-attachments/assets/7a3edc71-7967-4b3e-92fa-816fe73b0ee6" />

*käyttäjäkonfiguraatio (email peitetty) ja uusi commit*
<br>

Ensimmäisen kerran kun yritin viedä muutokset komennolla `git push`, kysyttiin github tunnuksia, koska en ollut tällä koneella vielä yhdistänyt SSH-avainta GitHubiini. Peruin pushauksen ja kävin viemässä public-avaimeni ~/.ssh/id_ed25519.pub -tiedostosta Githubin asetuksiin SSH and GPG keys, jonka jälkeen yritin pushia uudelleen. Tällä kertaa push onnistui ilman tunnuksia ja tehdyt muutokset tulivat näkyviin githubissa.

<img width="459" height="137" alt="kuva" src="https://github.com/user-attachments/assets/eedfb21e-2b29-4001-bc17-686d5cc5d505" />

*Push meni läpi*
<br>

<img width="919" height="313" alt="kuva" src="https://github.com/user-attachments/assets/493ff62f-a796-4a34-82d7-c79a478a850c" />

*Testikommentti README.md:ssä Githubissa*
<br>

<img width="505" height="202" alt="kuva" src="https://github.com/user-attachments/assets/1020080a-eb53-429a-a045-c68c7e775cb0" />

*Uusi lisätty shiningsun.txt-tiedosto Githubissa*
<br>

## c) Doh! --- "Tyhmä" muutos ja resetti

Tehtävänanto pyysi tekemään "tyhmän" muutoksen, joten käytin echo-komentoa ylikirjoittamaan README.md-tiedoston tekstin uudella `echo "hups! > README.md`. Tuloksena kaikki aiempi README:ssä oleva teksti tuhoutui ja tilalla oli ainoastaan uusi teksti.

<img width="639" height="79" alt="kuva" src="https://github.com/user-attachments/assets/76365655-1e3e-471f-baf1-eda935f5079b" />

*README.md -tiedoston päällekirjoitus "vahingossa" echo-komennolla*
<br>

Käytin  `git status` komentoa vielä tarkistaakseni että muutoksia oli tapahtunut, mutta ei stagettu eikä commitattu. Käytin sitten `git reset --hard` palaamaan takaisin aikaisempaan tallennettuun commit-versioon, joka palautti vanhan tekstin README.md-tiedostoon. Huomiona että reset --hard poistaa kaikki muutokset, ja jos haluttaisiin palauttaa vain yksi tiedosto aikaisempaan commit-tilaan, `git restore [tiedosto]` on siihen sopiva komento.

<img width="956" height="363" alt="kuva" src="https://github.com/user-attachments/assets/29c30a48-c98f-403e-ad99-0a1c60f97c5a" />

*git status ja reset*
<br>

## d) Tukki --- Lokin tarkastelu

Käytin komentoa `git log` näyttämään muutoslokin, jossa näkyi mm. kuka sen teki, aikaleima ja kommentit. Loki näyttää tapahtumat alhaalta ylöspäin kasvaen, eli uusimmat muutokset ovat ylimpänä. `git show` -komennolla sain vielä tarkemmin näkyviin mitä tiedostojen sisällä oli muutoksissa tehty. Tuloste näyttää vihreällä tekstillä "+..." mitä on lisätty ja mihin kohtaan.

<img width="979" height="716" alt="kuva" src="https://github.com/user-attachments/assets/0ab944af-9137-42d2-9ebd-aed5cc0aa845" />

*git log ja git show*
<br>

## e) Gitanbile --- Ansible-kansio Gittiin

Siirryin ansible-hakemistoon ja käytin komentoa `git init` joka alusti repon Gittiin, ja loi hakemistoon piilotetun .git/ -kansion, jota Git käyttää versionhallintaan.

<img width="803" height="653" alt="kuva" src="https://github.com/user-attachments/assets/a87f5090-1f24-4314-8b4b-5f967720b00d" />

*git init, ja .git/-kansio ilmestyi*
<br>

Tämän jälkeen tein commitin `git add --all` ja `git commit -m "initial ansible state"`, joka lisäsi ansible-hakemiston nykyisellään Gittiin.

<img width="769" height="362" alt="kuva" src="https://github.com/user-attachments/assets/0e882546-fbf7-4ba8-979c-4b3d497b74dd" />

*ansible-hakemiston commit Gittiin*
<br>

En ollut varma minkälaista muutosta tehtävänanto tässä kohtaa halusi, mutta kommentoin ulos site.yml:stä kaikki roolit paitsi *hello*. Ajoin playbookin, joka suoritti nyt vain hello-roolin, ja vein muutokset commitilla Gittiin. Lopuksi katsoin vielä `git log` ja `git show` -komennoilla muutokset.

<img width="722" height="570" alt="kuva" src="https://github.com/user-attachments/assets/f9ad822d-a07c-4b4a-ba2c-f035762006ae" />

*playbook suoritti nyt vain hello-roolin*
<br>


<img width="524" height="788" alt="kuva" src="https://github.com/user-attachments/assets/abc18a96-4012-4914-b0e3-3641ba964c1d" />

*git log ja show*
<br>


## f) Projektipari

Ilmoitus laitettu Moodlen foorumille 😉

<br>
<br>
<br>
<br>
<br>
<br>

Lähdeluettelo:

Chacon, S & Straub, B. 2014. Pro Git. 1.3 Getting Started - What is Git? Git. Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu: 27.4.2026.

Git. Reference. s.a. Luettavissa: https://git-scm.com/docs. Luettu: 27.4.2026.
