
**1. Création de l'environnement Docker :**

*   Choisissez une image Docker basée sur Ubuntu (ou une autre distribution Linux) :

```bash
docker pull ubuntu:latest
```

*   Lancez un conteneur interactif avec un nom personnalisé :

```bash
docker run -it --name environnement_securise ubuntu bash
```

**2. Création de l'arborescence :**

*   À l'intérieur du conteneur, créez l'arborescence de dossiers :

```bash
mkdir -p /data/public /data/confidentiel/tres_confidentiel
```

L'option `-p` dans la commande `mkdir` signifie "parents". Elle permet de créer tous les répertoires parents manquants dans le chemin spécifié.

Par exemple, si le répertoire `/data` n'existe pas, la commande `mkdir -p /data/public /data/confidentiel/tres_confidentiel` va créer :

1.  Le répertoire `/data`
2.  Le répertoire `/data/public`
3.  Le répertoire `/data/confidentiel`
4.  Le répertoire `/data/confidentiel/tres_confidentiel`

Sans l'option `-p`, la commande `mkdir` échouerait si le répertoire parent n'existait pas.


**3. Création et manipulation de fichiers :**

*   Créez des fichiers texte (`.txt`) dans chaque répertoire :

```bash
echo "données publiques" > /data/public/public.txt
echo "informations confidentielles" > /data/confidentiel/confidentiel.txt
echo "informations très confidentielles" > /data/confidentiel/tres_confidentiel/tres_confidentiel.txt
```

**Pourquoi utiliser echo dans ce cas ?**

Dans l'exercice de création de dossiers et de fichiers avec restrictions, nous voulons non seulement créer des fichiers, mais aussi y écrire du contenu spécifique (par exemple, "données publiques"). La commande echo combinée à la redirection (`) est le moyen le plus simple et direct d'y parvenir en une seule étape.

Si nous utilisions touch pour créer le fichier, nous devrions ensuite utiliser un éditeur de texte (comme vim ou nano) pour ouvrir le fichier et y écrire le contenu, ce qui nécessiterait une étape supplémentaire.

**En résumé :**

Utilisez touch lorsque vous voulez créer un fichier vide ou mettre à jour l'horodatage d'un fichier.
Utilisez echo avec la redirection (>) lorsque vous voulez créer un fichier et y écrire du contenu en même temps.

*   Utilisez `vim` ou `nano` pour modifier les fichiers :

```bash
vim /data/public/public.txt
```

**4. Gestion des permissions :**

*   Utilisez `chmod` pour modifier les permissions :

```bash
chmod 644 /data/public/public.txt          # Lecture/écriture pour le propriétaire, lecture seule pour les autres
chmod 640 /data/confidentiel/confidentiel.txt  # Lecture/écriture pour le propriétaire, lecture seule pour le groupe
chmod 600 /data/confidentiel/tres_confidentiel/tres_confidentiel.txt  # Lecture/écriture pour le propriétaire uniquement
chmod 750 /data/confidentiel                # Lecture/écriture/exécution pour le propriétaire, exécution pour le groupe
chmod 700 /data/confidentiel/tres_confidentiel # Lecture/écriture/exécution pour le propriétaire uniquement
```

*   Utilisez `chown` pour modifier le propriétaire (si nécessaire) :

Pour changer le propriétaire et le groupe d'un fichier avec `chown`, l'utilisateur et le groupe doivent exister au préalable sur le système. Voici comment créer un utilisateur et un groupe, puis utiliser `chown` dans ce contexte :

**A. Créer un groupe :**

*   **Commande :** `groupadd <nom_du_groupe>`
*   **Explication :** Cette commande crée un nouveau groupe avec le nom spécifié.
*   **Exemple :** `groupadd marketing` (crée un groupe nommé "marketing")

**B. Créer un utilisateur :**

*   **Commande :** `useradd -m -g <nom_du_groupe> <nom_d'utilisateur>`
*   **Explication :** 
    *   `-m` : Crée automatiquement le répertoire personnel de l'utilisateur.
    *   `-g <nom_du_groupe>` : Ajoute l'utilisateur au groupe spécifié.
