# Kreiranje tiketa preko REST servisa (API ključ)

> Engleska, tehnička verzija ovog uputstva: [create-ticket-rest-api.md](create-ticket-rest-api.md)

## Sadržaj

1. [Uvod](#1-uvod)
2. [Kako radi](#2-kako-radi)
3. [Korak 1: API ključ](#3-korak-1-api-ključ)
4. [Korak 2: Poziv servisa](#4-korak-2-poziv-servisa)
5. [Odgovor servisa](#5-odgovor-servisa)
6. [Greške i njihovo značenje](#6-greške-i-njihovo-značenje)
7. [Primeri poziva (curl)](#7-primeri-poziva-curl)
8. [Šta je potrebno pripremiti pre integracije](#8-šta-je-potrebno-pripremiti-pre-integracije)
9. [Bezbednost i ograničenja](#9-bezbednost-i-ograničenja)
10. [Česta pitanja](#10-česta-pitanja)

---

## 1. Uvod

Neobee omogućava da spoljni sistem (CRM, ERP, web portal, monitoring alat, skripta...) **automatski kreira tiket** u nekom Neobee projektu, bez ručnog unosa kroz korisnički interfejs.

Kreiranje se radi jednim HTTP POST pozivom na REST servis platforme. Poziv se autorizuje **API ključem** koji administrator vaše kompanije izdaje u administraciji Neobee-a.

Tipični primeri upotrebe:

- korisnički portal ili kontakt forma na sajtu otvara tiket u helpdesk projektu,
- sistem za nadzor (monitoring) automatski otvara incident kada detektuje problem,
- ERP ili CRM sistem pokreće zahtev (nabavka, odobrenje, reklamacija) u Neobee-u,
- migracija ili masovni uvoz zahteva skriptom.

---

## 2. Kako radi

```
 Spoljni sistem                      Neobee REST servis                     Neobee
 ─────────────                       ──────────────────                     ──────
 POST /rest/util/start_process/...   1. proverava X-KEY u tabeli API ključeva
 Header: X-KEY: <ključ>       ────►  2. proverava da projekat pripada
 Body: naziv, tip, polja...             istoj kompaniji kao i ključ
                                     3. prosleđuje zahtev procesnom servisu  ────►  kreira tiket,
                                                                                    popunjava polja,
                                     4. vraća podatke o kreiranom tiketu   ◄────   startuje proces
                              ◄────     (id, šifra tiketa, naziv...)
```

Ukratko:

1. Administrator jednom napravi **API ključ** za kompaniju (tenant).
2. Spoljni sistem u svakom pozivu šalje taj ključ u HTTP headeru `X-KEY`.
3. Servis prepoznaje kompaniju po ključu, proverava da ciljni projekat pripada toj kompaniji i kreira tiket.
4. Tiket se kreira i **odmah startuje**: dobija šifru (npr. `HD-1042`), ulazi u početno stanje procesa i pokreću se sve automatske akcije (post funkcije) koje su podešene na startu procesa, isto kao da je tiket otvoren kroz aplikaciju.

---

## 3. Korak 1: API ključ

### 3.1. Šta je API ključ

API ključ je tajni niz karaktera (podrazumevano UUID, npr. `9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11`) koji identifikuje **vašu kompaniju** prema REST servisu. Ključ:

- važi za **celu kompaniju**, ne za jedan projekat ili jednog korisnika,
- omogućava kreiranje tiketa u **bilo kom aktivnom projektu** te kompanije,
- može se u svakom trenutku **deaktivirati** bez brisanja.

### 3.2. Gde se pravi

Ključ se pravi u **administraciji tenanta** (aplikacija za podešavanja kompanije):

**Podešavanja procesa** (globalna podešavanja) → **API** → tab **API**

Putanja u aplikaciji: `/process-settings/api/apis`

Za pristup ovoj stranici korisnik mora da ima administratorsku privilegiju za globalna podešavanja procesa (`process_settings_page_client_main`).

### 3.3. Kreiranje ključa

1. Na stranici **API** kliknite dugme za **kreiranje** u zaglavlju stranice.
2. Popunite polje **Naziv**: opisni naziv po kom ćete prepoznati ključ, najbolje naziv spoljnog sistema (npr. `CRM integracija`, `Web portal`).
3. Polje **Ključ** je automatski popunjeno novogenerisanim UUID-om. Možete ga ostaviti ili zameniti sopstvenom vrednošću (do 65535 karaktera).
4. **Kopirajte vrednost ključa** i prosledite je timu koji radi integraciju. Ovo je vrednost koja se šalje u headeru `X-KEY`.
5. Sačuvajte.

Novi ključ je odmah **aktivan**.

### 3.4. Pregled, izmena i deaktivacija

- Tabela na stranici prikazuje sve ključeve kompanije (kolone *Naziv*, *Ključ*, akcije). Neaktivni ključevi su prikazani zasivljeno; prekidač **Samo aktivni** u zaglavlju ih sakriva.
- Klikom na ikonicu zupčanika u redu otvara se isti prozor sa dodatnim prekidačem **Aktivan**.
- Isključivanjem prekidača **Aktivan** ključ se deaktivira: servis odbija sve pozive sa tim ključem (odgovor `403 Forbidden`). Ključ se ne briše, pa se može ponovo aktivirati.
- Preporučena rotacija ključa: napravite novi ključ, prebacite spoljni sistem na njega, zatim deaktivirajte stari.

---

## 4. Korak 2: Poziv servisa

### 4.1. Adresa (URL)

```
POST https://<rest-host>/rest/util/start_process/process_project_id/{process_project_id}
```

| Deo | Značenje |
| -- | -- |
| `<rest-host>` | Adresa REST servisa za vaše okruženje. Dobijate je od Esteh tima uz pristupne podatke. Različita je za test i produkciju. |
| `/rest/util/start_process/process_project_id/` | Fiksni deo putanje. |
| `{process_project_id}` | Brojčani ID **projekta** u kom se kreira tiket. Projekat mora biti aktivan i pripadati kompaniji čiji je API ključ. |

### 4.2. HTTP headeri

| Header | Obavezan | Vrednost |
| -- | -- | -- |
| `X-KEY` | da | API ključ iz koraka 1. |
| `Content-Type` | da | `application/json` |

> Ne šaljite header `X-CONTEXT`. On je namenjen internim pozivima unutar platforme; ako je prisutan, `X-KEY` se ignoriše.

### 4.3. Telo zahteva (body)

Telo je JSON objekat čiji je jedini ključ `request_body`. Unutar njega su podaci o tiketu.

```json
{
  "request_body": {
    "name": "Štampač na 3. spratu ne radi",
    "task_type_id": "15",
    "ruser_id": "1024",
    "data_map": {
      "form.description.value": "Zaglavljen papir, greška E52",
      "form.priority.value": "2"
    }
  }
}
```

| Polje | Obavezno | Tip | Opis |
| -- | -- | -- | -- |
| `name` | **da** | string | Naziv (naslov) tiketa, onako kako će biti prikazan u aplikaciji. |
| `task_type_id` | **da** | string | ID **tipa zadatka** (npr. Incident, Zahtev, Reklamacija). Tip mora biti podešen u ciljnom projektu. |
| `ruser_id` | ne | string | ID Neobee **korisnika** koji se upisuje kao kreator tiketa i u čijem se kontekstu izvršavaju automatske akcije na startu. Ako se ne pošalje, tiket kreira sistem bez korisnika. |
| `data_map` | ne | objekat | Početne vrednosti **polja forme** tiketa. Vidi 4.4. |

> **Važno:** svi ID-jevi (`task_type_id`, `ruser_id`) šalju se kao **stringovi** (u navodnicima), ne kao brojevi.

### 4.4. Popunjavanje polja forme (`data_map`)

`data_map` je objekat u kom je svaki ključ oblika:

```
form.<šifra_polja>.value
```

- `form` i `value` su fiksni.
- `<šifra_polja>` je **šifra (kod) komponente** na formi projekta, onako kako je definisana u podešavanjima forme (npr. `description`, `priority`, `customer_email`).
- Ključevi koji nisu u ovom obliku se ignorišu.

Vrednost polja zavisi od tipa komponente:

| Tip komponente | Format vrednosti | Primer |
| -- | -- | -- |
| tekst, broj, datum | string | `"form.description.value": "Zaglavljen papir"` |
| jednostruki izbor (select, radio) | string sa šifrom ili vrednošću opcije | `"form.priority.value": "2"` |
| složene komponente (višestruki izbor, katalog, tabele, fajlovi) | JSON struktura (niz ili objekat) | zavisi od komponente |

Tačan format vrednosti za konkretno polje najlakše je proveriti na postojećem tiketu u aplikaciji, u prikazu **podataka za developere** (developer data), gde se vide vrednosti svih polja u istom obliku u kom ih servis očekuje. Listu šifara polja i ID tipa zadatka daje administrator projekta.

Polja koja nisu navedena u `data_map` ostaju prazna, odnosno dobijaju podrazumevane vrednosti definisane na formi.

---

## 5. Odgovor servisa

Uspešan poziv vraća HTTP status **200** i JSON u standardnom Neobee omotaču. Podaci o kreiranom tiketu su u `data`.

```json
{
  "data": {
    "id": 48213,
    "ext_code": "HD-1042",
    "process_euid": "0f4a2d3e-8b6c-4c8f-9c3a-6e1b2f7d9a10",
    "name": "Štampač na 3. spratu ne radi",
    "process_project_id": 7,
    "task_type_id": 15,
    "company_id": 3,
    "status_id": 1,
    "...": "..."
  },
  "version": "beta",
  "message": "",
  "messageCode": 1,
  "messageLevel": 1,
  "uuid": "…",
  "hash": "…"
}
```

Najvažniji podaci u `data`:

| Polje | Značenje |
| -- | -- |
| `id` | Interni brojčani ID tiketa. Koristi se u daljim pozivima servisa. |
| `ext_code` | **Šifra tiketa** koju vide korisnici (npr. `HD-1042`). Ovo je vrednost koju treba prikazati krajnjem korisniku ili sačuvati u spoljnom sistemu. |
| `process_euid` | Jedinstveni identifikator tiketa (UUID). |
| `name` | Naziv tiketa. |
| `process_project_id`, `task_type_id`, `company_id` | Projekat, tip zadatka i kompanija kojima tiket pripada. |

Pored navedenih, `data` sadrži i ostale kolone zapisa tiketa (datumi, statusi, dodeljeni korisnik...). Spoljni sistem treba da čuva bar `id` i `ext_code`.

Značenje polja omotača:

| Polje | Uspeh | Greška |
| -- | -- | -- |
| `messageCode` | `1` | `2` |
| `messageLevel` | `1` | `4` |
| `message` | prazno | tekst greške |

---

## 6. Greške i njihovo značenje

| HTTP status | `message` | Uzrok | Šta uraditi |
| -- | -- | -- | -- |
| `401 Unauthorized` | `Unauthorized` | Nije poslat header `X-KEY`. | Dodati header `X-KEY` sa važećim ključem. |
| `403 Forbidden` | `Forbidden operation` | Ključ ne postoji ili je **deaktiviran**; projekat sa datim ID-jem ne postoji ili nije aktivan; ključ i projekat pripadaju **različitim kompanijama**. | Proveriti da je ključ aktivan u administraciji, da je `process_project_id` tačan i da projekat pripada vašoj kompaniji. |
| `500 Internal Server Error` | `Server error` | Neispravno telo zahteva (nedostaje `name` ili `task_type_id`, telo nije validan JSON, ključ u `data_map` nije oblika `form.x.value`); nepostojeći `task_type_id`; greška pri kreiranju tiketa (npr. greška u post funkciji). | Proveriti telo zahteva prema odeljku 4.3. Ako je zahtev ispravan, prijaviti problem Esteh podršci uz vreme poziva i telo zahteva. |

Telo odgovora u slučaju greške ima isti omotač, sa praznim `data` i popunjenim `message`:

```json
{ "data": {}, "version": "beta", "message": "Forbidden operation", "messageCode": 2, "messageLevel": 4, "uuid": "…", "hash": "…" }
```

> Servis iz bezbednosnih razloga ne vraća detalje uzroka za `500`. Detalji su dostupni u logovima platforme, pa pri prijavi problema navedite tačno vreme poziva.

---

## 7. Primeri poziva (curl)

### 7.1. Kompletan primer sa poljima forme

```bash
curl -X POST "https://<rest-host>/rest/util/start_process/process_project_id/7" \
  -H "Content-Type: application/json" \
  -H "X-KEY: 9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11" \
  -d '{
    "request_body": {
      "name": "Štampač na 3. spratu ne radi",
      "task_type_id": "15",
      "ruser_id": "1024",
      "data_map": {
        "form.description.value": "Zaglavljen papir, greška E52",
        "form.priority.value": "2"
      }
    }
  }'
```

### 7.2. Minimalan primer

Samo obavezna polja, bez kreatora i bez vrednosti polja forme:

```bash
curl -X POST "https://<rest-host>/rest/util/start_process/process_project_id/7" \
  -H "Content-Type: application/json" \
  -H "X-KEY: 9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11" \
  -d '{"request_body": {"name": "Tiket iz spoljnog sistema", "task_type_id": "15"}}'
```

### 7.3. Telo zahteva iz fajla

Za duže zahteve, telo se može čuvati u fajlu (npr. `ticket.json`):

```bash
curl -X POST "https://<rest-host>/rest/util/start_process/process_project_id/7" \
  -H "Content-Type: application/json" \
  -H "X-KEY: 9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11" \
  --data @ticket.json
```

### 7.4. Prikaz HTTP statusa

Dodajte `-i` da bi curl ispisao i status liniju i headere odgovora, što olakšava razlikovanje `200`, `401`, `403` i `500`:

```bash
curl -i -X POST "https://<rest-host>/rest/util/start_process/process_project_id/7" \
  -H "Content-Type: application/json" \
  -H "X-KEY: 9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11" \
  -d '{"request_body": {"name": "Test", "task_type_id": "15"}}'
```

U primerima zamenite `<rest-host>`, vrednost `X-KEY`, ID projekta (`7`), ID tipa zadatka (`15`), ID korisnika (`1024`) i šifre polja svojim vrednostima.

---

## 8. Šta je potrebno pripremiti pre integracije

Pre nego što spoljni sistem počne da kreira tikete, treba prikupiti sledeće podatke:

| Podatak | Ko obezbeđuje | Gde se nalazi |
| -- | -- | -- |
| Adresa REST servisa (`<rest-host>`) | Esteh tim | Uz pristupne podatke za okruženje (test / produkcija). |
| API ključ | Administrator kompanije | Administracija → Podešavanja procesa → API (odeljak 3). |
| ID projekta (`process_project_id`) | Administrator projekta | Podešavanja projekta, odnosno URL projekta u aplikaciji. |
| ID tipa zadatka (`task_type_id`) | Administrator projekta | Podešavanja projekta → tipovi zadataka. |
| Šifre polja forme i format vrednosti | Administrator projekta | Podešavanja forme projekta; provera na postojećem tiketu kroz podatke za developere. |
| ID korisnika kreatora (`ruser_id`), ako je potreban | Administrator kompanije | Administracija korisnika. |

Preporuka je da se integracija prvo testira na **test okruženju** sa zasebnim API ključem, pa tek onda na produkciji.

---

## 9. Bezbednost i ograničenja

- **Ključ je tajna.** Ko ima ključ može da kreira tikete u svim aktivnim projektima vaše kompanije. Čuvajte ga kao lozinku: ne šaljite ga mejlom u čistom tekstu, ne upisujte ga u javne repozitorijume, čuvajte ga u sistemu za tajne (secret store) spoljnog sistema.
- **Ključ važi za celu kompaniju.** Ne postoji ograničenje po projektu, tipu zadatka ili korisniku. Ako različiti sistemi treba da imaju različit obim pristupa, koristite zasebne ključeve za svaki sistem radi lakše kontrole i deaktivacije.
- **Uvek koristite HTTPS.** Ključ se prenosi u headeru i mora biti zaštićen enkripcijom transporta.
- **Rotacija.** Menjajte ključ periodično i odmah po sumnji na kompromitovanje: napravite novi, prebacite integraciju, deaktivirajte stari.
- **Nema ograničenja broja poziva (rate limit)** na strani servisa. Spoljni sistem treba sam da vodi računa da ne šalje duplikate, npr. da ne ponavlja poziv ako je već dobio `200`.
- **Poziv nije idempotentan.** Svaki uspešan poziv kreira novi tiket. Ako veza padne posle slanja zahteva, a pre prijema odgovora, tiket je možda ipak kreiran. Pre ponavljanja poziva proverite u aplikaciji.
- Tiket se startuje kao **sistemska akcija**. Ako procesna logika (post funkcije, notifikacije, dodela) zahteva korisnika, obavezno pošaljite `ruser_id`.
- Preko API ključa je moguće **samo kreiranje i startovanje tiketa** (i još dva pomoćna poziva za čitanje brojača i preuzimanje fajla, opisana u engleskoj verziji). Izmena, komentarisanje ili zatvaranje tiketa nisu dostupni ovim putem.

---

## 10. Česta pitanja

**Može li se jednim pozivom kreirati više tiketa?**
Ne. Jedan poziv kreira tačno jedan tiket. Za više tiketa šalje se više poziva.

**Da li tiket može ostati u statusu nacrta (draft)?**
Ne. Servis kreira i odmah startuje tiket. Tiket dobija šifru i ulazi u početno stanje procesa.

**Šta ako pošaljem polje koje ne postoji na formi?**
Vrednost se ignoriše, tiket se kreira bez greške.

**Mogu li da pošaljem fajl (prilog) uz tiket?**
Ne direktno kroz ovaj poziv. Prilozi se dodaju naknadno, kroz druge mehanizme platforme. Kontaktirajte Esteh tim za detalje.

**Kako da znam koji je korisnik kreirao tiket kada ne pošaljem `ruser_id`?**
Tiket je kreiran od strane sistema, bez korisnika. Ako je važno ko je kreator, napravite namenski tehničkog korisnika (npr. `CRM integracija`) i šaljite njegov ID u `ruser_id`.

**Zašto dobijam `403` iako je ključ tačan?**
Najčešće zato što `process_project_id` pripada drugoj kompaniji, projekat nije aktivan, ili je ključ u međuvremenu deaktiviran u administraciji.

**Zašto dobijam `500` iako izgleda da je sve ispravno?**
Proverite da su `task_type_id` i `ruser_id` poslati kao stringovi, da `task_type_id` postoji u ciljnom projektu i da su svi ključevi u `data_map` oblika `form.<šifra>.value`. Ako je i dalje greška, verovatno pada neka automatska akcija na startu procesa; obratite se Esteh podršci sa vremenom poziva.
