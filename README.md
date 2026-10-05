# Trabalho 2 — Árvores Binárias e Análise de Complexidade

Implementação de uma biblioteca genérica de **Árvores Binárias de Busca** em Java, integrada a um programa de gestão de contatos via terminal. Este projeto faz parte da disciplina de **Técnicas de Programação Avançada** e contempla a análise matemática e empírica da complexidade dos algoritmos, comparando os tempos de execução entre árvores degeneradas, árvores perfeitamente balanceadas e listas encadeadas.

---

## Integrantes do Grupo

- Apoema Moreira Alves Fernandes
- Heloísa Hand
- Gabriela Demezio

---

## Estrutura do Projeto

O código-fonte está organizado nos seguintes pacotes:

| Pacote | Descrição |
|---|---|
| `src/main/java/colecao/` | Interface base (`IColecao.java`) comum a todas as estruturas. |
| `src/main/java/arvorebinaria/` | Biblioteca de árvores binárias (`ArvoreBinaria.java`, `ArvoreBinariaBase.java`, `NoArvore.java`). |
| `src/main/java/lista/` | Biblioteca de listas encadeadas herdada do Trabalho 1 (`ListaEncadeada.java`, `No.java`). |
| `src/main/java/app/` | Domínio, aplicação principal e geradores de massa de testes (`Contato.java`, `ProgramaContatos.java`, `GeradorArquivosOrdenados.java`, `GeradorArquivosBalanceados.java`). |

---

## Arquivos de Entrada

Para os testes de complexidade, foram gerados dois cenários distintos para cada tamanho de massa:

1. **Arquivos Ordenados (`entrada_<N>_ordenado.txt`):** telefones em ordem crescente. Ao serem inseridos na árvore indexada por telefone, produzem uma árvore **totalmente degenerada** (comportamento linear, O(n)).
2. **Arquivos Balanceados (`entrada_<N>_balanceado.txt`):** telefones emitidos na ordem "do meio do intervalo" (recursivamente), produzindo uma árvore **perfeitamente balanceada** já na carga (comportamento logarítmico, O(log n)).

O formato de cada linha do arquivo é: `Nome,telefone` — por exemplo:

```
Ana Silva,000123445
Bruno Lima,000049999
```

---

## Como Compilar e Executar 

Os comandos abaixo funcionam tanto no **PowerShell** quanto no **Prompt de Comando (CMD)**. Execute-os a partir da pasta onde está o código-fonte do projeto.

### Pré-requisitos

- Java JDK 8 ou superior instalado e adicionado ao `PATH`.
- Verifique com:
  ```powershell
  java -version
  javac -version
  ```

### 1. Navegar até a pasta do código

No PowerShell:

```powershell
cd "$env:USERPROFILE\Desktop\Trabalhos-TPA-main\src\main\java"
```

No CMD:

```cmd
cd %USERPROFILE%\Desktop\Trabalhos-TPA-main\src\main\java
```

> Ajuste o caminho conforme onde o projeto está na sua máquina. Se estiver em `Área de Trabalho` em português, use `Desktop` mesmo — é o nome real da pasta no sistema.

### 2. Compilar todos os pacotes

```powershell
javac app\*.java arvorebinaria\*.java colecao\*.java lista\*.java
```

Se não aparecer nenhuma mensagem, a compilação foi bem-sucedida. Os arquivos `.class` são gerados nas mesmas pastas dos respectivos `.java`.

### 3. Gerar os arquivos de entrada

```powershell
java app.GeradorArquivosOrdenados
java app.GeradorArquivosBalanceados
```

Os 8 arquivos são criados no diretório atual (`src\main\java`):

```
entrada_25000_ordenado.txt       entrada_25000_balanceado.txt
entrada_50000_ordenado.txt       entrada_50000_balanceado.txt
entrada_100000_ordenado.txt      entrada_100000_balanceado.txt
entrada_200000_ordenado.txt      entrada_200000_balanceado.txt
```

### 4. Rodar o programa principal

```powershell
java app.ProgramaContatos
```

O programa exibe um menu inicial para escolher a estrutura:

```
Escolha o tipo de estrutura:
1 - Lista ordenada
2 - Lista não ordenada
3 - Árvore binária
```

Em seguida, o menu de operações:

```
===== MENU =====
1 - Carregar dados de arquivo
2 - Adicionar contato
3 - Pesquisar contato por nome
4 - Pesquisar contato por telefone
5 - Remover contato por telefone
6 - Alterar dados de contato
7 - Sair
```

### 5. Roteiro do experimento

Para cada arquivo, siga os passos:

1. Opção **1** → digitar o nome do arquivo (ex.: `entrada_50000_balanceado.txt`).
2. Anotar o tempo de **carga** impresso.
3. Opção **4** → telefone da folha mais profunda → anotar tempo de **busca por telefone**.
4. Opção **3** → nome do contato correspondente → anotar tempo de **busca por nome**.
5. Opção **5** → mesmo telefone → anotar tempo de **remoção**.
6. Opção **7** → sair.

---

## Decisões de Projeto Relevantes

### Comparador genérico

A árvore é genérica (`ArvoreBinaria<T>`) e recebe um `Comparator<T>` no construtor. Isso permite usar a **mesma estrutura** para indexar os contatos por critérios diferentes (nome e telefone), sem duplicar código.

### Duplicatas na árvore por nome

Telefone é único no domínio, mas o **nome não**. Como o programa mantém duas árvores indexando os mesmos contatos, a árvore por nome foi configurada para **permitir duplicatas** — chaves iguais vão para a subárvore direita. Consequências:

- A busca por **telefone** sempre retorna o contato exato (chave única).
- A busca por **nome** retorna **um** dos contatos com aquele nome — o primeiro encontrado descendo pela árvore. Esse comportamento é o aceito pela especificação do trabalho.

## Observações sobre a Busca por Nome

Como o arquivo possui apenas 200 combinações possíveis de nome (20 nomes × 10 sobrenomes), mas pode ter dezenas de milhares de contatos, cada nome aparece muitas vezes. Ao buscar por nome, a árvore retorna **o primeiro contato daquele nome encontrado na descida** — tipicamente o mais "alto" na árvore (primeiro inserido), e não necessariamente o último do arquivo.

Para obter um contato específico, use a **busca por telefone**, que é única no domínio.

---

## Repositório

- **GitHub:** *(https://github.com/apoemafernandes/TRABALHO-2-TPA)*
