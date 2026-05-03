// ============================================================================
// PROBLEMA DO LABIRINTO - ALGORITMO DE BACKTRACKING
// ============================================================================
// FONTE ORIGINAL: GeeksforGeeks
// URL: https://www.geeksforgeeks.org/rat-in-a-maze-backtracking-2/
//
// ADAPTAÇÕES E REESCRITAS REALIZADAS:
// [1] Mudança na representação: 0 = livre, 1 = parede (invertido)
// [2] Adição de matriz de visitadas explícita (melhor controle)
// [3] Função separada para validar célula (mais legível)
// [4] Adição de contador de tentativas (didático)
// [5] Impressão do caminho passo a passo
// [6] Visualização melhorada com coordenadas
// ============================================================================

#include <stdio.h>
#include <string.h>
#include <stdbool.h>

#define TAMANHO 5

// Adicionei uma matriz de visitadas explícita
// Isso deixa mais claro quando uma célula foi visitada
int visitadas[TAMANHO][TAMANHO];
int solucao[TAMANHO][TAMANHO];
int tentativas = 0;  // [ADAPTAÇÃO 4] Contador de tentativas

// ============================================================================
// OBJETIVO: Validar se uma célula pode ser visitada
// FUNÇÃO AUXILIAR
// ============================================================================
// Esta função verifica se uma posição (x, y) é válida para ser visitada.
// Ela é chamada antes de tentar explorar uma nova célula.
//
// CRITÉRIO DE VALIDAÇÃO (escolha parcial válida):
// Uma célula é válida se:
// 1. Está dentro dos limites do labirinto (0 <= x < TAMANHO e 0 <= y < TAMANHO)
// 2. Não é uma parede (labirinto[x][y] == 0, pois 0 = livre, 1 = parede)
// 3. Ainda não foi visitada (visitadas[x][y] == 0)
//
// Criei uma função separada para validar célula
// Deixa o código mais legível e fácil de entender
// ============================================================================
bool celula_valida(int labirinto[TAMANHO][TAMANHO], int x, int y) {

    // CRITÉRIO 1: Verifica se está dentro dos limites
    // Se sair do mapa, a célula não é válida
    if (x < 0 || x >= TAMANHO || y < 0 || y >= TAMANHO) {
        return false;
    }

    // CRITÉRIO 2: Invertemos: 0 = livre, 1 = parede
    // Se for parede (1), não pode passar
    // Agora é mais intuitivo (0 = pode passar)
    if (labirinto[x][y] == 1) {
        return false;
    }

    // CRITÉRIO 3: Verifica se já foi visitada
    // Se já visitou, não volta (evita loop infinito)
    if (visitadas[x][y] == 1) {
        return false;
    }

    return true;
}

// Esta é a função principal do algoritmo. Ela tenta explorar todas as
// direções possíveis usando recursão. Se uma direção não leva à solução,
// ela retrocede e tenta outra direção.
//
// CONDIÇÃO DE PARADA DA RECURSÃO:
// O algoritmo para quando:
// 1. Chega ao destino (x == TAMANHO-1 && y == TAMANHO-1) -> retorna TRUE
// 2. Encontra uma célula inválida (parede, visitada ou fora dos limites) -> retorna FALSE
// 3. Nenhuma das 4 direções leva à solução -> retorna FALSE
//
// MOMENTO DE AVANÇO (tentativa):
// Quando uma célula é válida, o algoritmo:
// 1. Marca como visitada (visitadas[x][y] = 1)
// 2. Marca como parte da solução (solucao[x][y] = 1)
// 3. Tenta explorar em 4 direções: baixo, direita, cima, esquerda
// 4. Se alguma direção retornar TRUE, a solução foi encontrada
//
// MOMENTO DE RETROCESSO (backtrack):
// Quando nenhuma direção leva à solução:
// 1. Remove a célula da solução (solucao[x][y] = 0)
// 2. Retorna FALSE para tentar outra direção
// 3. A célula continua marcada como visitada (para não revisitar)

