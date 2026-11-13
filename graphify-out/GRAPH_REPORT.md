# Graph Report - .  (2026-11-13)

## Corpus Check
- Corpus is ~6,826 words - fits in a single context window. You may not need a graph.

## Summary
- 151 nodes · 175 edges · 6 communities (3 shown, 3 thin omitted)
- Extraction: 90% EXTRACTED · 10% INFERRED · 0% AMBIGUOUS · INFERRED: 17 edges (avg confidence: 0.88)
- Token cost: 101,012 input · 0 output

## Community Hubs (Navigation)
- Before After elementklasse
- Fotogalerij elementklasse
- Video Placeholder elementklasse
- Beveiliging en elementgedrag
- Bibliotheekregels en werkwijze
- Video Placeholder gedrag

## God Nodes (most connected - your core abstractions)
1. `BeforeAfter` - 36 edges
2. `Fotogalerij` - 36 edges
3. `VideoPlaceholder` - 36 edges
4. `Regels voor deze bibliotheek` - 11 edges
5. `Video Placeholder (README)` - 11 edges
6. `Fotogalerij (README)` - 10 edges
7. `Before After (README)` - 9 edges
8. `Elementen-index` - 6 edges
9. `Beveiliging: gevalideerde embed-URL's en expliciet escapen` - 5 edges
10. `Opslaan in Element Studio herschrijft element.php` - 5 edges

## Surprising Connections (you probably didn't know these)
- `Een element installeren op een site` --semantically_similar_to--> `Werkwijze: leeg element in builder, dan bestanden via API`  [INFERRED] [semantically similar]
  README.md → CLAUDE.md
- `Before After (README)` --references--> `BeforeAfter`  [INFERRED]
  elements/Before_After/README.md → elements/Before_After/element.php
- `Fotogalerij (README)` --references--> `Fotogalerij`  [INFERRED]
  elements/Fotogalerij/README.md → elements/Fotogalerij/element.php
- `Video Placeholder (README)` --references--> `VideoPlaceholder`  [INFERRED]
  elements/Video_Placeholder/README.md → elements/Video_Placeholder/element.php
- `Iframe-URL opgebouwd uit gevalideerd video-id en hostnamen-allowlist` --implements--> `Beveiliging: gevalideerde embed-URL's en expliciet escapen`  [INFERRED]
  elements/Video_Placeholder/README.md → CLAUDE.md

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Eén script via element-dependencies dat op document luistert (alleen front-end)** — elements_before_after_readme_document_script, elements_fotogalerij_readme_document_script, elements_video_placeholder_readme_document_script [INFERRED 0.85]
- **URL-validatie en escapen volgens beveiligingsregel** — claude_beveiliging, elements_before_after_readme_url_validatie, elements_fotogalerij_readme_url_validatie, elements_video_placeholder_readme_iframe_url_opbouw, elements_fotogalerij_readme_dubbel_escapen_data_title [INFERRED 0.85]
- **Installatiestroom: leeg element in Element Studio, bestanden via abilities, controle op site** — claude_werkwijze, claude_element_studio, claude_pdk_theme_options_element_abilities, claude_controle, readme_een_element_installeren_op_een_site [EXTRACTED 1.00]

## Communities (6 total, 3 thin omitted)

### Community 3 - "Beveiliging en elementgedrag"
Cohesion: 0.13
Nodes (21): Beveiliging: gevalideerde embed-URL's en expliciet escapen, Documentatie hoort bij de wijziging, Before After (README), clip-path met CSS-variabele --pos, Script via dependencies, luistert op document, Lege staat (grijze vlakken in builder), Slepen via pointer events op het hele element, Onzichtbare input type=range voor toetsenbord (+13 more)

### Community 4 - "Bibliotheekregels en werkwijze"
Cohesion: 0.17
Nodes (17): Controle: renderen op de site testen, default.css wordt ongewijzigd opgenomen, Oxygen 6 Element Studio, enableVariables (variabelenkiezer), Git: eigen branch en pull request naar main, Mapstructuur (vier Element Studio-bestanden + README), Opslaan in Element Studio herschrijft element.php, pdk-theme-options list/read/write-oxygen-element-file (+9 more)

### Community 5 - "Video Placeholder gedrag"
Cohesion: 0.38
Nodes (7): Click-to-load speler, Standaard icooncontrast 2,2:1 (onder WCAG 1.4.11), Klikscript via dependencies met vlag tegen dubbel binden, Icoon centreren op zwaartepunt van zichtbare vorm, Permissions-Policy-header (cPFence) en wp_headers-filter, Video Placeholder (README), youtube-nocookie.com en Vimeo dnt=1

## Knowledge Gaps
- **3 isolated node(s):** `Eigen lightbox per galerij`, `Kolommen-standaard op telefoons`, `Standaard icooncontrast 2,2:1 (onder WCAG 1.4.11)`
  These have ≤1 connection - possible missing edges or undocumented components.
- **3 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `VideoPlaceholder` connect `Video Placeholder elementklasse` to `Before After elementklasse`, `Video Placeholder gedrag`?**
  _High betweenness centrality (0.433) - this node is a cross-community bridge._
- **Why does `BeforeAfter` connect `Before After elementklasse` to `Beveiliging en elementgedrag`?**
  _High betweenness centrality (0.424) - this node is a cross-community bridge._
- **Why does `Fotogalerij` connect `Fotogalerij elementklasse` to `Before After elementklasse`, `Beveiliging en elementgedrag`?**
  _High betweenness centrality (0.423) - this node is a cross-community bridge._
- **What connects `Eigen lightbox per galerij`, `Kolommen-standaard op telefoons`, `Standaard icooncontrast 2,2:1 (onder WCAG 1.4.11)` to the rest of the system?**
  _3 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Before After elementklasse` be split into smaller, more focused modules?**
  _Cohesion score 0.05555555555555555 - nodes in this community are weakly interconnected._
- **Should `Fotogalerij elementklasse` be split into smaller, more focused modules?**
  _Cohesion score 0.05714285714285714 - nodes in this community are weakly interconnected._
- **Should `Video Placeholder elementklasse` be split into smaller, more focused modules?**
  _Cohesion score 0.05714285714285714 - nodes in this community are weakly interconnected._