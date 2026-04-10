Dessert Release App - Solution Code
=================================
Compte Rendu : Stocker les préférences localement avec DataStore
1. Introduction
Dans les applications Android modernes, il est souvent nécessaire de stocker des préférences utilisateur localement. Jetpack DataStore est une solution recommandée pour enregistrer de petites données sous forme de paires clé-valeur. Dans cet atelier, nous avons utilisé Preferences DataStore afin d’enregistrer la préférence d’affichage (mode grille ou mode liste) dans l’application Dessert Release.
2. Objectif de l’atelier
L’objectif principal est d’implémenter DataStore pour sauvegarder la préférence de mise en page choisie par l’utilisateur. Ainsi, lorsque l’utilisateur ferme l’application puis la rouvre, la mise en page sélectionnée reste enregistrée.
3. Ajout de la dépendance DataStore
La bibliothèque DataStore a été ajoutée dans le fichier build.gradle.kts afin de permettre l’utilisation du stockage de préférences.
implementation("androidx.datastore:datastore-preferences:1.0.0")
4. Création du dépôt UserPreferencesRepository
Une classe UserPreferencesRepository a été créée dans le package data. Cette classe gère la lecture et l’écriture des préférences utilisateur à l’aide de DataStore.
La clé de préférence est définie avec booleanPreferencesKey afin de stocker un booléen indiquant si l’application doit afficher une mise en page linéaire.
5. Écriture des données dans DataStore
La fonction suspend saveLayoutPreference() est utilisée pour enregistrer la préférence de mise en page. Cette fonction appelle la méthode edit() de DataStore afin de sauvegarder la valeur dans les préférences.
6. Lecture des données depuis DataStore
Les préférences sont lues sous forme de Flow. La propriété isLinearLayout retourne un Flow<Boolean> qui indique si la mise en page est linéaire. La fonction map() est utilisée pour transformer les données stockées dans DataStore en valeur booléenne utilisable par l’interface utilisateur.
7. Gestion des exceptions
Lors de l’accès aux fichiers du système, des erreurs peuvent survenir. Pour éviter les crashs, l’opérateur catch est utilisé pour intercepter les IOException. En cas d’erreur, emptyPreferences() est renvoyé afin de garantir une valeur par défaut.
8. Initialisation du DataStore
Une classe DessertReleaseApplication a été créée afin d’initialiser le DataStore et le dépôt UserPreferencesRepository au démarrage de l’application.
Cette classe agit comme conteneur de dépendances et fournit UserPreferencesRepository au ViewModel.
9. Utilisation du dépôt dans le ViewModel
Le DessertReleaseViewModel reçoit UserPreferencesRepository via injection de dépendances. Le ViewModel utilise ce dépôt pour enregistrer et lire la préférence de mise en page.
La fonction selectLayout() enregistre la préférence choisie par l’utilisateur en appelant saveLayoutPreference() dans une coroutine.
10. Gestion de l’état de l’interface utilisateur
Le Flow retourné par le dépôt est transformé en StateFlow à l’aide de la fonction stateIn(). Cette approche permet à l’interface Jetpack Compose d’observer les changements et de mettre à jour automatiquement l’affichage.
11. Résultat final
Après l’implémentation de DataStore, l’application mémorise la mise en page sélectionnée par l’utilisateur. Lorsque l’application est relancée, la préférence enregistrée est automatiquement appliquée.
Captures de réalisation
![WhatsApp Image 2026-04-10 at 22 14 38](https://github.com/user-attachments/assets/804511d3-28de-4b5a-929e-2c0ec17f579e)


