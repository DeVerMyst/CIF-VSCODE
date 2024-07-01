Mini-projet Docker & Linux : Manipulation sécurisée de fichiers

**Énoncé :**

L'objectif de ce projet est de mettre en pratique vos connaissances sur Docker et les commandes Linux pour créer un environnement isolé où vous manipulerez des fichiers et des répertoires de manière sécurisée.

**Tâches :**

1.  **Création de l'environnement Docker :**
    *   Utilisez une image Docker basée sur Ubuntu (ou une autre distribution Linux de votre choix).
    *   Lancez un conteneur interactif avec un nom personnalisé (par exemple, "environnement_securise").

2.  **Création de l'arborescence :**
    *   À l'intérieur du conteneur, créez l'arborescence de dossiers suivante :
        ```
        /data
            /public
            /confidentiel
                /tres_confidentiel
        ```

3.  **Création et manipulation de fichiers :**
    *   Créez des fichiers texte (`.txt`) dans chaque répertoire, avec un contenu approprié au niveau de confidentialité (par exemple, "données publiques" dans `/data/public`, "informations confidentielles" dans `/data/confidentiel`, etc.).
    *   Utilisez un éditeur de texte en ligne de commande (Vim ou Nano) pour modifier le contenu de certains fichiers.

4.  **Gestion des permissions :**
    *   Modifiez les permissions des fichiers et des répertoires pour restreindre l'accès :
        *   Rendez les fichiers du répertoire `/data/confidentiel` accessibles uniquement en lecture pour les autres utilisateurs.
        *   Rendez les fichiers du répertoire `/data/confidentiel/tres_confidentiel` accessibles uniquement par le propriétaire.
        *   Assurez-vous que seuls le propriétaire et le groupe peuvent accéder aux répertoires `confidentiel` et `tres_confidentiel`.
    *   Utilisez les commandes `chmod` et `chown` pour gérer les permissions et la propriété.

5.  **Vérification :**
    *   Vérifiez les permissions des fichiers et des répertoires avec la commande `ls -l`.
    *   Essayez d'accéder aux fichiers protégés avec un autre utilisateur pour vous assurer que les restrictions sont en place.

**Livrables :**

*   Un fichier texte contenant les commandes Docker et Linux utilisées pour réaliser le projet.
*   Une capture d'écran de la sortie de la commande `ls -l` montrant les permissions des fichiers et des répertoires.

**Conseils :**

*   Utilisez la documentation de Docker et les commandes Linux pour vous aider.
*   N'hésitez pas à expérimenter et à personnaliser le projet selon vos préférences.

Ce mini-projet vous permettra de consolider vos compétences en Docker et en manipulation de fichiers sous Linux, tout en mettant l'accent sur la sécurité.



