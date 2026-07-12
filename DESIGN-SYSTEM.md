# Design System — Exoflora

## Brand Overview

Exoflora est une maison de parfum futuriste. L'identité oscille entre **botanique** et **science-fiction** : fleurs sauvages, air métallique, musc solaire. Le design est sombre, atmosphérique, cinématographique.

---

## Palette

### Couleurs

| Token             | Valeur         | Usage                                        |
| ----------------- | -------------- | -------------------------------------------- |
| `--exo-bg`        | `#050505`      | Fond principal du site                       |
| `--exo-bg-soft`   | `#070707`      | Fond secondaire, dégradé                     |
| `--exo-bg-deep`   | `#030303`      | Fond des sections scroll                      |
| `--exo-cyan`      | `#bfeeff`      | Accent principal (liens, eybrows, glow)      |
| `--exo-purple`    | `#d8c2ff`      | Accent secondaire (radial gradients)          |
| `--white`         | `#ffffff`      | Texte principal, boutons primaires            |
| `--white/55`      | `rgba(255,255,255,0.55)` | Texte secondaire                 |
| `--white/40`      | `rgba(255,255,255,0.40)` | Texte tertiaire                  |
| `--glass`         | `rgba(255,255,255,0.07)` | Fond verre (glassmorphism)       |
| `--glass-border`  | `rgba(255,255,255,0.10)` | Bordure verre                    |

### Usage

- **Texte principal** : `#ffffff` sur fonds sombres
- **Texte secondaire** : `rgba(255,255,255,0.55)` pour descriptions
- **Accent** : `#bfeeff` (cyan clair) pour les eyebrows, tags, hover states
- **Fonds** : `#050505` (presque noir) comme base, dégradés radiaux pour la profondeur

---

## Typographie

| Usage               | Font               | Weight     | Style     |
| ------------------- | ------------------ | ---------- | --------- |
| Body / UI           | Inter              | 300–800    | Normal    |
| Titres display      | Playfair Display   | 400–600    | Italic    |
| Eyebrows / labels   | Inter              | 700–800    | Uppercase, letter-spacing: 0.24em |

### Échelles

- **Eyebrow** : 10–11px, uppercase, tracking large
- **Body** : 13–16px, Inter regular/medium
- **Titres** : clamp(36px, 8.6vw, 150px) selon section
- **Titres display** : Playfair Display italic, letter-spacing: -0.05em à -0.08em

```css
--font-sans: "Inter", system-ui, sans-serif;
--font-playfair: "Playfair Display", serif;
--tracking-exo: -0.02em;
```

---

## Bordures & Coins

| Token                | Valeur         |
| -------------------- | -------------- |
| --radius-sm          | 8px            |
| --radius-md          | 24px           |
| --radius-lg          | 28px           |
| --radius-xl          | 30px           |
| --radius-2xl         | 36px           |
| --radius-full        | 9999px         |
| --border-subtle      | 1px solid rgba(255,255,255,0.10) |
| --border-glass       | 1px solid rgba(255,255,255,0.12) |

---

## Glassmorphism

Pattern récurrent pour les cartes et panneaux :

```css
.glass-card {
  background: linear-gradient(160deg, rgba(255,255,255,0.07), rgba(255,255,255,0.018));
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.1), 0 30px 90px rgba(0,0,0,0.42);
  backdrop-filter: blur(18px);
}
```

---

## Ombres

| Usage               | Valeur                                          |
| ------------------- | ----------------------------------------------- |
| Glass card          | `0 30px 90px rgba(0,0,0,0.42)`                 |
| Carte magnetique    | `0 38px 110px rgba(0,0,0,0.55)` + glow         |
| Texte hero          | `drop-shadow(0 4px 28px rgba(0,0,0,0.85))`     |
| Navigation          | `0 24px 90px rgba(0,0,0,0.35)`                 |

---

## Espacements

