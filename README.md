# Fiche de déclaration de travaux — Adekma Ouest

Formulaire web autonome permettant de remplir, générer et envoyer par e-mail
les fiches de déclaration de travaux du garage mécanique (véhicules légers /
poids lourds / semi-remorques, et engins de levage).

## Utilisation

Il n'y a rien à installer ni à configurer : le fichier `index.html` est
autonome (HTML + CSS + JS + modèles PDF + logo, tout est intégré dans ce
seul fichier).

**En local :** double-cliquer sur le fichier l'ouvre dans le navigateur par
défaut.

**Hébergé (GitHub Pages) :** activer GitHub Pages sur ce dépôt
(Settings → Pages, brancher sur la branche principale, dossier racine `/`).
Le fichier s'appelant `index.html`, il sera automatiquement servi comme page
d'accueil du site — l'URL sera du type
`https://tonuser.github.io/tonrepo/`.

## Fonctionnement

1. Choix de la fiche à remplir : véhicules légers / poids lourds /
   semi-remorques, ou engins de levage.
2. Remplissage du formulaire (champs obligatoires : nom du demandeur et
   immatriculation / n° de parc).
3. Ajout possible de 2-3 photos (galerie ou appareil photo), insérées en
   page 2 du PDF en annexe.
4. Signature du demandeur directement à l'écran (souris ou tactile).
5. Un clic sur « Envoyer la fiche » génère le PDF (non modifiable une fois
   généré), le télécharge, et ouvre automatiquement un e-mail pré-rempli
   avec les bons destinataires.

## Destinataires par défaut de l'e-mail

- **À :** garage@adekmaouest.fr
- **Cc :** tony.dupont@adekmaouest.fr, regis.messe@adekmaouest.fr
  (Tony n'est pas mis en copie pour les fiches concernant un véhicule léger
  ou une grue mobile)

Ces adresses sont modifiables directement dans le formulaire avant l'envoi,
et paramétrables dans le code (`DEFAULT_RECIPIENT_TO`, `CC_TONY`,
`CC_REGIS`) si elles doivent changer durablement.

## Modèles PDF sources

Les fichiers `adekma_fiche_travaux_vl_pl_semi.pdf` et
`adekma_fiche_travaux_engins_levage.pdf` sont les modèles PDF remplissables
utilisés par le formulaire (déjà intégrés dans le fichier HTML — fournis ici
séparément à titre de référence/sauvegarde, pas nécessaires pour le
fonctionnement du formulaire).

## Suivi de version

Le numéro de version (visible en haut à droite de la page) suit la
convention `MAJEUR.mineur` : le premier chiffre change pour une évolution
majeure, les deux derniers pour une modification mineure. Il est défini dans
le fichier HTML via la constante `APP_VERSION`.
