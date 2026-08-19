# BF Technology — cenová nabídka FVE (A4 na výšku)

Jednosouborová aplikace: `index.html` (HTML + CSS + JS pohromadě, žádný build).
Otevírá se přímo v prohlížeči, tiskne se přes `⌘P` do PDF.

## Pro Claude — přečti si tohle jako první

**Na projektu pracují sessiony ze dvou počítačů.** Složka se synchronizuje přes Google Drive
(zrcadlení), takže tenhle soubor vidí obě strany. Paměť Clauda (`~/.claude/`) leží mimo
synchronizovanou složku a **nepřenáší se** — všechno podstatné patří sem.

Než začneš cokoli měnit:

1. Projdi **Kdo právě pracuje** a **Deník úprav** níže.
2. Zapiš se do „Kdo právě pracuje" (počítač + čas + co děláš) a po dokončení řádek smaž.
   Google Drive **neumí slučovat** — když dva sessiony upraví `index.html` současně,
   jedna verze se ztratí nebo vznikne kopie `index (1).html`.
3. Po dokončení práce **přidej řádek do deníku** (datum, co a proč).
4. Když měníš výchozí HTML bloku, který má `data-save`, **zvaž migraci** (viz Pasti níže).

## Kdo právě pracuje

_(prázdné = nikdo, můžeš začít)_

| počítač | od kdy | na čem |
|---|---|---|
| — | — | — |

## Struktura

| cesta | obsah |
|---|---|
| `index.html` | celá aplikace |
| `img/produkty/{panely,stridace,baterie,wallboxy,konstrukce}/` | fotky do katalogu, soupis v `img/produkty/README.md` |
| `img/`, `assets/`, `bft/` | fotky karet, titulní fotka, loga |
| `_orig_images/` | zálohy originálů před optimalizací (do gitu nepatří) |
| `_nepouzite/` | odložené nepoužívané soubory (do gitu nepatří) |
| `vystup/` | exportovaná PDF |

## Jak to funguje

- **Strany:** 1 titulka · 2 použité technologie · 3 cenová kalkulace + souhrn · 4 rozsah + platby + spolupráce + kontakty
- **Formulář a kalkulátor** jsou nad nabídkou, v tisku se skrývají (`@media print`)
- **Kalkulátor** počítá marži a propisuje ceny do stran 3 a 4 (`propagateKalkToOffer`)
- **Přepínač BFT/BFK** v liště mění logo, název, kontakty i barvy
- **localStorage** — klíč `bft-nabidka-a4-v1` a odvozené (`:kalk`, `:detaily`, `:manual`,
  `:dotace`, `:wallbox`, `:klientFoto`, katalog). **Mezi počítači se nepřenáší.**

## Pasti, na které se tu už narazilo

- **`data-save` bloky přebijí šablonu.** Změna výchozího HTML se uživateli s uloženou
  nabídkou neprojeví — `loadState()` mu vrátí starou verzi. Řeší se přes
  `TEMPLATE_SIGNATURES` v `restoreHtmlBlocks()` (podpis = řetězec, který má jen nová verze).
- **`.brand-name` u konstrukce je `<select>`.** `textContent` vrátí všechny volby najednou →
  používej `cardBrandText()`.
- **Popisky v cenové kalkulaci se skládají, neparsují.** Koncovka je v `data-suffix` buňky.
  Parsování textu kdysi způsobilo nabalování („− 21 kWh − 21 kWh − …").
- **PNG fotky nafukují PDF.** Chrome je vkládá bezztrátově (770 kB → 3,3 MB). Fotky patří
  jako JPEG; průhlednost před převodem podložit **bílou** (jinak vyjde černá).
- **Průhlednost v paletovém PNG** (`mode='P'`) běžná detekce alfa kanálu mine.

## Deník úprav

| datum | co |
|---|---|
| 5. 8. | Vznik A4 verze zkopírováním landscape nabídky; layout na výšku, karty 3×2 |
| 5. 8. | Sloučení stran (cenovka + souhrn, rozsah + platby + spolupráce + kontakty) → 4 strany |
| 5. 8. | Fotka domu klienta na titulku (vypínatelná, dvě velikosti); oprava `.title-page > .photo-slot` |
| 15. 8. | Optimalizace obrázků: PNG → JPEG, PDF 6,8 → 1,2 MB; zálohy v `_orig_images/` |
| 15. 8. | Wallbox 0–3 v kalkulátoru; 0 skryje kartu, řádek kalkulace, „wallbox" i „elektromobilitu" |
| 15. 8. | Platby 20 / 30 / 40 / 10 % + migrace `TEMPLATE_SIGNATURES` pro uložené nabídky |
| 15. 8. | Patička: IČO/DIČ až za adresu; lišta na dva řádky, ať s ní přepínač BFT/BFK nehýbe |
| 16. 8. | Katalog výrobců, galerie fotek podle kategorie, sekce 6 přes celou šířku (druhá session) |

## Co zbývá

- Doplnit chybějící fotky výrobců: Canadian Solar, JinkoSolar, LONGi, Sungrow, SolaX,
  baterie Solinteg — viz `img/produkty/README.md`
- Doplnit parametry u těch samých položek (rozměry, Wp, výkony)
- Zvážit, jestli IČO/DIČ nechat na straně 4 dvakrát (blok Dodavatel + patička)
