# Mandel

    gcc -o mandel mandel.c -lm -fopenmp
    export OMP_NUM_THREADS=2
    ./mandel

static

    Temps total de calcul : 2.535 sec

dynamic

    Temps total de calcul : 1.12543 sec

dynamic
avec 1 thread

    Temps total de calcul : 5.27974 sec

avec 2 threads

    Temps total de calcul : 2.76206 sec

avec 4

    Temps total de calcul : 1.7317 sec

avec 8 threads

    Temps total de calcul : 1.11411 sec

avec 16

    Temps total de calcul : 1.13456 sec

avec 32

    Temps total de calcul : 1.14206 sec

static
avec 1

    Temps total de calcul : 5.31778 sec

avec 2 threads

    Temps total de calcul : 2.75916 sec

avec 4

    Temps total de calcul : 2.7555 sec

avec 8 threads

    Temps total de calcul : 2.29963 sec

avec 16

    Temps total de calcul : 1.89546 sec

avec 32

    Temps total de calcul : 1.20037 sec

avec 64

    Temps total de calcul : 1.14964 sec

avec 128

    Temps total de calcul : 1.10645 sec

avec 256

    Temps total de calcul : 1.08768 sec

avec 512

    Temps total de calcul : 1.09058 sec

# Convolution

static

    ./convol
    gcc -o convol convol.c -lm -fopenmp
    export OMP_NUM_THREADS=2
    ./convol femme10.ras 4 100

    Temps total de calcul : 1.26235 seconde(s)

avec 1 thread

    Temps total de calcul : 2.3945 seconde(s)

avec 4

    Temps total de calcul : 0.987152 seconde(s)

avec8

    Temps total de calcul : 0.514363 seconde(s)

avec 16

    Temps total de calcul : 0.742823 seconde(s)

avec32

    Temps total de calcul : 0.84205 seconde(s)
