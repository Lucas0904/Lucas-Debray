# La bastide : check-list partagée

Petite appli web pour se répartir les tâches de remise en état de la bastide.
Elle s'ouvre par un simple lien sur n'importe quel téléphone, sans compte, et se synchronise en direct.

- **Hébergement** : GitHub Pages (gratuit), à l'adresse `https://lucas0904.github.io/Lucas-Debray/`
- **Stockage partagé** : Firebase Firestore (gratuit pour cet usage), compte Google requis pour Lucas seulement

## Installation (une seule fois, depuis le PC Windows, environ 15 minutes)

Tout se fait dans le navigateur (Edge ou Chrome). Rien à installer.

### Étape 1 : créer la base de données Firebase

1. Ouvre <https://console.firebase.google.com> et connecte-toi avec ton compte Google.
2. Clique sur **Créer un projet** (ou **Commencer avec un projet Firebase**).
3. Nom du projet : `bastide`. Coche l'acceptation des conditions, puis **Continuer**.
4. Si on te propose Gemini ou Google Analytics : **désactive-les** (inutiles ici), puis **Créer le projet**. Attends, puis **Continuer**.
5. Dans le menu de gauche, ouvre **Créer** (ou **Build**) puis **Firestore Database**.
6. Clique sur **Créer une base de données**.
   - Édition : **Standard** si on te le demande.
   - Emplacement : **eur3 (Europe)** ou **europe-west9 (Paris)**. Clique **Suivant**.
   - Mode : **Démarrer en mode production**. Clique **Créer**.
7. Une fois la base créée, ouvre l'onglet **Règles** (en haut de la page Firestore).
8. Efface tout le texte et colle à la place le contenu du fichier [`firestore.rules`](firestore.rules) de ce dépôt
   (ouvre-le sur GitHub, clique sur l'icône **Copier** en haut à droite du fichier).
9. Clique sur **Publier**.

### Étape 2 : récupérer la configuration

1. Toujours dans Firebase, clique sur la **roue dentée** à côté de « Vue d'ensemble du projet » (en haut à gauche), puis **Paramètres du projet**.
2. En bas de l'onglet **Général**, section « Vos applications », clique sur l'icône **`</>`** (Web).
3. Surnom de l'application : `bastide`. **Ne coche pas** « Firebase Hosting ». Clique **Enregistrer l'application**.
4. Firebase affiche un bloc de code. Repère la partie `const firebaseConfig = { ... };` : six lignes `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`. Garde cette page ouverte.

> Ces valeurs ne sont pas des mots de passe : elles sont faites pour être visibles dans une page web. La protection vient des règles de l'étape 1 et du code secret contenu dans le lien de la liste.

### Étape 3 : coller la configuration dans l'appli

Deux possibilités :

- **La plus simple** : copie le bloc `firebaseConfig` et envoie-le à Claude, qui l'ajoutera.
- **Toi-même sur GitHub** :
  1. Ouvre <https://github.com/Lucas0904/Lucas-Debray>.
  2. En haut à gauche de la liste des fichiers, clique sur le menu des branches et choisis **`claude/epic-hypatia-aj7ik7`**.
  3. Clique sur le fichier **`config.js`**, puis sur l'icône **crayon** (Modifier) en haut à droite.
  4. Remplis les six valeurs entre les guillemets, en recopiant celles de Firebase. Exemple : `apiKey: "AIzaSy...",`
  5. Clique sur le bouton vert **Commit changes...**, puis à nouveau **Commit changes**.

### Étape 4 : mettre l'appli en ligne avec GitHub Pages

1. Sur <https://github.com/Lucas0904/Lucas-Debray>, clique sur l'onglet **Settings** (tout à droite, sous le nom du dépôt).
2. Dans le menu de gauche, clique sur **Pages**.
3. Sous « Build and deployment » :
   - **Source** : `Deploy from a branch`
   - **Branch** : choisis `claude/epic-hypatia-aj7ik7`, dossier `/ (root)`, puis **Save**.
4. Attends 1 à 2 minutes et recharge la page : GitHub affiche « Your site is live at `https://lucas0904.github.io/Lucas-Debray/` ».

Si GitHub refuse la branche (règle de protection), dis-le à Claude : il proposera de fusionner dans `master`.

### Étape 5 : créer la liste et l'envoyer à ton père

1. Sur ton téléphone, ouvre `https://lucas0904.github.io/Lucas-Debray/`.
2. Touche **Créer la liste**. L'adresse se complète avec un code (`#l=...`) : c'est votre liste.
3. Touche le bouton **Partager** (flèche vers le haut, en haut à droite) et envoie le lien à ton père par SMS ou WhatsApp.
4. Ton père ouvre ce lien : il voit la même liste, sans compte.

**Important** : envoyez-vous toujours le lien complet avec son code. L'adresse sans code ouvre un écran d'accueil ; si quelqu'un y touche « Créer la liste », il obtient une nouvelle liste vide, distincte de la vôtre.
Une fois le lien ouvert une fois, le téléphone retient la liste.

### Astuce : l'ajouter à l'écran d'accueil

- **iPhone (Safari)** : bouton Partager, puis **Sur l'écran d'accueil**.
- **Android (Chrome)** : menu **⋮**, puis **Ajouter à l'écran d'accueil**.

## Utilisation

- **Onglets** : Tout, Ce soir, Demain matin, Géraldine, Au départ, À répartir. Le chiffre indique les tâches restantes.
- **Ajouter** : la tâche prend le moment de l'onglet ouvert (dans « Tout » ou « À répartir », elle va dans « À répartir »).
- **Cocher ou décocher** : touche la case. Les tâches faites descendent en bas, barrées.
- **Changer le moment ou supprimer** : touche l'étiquette colorée à droite de la tâche. La suppression demande confirmation.
- **Thème** : bouton rond en haut à droite (automatique, clair, sombre).
- **Hors réseau** : l'appli continue de fonctionner ; les changements partent dès le retour du réseau.

## Fichiers

| Fichier | Rôle |
| --- | --- |
| `index.html` | L'appli (interface et synchronisation) |
| `config.js` | Configuration Firebase à remplir |
| `firestore.rules` | Règles de sécurité à coller dans Firebase |
| `manifest.webmanifest`, `icon.svg` | Icône pour l'écran d'accueil |
