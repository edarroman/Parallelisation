# TD/TP2: Convolution

### 1/
Nous utilisons un tampon intermédiaire afin de ne pas changer les valeurs de départ des pixels pour calculer la convolution sur les voisins. Sinon le calcul des valeurs de convolution seraient faussées.

### 2/
Le calcul d'une convolution sur chaque pixel est parallélisable contrairement aux convolutions entre elles qui sont dépendantes (itérations).

### 3/
Il y a 9 multiplcations et 8 additions, donnant ainsi une compléxité théorique de o(1), on prévoit une stratégie statique.

### 4/
Dans ce contexte, il est naturel de découper par lignes.

### 5/
S'il on choisit de ne pas prendre les bords, on crée des zones blanches. L'autre choix est de communiquer avec son voisins pour calculer les bords.

### 6/

Algorithme bloquant

    DEBUT
    	si rank == MAITRE alors
    		lecture du fichier
    		récupération des paramètres
    	fin si
    	// envoi des paramètres
    	MPI_Bcast(params,2,MPI_INT,MAITRE,MPI8COMM_WORLD)
    FIN

    Calcul de h_loc
    Allocation dynamique de chaque bloc local
    Test de l'allocation dynamique
    Envoi des blocs d'images aux processus (MPI_SCATTER()) (se charge de répartir statiquement la charge de travail entre les processus)
    h_loc = h_loc + (1 si 0<rank<=p-2, 0 sinon) + (1 si 1<rank<=p-1, 0 sinon)

Données : r,h,w,rank

    DEBUT
    	h_loc = h/n_proc + (rank > 0 ? 1:0) + (rank < n_proc-1 ? 1:0)
    	// PAs bon : si rank == Maitre alors
    	//	ima = r.data;
    	//sinon
    		ima = malloc(h_loc*w*sizeof(unsigned char))
    		// test allocation
    	//finsi

    	MPI_Scatter(ima,w*h/n_proc,MPI_CHAR,ima + (rank>0?w:0,...))
    FIN

### 7/
Algorithme non bloquant

    pour i allant de 0 à nbiter faire
      si rank>0 faire
        Envoyer la ligne 1 et 2 au processus précédent(rank k-1)
      fin si
      si rank<p-1 faire
        Envoyer la ligne h_loc-2 et h_loc-3 au processus suivant (rank+1)
      fin si

    faire la convolution du bloc (qui va de la ligne 1 à h_loc-1)
      si rank>0 faire
        recevoir la ligne 0 et 1 du processus rank-1
      fin si
      si nombre<p-1 faire
        recevoir la ligne h_loc-1 et h_loc-2 du processus (rank+1)
      fin si
      faire la convolution de la ligne 1
      faire la convolution de la ligne h_loc-1


##### Résultats:
(voir /Convolution/Prisedenotes.md)

- Test numéro 1: Changement de filtre  
Image: Sukhotai 4080  
Processus: 4   
Itérations: 100   

| Filtre |	0  |	1  |  2  | 	3  |	4  |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |  
| Temps| 105.612 |	105.645 | 53.2798	 | 54.0516  |	1634.85 |

- Test numéro 2: Changement de nombre de processus  
Image: Sukhotai 4080  
Filtre: 2  
Itérations: 100  

| Processus |	2  |	4  |  8  | 	16  |	32  |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |  
| Temps| 101.591 |	53.2798	 | 55.7453 | 61.3817  |	erreur |  

- Test numéro 3: Changement de nombre d'itérations
Image: Sukhotai 4080  
Filtre: 2  
Processus: 8  

| Itérations |	10  |	100  |  1000  | 	10000  |
| ------------- | ------------- | ------------- | ------------- | ------------- |  
| Temps| 6.74346 |	55.7453	 |  530.638 | 7634  |


Les tests ne peuvent pas être comparé à des tests fait sans MPI mais on peut, déjà, conclure que le nombre de processus n'a pas besoin d'être supérieur à 8 et que du point de vue humain, l'algorithme est bien plus rapide sur le filtre 4.
