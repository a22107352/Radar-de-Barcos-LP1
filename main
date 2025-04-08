

#include <stdio.h>

struct Barco {
    char id;
    int linha;
    int coluna;
};

void imprimirTabela(char tabela[20][80]) {

    for (int i = 0; i < 20; i++) {
        for (int j = 0; j < 80; j++) {
            printf("%c", tabela[i][j]);
        }
        printf("\n");
    }
}

struct Barco encontrarBarco(char tabela[20][80], char id) {
    struct Barco barco = {id, -1, -1};
    for (int i = 0; i < 20; i++) {
        for (int j = 0; j < 80; j++) {
            if (tabela[i][j] == id) {
                barco.linha = i;
                barco.coluna = j;
                return barco;
            }
        }
    }
    return barco;
}

void listarMovimentos(char tabelaAntes[20][80], char tabelaDepois[20][80], char barcoAlvo) {
    struct Barco antes = encontrarBarco(tabelaAntes, barcoAlvo);
    struct Barco depois = encontrarBarco(tabelaDepois, barcoAlvo);

    if (antes.linha == -1 || depois.linha == -1) {
        printf("Barco desapareceu ou não foi encontrado.\n");
    } else if (antes.linha == depois.linha && antes.coluna == depois.coluna) {
        printf("Barco não se moveu.\n");
    } else {
        printf("Movimento: O barco moveu-se ");
        if (depois.linha < antes.linha) printf("para cima.\n");
        else if (depois.linha > antes.linha) printf("para baixo.\n");
        else if (depois.coluna < antes.coluna) printf("para a esquerda.\n");
        else if (depois.coluna > antes.coluna) printf("para a direita.\n");
    }
}


void lerTabelaDeFicheiro(char tabela[20][80], const char *nomeFicheiro) {
    // Abre o ficheiro para leitura
    FILE *ficheiro = fopen(nomeFicheiro, "r");

    // Verifica se o ficheiro foi aberto corretamente
    if (ficheiro == NULL) {
        printf("Erro ao abrir o ficheiro %s\n", nomeFicheiro);
        return; // Se não for possível abrir o ficheiro, a função termina imediatamente
    }

    // Percorre a matriz para preencher os 20x80 caracteres com dados do ficheiro
    for (int i = 0; i < 20; i++) {
        // Loop externo para as 20 linhas
        for (int j = 0; j < 80; j++) {
            // Loop interno para as 80 colunas
            char c = fgetc(ficheiro); // Lê um único carácter do ficheiro

            // Se o carácter for uma nova linha, ignora-o e lê o próximo carácter
            if (c == '\n') {
                c = fgetc(ficheiro);
            }

            // Armazena o carácter lido na matriz
            tabela[i][j] = c;
        }
    }

    // Fecha o ficheiro após a leitura
    fclose(ficheiro);
}

int main() {
    char tabelaAntes[20][80];
    char tabelaDepois[20][80];
    char id3;
    char id4;
    lerTabelaDeFicheiro(tabelaAntes, "tabela_antes.txt");
    lerTabelaDeFicheiro(tabelaDepois, "tabela_depois.txt");
    int opcao;
    do {
        printf("\nMenu:\n");
        printf("1 - Imprimir tabela \"antes\"\n");
        printf("2 - Imprimir tabela \"depois\"\n");
        printf("3 - Consultar as coordenadas de um barco\n");
        printf("4 - Listar barcos que se moveram\n");
        printf("5 - Sair\n");
        printf("Escolha uma opcao:");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                printf("\n");
                printf("Tabela Antes:\n");
                imprimirTabela(tabelaAntes);
                break;
            case 2:
                printf("\n");
            printf("Tabela Depois:\n");
                imprimirTabela(tabelaDepois);
                break;
            case 3:

                int tabelaEscolhida;
                printf(" Qual a tabela que quer consultar? Tabela antes - 1 Tabela depois - 2\n");
                scanf("%d", &tabelaEscolhida);
                printf("Escolha o barco que quer encontrar:\n");
                scanf(" %c", &id3);
                struct Barco barco = encontrarBarco(tabelaEscolhida == 1 ? tabelaAntes : tabelaDepois, id3);
                if (barco.linha == -1) {
                    printf("Barco %c nao encontrado.\n", id3);
                } else {
                    printf("O barco %c encontra-se na linha %d e na coluna %d\n", barco.id, barco.linha+1, barco.coluna+1);
                }
                break;

            case 4:
                printf(" Escolha qual o barco que quer listar o movimento:\n");
                scanf(" %c", &id4);
                listarMovimentos(tabelaAntes, tabelaDepois,id4);
            break;
            case 5:
                printf(" A sair do programa...\n");
                break;

            default:
                printf("Opcao invalida. Tente novamente.\n");
        }
    } while (opcao != 5);
    return 0;
}
