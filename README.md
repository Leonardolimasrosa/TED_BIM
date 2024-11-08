# TED_BIM
Nome dos integrantes: Cauã Brasil
                      Gabriel Calisto
                      Leonardo Rosa
                      Lucas Xavier
                      Rafael Lucietto 

# Caso não abra o arquivo, o código está digitado abaixo

#include <stdio.h>
#include <stdlib.h>

typedef struct {
    void **dados;    
    int topo;         
    int tamanho;       
    int capacidade;    
} Pilha;


Pilha* criarPilha(int capacidadeInicial) {
    Pilha *pilha = (Pilha *) malloc(sizeof(Pilha));
    if (pilha == NULL) return NULL;

    pilha->dados = (void **) malloc(sizeof(void *) * capacidadeInicial);
    if (pilha->dados == NULL) {
        free(pilha);
        return NULL;
    }

    pilha->topo = -1;  
    pilha->tamanho = 0;
    pilha->capacidade = capacidadeInicial;

    return pilha;
}


void dobrarCapacidade(Pilha *pilha) {
    int novaCapacidade = pilha->capacidade * 2;
    void *novosDados = (void *) realloc(pilha->dados, sizeof(void *) * novaCapacidade);
    if (novosDados == NULL) return;

    pilha->dados = novosDados;
    pilha->capacidade = novaCapacidade;
}


void empilhar(Pilha *pilha, void *elemento) {
    if (pilha->tamanho == pilha->capacidade) {
        dobrarCapacidade(pilha);
    }
    printf("Empilhando %d \n", *(int*)elemento);
    pilha->topo++;
    pilha->dados[pilha->topo] = elemento;
    pilha->tamanho++;
}


void* desempilhar(Pilha *pilha) {
    if (pilha->tamanho == 0){
        return NULL;  // Pilha vazia
    } 

    void *elementoRemovido = pilha->dados[pilha->topo];
    pilha->topo--;
    pilha->tamanho--;

    return elementoRemovido;
}


void limparPilha(Pilha *pilha) {
    if (pilha != NULL) {
        free(pilha->dados); 
        free(pilha);        
    }
}


int main() {
    Pilha *pilha = criarPilha(2);
    if (pilha == NULL) {
        printf("Erro ao criar a pilha!\n");
        return 1;
    }

    int a = 10, b = 20, c = 30;

    empilhar(pilha, &a);
    empilhar(pilha, &b);
    empilhar(pilha, &c);  // A pilha dobra a capacidade

    printf("Desempilhado: %d\n", *(int *)desempilhar(pilha)); 
    printf("Desempilhado: %d\n", *(int *)desempilhar(pilha)); 
    printf("Desempilhado: %d\n", *(int *)desempilhar(pilha)); 

    limparPilha(pilha);
    pilha = NULL; 

    return 0;
}
