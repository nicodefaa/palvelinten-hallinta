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

## b) Dolly --- Repon kloonaus ja testimuutoksia

Kloonasin äsken tekemäni sunshine-repon käyttämällä komentoa `git clone [repon URL]`.

Kloonauksen jälkeen kotihakemistoon tuli hakemisto "sunshine", ja sisältä löytyivät kopioituna GitHubissakin näkyvät **LICENSE** ja **README.md**.

<img width="1065" height="223" alt="kuva" src="https://github.com/user-attachments/assets/21e8c69a-f162-41a8-8ca9-1ac3b5dfd66a" />

Seuraavana tein pari muutosta; 

ensin lisäsin README.md-tiedostoon uuden kommentin, ja sitten loin vielä kokonaan uuden tekstitiedoston:

<img width="700" height="208" alt="kuva" src="https://github.com/user-attachments/assets/059ac968-3b61-4cdb-943e-93fd42553f0b" />

Käytin komentoa `git add --all` lisäämään kaikki muutokset staging-alueelle valmiiksi commit:ia varten.

Käytin komentoa `git commit -m "viesti"` committaamaan muutokset. Tämän yhteydessä tuli pyyntö 

<img width="1106" height="293" alt="kuva" src="https://github.com/user-attachments/assets/5553da9d-f1dc-454c-9ac0-6355f11bc3a3" />



Lähdeluettelo:

Chacon, S & Straub, B. 2014. Pro Git. 1.3 Getting Started - What is Git? Git. Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu: 27.4.2026.
