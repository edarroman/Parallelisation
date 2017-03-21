# TD/TP1: Ensemble de Mandelbrot

### Question 1:
Le calcul s'effectue dans le plan complexe, pour se faire on associe une coordonnées (x, y) à chaque pixel. Les coordonnées (xmin, ymin) sont les coordonnées du premier pixel de l'image dans le plan complexe et (xmax, ymax) celles du dernier pixel dans le plan complexe.  
A l'aide de deux boucles <i> for </i>, on parcourt l'ensemble des y et des x (de 0 à w-1 et de 0 à h-1, respectivement). Puisque l'ensemble est discret alors que le plan complexe est continu, on calcule l'incrément (xinc, yinc) entres les coordonnées des pixels continus.  

### Question 2:
On effectue la compilation par défault ainsi que les cinq exemples d'exécution.
#### 1/ Code original

    gcc -o mandel mandel.c -lm  
    ./mandel
    gimp mandel.ras

![Mandel original](/Fractales/Code_originel/images/mandel_fractale_default.jpg)

#### 2/ Exemples d'exécution

    ./mandel 800 800 0.35 0.355 0.353 0.358 200

![Mandel](/Fractales/Code_originel/images/mandel_800_800_0.35_0.355_0.353_0.358_200.jpg)

    ./mandel 800 800 -0.736 -0.184 -0.735 -0.183 500

![Mandel](/Fractales/Code_originel/images/mandel_800_800_-0.736_-0.184_-0.735_-0.183_500.jpg)

    ./mandel 800 800 -0.736 -0.184 -0.735 -0.183 300

![Mandel](/Fractales/Code_originel/images/mandel_800_800_-0.736_-0.184_-0.735_-0.183_300.jpg)

    ./mandel 800 800 -1.48478 0.00006 -1.48440 0.00044 100

![Mandel](/Fractales/Code_originel/images/mandel_800_800_-1.48478_0.00006_-1.48440_0.00044_100.jpg)

    ./mandel 800 800 -1.5 -0.1 -1.3 0.1 10000

![Mandel](/Fractales/Code_originel/images/mandel_800_800_-1.5_-0.1_-1.3_0.1_10000.jpg)

#### 3/ Commentaires

Après avoir exécuté les cinqs exemples ainsi que d'autres changements des 10 paramètres (voir /Fractales/Code_originel/Prisedenote.md), on a pu voir l'implication de chaque paramètres (rectangle de vu, zoom, itérations, etc ...) et que les temps d'exécution peuvent aller de 2 secondes pour un mandel original à 105 secondes pour un mandel zoomer avec un nombre important d'itérations.

### Question 3:
#### 1/
Le calcul aux différentes profondeurs (fonction xy2color) n'est pas parallélisable puisque la valeur de ce pixel à la profondeur n+1 est une fonction complexe de la valeur de ce pixel à la profondeur n (la valeur à la profondeur n+1 écrase en mémoire celle à la valeur n). En revanche, chaque pixel de l'image subit le même traitement (les 2 boucles embriquées) qui ne dépendent pas de la valeur de d'autres pixels.  
Autrement dit, le calcul de pima sur chaque pixel est indépendant (partie parallélisable) mais la fonction xy2color en elle-même n'est pas parallélisable, on fait donc une division de l'image.

#### 2/

On fait une division de l'image selon la hauteur car la mémoire est un tableau linéaire, c'est ainsi plus facile.
Pour paralléliser le code nous allons utiliser une stratégie statique (découpage en blocs selon le nombre de processus: une seule fois) et une stratégie dynamique (découpage par blocs pui envoie aux ouvriers et dès qu'ils ont finis, on en renvoie: plusieurs fois)

#### 3/
** Architecture des processeurs à mémoire distribuée : Stratégie statique **  
Données :   
H : Hauteur tableau  
W : largeur tableau  
rank : rang du processus  
h_local : hauteur d'un bloc

    Ymin_loc = Ymin * rank * Yinc  

    if (rank==master){
      - Allocation dynamique de l'image globale:
        w*h*sizeof(char)
      - Test de l'allocation dynamique
      - calcul de la position du début de l'image locale du maitre

    }


Envoi/réception des blocs  

Données: W,rank, h_local, ima, pima

    debut
      si rank == MAITRE alors
        pour tous les ouvriers faire
          //attente d'un message
          MPI_Probe()
          s= ;
          si s!= Maitre alors
            //assemblage du bloc
            MPI_REcv()
          fin si
        fin pour tous
        sauvegarde de l'image
        affichage chronomètre
      sinon
        MPI_Send()
      fin si
    fin

** Architecture des processeurs à répartition dynamique des charges : Stratégie dynamique **

- le processus Maitre va rien calculer
- le processus Maitre devrait recevoir les lignes traitées par les ouvriers et si besoin
de leur envoyer à nouveau d'autres lignes à traiter
- le nombre de blocs est un argument du programme => caractérisé par le nombre de lignes
à traiter
- à chaque fois qu'un ouvrier finit une portion de calcul à traiter, il l'envoie au maitre qui
devrait le mettre au bon endroit

algo Maitre  
    - allocation dynamique de l'image globale
    - test de l'allocation dynamique
    - pour i va de 0 à nb_proc faire
        si i!=Maitre
          on envoie à l'esclave de rang i num_bloc
          on incrémente num_bloc
    - pour i va de 0 à h/nb_lignes faire
        on recoit le num du bloc fait par l'ouvrier
        on détermine le rang de l'émetteur
        on recoit le calcul
        test de fin de calcul
          s'il reste des calculs à faire on envoie un num de bloc à calculer à l'ouvrier
          sinon on envoie un message en indiquant la fin du travail

### Question 4:
