Voici deux solutions possibles pour le TP sur les pointeurs en C, chacune commentée et expliquée pour faciliter votre apprentissage.

---

## Chapitre 1 : Solution Directe du TP - Adresses Mémoire

Cette première solution implémente directement les instructions de l'énoncé du TP, en se concentrant sur la déclaration, l'initialisation et l'affichage des adresses mémoire.


```c
#include <stdio.h> // Inclut la bibliothèque standard d'entrée/sortie pour utiliser printf

int main() {
    // 1. Déclaration et initialisation d'une variable entière
    // 'nombre' est une variable qui stocke la valeur 42.
    int nombre = 42;

    // 2. Déclaration d'un pointeur vers un entier
    // 'ptr_nombre' est un pointeur. Le type 'int *' signifie qu'il est destiné
    // à stocker l'adresse d'une variable de type 'int'.
    int *ptr_nombre;

    // 3. Initialisation du pointeur avec l'adresse de la variable 'nombre'
    // L'opérateur '&' (opérateur d'adresse de) est utilisé pour obtenir l'adresse mémoire
    // où la variable 'nombre' est stockée. Cette adresse est ensuite assignée à 'ptr_nombre'.
    ptr_nombre = &nombre;

    // 4. Affichage de l'adresse de la variable 'nombre'
    // Le spécificateur de format '%p' est utilisé dans printf pour afficher une adresse mémoire.
    // Il est recommandé de caster l'adresse en '(void *)' pour garantir la portabilité,
    // bien que pour les pointeurs de données, cela fonctionne souvent sans.
    printf("Adresse de la variable 'nombre' : %p\n", (void *)&nombre);

    // 5. Affichage de la valeur du pointeur 'ptr_nombre'
    // La "valeur" d'un pointeur est l'adresse mémoire qu'il contient.
    // Puisque nous avons initialisé 'ptr_nombre' avec '&nombre', cette valeur
    // doit être identique à l'adresse de 'nombre'.
    printf("Valeur du pointeur 'ptr_nombre' (adresse pointée) : %p\n", (void *)ptr_nombre);

    return 0; // Indique que le programme s'est terminé avec succès
}
```


### Explication et Résultats Attendus

Lorsque vous compilez et exécutez ce programme, vous devriez observer deux lignes affichant la même adresse mémoire.

**Exemple de compilation et d'exécution :**


```bash
gcc tp_pointeur_adresse.c -o tp_pointeur_adresse
./tp_pointeur_adresse
```


**Exemple de sortie :**


```
Adresse de la variable 'nombre' : 0x7ffee5c01b9c
Valeur du pointeur 'ptr_nombre' (adresse pointée) : 0x7ffee5c01b9c
```


Les adresses exactes varieront à chaque exécution et selon votre système d'exploitation, mais l'important est qu'elles soient identiques. Cela confirme que le pointeur `ptr_nombre` contient bien l'adresse de la variable `nombre`.

---

## Chapitre 2 : Solution Approfondie - Déréférencement et Taille Mémoire

Cette deuxième solution reprend les bases du TP et y ajoute des éléments pour approfondir votre compréhension, notamment le déréférencement d'un pointeur et l'utilisation de l'opérateur `sizeof` pour explorer la taille des variables et des pointeurs en mémoire.


```c
#include <stdio.h> // Inclut la bibliothèque standard d'entrée/sortie

int main() {
    // Déclaration et initialisation d'une variable entière
    int ma_valeur = 100;

    // Déclaration d'un pointeur vers un entier
    int *ptr_ma_valeur;

    // Initialisation du pointeur avec l'adresse de 'ma_valeur'
    ptr_ma_valeur = &ma_valeur;

    // Affichage des adresses pour confirmer que le pointeur contient bien l'adresse de la variable
    printf("Adresse de la variable 'ma_valeur' : %p\n", (void *)&ma_valeur);
    printf("Valeur du pointeur 'ptr_ma_valeur' (adresse pointée) : %p\n", (void *)ptr_ma_valeur);

    // Déréférencement du pointeur : Accéder à la valeur pointée
    // L'opérateur '*' (opérateur de déréférencement) est utilisé pour accéder à la valeur
    // stockée à l'adresse mémoire que le pointeur contient.
    // Ici, *ptr_ma_valeur nous donne la valeur de 'ma_valeur', soit 100.
    printf("Valeur de la variable 'ma_valeur' via le pointeur : %d\n", *ptr_ma_valeur);

    // Utilisation de sizeof pour comprendre l'occupation mémoire
    // sizeof() est un opérateur qui retourne la taille en octets d'un type ou d'une variable.
    // '%zu' est le spécificateur de format pour afficher une valeur de type size_t,
    // qui est le type retourné par sizeof.
    printf("Taille de la variable 'ma_valeur' (int) : %zu octets\n", sizeof(ma_valeur));
    // La taille d'un pointeur (int *) est généralement fixe pour une architecture donnée (ex: 4 ou 8 octets),
    // quelle que soit la taille du type qu'il pointe.
    printf("Taille du pointeur 'ptr_ma_valeur' (int *) : %zu octets\n", sizeof(ptr_ma_valeur));
    // L'adresse elle-même a la même taille qu'un pointeur.
    printf("Taille de l'adresse de 'ma_valeur' (&ma_valeur) : %zu octets\n", sizeof(&ma_valeur));

    return 0;
}
```


### Explication et Résultats Attendus

Cette solution montre non seulement que le pointeur stocke l'adresse de la variable, mais aussi comment utiliser cette adresse pour accéder à la valeur de la variable (déréférencement). L'utilisation de `sizeof` met en lumière une distinction cruciale : la taille d'une variable (`int`) est différente de la taille d'un pointeur (`int *`), même si ce pointeur pointe vers un `int`. La taille d'un pointeur est déterminée par l'architecture du système (par exemple, 8 octets sur un système 64 bits), car il doit pouvoir stocker n'importe quelle adresse mémoire valide.

**Exemple de sortie :**


```
Adresse de la variable 'ma_valeur' : 0x7ffee5c01b9c
Valeur du pointeur 'ptr_ma_valeur' (adresse pointée) : 0x7ffee5c01b9c
Valeur de la variable 'ma_valeur' via le pointeur : 100
Taille de la variable 'ma_valeur' (int) : 4 octets
Taille du pointeur 'ptr_ma_valeur' (int *) : 8 octets
Taille de l'adresse de 'ma_valeur' (&ma_valeur) : 8 octets
```


Les tailles en octets peuvent varier légèrement en fonction de votre compilateur et de votre architecture système, mais les relations (par exemple, la taille du pointeur est souvent 8 octets sur un système 64 bits, tandis qu'un `int` est souvent 4 octets) devraient être cohérentes.