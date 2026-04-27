# h5 Gitar Hero

## x) Tiivistelmä: 1.3 Getting Started - What is Git?

- Git tallentaa projektin tilan snapshotteina jokaisen commitin yhteydessä.
- Lähes kaikki Git:in toiminnot toimivat paikallisesti ilman verkkoa.
- **Commit** tallentaa projektin tilan paikallisesti ja **Push** vie projektin verkon yli valittuun online repositoryyn.
- Vanhaa dataa ei yleensä poisteta, vaan muutettu data lisätään vanhan päälle, jonka ansiosta kertaalleen commitattu data on turvallisesti tallessa.
- Muuttamatonta tiedostoa ei tallennetta uudelleen, vaan lisätään vain viittaus vanhaan versioon.

Lähde: Chacon & Straub 2014.

## a) Online --- GitHub varaston luonti

Loin tehtävää varten uuden repon tänne githubiin ja nimesin sen "sunshine":ksi vaatimuksen mukaan.

Pistin päälle option, joka loi repoon README-tiedoston, sekä valitsin lisenssiksi GPL-3.0:n, joka loi lisäksi LICENSE-tiedoston.

<img width="630" height="571" alt="kuva" src="https://github.com/user-attachments/assets/3a61d9a6-8c09-4605-8b70-0ce36d012d19" />
<br>

## b) Dolly --- Repon kloonaus ja testimuutoksia

Kloonasin äsken tekemäni sunshine-repon käyttämällä komentoa `git clone [repon URL]`.

Kloonauksen jälkeen kotihakemistoon tuli hakemisto "sunshine", ja sisältä löytyivät kopioituna GitHubissakin näkyvät **LICENSE** ja **README.md**.

<img width="1065" height="223" alt="kuva" src="https://github.com/user-attachments/assets/21e8c69a-f162-41a8-8ca9-1ac3b5dfd66a" />
<br>

Seuraavana tein pari muutosta; 

ensin lisäsin README.md-tiedostoon uuden kommentin, ja sitten loin vielä kokonaan uuden tekstitiedoston:

<img width="700" height="208" alt="kuva" src="https://github.com/user-attachments/assets/059ac968-3b61-4cdb-943e-93fd42553f0b" />
<br>

Käytin komentoa `git add --all` lisäämään kaikki muutokset staging-alueelle valmiiksi commit:ia varten.

Käytin komentoa `git commit -m "viesti"` committaamaan muutokset. Tämä ensimmäinen commit keskeytyi ja tuli pyyntö lisätä konfiguraatioon käyttäjänimi ja sähköposti.

<img width="1106" height="293" alt="kuva" src="https://github.com/user-attachments/assets/5553da9d-f1dc-454c-9ac0-6355f11bc3a3" />
<br>

Lisäsin pyydetyt tiedot annetuilla komennoilla `git config --global user.name` \ `user.email`, jonka jälkeen tein commitin uudelleen:

<img width="1104" height="131" alt="kuva" src="https://github.com/user-attachments/assets/7a3edc71-7967-4b3e-92fa-816fe73b0ee6" />

Ensimmäisen kerran kun yritin viedä muutokset komennolla `git push`, kysyttiin github tunnuksia, koska en ollut tällä koneella vielä yhdistänyt SSH-avainta GitHubiini. Kävin viemässä public-avaimeni ~/.ssh/id_ed25519.pub -tiedostosta Githubin asetuksiin SSH and GPG keys, jonka jälkeen yritin pushia uudelleen. Tällä kertaa push onnistui ja tehdyt muutokset tulivat näkyviin githubissa.

<img width="459" height="137" alt="kuva" src="https://github.com/user-attachments/assets/eedfb21e-2b29-4001-bc17-686d5cc5d505" />

<img width="738" height="247" alt="kuva" src="https://github.com/user-attachments/assets/21420786-6db9-4b88-b35f-1c1a27ee3442" />

<img width="654" height="295" alt="kuva" src="https://github.com/user-attachments/assets/3b22e2c6-239c-463a-a9c2-cb37e16cfbed" />

<img width="919" height="313" alt="kuva" src="https://github.com/user-attachments/assets/493ff62f-a796-4a34-82d7-c79a478a850c" />

<img width="505" height="202" alt="kuva" src="https://github.com/user-attachments/assets/1020080a-eb53-429a-a045-c68c7e775cb0" />





<br>
<br>
<br>
<br>
<br>
<br>

Lähdeluettelo:

Chacon, S & Straub, B. 2014. Pro Git. 1.3 Getting Started - What is Git? Git. Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu: 27.4.2026.
