Voici deux solutions possibles pour le TP sur les pointeurs et les tableaux en C, chacune commentée et expliquée pour vous aider à maîtriser ces concepts fondamentaux.

---

## Chapitre 1 : Solution avec Arithmétique de Pointeur `*(tableau + i)`

Cette première solution se concentre sur l'utilisation explicite de l'arithmétique de pointeurs sous la forme `*(tableau + i)` pour accéder et modifier les éléments du tableau. C'est une manière très directe de manipuler la mémoire via les pointeurs.


```c
#include <stdio.h> // Nécessaire pour la fonction printf
#include <stdlib.h> // Pourrait être utile pour d'autres fonctions, mais pas strictement pour ce TP

// Fonction pour afficher les scores en utilisant l'arithmétique de pointeurs
// 'tableau' est un pointeur vers le premier élément du tableau d'entiers.
// 'taille' indique le nombre d'éléments dans le tableau.
void afficher_scores(int *tableau, int taille) {
    printf("[");
    for (int i = 0; i < taille; i++) {
        // *(tableau + i) :
        // 'tableau + i' calcule l'adresse de l'i-ème élément après le début du tableau.
        // Le compilateur sait que 'tableau' pointe vers un 'int', donc 'i' est multiplié par sizeof(int).
        // '*' déréférence cette adresse pour obtenir la valeur stockée à cet emplacement.
        printf("%d", *(tableau + i));
        if (i < taille - 1) {
            printf(", "); // Ajoute une virgule et un espace entre les scores
        }
    }
    printf("]\n");
}

// Fonction pour appliquer un bonus aux scores
// Elle modifie directement les valeurs du tableau original grâce au pointeur.
void appliquer_bonus(int *tableau, int taille, int bonus) {
    for (int i = 0; i < taille; i++) {
        // Modification de la valeur à l'adresse *(tableau + i)
        *(tableau + i) += bonus;
        // S'assurer que le score ne dépasse pas 20
        if (*(tableau + i) > 20) {
            *(tableau + i) = 20;
        }
    }
}

// Fonction pour normaliser les scores sur une nouvelle échelle
void normaliser_scores(int *tableau, int taille, int score_max_actuel, int nouveau_score_max) {
    for (int i = 0; i < taille; i++) {
        // Calcul du nouveau score en utilisant la formule de normalisation.
        // Le cast en (float) est crucial pour effectuer une division flottante
        // avant de re-caster le résultat en (int) pour le stockage.
        *(tableau + i) = (int)(((float)*(tableau + i) / score_max_actuel) * nouveau_score_max);
    }
}

int main() {
    int scores[] = {12, 15, 9, 18, 10, 7, 14, 16};
    // Calcul de la taille du tableau :
    // sizeof(scores) donne la taille totale du tableau en octets.
    // sizeof(scores[0]) donne la taille d'un seul élément (ici, un int) en octets.
    // La division donne le nombre d'éléments.
    int taille = sizeof(scores) / sizeof(scores[0]);

    printf("--- Scores Initiaux ---\n");
    afficher_scores(scores, taille); // 'scores' est automatiquement converti en 'int *' (pointeur vers le premier élément)

    printf("\n--- Scores après Bonus (+2 points) ---\n");
    appliquer_bonus(scores, taille, 2);
    afficher_scores(scores, taille);

    printf("\n--- Scores Normalisés (sur 100) ---\n");
    // On suppose que les scores sont maintenant sur 20 après l'application du bonus.
    normaliser_scores(scores, taille, 20, 100);
    afficher_scores(scores, taille);

    return 0; // Indique que le programme s'est terminé avec succès
}
```


### Explication de l'approche

Cette solution met en évidence la relation directe entre les tableaux et les pointeurs en C. Lorsqu'un tableau est passé à une fonction, il est "dégradé" en un pointeur vers son premier élément. Ainsi, `int *tableau` dans les fonctions reçoit l'adresse du début du tableau `scores`.

L'expression `*(tableau + i)` est la pierre angulaire de cette approche. Elle illustre comment, en ajoutant un entier `i` à un pointeur `tableau`, on obtient l'adresse de l'élément `i` positions plus loin. Le compilateur gère automatiquement la multiplication par la taille du type pointé (`sizeof(int)` ici). Le déréférencement (`*`) permet ensuite d'accéder à la valeur à cette adresse.

Les fonctions `appliquer_bonus` et `normaliser_scores` modifient directement les valeurs du tableau original car elles travaillent sur les adresses mémoire des éléments. C'est un avantage majeur des pointeurs pour la modification "en place".

