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
