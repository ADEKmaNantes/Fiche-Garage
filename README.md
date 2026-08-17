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
   généré), le télécharge, et l'envoie **automatiquement par e-mail** aux
   bons destinataires — sans passer par la messagerie personnelle de la
   personne qui remplit la fiche.

## Envoi automatique de l'e-mail

L'envoi ne passe pas par un lien `mailto:` classique : le PDF est transmis
à un script Google Apps Script (compte dédié
`travaux.garage.adekmaouest@gmail.com`) qui envoie lui-même l'e-mail avec
le PDF en pièce jointe. L'expéditeur est donc toujours ce compte dédié,
quel que soit le collègue qui a rempli la fiche.

L'URL de ce script est définie dans le fichier HTML via la constante
`APPS_SCRIPT_URL`. Si ce webhook doit être recréé ou changé (nouveau
déploiement Apps Script), il faut mettre à jour cette constante.

**En cas d'échec de l'envoi automatique** (panne réseau, script
indisponible…), le formulaire affiche un message d'erreur avec deux
options : réessayer l'envoi automatique, ou basculer sur un envoi manuel
via la messagerie de l'utilisateur (`mailto:`, avec le PDF déjà téléchargé
à joindre soi-même).

## Matériel attitré

Chaque véhicule/engin demande désormais si le matériel est attitré à la
personne qui remplit la fiche (choix obligatoire à deux options : "m'est
attitré" / "ne m'est pas attitré", section "Véhicule/Engin concerné") —
utile pour distinguer le titulaire habituel du matériel de la personne qui
remplit la fiche, notamment en cas de choc ou d'accident. Le formulaire ne
demande pas à qui le matériel appartient si ce n'est pas le demandeur.

## Contexte de la déclaration et certification

Chaque fiche demande maintenant de préciser le contexte de la demande
(obligatoire) : entretien / maintenance, panne / anomalie constatée, ou
choc / accident pendant l'utilisation. Une case de certification (« Je
certifie l'exactitude des informations renseignées ci-dessus... ») doit
être cochée juste avant la signature pour pouvoir envoyer la fiche —
objectif : responsabiliser la personne qui déclare et limiter les
déclarations inexactes.

## Journalisation dans Google Sheets

En plus de l'e-mail, chaque envoi ajoute automatiquement une ligne dans un
tableau de suivi (Google Sheets nommé « Suivi Fiches Travaux - Garage
Adekma Ouest »), créé et rempli par le même script Apps Script. Colonnes :
date d'envoi, type de fiche, demandeur, immatriculation / n° de parc,
contexte de la déclaration, type de véhicule/engin, urgence, description,
nom du fichier PDF, destinataire, Cc.

Ce fichier se crée tout seul dans le Drive du compte
`travaux.garage.adekmaouest@gmail.com` lors du tout premier envoi — rien à
préparer à l'avance.

Le code du script Apps Script correspondant (`doPost`, `getOrCreateSheet`,
`logToSheet`) est géré séparément, directement dans l'éditeur
script.google.com — il ne fait pas partie de ce dépôt.

## Destinataires par défaut de l'e-mail

- **À :** garage@adekmaouest.fr
- **Cc :** travaux.garage.adekmaouest@gmail.com

Ces adresses sont modifiables directement dans le formulaire avant l'envoi,
et paramétrables dans le code (`DEFAULT_RECIPIENT_TO`, `DEFAULT_RECIPIENT_CC`)
si elles doivent changer durablement.

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
