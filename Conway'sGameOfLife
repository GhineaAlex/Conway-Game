#include <stdio.h>

int main()
{
    char tip_simulare;
    char lume[1000][1000], lume_cop[1000][1000];
    int m, n, k, ocupare = 0; //n- numarul de linii m- numar de coloane
    int i, j, gen; //gen- contor pentru generatii
    printf("Introduceti tipul simularii (Plan-P sau Toroid-T), numarul de linii, de coloane si numarul de generatii \n");
    scanf(" %c %d %d %d", &tip_simulare, &m, &n, &k); //citirea variabilelor
    for (i = 0; i < n; ++i)
    {
        for (j = 0; j < m; j++)
            scanf(" %d", &lume[i][j]);
    }

    if (tip_simulare == 'P') //prima conditie P-plan
    {
        for (i = 0; i < n; i++)
            for (j = 0; j < m; j++)
                ocupare = ocupare + lume[i][j];

        for (gen = 1; gen <= k; gen++) //o instructiune repetitiva pentru a genera primele k generatii
        {
            for (i = 0; i < n; i++)
                for (j = 0; j < n; j++)
                    lume_cop[i][j] = lume[i][j]; //memorarea unei matrice temporare

            for (i = 0; i < n; i++) //apelarea matricei
                for (j = 0; j < m; j++)
                {
                    int p, q, r, s, g, h, suma = 0; //suma- contor pentru memorarea vecinilor

                    //verificarea fiecarui vecin conform regulii planului
                    p = i - 1;
                    if (p < 0) p = 0;
                    q = j - 1;
                    if (q < 0) q = 0;
                    r = i + 1;
                    if (r >= n) r = n - 1;
                    s = j + 1;
                    if (s >= m) s = m - 1;

                    for (g = p; g <= r; g++)
                        for (h = q; h <= s; h++)
                            suma = suma + lume[g][h];

                    suma =suma - lume[i][j];

                    if (lume[i][j])
                    {
                        if (suma < 2 || suma > 3)
                            lume_cop[i][j] = 0;  //schimbarea valorii matricei conform valorii fiecarui vecin
                    }
                    else
                    {
                        if (suma == 3)
                            lume_cop[i][j] = 1;
                    }
                }

            int ocupare_curenta = 0; //nivelul de ocupare, numarul de valori 1 rapotat la restul matricei
            for (i = 0; i < n; i++)
                for (j = 0; j < n; j++)
                {
                    lume[i][j] = lume_cop[i][j];
                    ocupare_curenta = ocupare_curenta + lume[i][j];
                }

            if (ocupare_curenta > ocupare)
                ocupare = ocupare_curenta;
        }
    }
    else if (tip_simulare == 'T') //tipul de simulare toroidala
    {
        for (i = 0; i < n; i++)
            for (j = 0; j < m; j++)
                ocupare = ocupare + lume[i][j]; //initializarea unei matrice pentru valorea ocuparii lumii

        for (gen = 1; gen <= k; gen++) //un for pentru primele k generatii
        {
            for (i = 0; i < n; i++)
                for (j = 0; j < n; j++)
                    lume_cop[i][j] = lume[i][j]; //memorarea unei valori temporare pentru matrice

            for (i = 0; i < n; i++)
                for (j = 0; j < m; j++) //initializarea matricei
                {
                    int ineg = (i - 1) % n;
                    if (ineg < 0)
                        ineg += n;

                    int jneg = (j - 1) % m;
                    if (jneg < 0)
                        jneg += m;
                //am folosit un contor care memoreaza valorile veciunului folosind ultima coloana ca fiind langa prima,
                //respectiv prima linie langa ultima ca intr-un vector cu o singura dimensiune
                    int suma =
                        lume[ineg][jneg] +
                        lume[ineg][j % m] +
                        lume[ineg][(j + 1) % m] +
                        lume[i%n][jneg] +
                        lume[i%n][(j + 1) % m] +
                        lume[(i + 1) % n][jneg] + //mai intai trebuie realizata adunarea pe linie pentru a contoriza vecinul corespunzator
                        lume[(i + 1) % n][j % m] +
                        lume[(i + 1) % n][(j + 1) % m];

                    if (lume[i][j]) //instructiune daca matricea este diferita de 0
                    {
                        if (suma < 2 || suma > 3)
                            lume_cop[i][j] = 0; //daca suma data de contorul respectiv este mai mica decat 2 sau mai mare decat 3, valorea matricei temporare este 0 si elimina vecinul
                    }
                    else
                    {
                        if (suma == 3)
                            lume_cop[i][j] = 1;
                    }
                }

            int ocupare_curenta = 0;
            for (i = 0; i < n; i++)
                for (j = 0; j < n; j++) //initializarea matricei pentru a executa nivelul de ocupare al matricei de tip toroid
                {
                    lume[i][j] = lume_cop[i][j];
                    ocupare_curenta = ocupare_curenta+ lume[i][j];
                }

            if (ocupare_curenta > ocupare)
                ocupare = ocupare_curenta;
        }
    }

    printf("\n");
    for (i = 0; i < n; i++)
    {   for (j = 0; j < m; j++)
            printf("%d ", lume[i][j]); //afisarea matricei finale dupa k generatii
        printf("\n");
    }
    printf("Nivelul de ocupare al matricei este de:");
    printf("%.3f%%\n", (float)ocupare/(m*n)*100); //afisarea nivelul de ocupare in procentage
}

