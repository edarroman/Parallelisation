/* Rasperry */
Configuration telle que les raspberry peuvent communiquer par ssh sans mdp,
les raspberry soient déclarées entre elles (hostfile),
contiennent mpicc et mpi run.
Copie du fichier .c, des lib (rasterfile.h).
Compilation du .c.

    mpicc -o mandel_mpi mandel_MPI.c -lm
    mpirun --np 4 ./mandel_mpi
