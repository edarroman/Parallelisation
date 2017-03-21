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
