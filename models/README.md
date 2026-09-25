# Jak přidat nový model

1. Exportuj model z Blenderu jako **.glb** (File → Export → glTF 2.0,
   formát „glTF Binary (.glb)“). Před exportem projdi checklist níže.
2. Zkopíruj výsledný `.glb` soubor do této složky (`models/`): buď
   přetažením na GitHubu (tlačítko „Add file → Upload files“ v této
   složce), nebo přes `git add` / `git push`.
3. Otevři `manifest.json` v této složce a přidej řádek s názvem souboru
   a popiskem, který se zobrazí ve výběru na stránce:

```json
[
  { "name": "Židle - návrh v1", "file": "zidle_v1.glb" },
  { "name": "Skříňka kuchyňská", "file": "skrinka.glb" }
]
```

- `name` je text, který se zobrazí v rozbalovacím seznamu na stránce.
- `file` je přesný název souboru v této složce (včetně přípony `.glb`).
- Mezi řádky musí být čárka, za posledním ne.

4. Ulož a commitni změnu (na GitHubu stačí kliknout „Commit changes“).
   Po chvíli se model objeví ve výběru na nasazené stránce.

> **Pozor:** jiná cesta, jak modely přidat, není — viewer nemá tlačítko pro
> nahrání souboru z počítače. Jediný způsob, jak se model dostane ke
> kolegům, je nahrát ho do této složky přes GitHub (kroky výše). Seznam
> modelů navíc funguje jen na webu (GitHub Pages nebo lokální server), ne
> při otevření `index.html` dvojklikem.

## Checklist pro export z Blenderu

**Textury potřebují UV mapu.** glTF přenese jen textury napojené přes UV.
Mapování přes *Generated*, *Object* nebo *Box* projekci se ztratí a
textura se pak zobrazí jako šum nebo pruhy.

- Pro každý texturovaný objekt: Edit Mode → vyber vše (`A`) → `U` →
  **Smart UV Project**, u kvádrů případně **Cube Projection**.
  Po Booleanu to platí dvojnásob, protože Boolean UV rozbije.
- V Shader editoru napoj Image Texture na **Texture Coordinate → UV**
  (nebo nech vstup Vector prázdný), ne na Generated/Object.
- Procedurální textury (Noise, Voronoi, Brick…) glTF nepřenese vůbec.
  Je potřeba je zapéct (Cycles → Bake) do obrázku.
- Viewer umí chybějící UV nouzově dopočítat (panel „Světlo a textury“
  → „Opravit UV“), ale správné UV z Blenderu vypadá vždy lépe.

**Nastavení exportu:**

- Format: *glTF Binary (.glb)*
- Include → vypnout *Punctual Lights* (viewer má vlastní světlo)
- Data → Mesh → zapnout *Apply Modifiers*
- Textury ve 4K zbytečně zvětšují soubor; pro náhledy stačí 2K.
