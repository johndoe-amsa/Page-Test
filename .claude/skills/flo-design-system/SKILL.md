---
name: flo-design-system
description: >
  Charte graphique et standards UI personnalisés de Flo. Ce skill DOIT être utilisé
  chaque fois que l'utilisateur demande de générer du HTML, du CSS, une page web,
  un composant UI, un dashboard, un formulaire, une carte, un tableau, ou tout élément
  d'interface visuelle. Il DOIT aussi être utilisé quand l'utilisateur demande d'auditer,
  corriger, vérifier ou améliorer du code HTML/CSS existant pour qu'il respecte sa charte.
  Déclencher ce skill dès qu'il est question de : interface, UI, front-end, composant,
  page, layout, dashboard, data-viz, formulaire, bouton, carte, modale, tableau,
  navigation, design system, charte graphique, tokens CSS, ou toute demande de code
  visuel/front-end. Même si l'utilisateur ne mentionne pas explicitement la charte,
  ce skill s'applique à TOUTE génération de HTML/CSS.
---

# Charte Graphique & Standards UI — Flo Design System

## Modes d'utilisation

Ce skill a deux modes. Déterminer lequel appliquer selon la demande :

### Mode GÉNÉRATION
Quand l'utilisateur demande de créer du HTML/CSS (composant, page, dashboard…) :
1. Lire ce fichier + la référence pertinente (voir § Fichiers de référence)
2. Générer du code qui respecte **strictement** tous les tokens et règles ci-dessous
3. Ne jamais hardcoder de valeur — toujours utiliser les variables CSS `var(--…)`
4. Inclure le bloc `:root` complet avec les tokens + le dark mode

### Mode AUDIT
Quand l'utilisateur fournit du code existant à vérifier :
1. Lire ce fichier + la référence pertinente
2. Parcourir le code et lister chaque violation en citant la règle enfreinte
3. Proposer le code corrigé pour chaque violation
4. Structurer le retour : `❌ Violation` → `Règle` → `✅ Correction`

---

## Fichiers de référence

Lire le fichier approprié **avant** de générer ou auditer :

| Besoin | Fichier | Quand le lire |
|---|---|---|
| Boutons, inputs, cartes, modales, badges, tableaux, navigation, séparateurs, tab bar, search field | `references/components.md` | Dès qu'un composant UI est impliqué |
| Graphiques, charts, dashboards, data-viz | `references/data-viz.md` | Dès qu'il y a un graphique ou des données à visualiser |
| Animations, transitions, skeleton loaders, états spéciaux | `references/motion-states.md` | Dès qu'il y a du mouvement ou des états loading/empty/error |

---

## 6 Principes Fondamentaux

Ces règles gouvernent TOUTES les décisions de design :

1. **Le contenu est roi.** Contraste élevé, la donnée est le point focal. Rien ne doit distraire.
2. **Structure par la grille et le vide.** Espacement strict base 8px. Aucun bloc de couleur lourd.
3. **Typographie "Engineered".** Letter-spacing négatif sur les titres. Dense, technique, précis.
4. **États toujours visibles.** Focus, Hover, Active, Disabled — chaque état interactif doit être visuellement distinct.
5. **Élévation sans ombre.** `backdrop-blur` + bordures pour détacher les éléments flottants. Jamais de `box-shadow` lourde.
6. **Perception de vitesse.** Animations courtes, skeleton loaders, transitions instantanées.

---

## Tokens de Design (Variables CSS) — SOURCE DE VÉRITÉ

**Ne jamais hardcoder les valeurs. Toujours utiliser `var(--…)`.**

Tout fichier HTML généré DOIT inclure ce bloc `:root` complet :