*   **Exemple :** `useradd -m -g marketing alice` (crée un utilisateur nommé "alice" et l'ajoute au groupe "marketing")

**C. Définir un mot de passe pour l'utilisateur :**

*   **Commande :** `passwd <nom_d'utilisateur>`
*   **Explication :** Cette commande vous invite à entrer et à confirmer un mot de passe pour l'utilisateur.
*   **Exemple :** `passwd alice`

**D. Utiliser `chown` pour changer le propriétaire et le groupe d'un fichier :**

*   **Commande :** `chown <nom_d'utilisateur>:<nom_du_groupe> <chemin_du_fichier>`
*   **Explication :**
    *   `<nom_d'utilisateur>` : Nom de l'utilisateur qui deviendra le nouveau propriétaire du fichier.
    *   `<nom_du_groupe>` : Nom du groupe qui deviendra le nouveau groupe du fichier.
    *   `<chemin_du_fichier>` : Chemin complet vers le fichier dont vous voulez changer la propriété.
*   **Exemple :** `chown alice:marketing /data/confidentiel/tres_confidentiel/tres_confidentiel.txt` (attribue la propriété du fichier "tres_confidentiel.txt" à l'utilisateur "alice" et au groupe "marketing")

**Important :**

*   Vous devez généralement exécuter ces commandes avec les privilèges d'administrateur (en utilisant `sudo` devant la commande) si vous n'êtes pas déjà connecté en tant que root.
*   Assurez-vous que les noms d'utilisateur et de groupe que vous utilisez existent réellement sur le système. Vous pouvez les vérifier avec les commandes `cat /etc/passwd` (pour les utilisateurs) et `cat /etc/group` (pour les groupes).

**Application**
Voici les lignes de code pour créer un utilisateur et un groupe, puis changer le propriétaire et le groupe d'un fichier, avec des exemples concrets :

**I. Créer un groupe :**

```bash
sudo groupadd developpeurs  # Crée un groupe nommé "developpeurs"
```

**II. Créer un utilisateur :**

```bash
sudo useradd -m -g developpeurs jean  # Crée un utilisateur "jean" et l'ajoute au groupe "developpeurs"
```

**III. Définir un mot de passe pour l'utilisateur :**

```bash
sudo passwd jean  # Vous serez invité à entrer un mot de passe pour "jean"
```

**IV. Changer le propriétaire et le groupe d'un fichier :**

```bash
sudo chown jean:developpeurs /data/confidentiel/tres_confidentiel/budget_previsionnel.txt 
```

Cette commande attribue la propriété du fichier "budget_previsionnel.txt" à l'utilisateur "jean" et au groupe "developpeurs".

**Explications :**

*   `sudo` : Utilisé pour exécuter les commandes avec les privilèges d'administrateur (root).
*   `groupadd developpeurs` : Crée un nouveau groupe nommé "developpeurs".
*   `useradd -m -g developpeurs jean` :
    *   `-m` : Crée le répertoire personnel de l'utilisateur "jean".
    *   `-g developpeurs` : Ajoute l'utilisateur "jean" au groupe "developpeurs".
*   `passwd jean` : Permet de définir un mot de passe pour l'utilisateur "jean".
*   `chown jean:developpeurs /chemin/vers/le/fichier` :
    *   `jean` : Nouvel utilisateur propriétaire du fichier.
    *   `developpeurs` : Nouveau groupe propriétaire du fichier.
    *   `/data/confidentiel/tres_confidentiel/budget_previsionnel.txt` : Chemin complet vers le fichier à modifier.

**Important :**

*   Assurez-vous que les noms d'utilisateur et de groupe sont corrects et n'existent pas déjà sur le système avant de les créer.
*   Vous pouvez vérifier la liste des utilisateurs et des groupes existants avec les commandes `cat /etc/passwd` et `cat /etc/group`.




**5. Vérification :**

*   Utilisez `ls -l` pour vérifier les permissions :

```bash
ls -l /data
```

Vous devriez voir les permissions modifiées reflétées dans la sortie de la commande `ls -l`.

**Rappel :**

*   Les chiffres dans les permissions représentent les droits d'accès :
    *   Premier chiffre : propriétaire (4 = lecture, 2 = écriture, 1 = exécution)
    *   Deuxième chiffre : groupe
    *   Troisième chiffre : autres


