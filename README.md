# Site clarte-apps.fr — gamme « Clarté »

Site 100 % statique (HTML + CSS, zéro JavaScript, zéro cookie, zéro tracker), prêt pour GitHub Pages ou tout hébergement statique.

## Arborescence

```
site-clarte/
├── index.html                    Accueil (FR)
├── confidentialite/index.html    Politique de confidentialité  → clarte-apps.fr/confidentialite/
├── aide/index.html               Aide / mode d'emploi          → clarte-apps.fr/aide/
├── mentions-legales/index.html   Mentions légales              → clarte-apps.fr/mentions-legales/
├── en/                           Version anglaise (miroir)
│   ├── index.html                → clarte-apps.fr/en/
│   ├── privacy/index.html        → clarte-apps.fr/en/privacy/
│   ├── help/index.html           → clarte-apps.fr/en/help/
│   └── legal/index.html          → clarte-apps.fr/en/legal/
├── style.css                     Feuille unique (tokens Clarté en variables CSS, dark via prefers-color-scheme)
├── favicon.svg                   Favicon (pastille bleue + cercle blanc + loupe)
├── og.png                        Image Open Graph 1200×630
└── fonts/                        ← À CRÉER : polices auto-hébergées (voir ci-dessous)
```

Les URL utilisent des dossiers (`confidentialite/index.html`) pour obtenir `clarte-apps.fr/confidentialite/` sans configuration serveur. Les liens internes pointent vers `…/index.html` explicitement (fonctionne partout, y compris en local) ; GitHub Pages sert aussi la forme courte `…/confidentialite/`. L'URL à déclarer dans la Play Console : `https://clarte-apps.fr/confidentialite/`.

## Avant mise en ligne (3 choses)

1. **Polices auto-hébergées.** Télécharger Atkinson Hyperlegible (400 et 700) depuis fonts.google.com, placer les fichiers dans `fonts/` sous les noms `AtkinsonHyperlegible-Regular.woff2` et `AtkinsonHyperlegible-Bold.woff2`, puis **supprimer dans chaque page les 3 lignes marquées `PREVIEW UNIQUEMENT`** (le lien Google Fonts n'est là que pour la prévisualisation ; en production il violerait la contrainte « aucun appel externe »).
2. **Placeholders à remplacer** :
   - `mentions-legales/index.html` : `[Prénom Nom]` (éditeur) et `[Hébergeur — …]` (garder l'option GitHub Pages ou OVH).
   - `index.html` : vérifier l'URL Play `https://play.google.com/store/apps/details?id=fr.clarteapps.loupe` (id du package définitif).
3. **Domaine** : les balises `og:url` / `og:image` / `hreflang` pointent vers `https://clarte-apps.fr/` — adapter si le domaine final diffère.
4. **Bilingue** : chaque page porte un bouton FR ⇄ EN dans l'en-tête et des balises `hreflang` croisées. Le site est généraliste : les pages Confidentialité et Aide sont structurées par application (section « Clarté Loupe » aujourd'hui ; ajouter un `h2` + contenu par nouvelle app publiée). Toute modification de contenu est à reporter dans les deux langues.

## Tokens (style.css)

Variables CSS reprenant exactement le design system des apps : `--fond`, `--encre`, `--accent`, `--accent-fonce`, `--bandeau-fond`, `--bandeau-texte`, `--surface`, `--bordure`, `--sur-accent` + accents de gamme `--vert`, `--prune`, `--brun`. Mode sombre automatique via `@media (prefers-color-scheme: dark)` (accent vif #8FC3F0, texte sur accent #0B1623 — les accents de gamme sont éclaircis pour rester ≥ 7:1 sur fond sombre).

Règles reprises de la gamme : corps 20 px min (16 px minimum absolu nulle part enfreint), Atkinson Hyperlegible 400/700 uniquement, interlignage 1.6, colonne de lecture 42 rem (~68 ch), cartes rayon 16 px bordure 2 px, boutons ≥ 56 px avec icône + mot, focus visibles 4 px, contrastes AAA.

## Pictogrammes SVG fournis (inline dans les pages)

Traits épais (~3 px sur grille 24 px), cohérents avec les icônes des apps :
loupe (logo/favicon) · lecture ▶ (bouton Play Store) · bouclier (engagement données) · globe hors-ligne · bannière (publicité) · coche (sans aide) · enveloppe (contact) · pilule (Médicaments) · calculatrice · minuteur.

Pour en réutiliser un : copier le bloc `<svg>` correspondant ; couleur pilotée par `currentColor` (sauf pictos des pastilles d'apps, qui portent leur accent en dur sur cercle blanc).

## Accessibilité / SEO

- HTML sémantique : `header`/`main`/`footer`, un seul `h1` par page, landmarks nav étiquetés.
- Navigation clavier complète, `:focus-visible` très contrasté.
- Zoom navigateur 200 % : mise en page fluide, aucune casse (grille « Bientôt » repasse en colonne).
- Chaque page : `title` + `meta description` FR + Open Graph (`og.png`).
- Aucun JavaScript : rien à auditer, pas de bandeau cookies nécessaire.