- **Padding section** : `py-24` sur mobile, `py-32` à `py-40` sur desktop
- **Gap grilles** : `gap-5` (20px) pour les cartes produits, `gap-12` (48px) pour les layouts
- **Padding cards** : `p-3` à `p-9` selon l'importance
- **Max-width contenu** : `max-w-6xl` (1152px)

---

## Animations

### Timing & easing

```css
--ease-exo: cubic-bezier(0.16, 1, 0.3, 1);
```

Easing utilisé partout : cubique personnalisé, lent au début, rapide à la fin, rebond léger.

### Types d'animation

| Animation         | Déclencheur    | Description                                     |
| ----------------- | -------------- | ------------------------------------------------|
| `heroReveal`      | Page load      | Texte qui apparaît avec blur + translateY       |
| `heroFadeUp`      | Page load      | Éléments secondaires qui fade in                |
| `heroZoom`        | Page load      | Image hero qui dézoome (scale 1.12 → 1)         |
| `.reveal`         | Scroll         | Intersection observer : opacity 0→1, translateY |
| `.text-mask`      | Scroll         | Texte qui se dévoile de bas en haut             |
| `.image-mask`     | Scroll         | Image qui se clip de haut en bas                |
| Scrolling         | Scroll continu | Story, gather, archive : animations liées au %  |
| `magnetic-card`   | Hover          | Carte qui monte de 8px avec glow                |

### Transitions

Toutes les transitions utilisent `cubic-bezier(0.16, 1, 0.3, 1)` avec des durées de 0.35s à 1.25s selon l'importance.

### Reduced motion

Toutes les animations respectent `prefers-reduced-motion: reduce` et se désactivent complètement.

---

## Section scrolls

### Story Scroll
- Sticky section, 560vh de hauteur
- Contenu horizontal qui défile (story-track)
- 5 cartes qui défilent avec parallaxe
- Chapitres actifs mis à jour au scroll

### Cinema Scroll
- 420vh de hauteur
- 3 cadres qui se déplacent/transforment en 3D
- Étapes de progression (Source → Capture → Distill → Release)
- Fond qui se révèle progressivement

### Gather Scroll
- 240vh de hauteur
- Mots éparpillés qui se rassemblent au scroll
- Ghost text + glow progressifs

### Archive Scroll
- 340vh de hauteur
- Grille qui se déploie du centre
- Tuiles avec images, grayscale → couleur

---

## Composants

| Composant           | Fichier                         |
| ------------------- | ------------------------------- |
| Layout              | `src/layouts/Layout.astro`      |
| Header              | `src/components/Header.astro`   |
| Load Intro          | `src/components/LoadIntro.astro`|
| Hero                | `src/components/Hero.astro`     |
| Story Scroll        | `src/components/StoryScroll.astro`|
| Manifesto           | `src/components/Manifesto.astro`|
| Cinema Scroll       | `src/components/CinemaScroll.astro`|
| Gather Scroll       | `src/components/GatherScroll.astro`|
| Archive Scroll      | `src/components/ArchiveScroll.astro`|
| Products            | `src/components/Products.astro` |
| Vision              | `src/components/Vision.astro`   |
| Scent Architecture  | `src/components/ScentArchitecture.astro`|
| Field Notes         | `src/components/FieldNotes.astro`|
| CTA                 | `src/components/CTA.astro`      |
| FAQ                 | `src/components/FAQ.astro`      |
| Footer              | `src/components/Footer.astro`   |

## Images

Toutes les images sont hébergées sur Supabase Storage et Unsplash. Les CSS custom properties dans `Layout.astro` (`--base-image`, `--reveal-image`, etc.) centralisent les URLs.

Pour remplacer une image, modifier la variable dans `src/layouts/Layout.astro`.

---

## Créer une nouvelle page

1. Créer le fichier dans `src/pages/`
2. Utiliser le Layout global (`import Layout from "../layouts/Layout.astro"`)
3. Réutiliser les composants existants ou en créer dans `src/components/`
4. Suivre la palette et les espacements ci-dessus
5. Utiliser les classes Tailwind + les classes globales CSS (`.reveal`, `.glass-card`, etc.)
