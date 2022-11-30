# -analuizareiss
#include<stdio.h>
#include<stdlib.h>
#include<time.h>


int main(){
    FILE *arq1;
    int vet[100];
    srand(time(0));
    arq1 = fopen("vet1","w");
    if(arq1 == NULL){
        printf("Erro ao abrir o arquivo");
    }
    for(int i=0;i<100;i++){
        vet[i] = rand()%100000;
        if(vet[i]<10000){
            vet[i] = rand()%100000;
            i = -1;
        }
    }

    for(int i=0;i<100;i++){
        printf("%i ",vet[i]);
    }

    for(int i=0;i<100;i++){
        fprintf(arq1,"%i\n",vet[i]);
    }

    fseek(arq1,0,SEEK_END);
    long tamanho = ftell(arq1);
    fclose(arq1);
    printf("\nO arquivo possui texto %li bytes.\n",tamanho);
    
    
    //binario:

    FILE *arq2;
    arq2 = fopen("vet","wb");
    if(arq2 == NULL){
        printf("Erro ao abrir o arquivo");
    }

    for(int i=0;i<100;i++){
        fwrite(&vet[i],sizeof(int),1,arq2);;
    }
    fseek(arq2,0,SEEK_END);
    long tamanho2 = ftell(arq2);
    fclose(arq2);
     printf("O arquivo possui binario %li bytes.\n",tamanho2);

}

    //explicação:
    //Em arquivos texto cada dígito representa 1 byte,já em binários
    //uma sequencia representa um byte.
    //ex:
    //número 42 em texto ocupa um byte por dígito
    //já 42 em binário,101010,ocupa um byte. 
