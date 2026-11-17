# Cordeau — Design system v0.1

Appli mobile de suivi de chantier pour particuliers (primo-accédants qui rénovent).
Nom de travail : **Cordeau**, le cordeau traceur bleu qu'on claque sur un mur pour tracer une ligne droite. Promesse : garder la ligne de son budget.

## 1. Principes
1. **Le chiffre d'abord.** Les montants sont plus grands que leurs libellés (« 12 480 € » avant « Engagé »).
2. **Calme quand tout va bien, net quand ça dérape.** L'interface reste neutre ; la couleur ne sert qu'à signaler un état (dépassement, à payer, validé).
3. **Une seule audace : la jauge mètre ruban.** Le budget s'affiche comme un mètre ruban gradué. Tout le reste est sobre.
4. **Tout dans la zone du pouce.** Actions principales en bas d'écran ; bouton « Scanner » toujours accessible.
5. **Mouvement utile uniquement** (Emil Kowalski) : réponse à une action, jamais décoratif sur les écrans vus 10 fois par jour.

## 2. Couleurs
| Token | Hex | Rôle |
|---|---|---|
| plâtre | #F3F4F1 | Fond de l'app (60 %) |
| blanc | #FFFFFF | Cartes, feuilles |
| graphite | #1C2127 | Texte principal (30 %) |
| béton | #6B737B | Texte secondaire, icônes inactives |
| joint | #DADDD8 | Séparateurs, contours d'inputs |
| cordeau | #1F4FD8 | Accent : actions, sélection, liens (10 %) |
| cordeau-5 | #1F4FD8 à 6 % | Fond des boutons secondaires, chips actives |
| mètre | #F2C230 | Jauge budget, réserve pour imprévus |
| validé | #1F8A5B | Payé, réception OK |
| alerte | #D9822B | Bientôt dépassé, paiement à venir |
| dépassé | #CF3B32 | Budget dépassé, défaut de réception |

Règles : rouge réservé aux vrais dépassements ; ombres teintées graphite, jamais noir pur.

### Corrections v0.2 (audit WCAG 2.2 / Apple / Material)
- béton → #5E666E (5,28:1 sur plâtre, AA) ; valide/500 → #1A7A50 ; cordeau léger → #E6EAF0 (fond secondaire visible).
- Nouveaux : alerte/600 #B86A1F (graphiques, 3:1), metre/700 #9A7406 (contour de la réserve, 3:1), color/border/input #878E95 (3,3:1 sur blanc), color/border/focus, color/bg/surface-raised, color/bg/scrim, color/text/on-danger.
- Textes de statut toujours en /800 ; jamais de /500 en texte sur plâtre.
- Mode sombre : collection « Couleurs — Sombre » dans Figma (le plan Starter limite à 1 mode par collection) — app #111417, surface #1B2026, surélevée #252B32, texte #ECEEEA / #A4ACB4, accent #3D65E8 / texte accent #93AEFF.

## 3. Typographie
- **Bricolage Grotesque** (titres, montants) — clin d'œil au bricolage, optical size, caractère sans être fantaisiste.
- **Inter** (texte d'interface) — lisibilité, chiffres tabulaires pour les colonnes de montants.

| Style | Police | Taille / interligne | Graisse | Tracking |
|---|---|---|---|---|
| Montant XL | Bricolage | 40 / 44 | 700 | -0,02em, chiffres tabulaires |
| Titre écran | Bricolage | 28 / 32 | 700 | -0,02em |
| Titre section | Bricolage | 20 / 26 | 600 | -0,01em |
| Corps | Inter | 16 / 24 | 400 | 0 |
| Corps fort | Inter | 16 / 24 | 600 | 0 |
| Légende | Inter | 13 / 18 | 400 | +0,01em |

Pas de capitales pour les libellés ; casse de phrase partout. Inputs à 16 px minimum (pas de zoom iOS).

## 4. Espacements, grille, rayons
- Grille de 4 pt : 4, 8, 12, 16, 24, 32, 48.
- Marges d'écran 20 pt ; espacement entre groupes = 2 × espacement interne.
- Rayons hiérarchisés : 8 (inputs, chips), 16 (cartes), 28 (feuilles du bas), pilule (boutons flottants, tags).
- Zones tactiles ≥ 48 × 48 (couvre Apple 44 pt et Android 48 dp), 8 minimum entre deux cibles. Largeur de référence : 390 pt (iPhone 15) ; vérification à 375 pt.

## 5. Élévation
- Niveau 0 : à plat sur le plâtre (listes).
- Niveau 1 : cartes — 0 1px 2px rgba(28,33,39,.06), 0 4px 12px rgba(28,33,39,.05).
- Niveau 2 : feuilles et barre d'onglets — 0 -8px 24px rgba(28,33,39,.08) + scrim graphite 40 %.

## 6. Mouvement (d'après Emil Kowalski / Apple)
| Token | Valeur | Usage |
|---|---|---|
| ease-out | cubic-bezier(0.23, 1, 0.32, 1) | Entrées, menus, toasts |
| ease-in-out | cubic-bezier(0.77, 0, 0.175, 1) | Déplacements à l'écran |
| ease-drawer | cubic-bezier(0.32, 0.72, 0, 1) | Feuilles du bas |
| press | 120 ms, scale 0.97 | Tout élément tapable, au toucher (pas au relâchement) |
| petit | 180 ms | Chips, menus |
| feuille | 400 ms ou ressort amortissement 1.0 / réponse 0.35 | Feuilles du bas, glisser pour fermer avec vitesse |

Règles : jamais d'ease-in ; jamais d'apparition depuis scale(0) (partir de 0.95 + opacité) ; sortie plus rapide que l'entrée ; aucune animation sur la navigation par onglets ; respect de « réduire les animations » (fondus seulement).
Moment fort (pic émotionnel) : réception des travaux validée → le mètre ruban se referme, retour haptique.

## 7. Composants de base
1. Bouton : principal (cordeau plein), secondaire (cordeau léger), discret (texte), destructif × états Repos / Appuyé (couche 12 %) / Désactivé (38 %) / Chargement / Focus (anneau 2 px).
2. Jauge mètre ruban : prévu / engagé / payé, graduations, réserve en jaune mètre.
3. Carte de lot : nom, montant engagé / prévu, mini-jauge, statut.
4. Ligne de document : vignette, type (devis, facture, ticket), artisan, montant, date.
5. Chip de statut : à payer, payé, en retard, dépassé, validé.
6. Champ montant : clavier décimal, suffixe €, chiffres tabulaires.
7. Barre d'onglets : Budget, Travaux, Documents, Plans, Artisans + bouton flottant « Scanner ».
8. Feuille du bas : poignée, glisser pour fermer, 2 hauteurs.
9. Toast (style Sonner) : « Facture ajoutée au lot Cuisine ».
10. État vide : une phrase qui dit quoi faire + l'action (« Scanne ton premier devis »).
11. Repère sur plan : pastille numérotée, couleur selon le type (photo, défaut, tâche).

## Sources
- Emil Kowalski — emil-design-eng, apple-design, mobile-native, ui-cheatsheet (github.com/emilkowalski/skills)
- ceorkm — mobile-app-ui-design (60/30/10, grille 8 pt, zone du pouce, pic-fin)
- Anthropic — frontend-design (éviter les styles par défaut, une seule audace)
