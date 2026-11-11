# PILHAS-FILAS-


#include <stdio.h>
#include <string.h>

#define MAX 5

char fila[MAX][10]; /* FILA DE PACOTES */
int qtdFila = 0; /* QUANTIDADE DE PACOTES NA FILA */

char pilha[MAX][10]; /* PILHA DE PACOTES */
int topo = -1; /* VARIAVEL QUE CONTROLA O TOPO DA PILHA */

void incluirPacote() { /* FUNCAO PARA INCLUIR PACOTES NA FILA */
    char codigo[10];

    if (qtdFila < MAX) {
        printf("Digite o codigo do pacote: ");
        scanf("%9s", codigo);

        strcpy(fila[qtdFila], codigo);
        qtdFila++;

        printf("Pacote %s incluido na fila.\n", codigo);
    } else {
        printf("Fila cheia!\n");
    }
}

void carregarPacote() { /* FUNCAO PARA CARREGAR PACOTES NO CAMINHAO */
    char pacote[10];
    int i;

    if (qtdFila == 0) {
        printf("Romaneio vazio, nada a carregar!\n");
        return;
    }

    if (topo == MAX - 1) {
        printf("Caminhao cheio, o pacote %s continua no Romaneio.\n", fila[0]);
        return;
    }

    strcpy(pacote, fila[0]);

    for (i = 0; i < qtdFila - 1; i++) {
        strcpy(fila[i], fila[i + 1]);
    }

    qtdFila--;

    topo++;

    strcpy(pilha[topo], pacote);

    printf("Pacote %s carregado no caminhao.\n", pacote);
}

void retirarDocaminhao() { /* FUNCAO PARA DESCARREGAR PACOTES DO CAMINHAO */

    if (topo == -1) {
        printf("Caminhao vazio, nada a descarregar!\n");
        return;
    }

    printf("Pacote %s retirado do caminhao.\n", pilha[topo]);

    topo--;
}

void mostrar() { /* FUNCAO PARA MOSTRAR O ROMANEIO E O CAMINHAO */
    int i;

    printf("\nRomaneio (frente ao fim): ");

    for (i = 0; i < qtdFila; i++) {
        printf("%s ", fila[i]);
    }

    printf("\n");

    printf("Caminhao (base ao topo): ");

    for (i = 0; i <= topo; i++) {
        printf("%s ", pilha[i]);
    }

    printf("\n");
}

int main() {
    int opcao;

    do {
        printf("\n===== MENU =====\n");
        printf("1. Incluir pacote no romaneio\n");
        printf("2. Retirar pacote da fila e carregar\n");
        printf("3. Retirar pacote do caminhao\n");
        printf("4. Mostrar romaneio e caminhao\n");
        printf("0. Sair\n");

        printf("Opcao: ");
        scanf("%d", &opcao);

        if (opcao == 1) {
            incluirPacote();

        } else if (opcao == 2) {
            carregarPacote();

        } else if (opcao == 3) {
            retirarDocaminhao();

        } else if (opcao == 4) {
            mostrar();

        } else if (opcao != 0) {
            printf("Opcao invalida!\n");
        }

    } while (opcao != 0);

    return 0;
}
