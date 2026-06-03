# MailBotEBP-releases
## Présentation

**Assistant EBP Paramètre Mail** est un outil complémentaire à EBP Invoicing qui automatise l'envoi de mails depuis vos données de gestion.

Sans intervention manuelle, il génère et expédie des documents (factures, relances, bons de commande…) directement depuis votre base EBP, avec ou sans pièce jointe PDF.

### Ce que ça fait

- Configure votre boîte mail SMTP en quelques étapes
- Génère les documents PDF à partir d'EBP et les joint automatiquement
- Envoie les mails selon des modèles personnalisables
- Planifie les envois via le Planificateur de tâches Windows
- Suit les envois en temps réel et conserve un historique CSV

### Pour qui ?

Toute entreprise utilisant **EBP Invoicing** qui souhaite automatiser ses envois de documents sans recourir à une solution complexe ou coûteuse.

### Comment ?

Vous créez un **template de mail** (objet, corps, pièce jointe) directement dans l'assistant. Les destinataires et les données du mail sont issus d'une **vue EBP** que vous gérez avec vos outils habituels EBP. La fréquence d'envoi est pilotée par le **Planificateur de tâches Windows** : quotidien, hebdomadaire, ou à la demande.

## Installation

### Prérequis

Avant de lancer l'installation, assurez-vous de disposer des éléments suivants :

- **EBP Invoicing** installé et configuré sur le poste
- **Un compte administrateur EBP** (login et mot de passe)
- **Un compte mail avec accès SMTP** (ex. Gmail, Outlook, serveur d'entreprise)

> Le .NET Framework requis est installé automatiquement par le setup si nécessaire.

### Étapes

**1. Télécharger le setup**
Téléchargez `setup.exe` et lancez-le en tant qu'administrateur.

**2. Suivre l'assistant d'installation**
L'installeur déploie l'application et ses dépendances automatiquement.

**3. Première exécution**
Au premier lancement, l'assistant vous guide pour configurer :
- Le **raccourci EBP** (.ebp) à utiliser
- Votre **identifiant et mot de passe EBP**
- Votre **adresse mail expéditeur**

**4. Configurer la boîte mail SMTP**
Depuis le menu principal, choisissez *Editer une boîte mail SMTP* pour renseigner le serveur, le port et le mot de passe de votre compte mail.

Une fois ces étapes complétées, l'application est prête à l'emploi.

## Utilisation

L'application se pilote depuis une interface en ligne de commande accessible via le raccourci installé sur votre bureau.

### Menu principal

Au lancement, le menu principal propose cinq actions :

| # | Option | Rôle |
|---|--------|------|
| 1 | Editer un utilisateur EBP | Enregistrer ou mettre à jour les identifiants EBP |
| 2 | Editer un modèle de mail | Créer ou modifier un template de mail |
| 3 | Editer une commande | Configurer et générer la commande d'envoi |
| 4 | Editer une boîte mail SMTP | Paramétrer le compte mail expéditeur |
| 5 | Envoyer le fichier de log | Transmettre les logs en cas de problème |

---

### Étape 1 — Créer un modèle de mail

Un modèle définit le contenu de vos mails. Il est associé à un **type de document EBP** et à une **vue EBP** qui fournit les données (destinataires, variables, filtres).

#### Types de document pris en charge

- Echéancier
- Facture / Avoir
- Commande
- Facture achat / Avoir achat
- Commande achat

#### Configuration du modèle

Via *Editer un modèle de mail*, vous configurez :
- Le **type de document** et la **vue EBP** source des données
- L'**objet** et le **corps** du mail
- L'éventuelle **pièce jointe PDF**
- Le **champ EBP** dans lequel l'envoi sera enregistré une fois le mail expédié

> **Conseil** : créez un champ personnalisé dans la table EBP correspondant au type de document (ex. *MailEnvoye*, *DateEnvoiMail*). Le programme y enregistre automatiquement l'envoi, ce qui permet d'éviter les doublons et de tracer les envois directement dans EBP.

> La vue EBP se gère avec vos outils habituels EBP (filtres, colonnes, tri). L'application l'exploite telle quelle.

---

### Étape 2 — Configurer une commande

Via *Editer une commande*, vous associez un modèle à une planification. L'assistant génère automatiquement la **ligne de commande** à copier dans le Planificateur de tâches Windows.

#### Redirection des mails

Avant de basculer en production, il est vivement conseillé de renseigner une **adresse de redirection**. Pendant cette phase de validation, tous les mails sont redirigés vers cette adresse — le client final ne reçoit rien.

Cela vous permet de vérifier le contenu, la mise en forme et les pièces jointes dans des conditions réelles, sans risque d'envoi prématuré.

Une fois les envois validés, il suffit de supprimer l'adresse de redirection pour basculer en production.

#### Test et suivi

Vous pouvez **tester la commande** directement depuis l'assistant avant de la planifier, et ouvrir la fenêtre de suivi pour vérifier les envois en temps réel.
---

### Étape 3 — Planifier les envois

Collez la commande générée dans une **tâche planifiée Windows** (Planificateur de tâches). Définissez la fréquence souhaitée : quotidienne, hebdomadaire, horaire, ou à la demande.

À chaque exécution, l'application :
1. Interroge la vue EBP
2. Génère les mails (et les PDF si nécessaire)
3. Envoie les mails via votre boîte SMTP
4. Archive les envois et met à jour l'historique

---

### Suivi des envois

Une fenêtre de suivi en temps réel est disponible pendant l'exécution. Elle affiche l'état de chaque mail (en attente, envoyé, erreur).

Un fichier **Report.csv** est également généré dans le dossier de suivi. Il recense chaque document envoyé avec succès (référence, modèle, catégorie, date d'envoi) pour une exploitation ultérieure.

---

### En cas de problème

Consultez le fichier de log via *Envoyer le fichier de log* pour transmettre les détails techniques au support.
