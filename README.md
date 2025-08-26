# Ordinacija – Obrazec s podpisom → PDF → E-mail (Vercel + Resend)

Ta projekt je pripravljena **Next.js** aplikacija, kjer pacient izpolni obrazec, podpiše na tablici, sistem pa ustvari **PDF** in ga pošlje na **e-mail pacienta in ordinacije**.

## Hiter zagon (lokalno)

1. Namesti odvisnosti:
   ```bash
   npm i
   ```
2. Uredi `.env.local` (glej spodaj).
3. Zaženi dev strežnik:
   ```bash
   npm run dev
   ```
4. Odpri `http://localhost:3000`.

## Namestitev na Vercel (priporočeno)

1. Ustvari brezplačen račun na vercel.com.
2. Uvozi ta projekt (npr. kot GitHub repo ali naloži ZIP).
3. V Vercel **Project Settings → Environment Variables** dodaj:
   - `RESEND_API_KEY` – API ključ iz resend.com
   - `FROM_EMAIL` – e-mail pošiljatelja (npr. no-reply@tvoja-domena.si ali iz Resend domen)
   - `DOCTOR_EMAIL` – e-mail ordinacije (prejemnik)
4. Deploy. Aplikacija bo takoj pripravljena za uporabo.
5. Test: izpolni obrazec, podpiši, pritisni *Oddaj...* in preveri e-pošto.

> **Opomba:** Vercel navadno blokira neposreden SMTP iz serverless funkcij. Zato tukaj uporabljamo **Resend API**, ki deluje z Vercel brez posebnih nastavitev.

## E-mail ponudnik (Resend)

- Ustvari račun na https://resend.com, vzemi **API Key**.
- V Settings lahko dodaš/overiš domeno za pošiljanje (da bo `FROM_EMAIL` videti profesionalen). Za test lahko uporabiš tudi njihov "onboarding" pošiljatelj.

## Konfiguracija (ENV)

Ustvari datoteko `.env.local` (lokalno) ali nastavi te spremenljivke v Vercel:

```
RESEND_API_KEY=...
FROM_EMAIL=no-reply@tvoja-domena.si
DOCTOR_EMAIL=ordinacija@example.com
```

## Kaj vsebuje

- `app/page.tsx` – obrazec + podpis (react-signature-canvas).
- `app/api/submit/route.ts` – generira PDF (pdf-lib) in pošlje e-mail (Resend).
- `lib/pdf.ts` – postavitev PDF (A4), vključi sliko podpisa.
- Minimalni styling v `app/globals.css`.

## Prilagoditve

- V `app/page.tsx` dodaj več vprašanj / checkboxe / potrditve.
- V `lib/pdf.ts` spremeni izgled PDF (logotip, dodatna polja, poravnave).
- Dodaj več obrazcev kot ločene strani (npr. `/obrazci/anamneza`, `/obrazci/privolitev`), vsaka stran lahko uporablja isto API pot.

## Varnost in zasebnost

- Aplikacija pošilja PDF po e-pošti – če želiš arhiviranje, lahko dodaš shranjevanje v S3/Cloud storage.
- Če želiš šifriranje prilog ali naprednejše DPA/GDPR zahteve, to je možno dodati (npr. geslo za PDF, KMS, itd.).

## Licenca

MIT – uporabi, spremeni, razširi.
