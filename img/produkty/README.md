# Fotky produktů — struktura

Kalkulátor (sekce 6 · Detaily technologií) hledá fotky přesně na těchto cestách.
Když soubor chybí, výrobce se v galerii prostě nezobrazí — nic se nerozbije.

```
img/produkty/
  panely/      trina.jpg ✅   canadian-solar.jpg ❌   jinkosolar.jpg ❌   longi.jpg ❌
  stridace/    solinteg.jpg ✅   sungrow.jpg ❌   solax.jpg ❌
  baterie/     dyness-tower.jpg ✅   dyness-stack.jpg ✅   pylontech.jpg ✅   solinteg.jpg ❌
  wallboxy/    solinteg-s11.jpg ✅
  konstrukce/  hak.jpg ✅   falc.jpg ✅   zatez.jpg ✅
```

❌ = soubor zatím chybí. Dvě cesty, jak ho doplnit:

1. **Nahrát přes prohlížeč** — v kalkulátoru klikni u dané kategorie na
   „📷 Fotky" → „＋ Nahrát fotku". Fotka se zmenší na max. 900 px, uloží se do
   galerie kategorie v prohlížeči a půjde pak vybírat u dalších nabídek.
   Pozor: je uložená jen v tomhle prohlížeči, ne v souborech projektu.

2. **Nahrát soubor sem** — pojmenovat přesně podle tabulky výše. Tahle cesta je
   trvalá a přenese se s projektem i na druhý počítač.

Doporučený formát: JPG, delší strana 800–1200 px, bílé nebo průhledné pozadí
oříznuté na produkt. Velké soubory zbytečně nafukují výsledné PDF.
