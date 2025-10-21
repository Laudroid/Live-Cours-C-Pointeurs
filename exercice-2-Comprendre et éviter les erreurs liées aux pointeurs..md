
## TP : Pointeur Dangereux - Analyse et Correction en C

### Objectif du TP

Comprendre et éviter les erreurs courantes liées aux pointeurs, en particulier celles concernant la gestion de la mémoire et la portée des variables.

### Contexte

La manipulation de chaînes de caractères est une tâche fréquente en programmation C. Elle implique souvent l'allocation dynamique de mémoire et l'utilisation de pointeurs. Une mauvaise gestion peut entraîner des comportements imprévisibles, des plantages (segmentation fault) et des failles de sécurité. Ce TP vous mettra face à un cas concret d'erreur de pointeur dans une fonction de manipulation de chaînes.

### Énoncé du Problème

Vous disposez d'une fonction `concatenerChaines` dont l'objectif est de prendre deux chaînes de caractères en entrée et de retourner une *nouvelle* chaîne qui est la concaténation des deux premières. Cependant, cette fonction contient une erreur de pointeur qui la rend dangereuse et inopérante dans certains contextes.

Voici le code à analyser :

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Fonction censée concaténer deux chaînes et retourner le résultat
char* concatenerChaines(const char* s1, const char* s2) {
    char resultat[100]; // Buffer local
    strcpy(resultat, s1);
    strcat(resultat, s2);
    return resultat; // Retourne l'adresse du buffer local
}

int main() {
    const char* chaine1 = "Bonjour, ";
    const char* chaine2 = "monde !";

    printf("Chaîne 1 : %s\n", chaine1);
    printf("Chaîne 2 : %s\n", chaine2);

    char* chaineConcatenee = concatenerChaines(chaine1, chaine2);
    printf("Chaîne concaténée (tentative 1) : %s\n", chaineConcatenee);

    // Ajout d'une opération pour potentiellement écraser la mémoire
    int a = 10;
    int b = 20;
    int somme = a + b;
    printf("Somme de a et b : %d\n", somme);

    printf("Chaîne concaténée (tentative 2, après autre opération) : %s\n", chaineConcatenee);

    return 0;
}
```

### Tâches à Réaliser

1.  **Exécution et Observation**
    *   Compilez et exécutez le code fourni.
    *   Décrivez précisément le comportement observé. Est-ce conforme à l'attendu pour la chaîne concaténée, en particulier après l'affichage de la somme ? Expliquez pourquoi le comportement peut varier d'une exécution à l'autre ou d'un environnement à l'autre.

2.  **Analyse de l'Erreur**
    *   Identifiez la ou les erreurs de pointeur présentes dans la fonction `concatenerChaines`.
    *   Expliquez en détail pourquoi cette erreur se produit. Quels concepts de la gestion mémoire en C sont violés ? (Portée des variables, durée de vie, pointeurs invalides, etc.)

3.  **Proposition de Correction**
    *   Proposez une solution pour corriger la fonction `concatenerChaines` afin qu'elle fonctionne correctement et de manière sécurisée. Votre solution doit garantir que la chaîne retournée est valide et persistante après l'appel de la fonction.
    *   Pensez à la manière dont la mémoire doit être allouée et gérée pour le résultat.

4.  **Implémentation et Validation**
    *   Implémentez votre solution. Assurez-vous de gérer l'allocation et la libération de la mémoire de manière appropriée.
    *   Modifiez la fonction `main` pour utiliser votre version corrigée de `concatenerChaines` et pour gérer correctement la mémoire allouée.
    *   Testez votre code corrigé avec différents jeux de données (chaînes vides, chaînes longues, etc.).
    *   Expliquez comment votre correction résout le problème initial et garantit la validité du pointeur retourné.

5.  **Réflexion Post-Correction**
    *   Dans votre version corrigée, qui est responsable de la libération de la mémoire allouée par `concatenerChaines` ? Pourquoi est-ce important de le savoir et de le faire ?
    *   Que se passerait-il si vous oubliiez de libérer cette mémoire ? Quel est le terme technique pour ce type de problème ?

### Conseils

*   Utilisez un débogueur (comme GDB) si vous en avez l'occasion pour suivre l'état des pointeurs et de la mémoire à différentes étapes de l'exécution. C'est un excellent moyen de visualiser le problème des pointeurs "pendants" ou "dangling pointers".
*   Pensez à la taille nécessaire pour la chaîne résultante, y compris le caractère nul de fin de chaîne (`\0`).
*   La fonction `strlen()` est votre amie pour déterminer la longueur des chaînes.

### Rendu

Votre rapport devra inclure :
*   Le code initial fourni.
*   Le comportement observé lors de l'exécution du code initial.
*   L'analyse détaillée de l'erreur (réponses à la tâche 2).
*   Le code corrigé de la fonction `concatenerChaines` et de la fonction `main`.
*   Le comportement observé après correction.
*   Les réponses aux questions de réflexion (tâche 5).

Bon courage !