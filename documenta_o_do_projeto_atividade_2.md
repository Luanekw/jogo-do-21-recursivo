# 🃏 Jogo do 21 em C (Recursividade + Lista Simplesmente Encadeada)

> **Disciplina:** Estrutura de Dados — Atividade Avaliativa 2  
> **Linguagem:** C pura (Alocação Dinâmica de Memória)

Este projeto dá continuidade ao **Jogo do 21 (Blackjack)** desenvolvido na Atividade 1, incorporando uma **Lista Simplesmente Encadeada** alocada dinamicamente para registrar, ordenar e apresentar o ranking de pontuações dos jogadores ao longo das partidas.

---

## 📌 Sumário

* [Sobre o Projeto](#-sobre-o-projeto)
* [Estrutura de Dados Dinâmica](#-estrutura-de-dados-dinâmica)
* [Lógica de Recursividade](#-lógica-de-recursividade)
* [Funcionalidades Implementadas](#-funcionalidades-implementadas)
* [Como Compilar e Executar](#-como-compilar-e-executar)
* [Demonstração de Execução](#-demonstração-de-execução)
* [Código-Fonte Completo](#-código-fonte-completo)
* [Autora](#-autora)

---

## 💡 Sobre o Projeto

A aplicação integra dois conceitos fundamentais de **Estrutura de Dados**:
1. **Recursividade:** Utilizada na mecânica principal do jogo para gerenciar a compra sucessiva de cartas pelo jogador.
2. **Alocação Dinâmica e Lista Encadeada:** Utilizada para armazenar o histórico de partidas sem o uso de vetores de tamanho fixo, permitindo que o ranking cresça sob demanda e exiba os resultados ordenados pelo melhor desempenho.

---

## 🔗 Estrutura de Dados Dinâmica

Para gerenciar as pontuações foi implementada uma **Lista Simplesmente Encadeada** por meio da estrutura `Jogador`:

```c
typedef struct Jogador {
    char nome[50];
    int pontuacao;
    struct Jogador *proximo; // ponteiro para o próximo nó da lista
} Jogador;
```

### Operações da Lista Encadeada:
* **`criarLista()`:** Inicializa o ponteiro de início da lista como `NULL`.
* **`inserirOrdenado()`:** Utiliza `malloc(sizeof(Jogador))` para alocar dinamicamente um novo nó na memória e o insere diretamente na posição correta em **ordem decrescente de pontuação**.
  * *Regra de classificação:* Jogadores com pontuação válida ($\le 21$) ocupam o topo do ranking (do maior para o menor valor). Jogadores que ultrapassaram 21 pontos (*estouraram*) recebem prioridade inferior (`-1`) e são posicionados ao final da lista.
* **`exibirRanking()`:** Percorre toda a lista encadeada do início ao fim exibindo a colocação, o nome do jogador e sua pontuação.
* **`liberarLista()`:** Percorre os nós liberando toda a memória alocada dinamicamente com `free()` antes do encerramento do programa, evitando vazamentos de memória (*memory leaks*).

---

## 🔄 Lógica de Recursividade

A função recursiva `pedirCarta(int pontuacaoAtual)` controla o turno do jogador sem o uso de laços `while` ou `for`:

* **Casos Base (Condições de Parada):**
  1. `pontuacaoAtual > 21` — O jogador estourou o limite e a partida encerra.
  2. `pontuacaoAtual == 21` — O jogador atingiu a pontuação perfeita e vence imediatamente.
  3. `opcao != 's' && opcao != 'S'` — O jogador opta por parar de comprar cartas.
* **Passo Recursivo:** Caso o jogador deseje continuar, uma nova carta aleatória (de 1 a 10) é sorteada e a função chama a si mesma passando a pontuação acumulada (`pedirCarta(pontuacaoAtual + novaCarta)`).

---

## ⚙️ Funcionalidades Implementadas

* **Menu Interativo:** Permite jogar múltiplas partidas consecutivas, consultar o ranking atualizado a qualquer momento ou encerrar o programa.
* **Cadastro Dinâmico:** Solicita o nome do jogador antes de cada partida e registra automaticamente o resultado obtido ao final da rodada.
* **Ranking Ordenado:** Apresenta o desempenho comparativo de todos os participantes da sessão.

---

## 🚀 Como Compilar e Executar

### Pré-requisitos
* Compilador C (`gcc`, `clang` ou `MinGW`) instalado no sistema.

### Passo a Passo

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/Luanekw/jogo-do-21-recursivo.git
   cd jogo-do-21-recursivo
   ```

2. **Compile o código-fonte:**
   ```bash
   gcc main.c -o jogo21
   ```

3. **Execute o programa:**
   * **Linux / macOS:**
     ```bash
     ./jogo21
     ```
   * **Windows:**
     ```cmd
     jogo21.exe
     ```

---

## 🖥️ Demonstração de Execução

Abaixo está um exemplo de fluxo de execução no terminal demonstrando o cadastro de múltiplos jogadores e a exibição do ranking ordenado:

```text
=== MENU PRINCIPAL - JOGO DO 21 ===
1. Jogar nova partida (Cadastrar pontuacao)
2. Exibir ranking ordenado dos jogadores
0. Sair
Escolha uma opcao: 1
Digite o nome do jogador: Luane
Suas cartas iniciais valem: 9 e 8
Pontuação total: 17
Deseja comprar nova carta? (s/n)
s
Você tirou uma carta no valor de: 3
Pontuação total: 20
Deseja comprar nova carta? (s/n)
n
Você venceu!
Sua pontuação: 20
Pontuação da máquina: 18

>> Pontuacao de Luane registrada no ranking!

=== MENU PRINCIPAL - JOGO DO 21 ===
1. Jogar nova partida (Cadastrar pontuacao)
2. Exibir ranking ordenado dos jogadores
0. Sair
Escolha uma opcao: 1
Digite o nome do jogador: Carlos
Suas cartas iniciais valem: 10 e 7
Pontuação total: 17
Deseja comprar nova carta? (s/n)
s
Você tirou uma carta no valor de: 8
Pontuação total: 25
Você estourou 21! Fim de jogo

>> Pontuacao de Carlos registrada no ranking!

=== MENU PRINCIPAL - JOGO DO 21 ===
1. Jogar nova partida (Cadastrar pontuacao)
2. Exibir ranking ordenado dos jogadores
0. Sair
Escolha uma opcao: 1
Digite o nome do jogador: Ana
Suas cartas iniciais valem: 10 e 1
Pontuação total: 11
Deseja comprar nova carta? (s/n)
s
Você tirou uma carta no valor de: 10
Pontuação total: 21
Pontuação perfeita! Você venceu

>> Pontuacao de Ana registrada no ranking!

=== MENU PRINCIPAL - JOGO DO 21 ===
1. Jogar nova partida (Cadastrar pontuacao)
2. Exibir ranking ordenado dos jogadores
0. Sair
Escolha uma opcao: 2

=========================================
       RANKING DE PONTUACOES (21)        
=========================================
1º Lugar | Jogador: Ana             | Pontos: 21
2º Lugar | Jogador: Luane           | Pontos: 20
3º Lugar | Jogador: Carlos          | Pontos: 25 (Estourou)
=========================================
```

---

## 💻 Código-Fonte Completo

```c
/*
Estrutura de Dados
Atividade 2: jogo com recursividade e estrutura dinâmica
jogo: jogo do 21
*/

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>


//estrutura dinâmica


typedef struct Jogador {
    char nome[50];
    int pontuacao;
    struct Jogador *proximo; //ponteiro para o próximo nó da lista
} Jogador;

//inicializa lista vazia

Jogador* criarLista() {
    return NULL;
}

//
//
Jogador* inserirOrdenado(Jogador *inicio, const char *nome, int pontuacao) {
    
    //alocação dinâmica de memória
    Jogador *novo = (Jogador*)malloc(sizeof(Jogador));
    
    if(novo == NULL) {
        printf("ERRO: Falha na alocação!");
        return inicio;
    }
    
    strcpy(novo->nome, nome);
    novo->pontuacao = pontuacao;
    novo->proximo = NULL;
    
    //define uma pontuação de classificação 
    int scoreNovo = (pontuacao <= 21) ? pontuacao : -1;
    
    //Se a lista estiver vazia
    if (inicio == NULL) {
        return novo;
    }
    
    //Se a um novo jogador tem uma pontuação maior que o primeiro da lista
    int scoreInicio = (inicio->pontuacao <= 21) ? inicio->pontuacao : -1;
    if (scoreNovo > scoreInicio) {
        novo->proximo = inicio;
        return novo;
    }
    
    //percorre a lista para encontrar a posição correta mantendo a ordem decrescente da pontuação
    Jogador *atual = inicio;
    while (atual->proximo != NULL) {
        int scoreProximo = (atual->proximo->pontuacao <= 21) ? atual->proximo->pontuacao : -1;
        if (scoreNovo > scoreProximo) {
            break;
        }
        atual = atual->proximo;
    }

    novo->proximo = atual->proximo;
    atual->proximo = novo;

    return inicio;
    
}

//percorre a lista e mostra em ordem
void exibirRanking(Jogador *inicio) {
    printf("\n=========================================\n");
    printf("       RANKING DE PONTUACOES (21)        \n");
    printf("=========================================\n");

    if (inicio == NULL) {
        printf("Nenhuma partida registrada ainda.\n");
        printf("=========================================\n");
        return;
    }

    Jogador *atual = inicio;
    int posicao = 1;

    while (atual != NULL) {
        if (atual->pontuacao <= 21) {
            printf("%dº Lugar | Jogador: %-15s | Pontos: %d\n", 
                   posicao, atual->nome, atual->pontuacao);
        } else {
            printf("%dº Lugar | Jogador: %-15s | Pontos: %d (Estourou)\n", 
                   posicao, atual->nome, atual->pontuacao);
        }
        
        //%-15s significado: %s => string; - => alinha o texto para a esquerda; 15 => separa 15 espaços para o nome
        
        atual = atual->proximo;
        posicao++;
    }
    printf("=========================================\n");
}


// Libera toda a memória alocada dinamicamente antes de encerrar o programa
void liberarLista(Jogador *inicio) {
    Jogador *atual = inicio;
    while (atual != NULL) {
        Jogador *temp = atual;
        atual = atual->proximo;
        free(temp);
    }
}



//Lógica geral do jogo 21 (Atividade 1)

int pedirCarta(int pontuacaoAtual) {
    char opcao;
    
    //condição de estouro (para o jogo)
    if (pontuacaoAtual > 21) {
        printf("Você estourou 21! Fim de jogo\n");
        return pontuacaoAtual;
    } 
    
    //condição de pontuação máxima/vitória (para o jogo)
    if (pontuacaoAtual == 21) {
        printf("Pontuação perfeita! Você venceu\n");
        return pontuacaoAtual;
    }
    
    printf("Deseja comprar nova carta? (s/n)\n");
    scanf(" %c", &opcao);
    
    //sair caso não queira mais comprar carta
    if (opcao != 's' && opcao != 'S') {
        return pontuacaoAtual;
    }
    
    int novaCarta = (rand() % 10) + 1; //carta de 1 a 10
    printf("Você tirou uma carta no valor de: %d\n", novaCarta);
    printf("Pontuação total: %d\n", pontuacaoAtual + novaCarta);
    
    //recursividade somando a nova carta
    return pedirCarta(pontuacaoAtual + novaCarta);
}


int jogarPartida() {
    
    int cartaInicial1,
        cartaInicial2,
        pontuacaoInicial;
    
    //valor inicial aleatório entre 1 e 10
    cartaInicial1 = (rand() % 10) + 1;
    cartaInicial2 = (rand() % 10) + 1;
    
    pontuacaoInicial = cartaInicial1 + cartaInicial2;
    
    printf("Suas cartas iniciais valem: %d e %d\n", cartaInicial1, cartaInicial2);
    printf("Pontuação total: %d\n", pontuacaoInicial);
    
    //chama função recursiva
    int pontuacaoFinal = pedirCarta(pontuacaoInicial);
    
    //criar uma pontuação para a máquina entre 15 a 20 para competir com o jogador
    if (pontuacaoFinal < 21) {
        int pontuacaoMaquina = 15 + (rand() % 6);
        
        if (pontuacaoFinal > pontuacaoMaquina) {
            printf("Você venceu!\n");
            printf("Sua pontuação: %d\n", pontuacaoFinal);
            printf("Pontuação da máquina: %d\n", pontuacaoMaquina);
        } else if (pontuacaoFinal < pontuacaoMaquina) {
            printf("A máquina venceu!\n");
            printf("Sua pontuação: %d\n", pontuacaoFinal);
            printf("Pontuação da máquina: %d\n", pontuacaoMaquina);
        } else {
            printf("Empate!\n");
            printf("Sua pontuação: %d\n", pontuacaoFinal);
            printf("Pontuação da máquina: %d\n", pontuacaoMaquina);
        }
    }
        
    return pontuacaoFinal;
}


//função principal (MENU)

int main() {
    
    //inicializa gerador de número aleatório    
    srand(time(NULL));
    
    //inicializa a lista encadeada dinâmica
    Jogador *ranking = criarLista();
    int opcaoMenu;
    char nomeJogador[50];
    
    do {
        printf("\n=== MENU PRINCIPAL - JOGO DO 21 ===\n");
        printf("1. Jogar nova partida (Cadastrar pontuacao)\n");
        printf("2. Exibir ranking ordenado dos jogadores\n");
        printf("0. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcaoMenu);
        getchar(); // Limpa o '\n' do buffer de entrada
        
        switch (opcaoMenu) {
            case 1:
                printf("Digite o nome do jogador: ");
                fgets(nomeJogador, sizeof(nomeJogador), stdin);
                nomeJogador[strcspn(nomeJogador, "\n")] = '\0'; // Remove quebra de linha

                int pontuacaoObtida = jogarPartida();
                
                // Armazena dinamicamente na lista encadeada já em ordem de classificação
                ranking = inserirOrdenado(ranking, nomeJogador, pontuacaoObtida);
                printf("\n>> Pontuacao de %s registrada no ranking!\n", nomeJogador);
                break;

            case 2:
                exibirRanking(ranking);
                break;

            case 0:
                printf("Saindo...\n");
                liberarLista(ranking);
                break;

            default:
                printf("Opcao invalida! Tente novamente.\n");
        }

    } while (opcaoMenu != 0);
    
    return 0;
}
```

---

## 👩‍💻 Autora

* **Luane Narumi Sato Kawai**  
*Trabalho desenvolvido para a disciplina de Estrutura de Dados.*