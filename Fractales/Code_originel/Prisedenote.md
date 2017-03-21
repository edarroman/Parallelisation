Mandel original

    ./mandel 800 800 -2.0 -2.0 2.0 2.0 10000

mandel_1:
Diminution de dimX

    ./mandel 400 800 -2.0 -2.0 2.0 2.0 10000

    Domaine: {[-2,-2]x[2,2]}
    Increment : 0.0100251 0.00500626
    Prof: 10000
    Dim image: 400x800
    Temps total de calcul : 2.64417 sec
    2.64417


mandel_2:
Diminution de dimY

    ./mandel 800 400 -2.0 -2.0 2.0 2.0 10000
    Domaine: {[-2,-2]x[2,2]}
    Increment : 0.00500626 0.0100251
    Prof: 10000
    Dim image: 800x400
    Temps total de calcul : 2.64953 sec
    2.64953

mandel_3:
Changement de xmin

    ./mandel 800 800 -1.0 -2.0 2.0 2.0 10000
    Domaine: {[-1,-2]x[2,2]}
    Increment : 0.00375469 0.00500626
    Prof: 10000
    Dim image: 800x800
    Temps total de calcul : 6.51753 sec
    6.51753

mandel_4:
Changement de ymin

    ./mandel 800 800 -2.0 -4.0 2.0 2.0 10000
    Domaine: {[-2,-4]x[2,2]}
    Increment : 0.00500626 0.00750939
    Prof: 10000
    Dim image: 800x800
    Temps total de calcul : 3.5321 sec
    3.5321

mandel_5:
Changement de xmax

    ./mandel 800 800 -2.0 -2.0 1.0 2.0 10000
    Domaine: {[-2,-2]x[1,2]}
    Increment : 0.00375469 0.00500626
    Prof: 10000
    Dim image: 800x800
    Temps total de calcul : 7.03137 sec
    7.03137

mandel_6:
Changement de ymax

    ./mandel 800 800 -2.0 -2.0 2.0 5.0 10000
    Domaine: {[-2,-2]x[2,5]}
    Increment : 0.00500626 0.00876095
    Prof: 10000
    Dim image: 800x800
    Temps total de calcul : 3.02632 sec
    3.02632

mandel_7:
Diminution de prof

    ./mandel 800 800 -2.0 -2.0 2.0 2.0 200
    Domaine: {[-2,-2]x[2,2]}
    Increment : 0.00500626 0.00500626
    Prof: 200
    Dim image: 800x800
    Temps total de calcul : 0.139934 sec
    0.139934

mandel_8:
Diminution de prof

    ./mandel 800 800 -2.0 -2.0 2.0 2.0 100
    Domaine: {[-2,-2]x[2,2]}
    Increment : 0.00500626 0.00500626
    Prof: 100
    Dim image: 800x800
    Temps total de calcul : 0.088258 sec
    0.088258

mandel_9:
zoom

    ./mandel 800 800 0.25 0.25 0.5 0.5 10000
    Domaine: {[0.25,0.25]x[0.5,0.5]}
    Increment : 0.000312891 0.000312891
    Prof: 10000
    Dim image: 800x800
    Temps total de calcul : 21.0185 sec
    21.0185

mandel_10:
Diminution prof

    ./mandel 800 800 0.25 0.25 0.5 0.5 100
    Domaine: {[0.25,0.25]x[0.5,0.5]}
    Increment : 0.000312891 0.000312891
    Prof: 100
    Dim image: 800x800
    Temps total de calcul : 0.289537 sec
    0.289537

mandel_11:
Augmentation prof

    ./mandel 800 800 0.25 0.25 0.5 0.5 50000
    Domaine: {[0.25,0.25]x[0.5,0.5]}
    Increment : 0.000312891 0.000312891
    Prof: 50000
    Dim image: 800x800
    Temps total de calcul : 105.689 sec
    105.689