bool resolver_util(int labirinto[TAMANHO][TAMANHO], int x, int y) {

    tentativas++;  // Conta cada tentativa

    // ========== CONDIÇÃO DE PARADA 1: Chegou ao destino ==========
    // Se chegou no canto inferior direito (TAMANHO-1, TAMANHO-1),
    // encontrou a solução! Marca como parte da solução e retorna TRUE
    if (x == TAMANHO - 1 && y == TAMANHO - 1) {
        solucao[x][y] = 1;
        return true;
    }

    // ========== CRITÉRIO DE VALIDAÇÃO: Verifica se a célula é válida ==========
    // Antes de explorar, verifica se a posição atual é válida
    // Se não for válida (parede, visitada ou fora dos limites), retorna FALSE
    if (!celula_valida(labirinto, x, y)) {
        return false;
    }

    // ========== AVANÇO: Marca como visitada e adiciona à solução ==========
    // Se chegou aqui, a célula é válida. Marca como visitada
    visitadas[x][y] = 1;
    solucao[x][y] = 1;

    // Imprime o caminho passo a passo
    printf("  Visitando: (%d, %d)\n", x, y);

    // ========== TENTATIVA 1: Tenta mover para BAIXO ==========
    // Tenta explorar a célula abaixo (x+1, y)
    // Se encontrar solução nessa direção, retorna TRUE
    if (resolver_util(labirinto, x + 1, y)) {
        return true;
    }

    // ========== TENTATIVA 2: Tenta mover para DIREITA ==========
    // Se baixo não funcionou, tenta a célula à direita (x, y+1)
    // Se encontrar solução nessa direção, retorna TRUE
    if (resolver_util(labirinto, x, y + 1)) {
        return true;
    }

    // ========== TENTATIVA 3: Tenta mover para CIMA ==========
    // Se direita não funcionou, tenta a célula acima (x-1, y)
    // Uma adição que o código original não tinha
    if (resolver_util(labirinto, x - 1, y)) {
        return true;
    }

    // ========== TENTATIVA 4: Tenta mover para ESQUERDA ==========
    // Se cima não funcionou, tenta a célula à esquerda (x, y-1)
    // Uma adição que o código original não tinha
    if (resolver_util(labirinto, x, y - 1)) {
        return true;
    }

    // ========== RETROCESSO (BACKTRACK) ==========
    // Se nenhuma das 4 direções levou à solução, remove a célula da solução
    // Isso desfaz a escolha anterior e permite tentar outro caminho
    // A célula continua marcada como visitada (para não revisitar)
    solucao[x][y] = 0;
    printf("  Retrocedendo de: (%d, %d)\n", x, y);

    return false;
}

// OBJETIVO: Inicializar o processo de busca
// FUNÇÃO PRINCIPAL
// Esta função:
// 1. Inicializa as matrizes de visitadas e solução
// 2. Reseta o contador de tentativas
// 3. Chama a função recursiva começando do ponto (0, 0)
// 4. Retorna TRUE se encontrou solução, FALSE caso contrário

bool resolver_labirinto(int labirinto[TAMANHO][TAMANHO]) {

    // Inicializa a matriz de visitadas com zeros (nada visitado)
    memset(visitadas, 0, sizeof(visitadas));

    // Inicializa a matriz de solução com zeros (nenhum caminho)
    memset(solucao, 0, sizeof(solucao));

    // Reseta o contador de tentativas
    tentativas = 0;

    // Começa o backtracking do ponto inicial (0, 0)
    // Se encontrar solução, ela será armazenada em 'solucao'
    if (resolver_util(labirinto, 0, 0) == false) {
        printf("\nSolucao nao existe!\n");
        return false;
    }

    return true;
}

// OBJETIVO: Exibir o labirinto em formato visual
// FUNÇÃO AUXILIAR

// Imprime o labirinto com coordenadas para melhor visualização
// Visualização melhorada com coordenadas

void imprimir_labirinto(int labirinto[TAMANHO][TAMANHO]) {
    printf("\nLabirinto (0 = livre, 1 = parede):\n");
    printf("   ");
    for (int j = 0; j < TAMANHO; j++) {
        printf("%d ", j);
    }
    printf("\n");

    for (int i = 0; i < TAMANHO; i++) {
        printf("%d: ", i);
        for (int j = 0; j < TAMANHO; j++) {
            if (labirinto[i][j] == 1) {
                printf("█ ");  // Parede
            } else {
                printf("· ");  // Livre
            }
        }
        printf("\n");
    }
}

// OBJETIVO: Exibir a solução encontrada
// FUNÇÃO AUXILIAR

