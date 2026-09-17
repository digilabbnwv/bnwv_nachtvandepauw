# Luisterfragmenten – Bibliotheek Noordwest Veluwe

Eenvoudige webpagina voor een iPad in kioskmodus. Bezoekers kiezen één van
drie audiofragmenten; het gekozen fragment speelt oneindig op herhaling.
Bedoeld voor kinderen van 8–12 jaar en bezoekers zonder uitleg.

## Bestanden in de repo

```
index.html                        ← de hele app (HTML + CSS + JS + lettertype, alles inline)
de-geheime-tuin.mp3               ← audio fragment 1
films-die-nergens-draaien.mp3     ← audio fragment 2
lampje.mp3                        ← audio fragment 3
```

Alle bestanden staan **in de root** van de repo, naast elkaar. `index.html`
verwijst naar de drie MP3's in dezelfde map. Er zijn geen externe
dependencies of CDN's; het lettertype (Nunito, huisstijl BNWV) zit ingebed in
`index.html`. Zodra de pagina één keer geladen is, werkt alles offline.

> De originele `.wav`-bestanden worden **niet** meegecommit (te groot voor
> GitHub) en staan in `.gitignore`. Alleen de MP3's horen in de repo.

## Labels aanpassen

Open `index.html` en pas bovenin het `<script>` de lijst `FRAGMENTEN` aan:

```js
var FRAGMENTEN = [
  { label: 'Lampje',                    bestand: 'lampje.mp3',                    kleur: '#00B4D8' },
  { label: 'Films die nergens draaien', bestand: 'films-die-nergens-draaien.mp3', kleur: '#FF6B6B' },
  { label: 'De geheime tuin',           bestand: 'de-geheime-tuin.mp3',           kleur: '#A78BFA' }
];
```

- `label`  = de tekst op de knop.
- `bestand` = de MP3-bestandsnaam (in dezelfde map).
- `kleur`  = huisstijlkleur van de knop (mag je laten staan).

## Publiceren via GitHub Pages

1. Push naar de `main`-branch.
2. Ga in GitHub naar **Settings → Pages**.
3. Kies bij **Source**: *Deploy from a branch*, branch `main`, map `/ (root)`.
4. Na een paar minuten staat de pagina op
   `https://digilabbnwv.github.io/bnwv_nachtvandepauw/`.

## Op de iPad zetten (kioskmodus)

1. Open de GitHub Pages-URL in Safari en laat de pagina één keer volledig laden
   (daarna werkt hij offline).
2. Zet Safari in **Begeleide toegang** (Instellingen → Toegankelijkheid →
   Begeleide toegang) of gebruik je MDM-kioskprofiel.
3. Leg de iPad liggend (landscape) neer. De **eerste tik** ontgrendelt het
   geluid (iOS blokkeert automatisch afspelen), daarna kiest de bezoeker een
   fragment.

## Nieuwe audio toevoegen of vervangen

Vervang een MP3 met dezelfde bestandsnaam, of zet een nieuwe MP3 in de map en
pas de `FRAGMENTEN`-lijst aan. WAV omzetten naar MP3 kan met ffmpeg:

```bash
ffmpeg -i bron.wav -codec:a libmp3lame -b:a 192k fragment.mp3
```
