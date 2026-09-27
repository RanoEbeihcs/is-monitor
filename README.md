[README.md](https://github.com/user-attachments/files/32698753/README.md)
# Ice Acoustic Monitor v2 — Calibration Mode

## Vad v2 gör
Version 2 är byggd för att skapa ett första tränings-/kalibreringsdataset.

Arbetsflöde:

1. Starta mikrofonen.
2. Starta en 1–15 sekunders kalibreringsinspelning.
3. Verktyget analyserar spektrumet och visar upp till sex möjliga smala spektrala toppar.
4. Välj den frekvens som du bedömer vara isresonansen.
5. Mät den verkliga istjockleken, t.ex. `5.6 cm`.
6. Ange istyp, temperatur och ljudkälla.
7. Spara mätningen.
8. Exportera JSON/CSV och ladda ner ljudprovet.

## Exempel
En datapunkt kan bli ungefär:

- frequency_hz: 842
- thickness_cm: 5.6
- ice_type: sötvattenis
- temperature_c: -4.5
- source: skridskoslag

Det är viktigt att inte hardkoda `842 Hz = 5.6 cm`. Flera mätningar behövs eftersom resonansfrekvensen påverkas av fler faktorer än tjockleken.

## Vad som ska samlas in
För varje plats/mättillfälle är det bra att få:
- flera ljudprov vid samma tjocklek
- flera tjocklekar
- samma och olika temperaturer
- olika istyper
- ljudkälla (skridskoåkning, tappning, hopp, naturligt isljud)
- gärna plats/GPS i ett separat fält om du senare vill analysera geografiska skillnader
- exakt borrmätt tjocklek som referens

## Nästa AI-steg
När datasetet börjar bli större kan vi bygga:
1. en modell som klassificerar `isresonans` vs `annat ljud`
2. en modell som använder hela tids-/frekvensmönstret, inte bara dominant frekvens
3. en regressionsmodell för tjocklek med osäkerhetsintervall
4. ett Skate Mode som kontinuerligt detekterar och varnar

För ML bör råa ljudklipp sparas tillsammans med metadata. Den nuvarande v2 sparar metadata i browserns localStorage och låter dig exportera JSON/CSV. Ljudprovet laddas ner separat.

## Viktig begränsning
Detta är en forskningsprototyp och inte ett certifierat säkerhetssystem. Appen ska inte ensam användas för att avgöra om naturis är säker att beträda.