// Imprime o labirinto com o caminho da solução destacado
// ✓ = célula que faz parte do caminho
// █ = parede
// · = célula livre não visitada
// Visualização melhorada com coordenadas


void imprimir_solucao(int labirinto[TAMANHO][TAMANHO], int sol[TAMANHO][TAMANHO]) {
    printf("\nSolucao encontrada:\n");
    printf("   ");
    for (int j = 0; j < TAMANHO; j++) {
        printf("%d ", j);
    }
    printf("\n");

    for (int i = 0; i < TAMANHO; i++) {
        printf("%i: ", i);
        for (int j = 0; j < TAMANHO; j++) {
            if (sol[i][j] == 1) {
                printf("✓ ");  // Parte do caminho
            } else if (labirinto[i][j] == 1) {
                printf("█ ");  // Parede
            } else {
                printf("· ");  // Não visitado
            }
        }
        printf("\n");
    }
}

// OBJETIVO: Exibir o caminho em formato de coordenadas
// FUNÇÃO AUXILIAR

// Imprime as coordenadas do caminho de forma sequencial
// Exemplo: (0,0) -> (1,0) -> (2,0) -> ...
// Função para imprimir o caminho em coordenadas


void imprimir_caminho(int sol[TAMANHO][TAMANHO]) {
    printf("\nCaminho da solucao:\n");
    printf("(0,0)");

    for (int i = 0; i < TAMANHO; i++) {
        for (int j = 0; j < TAMANHO; j++) {
            if (sol[i][j] == 1 && !(i == 0 && j == 0)) {
                printf(" -> (%d,%d)", i, j);
            }
        }
    }
    printf("\n");
}

int main() {

    printf("============================================================\n");
    printf("PROBLEMA DO LABIRINTO - BACKTRACKING\n");
    printf("Adaptacao do codigo original do GeeksforGeeks\n");
    printf("============================================================\n");
    int labirinto[TAMANHO][TAMANHO] = {
        {0, 1, 0, 0, 0},
        {0, 1, 0, 1, 0},
        {0, 0, 0, 1, 0},
        {1, 1, 0, 0, 0},
        {0, 0, 0, 1, 0}
    };

    imprimir_labirinto(labirinto);

    printf("\nIniciando busca...\n");

    if (resolver_labirinto(labirinto)) {
        printf("\n✓ Solucao encontrada!\n");
        printf("Total de tentativas: %d\n", tentativas);
        imprimir_solucao(labirinto, solucao);
        imprimir_caminho(solucao);
    } else {
        printf("\n✗ Nenhuma solucao encontrada.\n");
    }

    printf("\n" "============================================================\n");
    printf("EXEMPLO 2 - Labirinto Mais Complexo\n");
    printf("============================================================\n");

    int labirinto2[TAMANHO][TAMANHO] = {
        {0, 0, 1, 0, 0},
        {0, 1, 0, 1, 0},
        {0, 1, 0, 0, 0},
        {1, 0, 1, 1, 0},
        {0, 0, 0, 0, 0}
    };

    imprimir_labirinto(labirinto2);

    printf("\nIniciando busca...\n");

    if (resolver_labirinto(labirinto2)) {
        printf("\n✓ Solucao encontrada!\n");
        printf("Total de tentativas: %d\n", tentativas);
        imprimir_solucao(labirinto2, solucao);
        imprimir_caminho(solucao);
    } else {
        printf("\n✗ Nenhuma solucao encontrada.\n");
    }

    printf("\n" "============================================================\n");
    printf("EXEMPLO 3 - Labirinto Sem Solucao\n");
    printf("============================================================\n");

    int labirinto3[TAMANHO][TAMANHO] = {
        {0, 1, 0, 0, 0},
        {0, 1, 1, 1, 0},
        {0, 0, 0, 1, 0},
        {1, 1, 0, 1, 0},
        {0, 0, 0, 1, 1}
    };

    imprimir_labirinto(labirinto3);

    printf("\nIniciando busca...\n");

    if (resolver_labirinto(labirinto3)) {
        printf("\n✓ Solucao encontrada!\n");
        printf("Total de tentativas: %d\n", tentativas);
        imprimir_solucao(labirinto3, solucao);
        imprimir_caminho(solucao);
    } else {
        printf("\n✗ Nenhuma solucao encontrada.\n");
        printf("(A saida esta bloqueada)\n");
    }

    return 0;
}
