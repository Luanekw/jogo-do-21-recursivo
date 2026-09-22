# 🃏 Jogo do 21 em C (Com Recursividade)

Este projeto consiste em uma implementação simplificada do tradicional **Jogo do 21 (Blackjack)** utilizando a linguagem C. Desenvolvido como atividade prática para a disciplina de **Estrutura de Dados**, o objetivo principal do projeto é aplicar conceitos de **recursividade** no controle de fluxo do jogo.

## 📌 Sumário

* [Sobre o Projeto](#-sobre-o-projeto)

* [Estrutura do Código e Recursividade](#-estrutura-do-código-e-recursividade)

* [Regras do Jogo](#-regras-do-jogo)

* [Como Executar o Projeto](#-como-executar-o-projeto)

  * [Pré-requisitos](#pré-requisitos)

  * [Passo a Passo](#passo-a-passo)

* [Código-Fonte](#-código-fonte)

* [Autora](#-autora)

## 💡 Sobre o Projeto

O **Jogo do 21** é uma aplicação interativa via terminal na qual o jogador busca atingir a pontuação máxima de **21 pontos** sem ultrapassá-la. O jogo sorteia cartas aleatórias (com valores de 1 a 10) e permite ao jogador decidir se deseja comprar mais cartas ou parar. Ao final da rodada do jogador, a pontuação é comparada com a pontuação gerada para a máquina (adversário).

## 🔄 Estrutura do Código e Recursividade

A principal diretiva deste projeto é a utilização de **recursividade** em substituição a laços de repetição tradicionais (`while` / `for`) para gerenciar as rodadas de compra de cartas.

### Como a função `pedirCarta` funciona:

1. **Caso Base 1 (Estouro):** Se a pontuação acumulada ultrapassar 21, a recursão encerra indicando a derrota imediata.

2. **Caso Base 2 (Vitória Perfeita):** Se a pontuação for exatamente 21, a recursão encerra.

3. **Caso Base 3 (Parada do Jogador):** Se o jogador optar por não comprar mais cartas (`'n'` ou `'N'`), a função retorna a pontuação atual.

4. **Passo Recursivo:** Se o jogador desejar continuar (`'s'` ou `'S'`), uma nova carta aleatória é gerada e a função `pedirCarta` chama a si mesma passando como argumento a **nova pontuação somada** (`pontuacaoAtual + novaCarta`).

## 🎮 Regras do Jogo

* O jogador inicia com **2 cartas** sorteadas aleatoriamente (valores entre 1 e 10).

* Em cada rodada, o jogador pode optar por pedir uma nova carta ou manter a pontuação atual.

* Se a pontuação ultrapassar **21**, o jogador perde automaticamente.

* Se a pontuação atingir exatos **21**, o jogador ganha de forma imediata.

* Caso o jogador opte por parar com menos de 21 pontos, a máquina sorteia uma pontuação entre **15 e 20 pontos** para competir.

* **Resultado final:** Vence quem tiver a maior pontuação sem ultrapassar 21. Em caso de pontuações iguais, ocorre empate.

## 🚀 Como Executar o Projeto

### Pré-requisitos

Para compilar e executar este programa, você precisará de um compilador C instalado em seu ambiente (como GCC, Clang ou MinGW).

* **Linux / MacOS:** Geralmente já possuem o `gcc` pré-instalado.

* **Windows:** É possível utilizar o MinGW, WSL, ou IDEs como Dev-C++, Code::Blocks ou VS Code com extensão C/C++.

### Passo a Passo

1. **Clonar o Repositório:**

   ```bash
   git clone https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git
   cd SEU_REPOSITORIO
   ```

2. **Compilar o Código:**
   Utilize o GCC no seu terminal/prompt de comando:

   ```bash
   gcc main.c -o jogo21
   ```

3. **Executar a Aplicação:**

   * **Linux / MacOS:**

     ```bash
     ./jogo21
     ```

   * **Windows:**

     ```cmd
     jogo21.exe
     ```

## 💻 Código-Fonte

```c
/*
 * Disciplina: Estrutura de Dados
 * Atividade 1: Jogo com Recursividade
 * Jogo: Jogo do 21 (Blackjack)
 */

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

/**
 * Função recursiva responsável pela dinâmica de compra de cartas do jogador.
 * @param pontuacaoAtual A soma atual dos valores das cartas do jogador.
 * @return A pontuação final atingida pelo jogador.
 */
int pedirCarta(int pontuacaoAtual) {
    char opcao;
    
    // Condição de estouro (Condição de Parada 1)
    if (pontuacaoAtual > 21) {
        printf("Você estourou 21! Fim de jogo\n");
        return pontuacaoAtual;
    } 
    
    // Condição de pontuação máxima (Condição de Parada 2)
    if (pontuacaoAtual == 21) {
        printf("Pontuação perfeita! Você venceu\n");
        return pontuacaoAtual;
    }
    
    printf("Deseja comprar nova carta? (s/n)\n");
    scanf(" %c", &opcao);
    
    // Condição de parada por escolha do jogador (Condição de Parada 3)
    if (opcao != 's' && opcao != 'S') {
        return pontuacaoAtual;
    }
    
    // Gera uma nova carta com valor entre 1 e 10
    int novaCarta = (rand() % 10) + 1; 
    printf("Você tirou uma carta no valor de: %d\n", novaCarta);
    printf("Pontuação total: %d\n", pontuacaoAtual + novaCarta);
    
    // Chamada recursiva acumulando o valor da nova carta
    return pedirCarta(pontuacaoAtual + novaCarta);
}

int main() {
    // Inicializa o gerador de números aleatórios com a semente do tempo atual
    srand(time(NULL));
    
    printf("========== JOGO DO 21 ==========\n\n");
    
    int cartaInicial1, cartaInicial2, pontuacaoInicial;
    
    // Sorteio das duas cartas iniciais (valores entre 1 e 10)
    cartaInicial1 = (rand() % 10) + 1;
    cartaInicial2 = (rand() % 10) + 1;
    pontuacaoInicial = cartaInicial1 + cartaInicial2;
    
    printf("Suas cartas iniciais valem: %d e %d\n", cartaInicial1, cartaInicial2);
    printf("Pontuação total: %d\n\n", pontuacaoInicial);
    
    // Início da sequência recursiva para compra de cartas
    int pontuacaoFinal = pedirCarta(pontuacaoInicial);
    
    // Processamento da rodada da máquina caso o jogador não tenha estourado
    if (pontuacaoFinal < 21) {
        // Gera pontuação para a máquina no intervalo entre 15 e 20
        int pontuacaoMaquina = 15 + (rand() % 6);
        
        printf("\n--- RESULTADO FINAL ---\n");
        if (pontuacaoFinal > pontuacaoMaquina) {
            printf("Você venceu!\n");
        } else if (pontuacaoFinal < pontuacaoMaquina) {
            printf("A máquina venceu!\n");
        } else {
            printf("Empate!\n");
        }
        
        printf("Sua pontuação: %d\n", pontuacaoFinal);
        printf("Pontuação da máquina: %d\n", pontuacaoMaquina);
    }
    
    return 0;
}
```

## 👩‍💻 Autora

* **Luane Narumi Sato Kawai**

*Trabalho desenvolvido para a disciplina de Estrutura de Dados.*