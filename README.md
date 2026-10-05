# Trabalho 2 - Árvores Binárias e Análise de Complexidade

## Descrição
Implementação de uma biblioteca genérica de Árvores Binárias de Busca em Java, integrada com um programa de gestão de contactos via terminal. Este projeto faz parte da disciplina de **Técnicas de Programação Avançada** e contempla a análise matemática e empírica da complexidade dos algoritmos, comparando os tempos de execução entre árvores degeneradas e árvores perfeitamente balanceadas.

## Integrantes do Grupo
* Apoema Moreira Alves Fernandes
* Heloísa Hand
* Gabriela Demezio

## Estrutura do Projeto
O código-fonte está organizado nos seguintes pacotes:
* `src/main/java/colecao/`: Interface base (`IColecao.java`).
* `src/main/java/arvorebinaria/`: Biblioteca de árvores binárias (`ArvoreBinaria.java`, `ArvoreBinariaBase.java`, `NoArvore.java`).
* `src/main/java/lista/`: Biblioteca de listas encadeadas herdada do Trabalho 1 (`ListaEncadeada.java`, `No.java`).
* `src/main/java/app/`: Domínio, aplicação principal e gerador de massa de testes (`Contato.java`, `ProgramaContatos.java`, `GeradorArquivosOrdenados.java`, `GeradorArquivosBalanceados.java`).

## Arquivos de Entrada (Testes Empíricos)
Para os testes de complexidade, o programa `GeradorArquivos.java` foi adaptado para gerar dois cenários distintos:
1. **Ficheiros Ordenados:** Telefones em ordem crescente para forçar a criação de árvores totalmente degeneradas (comportamento de lista $O(n)$).
2. **Ficheiros Balanceados:** Inserções calculadas com divisão de intervalos para gerar árvores perfeitamente balanceadas logo na carga (comportamento $O(\log n)$).

O formato de cada linha do ficheiro é: `Nome,telefone` (Exemplo: `Ana Silva,123445555`).

## Como Compilar e Executar

### Pré-requisitos
* Java JDK 8 ou superior.

### Compilação
No terminal, dentro da pasta raiz do projeto, execute o seguinte comando:
```bash
javac -d . src/main/java/colecao/*.java src/main/java/lista/*.java src/main/java/arvorebinaria/*.java src/main/java/app/*.java