```css
:root {
  /* Couleurs — Light Mode */
  --color-bg:           #FFFFFF;
  --color-bg-secondary: #FAFAFA;
  --color-bg-tertiary:  #F2F2F2;

  --color-text:         #000000;
  --color-text-muted:   #666666;
  --color-text-subtle:  #999999;

  --color-border:       #EAEAEA;
  --color-border-strong:#000000;
  --color-border-focus: #000000;

  /* Couleurs Sémantiques — JAMAIS décoratives */
  --color-success:      #0070F3;
  --color-error:        #EE0000;
  --color-warning:      #F5A623;

  /* Couleurs Data-Viz (graphiques EXCLUSIVEMENT) */
  --color-data-1:       #0070F3;
  --color-data-2:       #06B6D4;
  --color-data-3:       #7928CA;
  --color-data-4:       #FF0080;
  --color-data-5:       #FF4D4D;
  --color-data-6:       #F5A623;
  --color-data-7:       #10B981;
  --color-data-grid: var(--color-border);

  /* Typographie */
  --font-sans:   'Geist', system-ui, -apple-system, sans-serif;
  --font-mono:   'Geist Mono', Menlo, monospace;

  /* Espacement (base 8px) */
  --space-1:  4px;
  --space-2:  8px;
  --space-3:  12px;
  --space-4:  16px;
  --space-6:  24px;
  --space-8:  32px;
  --space-12: 48px;
  --space-16: 64px;

  /* Radius */
  --radius-sm:   6px;
  --radius-md:   8px;
  --radius-lg:  12px;
  --radius-full: 9999px;

  /* Élévation (3 niveaux UNIQUEMENT) */
  --elevation-0: none;
  --elevation-1: 0 4px 12px rgba(0,0,0,0.05);
  --elevation-2: 0 8px 32px rgba(0,0,0,0.08);

  /* Backdrop (modales, menus flottants) */
  --backdrop:    blur(12px);
  --backdrop-bg: rgba(255,255,255,0.85);

  /* Transitions */
  --duration-fast:   150ms;
  --duration-base:   200ms;
  --duration-slow:   300ms;
  --ease-out:        cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out:     cubic-bezier(0.4, 0, 0.2, 1);
}

/* Dark Mode — préférence système (sauf override manuel light) */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --color-bg:           #000000;
    --color-bg-secondary: #0A0A0A;
    --color-bg-tertiary:  #111111;

    --color-text:         #EDEDED;
    --color-text-muted:   #888888;
    --color-text-subtle:  #555555;

    --color-border:       #333333;
    --color-border-strong:#FFFFFF;
    --color-border-focus: #FFFFFF;

    --backdrop-bg: rgba(0,0,0,0.85);
    --elevation-1: 0 4px 12px rgba(0,0,0,0.3);
    --elevation-2: 0 8px 32px rgba(0,0,0,0.5);

    /* Data-Viz Dark Mode */
    --color-data-1: #3291FF;
    --color-data-2: #22D3EE;
    --color-data-3: #8A2BE2;
    --color-data-4: #FF1493;
    --color-data-5: #FF5C5C;
    --color-data-6: #FBBF24;
    --color-data-7: #34D399;
    --color-data-grid: var(--color-border);
  }
}

/* Dark Mode — forcé manuellement via toggle */
:root[data-theme="dark"] {
  --color-bg:           #000000;
  --color-bg-secondary: #0A0A0A;
  --color-bg-tertiary:  #111111;

  --color-text:         #EDEDED;
  --color-text-muted:   #888888;
  --color-text-subtle:  #555555;

  --color-border:       #333333;
  --color-border-strong:#FFFFFF;
  --color-border-focus: #FFFFFF;

  --backdrop-bg: rgba(0,0,0,0.85);
  --elevation-1: 0 4px 12px rgba(0,0,0,0.3);
  --elevation-2: 0 8px 32px rgba(0,0,0,0.5);

  /* Data-Viz Dark Mode */
  --color-data-1: #3291FF;
  --color-data-2: #22D3EE;
  --color-data-3: #8A2BE2;
  --color-data-4: #FF1493;
  --color-data-5: #FF5C5C;
  --color-data-6: #FBBF24;
  --color-data-7: #34D399;
  --color-data-grid: var(--color-border);
}
```

---

## Palette — Règles Strictes

- L'interface est **monochrome**. Noir, blanc, gris uniquement.
- Les couleurs sémantiques (`success`, `error`, `warning`) sont réservées aux états fonctionnels. **Jamais décoratives.**
- Les couleurs `--color-data-*` sont **exclusivement** pour les graphiques (SVG, Canvas, charts). Jamais pour des boutons, badges, textes d'interface, ou fonds de layout.
- La couleur seule ne doit **jamais** être le seul vecteur d'information — toujours doubler d'une icône ou d'un texte.

---

## Typographie

### Polices
- **Corps / UI :** `var(--font-sans)` → Geist, system-ui, -apple-system, sans-serif
- **Code / Data :** `var(--font-mono)` → Geist Mono, Menlo, monospace

### Échelle Typographique

| Rôle | Taille | Weight | Line-height | Letter-spacing | Casse |
|---|---|---|---|---|---|
| Titre App (H1) | 36–48px | 700 | 1.1 | −0.04em | Titre |
| Titre Section (H2) | 24–32px | 600 | 1.2 | −0.03em | Titre |
| Titre Carte (H3) | 18–20px | 600 | 1.3 | −0.02em | Titre |
| Corps (défaut) | 16px | 400 | 1.5 | 0 | Normal |
| Corps (dense) | 14px | 400 | 1.5 | 0 | Normal |
| Label / Surtitre | 12px | 500 | 1 | +0.05em | UPPERCASE |
| Code inline | 13px | 400 | 1.6 | 0 | Normal |

### Règles typo strictes
- **Jamais** de texte en dessous de 12px.
- **Maximum 3 poids** de fonte dans une même interface.
- Labels 12px uppercase → toujours en `var(--color-text-muted)`.
- Code inline → `var(--font-mono)`, fond `var(--color-bg-tertiary)`, `padding: 2px 6px`, `border-radius: var(--radius-sm)`.
- Tout affichage de valeur numérique (KPI, tableau, date, compteur) doit utiliser `font-variant-numeric: tabular-nums` pour garantir l'alignement des colonnes.

