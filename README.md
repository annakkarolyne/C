#include <stdio.h>
#include <stdlib.h>


typedef struct No {
    int valor;
    struct No *esquerda;
    struct No *direita;
} No;


No* criarNo(int valor) {
    No *novo = (No*)malloc(sizeof(No));
    novo->valor = valor;
    novo->esquerda = NULL;
    novo->direita = NULL;
    return novo;
}


No* inserir(No *raiz, int valor) {
    if (raiz == NULL) {
        return criarNo(valor);
    }
    
    if (valor < raiz->valor) {
        raiz->esquerda = inserir(raiz->esquerda, valor);
    } else if (valor > raiz->valor) {
        raiz->direita = inserir(raiz->direita, valor);
    }
    
    return raiz;
}


No* buscar(No *raiz, int valor) {
    if (raiz == NULL || raiz->valor == valor) {
        return raiz;
    }
    
    if (valor < raiz->valor) {
        return buscar(raiz->esquerda, valor);
    }
    
    return buscar(raiz->direita, valor);
}


void emOrdem(No *raiz) {
    if (raiz != NULL) {
        emOrdem(raiz->esquerda);
        printf("%d ", raiz->valor);
        emOrdem(raiz->direita);
    }
}


void preOrdem(No *raiz) {
    if (raiz != NULL) {
        printf("%d ", raiz->valor);
        preOrdem(raiz->esquerda);
        preOrdem(raiz->direita);
    }
}


void posOrdem(No *raiz) {
    if (raiz != NULL) {
        posOrdem(raiz->esquerda);
        posOrdem(raiz->direita);
        printf("%d ", raiz->valor);
    }
}


void liberarArvore(No *raiz) {
    if (raiz != NULL) {
        liberarArvore(raiz->esquerda);
        liberarArvore(raiz->direita);
        free(raiz);
    }
}

int main() {
    No *raiz = NULL;
    
  
    raiz = inserir(raiz, 50);
    raiz = inserir(raiz, 30);
    raiz = inserir(raiz, 70);
    raiz = inserir(raiz, 20);
    raiz = inserir(raiz, 40);
    raiz = inserir(raiz, 60);
    raiz = inserir(raiz, 80);
    
    printf("Percurso em ordem: ");
    emOrdem(raiz);
    printf("\n");
    
    printf("Percurso pré-ordem: ");
    preOrdem(raiz);
    printf("\n");
    
    printf("Percurso pós-ordem: ");
    posOrdem(raiz);
    printf("\n");
    
 
    int valorBusca = 40;
    No *resultado = buscar(raiz, valorBusca);
    if (resultado != NULL) {
        printf("\nValor %d encontrado na árvore!\n", valorBusca);
    } else {
        printf("\nValor %d não encontrado na árvore.\n", valorBusca);
    }
    

    liberarArvore(raiz);
    
    return 0;
}
