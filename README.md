#include <stdio.h> 
#include <stdlib.h> 
int main(void) 
{ 
int nU, nR; 
printf("Enter number of Unit Hydrograph ordinates (nU): "); 
if (scanf("%d", &nU) != 1 || nU <= 0) { 
fprintf(stderr, "Invalid nU.\n"); 
return 1; 
} 
printf("Enter number of Effective Rainfall Hytograph (cm) (nR): "); 
if (scanf("%d", &nR) != 1 || nR <= 0) 
{ 
fprintf(stderr, "Invalid nR.\n"); 
return 1; 
} 
double *UH = (double*)calloc(nU, sizeof(double)); 
double *R = (double*)calloc(nR, sizeof(double)); 
if (!UH || !R) 
{ 
fprintf(stderr, "failed.\n"); 
free(UH); free(R); 
return 1; 
} 
printf("Enter %d UH ordinates :\n", nU); 
for (int i = 0; i < nU; ++i) 
{ 
if (scanf("%lf", &UH[i]) != 1) 
{ 
fprintf(stderr, "Failed [%d].\n", i); 
free(UH); free(R); 
return 1; 
}} 
printf("Enter %d ERH pulses (excess rainfall in cm for each step):\n", nR); 
for (int i = 0; i < nR; ++i) 
{ 
if (scanf("%lf", &R[i]) != 1) 
{ 
fprintf(stderr, "Failed to read R[%d].\n", i); 
free(UH); free(R); 
return 1; 
}} 
int nD = nU + nR - 1; 
double *DRH = (double*)calloc(nD, sizeof(double)); 
if (!DRH) 
{ 
fprintf(stderr, "failed.\n"); 
free(UH); free(R); 
return 1; 
} 
for (int i = 0; i < nR; ++i) 
{ 
for (int j = 0; j < nU; ++j) { 
DRH[i + j] += R[i] * UH[j]; 
}} 
printf("\nIndex\tDRH\n"); 
for (int t = 0; t < nD; ++t) 
{ 
printf("%d\t%.6f\n", t+1, DRH[t]); 
} 
free(UH); 
free(R); 
free(DRH); 
return 0; 
} 