---

## Iconographie

- **Bibliothèque :** Lucide Icons ou Radix Icons exclusivement.
- **Style :** Ligne (stroke) uniquement — **jamais** d'icônes remplies (fill).
- **Stroke-width :** `1.5px` (compact) ou `2px` (accent). Constant dans toute l'interface.
- **Tailles :** `16px` (inline/label), `20px` (bouton/action), `24px` (accent décoratif max).
- **Alignement :** Toujours aligné verticalement avec le texte adjacent.

---

## Espacement & Layout

### Grille
- **Desktop :** 12 colonnes, `gap: 24px`, `max-width: 1200px`, centré.
- **Tablette (768–1024px) :** 8 colonnes, `gap: 16px`.
- **Mobile (<768px) :** 4 colonnes ou linéaire, `gap: 16px`, padding `16px`.

### Breakpoints
```css
--bp-mobile:  480px;
--bp-tablet:  768px;
--bp-desktop: 1024px;
--bp-wide:    1280px;
```

### Règles d'espacement
- Toujours des multiples de 8px : `4, 8, 12, 16, 24, 32, 48, 64px`.
- **Padding de page :** `64px` (desktop) → `32px` (tablette) → `16px` (mobile).
- **Gap entre sections :** `48–64px`.
- **Gap entre composants dans une section :** `16–24px`.
- **Padding interne d'une carte :** `24px`.

### Layout Dashboard (Sidebar + Main)

**Desktop :** Sidebar `260px` fixe, `position: sticky`, hauteur `100vh - nav`. Séparée du contenu principal par `border-right: 1px solid var(--color-border)`.

**Mobile (`≤768px`) :** La sidebar perd sa position sticky et devient une **bande horizontale** en haut du contenu (`width: 100%`, `height: auto`, `border-right: none`, `border-bottom: 1px solid var(--color-border)`). Les filtres s'organisent en `flex-direction: row; flex-wrap: wrap`.

---

## Élévation & Profondeur

3 niveaux UNIQUEMENT. Aucune shadow arbitraire.

| Niveau | Valeur | Usage |
|---|---|---|
| 0 | `none` | Flat — cartes par défaut |
| 1 | `var(--elevation-1)` | Card hover, dropdowns |
| 2 | `var(--elevation-2)` | Modales, command palette |

Pour les éléments flottants : toujours combiner `elevation-2` + `backdrop-filter: blur(12px)` + `border: 1px solid var(--color-border)`.

---

## Accessibilité — Obligatoire

### Focus (ne jamais supprimer)
```css
*:focus { outline: none; }
*:focus-visible {
  outline:        2px solid var(--color-border-focus);
  outline-offset: 2px;
  border-radius:  var(--radius-sm);
}
```

### Contrastes WCAG AA
| Texte | Rapport minimum |
|---|---|
| Corps (16px+) | 4.5:1 |
| Grand texte (18px+) | 3:1 |
| Composants UI | 3:1 |

### Règles
- Tous les inputs ont un `<label>` associé (jamais placeholder seul).
- Icônes décoratives : `aria-hidden="true"`.
- Icônes fonctionnelles : `aria-label` explicite.
- Couleurs sémantiques jamais seul vecteur d'info.
- Modales : focus-trap + fermeture `Escape`.
- Ordre de tabulation logique et visible.
- Toujours respecter `prefers-reduced-motion`.

---

## Do / Don't — Checklist Rapide

### ✅ TOUJOURS
- Tokens CSS `var(--…)` — jamais de valeurs hardcodées
- Chaque bloc de tokens dark mode doit apparaître deux fois : dans `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) }` ET dans `:root[data-theme="dark"]`
- Skeleton loaders reprenant la géométrie exacte du contenu
- `focus-visible` sur tous les éléments interactifs
- Transitions sur `transform` et `opacity` uniquement
- `border-radius` cohérent (pill = bouton, 12px = carte, 6px = badge)
- États vides et d'erreur explicites
- `prefers-reduced-motion`

### ❌ JAMAIS
- Spinner plein écran
- `box-shadow` hors des 3 niveaux définis
- Gradients décoratifs
- Couleur seule pour info sémantique
- Icônes remplies (fill)
- Animer `width`, `height`, `top`, `left`, `margin`, `padding` — **sauf exception explicite** : l'expansion d'un champ de recherche au focus (`.search-field__input`) peut animer `width` car l'effet est fonctionnel et l'élément reste dans le flux
- Supprimer `outline` sans `:focus-visible`
- Texte < 12px
- Plus de 3 poids de fonte
- Classes Tailwind mélangées avec du CSS custom pour les mêmes propriétés
