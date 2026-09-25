# 3D Viewer

Jednoduchý prohlížeč 3D modelů (.glb) z Blenderu, který se sdílí s kolegy
zdarma přes GitHub Pages. Žádný server, žádné uploadové limity — modely se
verzují přímo v tomto repozitáři.

**Živá stránka:** https://peetik.github.io/3Dprohlizec/

## Co umí

- Výběr modelu ze seznamu (nahraného v repu) přes rozbalovací nabídku.
- Orbit ovládání myší/dotykem — rotace, zoom (kolečko/pinch), posun (pravé
  tlačítko/dva prsty).
- Automatické vycentrování a přiblížení modelu po načtení, tlačítko
  „Reset view“ pro návrat k výchozímu pohledu.
- Panel „Světlo a textury“ — nastavení slunce, okolního světla, expozice,
  stínů, barvy pozadí a nouzová oprava chybějících UV souřadnic.

Modely se přidávají výhradně nahráním do složky `models/` v repu — žádné
tlačítko pro nahrání souboru z počítače v prohlížeči záměrně není, aby
nevznikal dojem, že se tím model sdílí s kolegy (viz níže).

## Jak přidat nový model pro kolegy

Viz [models/README.md](models/README.md) — stručně: nahraj `.glb` do
složky `models/` a přidej záznam do `models/manifest.json`.

## Jak spustit lokálně

Stránka používá `fetch()` pro načtení seznamu modelů, takže nejde otevřít
přímo dvojklikem (`file://`) — je potřeba lokální statický server:

```bash
# Python (obvykle už nainstalovaný)
python -m http.server 8080

# nebo Node.js, bez instalace
npx serve .
```

Poté otevři `http://localhost:8080` (nebo port, který nástroj vypíše).

## Jak nasadit na GitHub Pages (poprvé)

1. Na [github.com](https://github.com) klikni **New repository**, zadej
   název (např. `3d-viewer`), zvol **Public** a repozitář založ (bez
   README, ten už tu je).
2. V tomto adresáři spusť:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: 3D GLB viewer"
   git branch -M main
   git remote add origin https://github.com/<tvuj-ucet>/<nazev-repa>.git
   git push -u origin main
   ```
3. Na GitHubu otevři repozitář → **Settings → Pages**.
4. V sekci **Build and deployment** vyber **Source: Deploy from a
   branch**, **Branch: main**, složka **/ (root)** → **Save**.
5. Po 1–2 minutách bude stránka dostupná na
   `https://<tvuj-ucet>.github.io/<nazev-repa>/`.

Při každém dalším nahrání modelu (viz výše) se stránka na GitHub Pages
automaticky aktualizuje po commitu — není potřeba nic dalšího nastavovat.

## Technické poznámky

- Postaveno na [Three.js](https://threejs.org) (načítá se z CDN přes
  import mapu v `index.html`, žádný build krok ani npm instalace).
- Podporuje komprimované modely (Draco) i běžné `.glb`/`.gltf`.
- Velikost repozitáře: GitHub doporučuje repo do ~1 GB a jednotlivé
  soubory do 100 MB — pro běžné exporty z Blenderu (typicky jednotky až
  nízké desítky MB) to bohatě stačí. Pro velmi velké modely zvaž zmenšení
  textur nebo Draco kompresi při exportu.
