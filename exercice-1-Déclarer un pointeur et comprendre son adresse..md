
## TP : Pointeur C - Adresses Mémoire

### Objectif du TP

*   Maîtriser la déclaration d'un pointeur.
*   Comprendre la relation entre une variable et son adresse mémoire.
*   Afficher l'adresse mémoire d'une variable et la valeur d'un pointeur.

### Contexte

Les pointeurs sont un concept fondamental en C, permettant une manipulation directe de la mémoire. Comprendre comment une variable est stockée et comment y accéder via son adresse est la première étape essentielle pour maîtriser la gestion de la mémoire et des structures de données complexes.

L'utilisation d'outils d'intelligence artificielle pour explorer des solutions ou comprendre des concepts est encouragée. L'objectif est d'apprendre et de comprendre, pas de simplement reproduire. N'hésitez pas à interroger l'IA sur le *pourquoi* et le *comment* des mécanismes que vous mettez en œuvre.

### Énoncé du TP

Vous allez créer un programme C simple qui :
1.  Déclare une variable entière.
2.  Déclare un pointeur capable de "pointer" vers cette variable entière.
3.  Initialise le pointeur avec l'adresse de la variable entière.
4.  Affiche l'adresse de la variable entière.
5.  Affiche la valeur stockée dans le pointeur (qui doit être l'adresse de la variable).

### Instructions Détaillées

Suivez ces étapes pour réaliser le programme :

1.  **Création du fichier**
    *   Créez un nouveau fichier nommé `tp_pointeur_adresse.c`.

2.  **Structure de base**
    *   Commencez par la structure minimale d'un programme C :
        ```c
        #include <stdio.h> // Pour la fonction printf

        int main() {
            // Votre code ici
            return 0;
        }
        ```

3.  **Déclaration de la variable entière**
    *   À l'intérieur de `main`, déclarez une variable entière et initialisez-la avec une valeur de votre choix (par exemple, `int nombre = 42;`).

4.  **Déclaration du pointeur**
    *   Déclarez un pointeur qui pourra stocker l'adresse d'un entier. Rappelez-vous que le type du pointeur doit correspondre au type de la variable qu'il va pointer.
    *   Exemple : `int *ptr_nombre;`

5.  **Initialisation du pointeur**
    *   Assignez l'adresse de votre variable entière (`nombre`) au pointeur (`ptr_nombre`). L'opérateur `&` (adresse de) est utilisé pour obtenir l'adresse d'une variable.
    *   Exemple : `ptr_nombre = &nombre;`

6.  **Affichage des adresses**
    *   Utilisez `printf` pour afficher :
        *   L'adresse de la variable `nombre`.
        *   La valeur du pointeur `ptr_nombre`.
    *   Pour afficher une adresse mémoire, utilisez le spécificateur de format `%p`.
    *   Exemple :
        ```c
        printf("Adresse de la variable 'nombre' : %p\n", &nombre);
        printf("Valeur du pointeur 'ptr_nombre' (adresse pointée) : %p\n", ptr_nombre);
        ```

7.  **Compilation et exécution**
    *   Enregistrez votre fichier.
    *   Compilez le programme à l'aide de GCC (ou votre compilateur C habituel) :
        ```bash
        gcc tp_pointeur_adresse.c -o tp_pointeur_adresse
        ```
    *   Exécutez le programme :
        ```bash
        ./tp_pointeur_adresse
        ```

### Résultat Attendu

Votre programme devrait afficher deux lignes, chacune montrant une adresse mémoire. Ces deux adresses devraient être identiques.

Exemple de sortie (les adresses exactes varieront à chaque exécution et selon votre système) :

```
Adresse de la variable 'nombre' : 0x7ffee5c01b9c
Valeur du pointeur 'ptr_nombre' (adresse pointée) : 0x7ffee5c01b9c
```

### Questions de Réflexion

Répondez à ces questions pour consolider votre compréhension :

1.  Pourquoi les deux adresses affichées sont-elles identiques ?
2.  Quelle est la différence fondamentale entre `nombre` et `&nombre` ?
3.  Quelle est la différence fondamentale entre `ptr_nombre` et `*ptr_nombre` (même si `*ptr_nombre` n'est pas utilisé dans ce TP, réfléchissez à ce que cela signifierait) ?
4.  Que se passerait-il si vous déclariez `ptr_nombre` mais ne l'initialisiez pas avant de tenter de l'afficher ou de l'utiliser ?
5.  Si vous deviez changer la valeur de la variable `nombre` en utilisant *uniquement* le pointeur `ptr_nombre`, comment feriez-vous ?

### Pour Aller Plus Loin (Optionnel)

*   Modifiez votre programme pour afficher également la *valeur* de `nombre` en utilisant le pointeur `ptr_nombre` (c'est-à-dire en déréférençant le pointeur).
*   Déclarez une deuxième variable entière et un deuxième pointeur. Faites en sorte que les deux pointeurs pointent vers la *même* variable entière. Affichez les adresses pour vérifier.
*   Utilisez l'opérateur `sizeof` pour afficher la taille en octets de `nombre`, de `ptr_nombre`, et de `&nombre`. Que remarquez-vous ?

---

N'oubliez pas que l'expérimentation est la clé de l'apprentissage en programmation. Modifiez le code, observez les erreurs, et comprenez pourquoi elles se produisent. Bon courage !