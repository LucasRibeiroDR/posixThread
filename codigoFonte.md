# posixThread
///MULTITHREAD///
///LUCAS RIBEIRO E NATHALIA DE LIMA///

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <windows.h>
#include <unistd.h>

int i;
int x;

void * func (void *arg){
    int *valorThread = (int *)(arg);
    if(*valorThread == 1){
        printf("Thread 1 compilando... Definindo valor numerico para uma variavel 'X'...\n\n");
        x=522;


    }if(*valorThread == 2){
        printf("Thread 2 compilando... Inserindo valor de 'X' no arquivo 'dados.txt'.\nOBS: O arquivo estara no diretorio do proprio projeto...\n\n");
        FILE *file;
        file = fopen("dados.txt","w");
        fprintf(file, "Valor do numero 'X' = %d\n\n\n\n", x);
        fclose(file);


    }if(*valorThread == 3){
        printf("Thread 3 compilando... Exibindo o valorThread de 'X' ao usuario...\n\n");
        Sleep(4000);
        printf("    Numero gerado: %i\n",x);
        printf("    Arquivo gerado/atualizado com sucesso! Finalizando programa...\n");
        }
    }

int main()
{
    pthread_t thread1,thread2,thread3;
    int argumento1=1;
    int argumento2=2;
    int argumento3=3;

    pthread_create(&thread1, NULL, func, (void *)(&argumento1));
    pthread_create(&thread2, NULL, func, (void *)(&argumento2));
    pthread_create(&thread3, NULL, func, (void *)(&argumento3));

    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);
    pthread_join(thread3, NULL);

    exit(0);
}