---

## Chapitre 2 : Solution avec Pointeur Itérateur

Cette deuxième solution utilise une technique d'itération courante en C : un pointeur temporaire qui se déplace directement dans le tableau. C'est souvent considéré comme une approche très "C-esque" et peut être légèrement plus performante dans certains contextes car elle évite le calcul d'adresse `tableau + i` à chaque itération.


```c
#include <stdio.h> // Nécessaire pour la fonction printf

// Fonction pour afficher les scores en utilisant un pointeur qui se déplace
// 'tableau' est le pointeur vers le début du tableau.
// 'taille' est le nombre d'éléments.
void afficher_scores_ptr_iter(int *tableau, int taille) {
    printf("[");
    // Déclaration d'un pointeur temporaire 'p' initialisé avec l'adresse du début du tableau.
    int *p = tableau;
    // 'fin_tableau' est un pointeur qui pointe juste après le dernier élément du tableau.
    // Il sert de condition d'arrêt pour la boucle.
    int *fin_tableau = tableau + taille;

    // Boucle tant que le pointeur 'p' n'a pas atteint la fin du tableau.
    while (p < fin_tableau) {
        // Déréférencement de 'p' pour obtenir la valeur de l'élément actuel.
        printf("%d", *p);
        p++; // Incrémente le pointeur pour qu'il pointe vers l'élément suivant.
             // Le compilateur gère l'incrémentation par sizeof(int).
        if (p < fin_tableau) { // Ajoute une virgule si ce n'est pas le dernier élément
            printf(", ");
        }
    }
    printf("]\n");
}

// Fonction pour appliquer un bonus aux scores en utilisant un pointeur itérateur
void appliquer_bonus_ptr_iter(int *tableau, int taille, int bonus) {
    int *p = tableau;
    int *fin_tableau = tableau + taille;

    while (p < fin_tableau) {
        // Modification de la valeur pointée par 'p'
        *p += bonus;
        // S'assurer que le score ne dépasse pas 20
        if (*p > 20) {
            *p = 20;
        }
        p++; // Passe à l'élément suivant
    }
}

// Fonction pour normaliser les scores en utilisant un pointeur itérateur
void normaliser_scores_ptr_iter(int *tableau, int taille, int score_max_actuel, int nouveau_score_max) {
    int *p = tableau;
    int *fin_tableau = tableau + taille;

    while (p < fin_tableau) {
        // Calcul du nouveau score et modification de la valeur pointée par 'p'
        *p = (int)(((float)*p / score_max_actuel) * nouveau_score_max);
        p++; // Passe à l'élément suivant
    }
}

int main() {
    int scores[] = {12, 15, 9, 18, 10, 7, 14, 16};
    int taille = sizeof(scores) / sizeof(scores[0]);

    printf("--- Scores Initiaux ---\n");
    afficher_scores_ptr_iter(scores, taille);

    printf("\n--- Scores après Bonus (+2 points) ---\n");
    appliquer_bonus_ptr_iter(scores, taille, 2);
    afficher_scores_ptr_iter(scores, taille);

    printf("\n--- Scores Normalisés (sur 100) ---\n");
    normaliser_scores_ptr_iter(scores, taille, 20, 100);
    afficher_scores_ptr_iter(scores, taille);

    return 0;
}
```


### Explication de l'approche

Cette solution utilise un pointeur `p` qui est initialisé au début du tableau (`tableau`). À chaque itération de la boucle `while`, le pointeur `p` est incrémenté (`p++`). Grâce à l'arithmétique de pointeurs, `p++` ne signifie pas ajouter 1 octet, mais ajouter `sizeof(int)` octets, ce qui fait que `p` pointe vers l'élément `int` suivant dans la mémoire.

La condition de la boucle `p < fin_tableau` est une manière robuste de s'assurer que l'on ne dépasse pas les limites du tableau. `fin_tableau` est calculé une seule fois et pointe juste après le dernier élément valide.

Cette méthode est très efficace car elle implique des opérations simples d'incrémentation de pointeur et de déréférencement, souvent optimisées par les compilateurs. Elle est particulièrement utile lorsque vous parcourez de grands tableaux et que vous souhaitez une performance maximale.

---

Ces deux solutions sont valides et illustrent différentes manières de manipuler les tableaux avec des pointeurs en C. La première met l'accent sur la relation index-pointeur, tandis que la seconde montre une itération plus directe et souvent plus idiomatique. Comprendre les deux vous donnera une base solide pour travailler avec la mémoire en C.