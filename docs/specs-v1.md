# Cordeau — Spécifications v1

## Cible
Primo-accédants qui achètent un appartement ou une maison à rénover et pilotent eux-mêmes leurs artisans. Ils ont peur du dépassement de budget, perdent leurs devis et factures, et ne savent pas comment réceptionner les travaux.

## Modèle de données (v1)
- **Projet** : nom, adresse, surface, budget total, réserve pour imprévus (% conseillé 10-15), date d'emménagement visée.
- **Lot** : projet, nom (Cuisine, Électricité…), budget prévu, statut calculé (À venir / En cours / Payé / Dépassé).
- **Document** : lot, type (devis / facture / acompte / ticket), artisan, montant TTC, date, photo ou PDF, signé oui/non.
- **Paiement** : document, montant, date prévue, date payée.
- **Artisan** : nom, métier, téléphone, e-mail, RGE oui/non.
- **Plan** : projet, image ou PDF, version (avant / après), date.
- **Repère** : plan, x/y relatifs, type (défaut / photo / tâche), lien vers point de réception, photo ou tâche.
- **Point de réception** : lot, intitulé, état (À vérifier / Conforme / Défaut), photo, note.

Règles de calcul : engagé d'un lot = somme des devis signés (ou des factures si pas de devis) ; payé = somme des paiements faits ; dépassé si engagé > prévu ; reste à engager = budget total − engagé.

## Écrans v1 (voir `design/maquettes/`)
1. **Budget** (accueil) : reste à engager, jauge mètre ruban, déjà payé / reste à payer, prochaine échéance, cartes de lots, bouton flottant Scanner.
2. **Détail d'un lot** : montant engagé vs prévu, jauge, liste des documents, paiements à venir, ajout de document.
3. **Scan / ajout d'un document** : photo, champs pré-remplis (saisie manuelle en v1), choix du lot, rangement.
4. **Plans** : import d'un plan, avant/après, repères numérotés, liste des repères.
5. **Réception des travaux** : check-list par lot, défauts avec photo et repère sur le plan, génération d'un PDF « PV avec réserves ».
6. Onboarding court : créer le projet, budget, premiers lots (modèles proposés).

## Hors v1
Lecture automatique des devis (OCR), dossier d'aides MaPrimeRénov', synchro cloud et partage avec le conjoint, export comptable, mesure de pièces au LiDAR.

## Monétisation (à valider)
Gratuit pour 1 lot ou quelques documents, puis achat unique par projet (~24,99 €), avec essai long. À tester avant de coder le paywall.

## Ordre de développement proposé
1. Initialiser Expo + TypeScript + Expo Router + tokens du design system (thème clair/sombre).
2. Composants de base : Bouton, Chip de statut, Jauge mètre ruban, Carte de lot, Ligne de document, Champ, Barre d'onglets.
3. Base locale SQLite + modèle Projet / Lot / Document + logique de budget testée.
4. Écrans Budget et Détail de lot avec données réelles.
5. Ajout de document (photo + saisie), puis Plans, puis Réception + export PDF.
