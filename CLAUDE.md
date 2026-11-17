# Cordeau — appli mobile de suivi de chantier

Lis ce fichier en entier avant de coder. Le porteur du projet est Victor, étudiant en école de commerce, développeur solo. Réponds-lui en français.

## Le produit
Carnet de chantier pour les **particuliers qui rénovent leur logement**, en priorité les primo-accédants qui achètent un bien à rénover. Promesse : garder la ligne de son budget de travaux (le nom vient du cordeau traceur bleu des maçons).

Concurrents connus (petits, aucun dominant) : DomuTrack (Android), Chantiers Facile, Ma-Gestion-Rénovation.fr. Différenciation visée : la check-list de réception des travaux (PV de réserves) et le dossier d'aides (alerte « ne signe pas le devis avant de déposer ta demande MaPrimeRénov' »), une jauge budget très lisible, iOS + Android dès le départ.

Specs détaillées : `docs/specs-v1.md`. Design system : `docs/design-system.md` + `design/tokens.json`. Maquettes de référence : `design/maquettes/*.dc.html` (HTML/CSS lisible, ce n'est pas du code de l'app).

## Stack proposée (à confirmer avec Victor avant d'initialiser)
- **Expo (React Native) + TypeScript**, Expo Router pour la navigation (5 onglets : Budget, Travaux, Documents, Plans, Artisans).
- **Données en local d'abord** : expo-sqlite (ou Drizzle sur SQLite), pas de compte obligatoire en v1. Synchro cloud plus tard.
- Scan : expo-camera / expo-image-picker ; lecture des montants sur l'appareil (ML Kit / Vision) en v2, saisie manuelle assistée en v1.
- Animations : react-native-reanimated + react-native-gesture-handler (voir `.claude/skills/animate-expo`).
- Tests : Jest + React Native Testing Library sur la logique de budget.

## Règles de design (non négociables)
- Utiliser **uniquement les tokens** de `design/tokens.json` (couleurs claires ET sombres, espacements 4-pt, rayons, typo, mouvement). Pas de hex en dur dans les composants.
- Montants : plus grands que leurs libellés, chiffres tabulaires, jamais tronqués (le libellé se tronque, pas le montant).
- Couleur jamais seule pour une info (WCAG 1.4.1) : statut = couleur + icône + texte. Rouge réservé aux vrais dépassements.
- Contrastes AA vérifiés : texte 4,5:1, éléments graphiques 3:1. Le gris secondaire est #5E666E (pas #6B737B).
- Zones tactiles ≥ 48, inputs en 16 (pas de zoom iOS), Dynamic Type / taille de police Android jusqu'à 200 %.
- Mouvement (skills Emil Kowalski dans `.claude/skills/`) : retour au toucher immédiat (scale 0.97, 120 ms ease-out), pas d'animation sur la navigation par onglets, feuilles en ressort, tout supprimé ou remplacé par un fondu si « réduire les animations ».
- Mode sombre prévu dès le départ via les tokens `color.dark`.

## Façon de travailler
- Petites étapes, une fonctionnalité à la fois, testée avant de passer à la suivante.
- Explique simplement ce que tu fais : Victor apprend en même temps.
- Commits clairs en français ; branche par fonctionnalité, PR vers `main`.
- Ne publie rien sur les stores et ne crée aucun service payant sans accord explicite.
