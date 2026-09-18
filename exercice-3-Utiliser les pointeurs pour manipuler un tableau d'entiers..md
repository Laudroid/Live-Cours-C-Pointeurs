
## TP C - Pointeur et Tableaux : Gestion de Scores

### Objectif Pédagogique

Utiliser les pointeurs pour manipuler et modifier un tableau d'entiers, en comprenant l'arithmétique de pointeurs et le déréférencement pour accéder et modifier les éléments.

### Contexte du Mini-Projet

Imaginez que vous développez un petit module pour un système de gestion de notes d'étudiants. Ce module doit permettre d'afficher les scores, d'appliquer un bonus collectif, et de normaliser les scores sur une nouvelle échelle. Vous devrez impérativement utiliser des pointeurs pour toutes les opérations sur le tableau de scores.

### Prérequis

*   Connaissances de base du langage C (variables, types, boucles, conditions).
*   Compréhension des fonctions et de leur appel.
*   Notions sur les tableaux en C.

### Consignes Générales

*   Utilisez un compilateur C (par exemple, GCC).
*   Commentez votre code de manière claire et concise.
*   **Utilisation de l'IA :** L'utilisation d'outils d'IA est encouragée pour la compréhension des concepts, l'explication de portions de code, ou la détection d'erreurs potentielles. Cependant, la solution finale doit être le fruit de votre réflexion et de votre compréhension. N'hésitez pas à demander à l'IA *pourquoi* une solution fonctionne ou *comment* un concept s'applique, plutôt que de simplement lui demander la solution complète.

### Exercices

#### Étape 1 : Initialisation et Affichage des Scores (Lecture avec Pointeur)

1.  **Déclarez** un tableau d'entiers `int scores[] = {12, 15, 9, 18, 10, 7, 14, 16};` dans votre fonction `main`.
2.  **Écrivez une fonction** nommée `void afficher_scores(int *tableau, int taille)` :
    *   Cette fonction prendra en paramètre un pointeur vers le premier élément du tableau (`int *tableau`) et la taille du tableau (`int taille`).
    *   Elle devra parcourir le tableau *en utilisant l'arithmétique de pointeurs* (par exemple, `*(tableau + i)` ou `tableau[i]` mais en comprenant la relation avec les pointeurs) et afficher chaque score.
    *   N'utilisez *pas* l'opérateur `[]` directement pour l'accès aux éléments si vous voulez pratiquer l'arithmétique de pointeurs pure, mais sachez que `tableau[i]` est syntaxiquement équivalent à `*(tableau + i)`. Pour cet exercice, privilégiez la forme `*(tableau + i)`.
3.  **Appelez** `afficher_scores` depuis votre `main` pour vérifier son fonctionnement.

#### Étape 2 : Application d'un Bonus (Modification avec Pointeur)

1.  **Écrivez une fonction** nommée `void appliquer_bonus(int *tableau, int taille, int bonus)` :
    *   Cette fonction prendra en paramètre un pointeur vers le premier élément du tableau, la taille du tableau, et la valeur du bonus à appliquer.
    *   Elle devra parcourir le tableau *en utilisant l'arithmétique de pointeurs* et *modifier* chaque score en lui ajoutant la valeur du `bonus`.
    *   Assurez-vous que les scores ne dépassent pas 20 après l'application du bonus (si un score est 18 et le bonus est 5, le nouveau score doit être 20).
2.  **Appelez** `appliquer_bonus` depuis votre `main` avec un bonus de votre choix (par exemple, 2 points).
3.  **Appelez** de nouveau `afficher_scores` après l'application du bonus pour voir les modifications.

#### Étape 3 : Normalisation des Scores (Modification Avancée avec Pointeur)

1.  **Écrivez une fonction** nommée `void normaliser_scores(int *tableau, int taille, int score_max_actuel, int nouveau_score_max)` :
    *   Cette fonction prendra en paramètre un pointeur vers le premier élément du tableau, la taille du tableau, le score maximum actuel (par exemple, 20), et le nouveau score maximum souhaité (par exemple, 100).
    *   Elle devra parcourir le tableau *en utilisant l'arithmétique de pointeurs* et *modifier* chaque score selon la formule de normalisation suivante :
        `nouveau_score = (int)(((float)score_actuel / score_max_actuel) * nouveau_score_max);`
        *(N'oubliez pas le cast en `float` pour éviter la division entière !)*
2.  **Appelez** `normaliser_scores` depuis votre `main` pour transformer les scores sur 100 (en supposant qu'ils étaient sur 20 après le bonus).
3.  **Appelez** une dernière fois `afficher_scores` pour visualiser les scores normalisés.

#### Étape 4 : Le Programme Principal (`main`)

Votre fonction `main` devra orchestrer tous les appels aux fonctions que vous avez créées, en respectant l'ordre des étapes.

```c
#include <stdio.h>

// Déclarez ici vos fonctions :
// void afficher_scores(int *tableau, int taille);
// void appliquer_bonus(int *tableau, int taille, int bonus);
// void normaliser_scores(int *tableau, int taille, int score_max_actuel, int nouveau_score_max);

int main() {
    int scores[] = {12, 15, 9, 18, 10, 7, 14, 16};
    int taille = sizeof(scores) / sizeof(scores[0]);

    printf("--- Scores Initiaux ---\n");
    // Appel à afficher_scores

    printf("\n--- Scores après Bonus (+2 points) ---\n");
    // Appel à appliquer_bonus
    // Appel à afficher_scores

    printf("\n--- Scores Normalisés (sur 100) ---\n");
    // Appel à normaliser_scores
    // Appel à afficher_scores

    return 0;
}
```

### Questions de Réflexion et d'Approfondissement

Ces questions sont là pour vous aider à consolider votre compréhension. N'hésitez pas à les discuter avec vos pairs ou à utiliser une IA pour explorer les réponses.

1.  **Syntaxe :** Quelle est la différence fondamentale entre `tableau[i]` et `*(tableau + i)` en termes de ce qu'ils représentent pour le compilateur C ?
2.  **Passage de Tableau :** Pourquoi est-il nécessaire de passer explicitement la `taille` du tableau à vos fonctions, alors que ce n'est pas toujours le cas dans d'autres langages ?
3.  **Impact du Déréférencement :** Si, dans la fonction `appliquer_bonus`, vous aviez écrit `(tableau + i) = (tableau + i) + bonus;` au lieu de `*(tableau + i) = *(tableau + i) + bonus;`, que se serait-il passé ? Expliquez.
4.  **Modification en Place :** Comment les pointeurs permettent-ils à une fonction de modifier directement les valeurs d'un tableau passé en argument, alors que les variables simples sont généralement passées par valeur (copie) ?
5.  **Utilisation de l'IA pour la Vérification :** Sans demander à l'IA de vous donner la solution complète de `normaliser_scores`, comment pourriez-vous l'utiliser pour vérifier si votre formule de normalisation est correcte ou pour comprendre pourquoi un certain score ne se normalise pas comme attendu ?
6.  **Erreurs Courantes :** Si vous rencontrez une erreur de segmentation (`Segmentation fault`), comment une IA pourrait-elle vous aider à diagnostiquer la cause probable, en lui fournissant votre code et le message d'erreur ?

---

Bon courage pour ce TP ! N'oubliez pas que la pratique est la clé de la maîtrise des pointeurs.