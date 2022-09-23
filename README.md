<h1 align=center>Node zadatci</h1>
<p align=center>Node zadaci za vježbanje.</p>

## Opis

Svaki zadatak radi se na posebnom branchu istog imena kao i direktorij unutar kojeg se nalazi zadatak npr. ako je direktorij imena 1-zadatak to je ujedno i ime brancha.

Unutar svakog direktorija ponovo se radi novi projekt s `npm init` proizvoljnih informacija prilikom setupa ali po mogućnosti nešto nalik na temu zadatka.

Typescript se neće koristiti.

## Zadatak 1 - REST API

Potrebno je napraviti REST API uz pomoć [Expressa](https://github.com/expressjs/express). U cijelosti radi se o backend sustavu informatičkog dućana.

Model podatka o kojem ovisi cijeli API je proizvod tj. item. Polja koja item posjeduje su:

- **id** - Jedinstveni GUID - string
- **name** - Naziv proizvoda - string
- **price** - Cijena proizvoda izraženo u HRK - number
- **category** - Kategorija proizvoda, označeno poljem brojeva ali se svaka vrijednost polja odnosi na enumeraciju koja se treba napraviti zasebno - number[]
- **manufacturer** - Proizvođač, enumeracija koju je potrebno napraviti zasebno - number
- **released** - Kada je izdan proizvod - Date

Proizvodi se trebaju nalaziti unutar polja koje će se mijenjati naknadno, tj. koristiti će se in-memory baza podataka. Na pokretanju programa potrebno je to polje popuniti s barem 100 nasumično generiranih proizvoda.

Rute koje je potrebno napraviti su:

**GET** `/items` - Dohvaća sve proizvode koji se prodaju u dućanu, parametri za filtriranje koji se ujedno mogu slati su:

- `name` - Naziv proizvoda, filtrira se s `includes` funkcijom
- `priceFrom` - Cijena od
- `priceTo` - Cijena do
- `category` - Popis kategorija po kojima se filtrira
- `manufacturer` - Proizvođač proizvoda
- `releasedYear` - Godina koje je izdan proizvod
- `skip` - Dodatni podataka za paginaciju sadržaja, opisuje koliko se elemenata mora preskočiti
- `take` - Dodatni podataka za paginaciju sadržaja, opisuje koliko se elemenata mora uzeti

Ruta za dohvat može izgledati kao nešto nalik ovome: `/items?name=RTX&priceFrom=2000`

**GET** `/items/{id}` - Dohvaća specifični proizvod

**POST** `/items` - Stvara novi proizvod, u slučaju da su neka polja pogrešnog oblika npr. ne postoji enumeracija potrebno je poslati poruku greške

**PUT** `/items/{id}` - Ažurira samo navedena polja proizvoda, u slučaju da su neka polja pogrešnog oblika npr. ne postoji enumeracija potrebno je poslati poruku greške

**DEL** `/items/{id}` - Briše određeni proizvod

### Dodatno

- Spojiti izvor podataka na MySQL server umjesto na in-memory bazu podataka

- Napraviti dodatne rute za autentifikaciju:
  - **POST** `/auth/login` - Prijava korisnika koja vraća natrag JWT token, unutar JWT tokena pospremiti samo ID korisnika
  - **POST** `/auth/register` - Registracija korisnika s dva parametra: `email` i `password`, potrebno je vratiti poruku greške ako korisnik postoji u bazi, a lozinku kriptirati uz pomoć `bcrypt`
  - Rute koje nisu dohvaćene `GET` metodom potrebno je zaštiti na način da se request odbija i vraća poruka greške statusnog koda `401`, autentifikacijski dio šalje se preko [`Authorization Bearer`](https://stackoverflow.com/questions/22229996/basic-http-and-bearer-token-authentication) HTTP headera

## Zadatak 2 - Razno

Potrebno je riješiti razne slučajeve, svaki slučaj staviti u posebnu datoteku proizvoljnog imena i exportati u glavnu datoteku `main.js` gdje će se importati i koristiti

- Napisati funkciju koja će grupirati popis objekata po određenom polju, npr.

```javascript
const employees = [
  { name: "Alina", company: "Google", id: 1 },
  { name: "Vika", company: "Coca Cola", id: 2 },
  { name: "Alex", company: "Jonson & Jonson", id: 3 },
  { name: "Vlad", company: "Google", id: 4 },
  { name: "Fibi", company: "Coca Cola", id: 5 },
  { name: "Joey", company: "Google", id: 6 }
];
```

Ovo polje grupira se po polju "company":

```javascript
{
  Google: [
    {
      name: "Alina",
      id: 1
    },
    {
      name: "Vlad",
      id: 4
    },
    {
      name: "Joey",
      id: 6
    }
  ],
  "Coca Cola": [
    {
      name: "Vika",
      id: 2
    },
    {
      name: "Fibi",
      id: 5
    }
  ],
  "Jonson & Jonson": [
    {
      name: "Alex",
      id: 3
    }
  ]
}
```

- Napisati funkciju koja će iz popisa objekata vratiti to isto polje bez duplikata, duplikat se smatra objekt sa svim istim imenima polja i vrijednostima polja
- Pronaći 3 besplatna API-a po izboru i isčekati istovremeno sve pozive uz pomoć `Promise.all` funkcije, nakon što se sve dohvati ispisati sve rezultate
- Napisati funkciju koja će parsirati URL predan u parametru, tj. koja će vraćati domenu, query parametre i sve dijelove URL-a u obliku objekata
- Napisati program koji će primiti samo jedan input argument (putanja na disku) i ispisati sve datoteke u tom direktoriju, npr. `program.js "C:/Users"`
- Napisati program koji će primiti beskonačno mnogo putanji do datoteka na disku i od njih stvoriti zippanu datoteku imena jednakom današnjem datumu u ISO formatu, npr. `program.js "./text.txt" "../test.json"`
- Napisati program koji će poslati mail preko SMTP protokola na GMAIL adresu, proizvoljnog sadržaja
- Napisati program koji će ispisati lokalnu IP adresu računala
