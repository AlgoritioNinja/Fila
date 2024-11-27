# Explicação do Código em C: Fila Estática

Este código demonstra como implementar uma **fila estática** em C utilizando um array, com as operações de inicialização, enfileiramento, desenfileiramento e impressão.

---

## Código

```c
#include <stdio.h>
#include <stdlib.h>
#define TAMANHO 5 // Tamanho máximo da fila

typedef struct {
    int itens[TAMANHO];
    int frente;  // Índice do início da fila
    int tras;    // Índice do final da fila
} Fila;

// Inicializa a fila
void inicializarFila(Fila* fila) {
    fila->frente = -1;
    fila->tras = -1;
}

// Verifica se a fila está cheia
int estaCheia(Fila* fila) {
    return fila->tras == TAMANHO - 1;
}

// Verifica se a fila está vazia
int estaVazia(Fila* fila) {
    return fila->frente == -1 || fila->frente > fila->tras;
}

// Enfileira um elemento
void enfileirar(Fila* fila, int valor) {
    if (estaCheia(fila)) {
        printf("Erro: Fila cheia!\n");
        return;
    }
    if (fila->frente == -1) fila->frente = 0; // Primeiro elemento
    fila->tras++;
    fila->itens[fila->tras] = valor;
    printf("Enfileirado: %d\n", valor);
}

// Desenfileira um elemento
int desenfileirar(Fila* fila) {
    if (estaVazia(fila)) {
        printf("Erro: Fila vazia!\n");
        return -1;
    }
    int valor = fila->itens[fila->frente];
    fila->frente++;
    return valor;
}

// Imprime a fila
void imprimirFila(Fila* fila) {
    if (estaVazia(fila)) {
        printf("Fila vazia!\n");
        return;
    }
    printf("Fila: ");
    for (int i = fila->frente; i <= fila->tras; i++) {
        printf("%d ", fila->itens[i]);
    }
    printf("\n");
}

int main() {
    Fila fila;
    inicializarFila(&fila);

    enfileirar(&fila, 10);
    enfileirar(&fila, 20);
    enfileirar(&fila, 30);
    imprimirFila(&fila);

    printf("Desenfileirado: %d\n", desenfileirar(&fila));
    imprimirFila(&fila);

    return 0;
}
