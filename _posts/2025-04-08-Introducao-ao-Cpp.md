---
title: Introdução ao C++ para Programação Competitiva
date: 2025-04-08 20:40:00 -300
description: Uma introdução direta a C++ para programação competitiva. 
author: buzz
categories: [Tópicos-Introdutórios,C++]
tags: [easy-level,starter-topics,c++,programacao-competitiva]
---


# Introdução ao C++ para Programação Competitiva

### O que é C++?

C++ é uma linguagem compilada, criada como uma extensão da linguagem C, que adiciona recursos de programação orientada a objetos e abstrações de alto nível sem sacrificar a performance. É uma linguagem multiparadigma, o que significa que você pode escrever código procedural, orientado a objetos ou até funcional, dependendo da sua necessidade.

### Como funciona o C++?

C++ é traduzido por um **compilador** (como o `g++`) diretamente para código de máquina, o que resulta em programas extremamente rápidos. O código fonte passa por etapas como pré-processamento, compilação e linkagem antes de se tornar um executável. Essa abordagem de compilação, aliada ao controle fino sobre memória e tempo de execução, é o que garante a eficiência que a linguagem oferece.

### Por que C++ é a linguagem favorita na programação competitiva?

- **Velocidade**: O tempo de execução do C++ é inferior ao de linguagens interpretadas como Python ou JavaScript.
- **Controle**: C++ permite um controle detalhado sobre a complexidade, memória e otimizações, o que é valioso em problemas limites.
- **Tutoriais**: A maioria dos tutoriais, soluções e problemas clássicos estão disponíveis em C++, o que facilita o aprendizado e a troca de conhecimento.

### Como começar com C++ ?

Você pode optar por instalar C++ na máquina, seguindo algum tutorial no youtube. Mas você pode utilizar compiladores online que funcionam super bem na maioria dos casos, como:

- [Codechef Compiler - +Recomendado](https://www.codechef.com/cpp-online-compiler)
- [Online GDB Compiler](https://www.onlinegdb.com/online_c++_compiler)

---

## Entendendo a Estrutura Base de um programa `.cpp`

### Escrevendo nosso Hello World

Inicialmente, é importante entender a estrutura básica de qualquer programa na linguagem. Vamos começar com o “Hello World”, um exemplo que já nos mostra vários elementos fundamentais de um código em C++:

```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello World" << endl;
    return 0;
}
```

**Vamos analisar o que cada parte faz:**

---

- **`#include <iostream>`**
    
    Essa linha é uma diretiva de pré-processador. Ela informa ao compilador que queremos incluir a biblioteca padrão **`iostream`**, que nos permite fazer entrada e saída de dados — como imprimir na tela com `cout` e ler com `cin`.
    
    > “iostream” vem de “input/output stream” — fluxo de entrada e saída.
    > 

---

- **`using namespace std;`**
    
    C++ organiza seu código em **namespaces** (espaços de nomes). A maioria das funções e objetos da biblioteca padrão estão dentro do namespace `std`.
    
    Se não usássemos essa linha, teríamos que escrever `std::cout` e `std::endl` sempre.
    
    Você pode pensar nela como uma forma de evitar repetir `std::` o tempo todo.
    

---

- **`int main()`**
    
    Esse é o ponto de entrada de qualquer programa em C++.
    
    O programa sempre começa sua execução pela função `main`. Ela retorna um `int` (inteiro), que é o código de saída do programa:
    
    - `return 0;` → significa que o programa terminou com sucesso.
    - Um valor diferente de zero indica erro.

---

- `cout << "Hello World" << endl;`:
    
    Aqui usamos o `cout` (console output) para imprimir na tela. O operador `<<` envia dados para a saída padrão (geralmente o terminal).
    
    - `"Hello World"` é a mensagem que será impressa.
    - `<< endl` adiciona uma quebra de linha **e força a atualização da saída (flush)**, o que garante que o texto será realmente exibido naquele momento.
    
    > Geralmente utilizamos `'\n’` ao invés de `endl` pois é em alguns casos que estamos exibindo diversas vezes uma quebra de linha, fazer essa substituição deixa o código com um tempo bem menor de execução.
    > 

---

- `return 0;`
    
    Como dito antes, indica que o programa terminou corretamente. Em competições, mesmo que o `return` não seja obrigatório nas versões mais recentes do C++, ainda é uma boa prática mantê-lo, pois alguns juízes automáticos esperam essa convenção.
    

---

## Lidando com Dados: Entrada, Tipos, Operações e Controle

### 📥 Entrada de Dados

A leitura de dados é feita principalmente com `cin`, que funciona em conjunto com o operador `>>`. Ele lê dados da entrada padrão (geralmente o teclado ou, em competições, arquivos ou testes automáticos).

```cpp
int x;
cin >> x;
```

É possível ler múltiplos valores em sequência:

```cpp
int a, b;
cin >> a >> b;
```

C++ também suporta leitura de strings com `cin` (sem espaços) e `getline` (com espaços):

```cpp
string nome;
cin >> nome; // lê até o primeiro espaço

string frase;
getline(cin, frase); // lê a linha completa
```

---

### 🧮 Tipos de Variáveis

C++ é uma linguagem **estaticamente tipada**, ou seja, você precisa declarar o tipo da variável antes de usá-la.

Alguns tipos mais usados em competições:

| Tipo | Descrição | Exemplo |
| --- | --- | --- |
| `int` | Números inteiros (até ±2*10⁹) | `int idade = 18;` |
| `long long` | Números inteiros grandes | `long long x = 1e18;` |
| `double` | Números reais (ponto flutuante) | `double pi = 3.14;` |
| `char` | Um único caractere | `char letra = 'A';` |
| `string` | Sequência de caracteres (texto) | `string nome = "João";` |
| `bool` | Valores lógicos (true ou false) | `bool certo = true;` |

> Use long long quando estiver lidando com somas ou multiplicações que podem ultrapassar o limite de int.
> 

---

### ➕ Operações Matemáticas

C++ suporta todas as operações aritméticas básicas:

```cpp
int a = 5, b = 2;

int soma = a + b;
int sub = a - b;
int mult = a * b;
int div = a / b;     // divisão inteira: 5 / 2 = 2
int mod = a % b;     // resto da divisão: 5 % 2 = 1

```

Para números reais (decimais), use `double`:

```cpp
double x = 5.0 / 2.0; // 2.5
```

---

### 🔁 Estruturas de Controle e Condicionais

As estruturas de controle definem o fluxo do programa: decisões, repetições e laços.

### `if`, `else if`, `else`

```cpp
int x;
cin >> x;

if (x > 0) {
    cout << "Positivo";
} else if (x == 0) {
    cout << "Zero";
} else {
    cout << "Negativo";
}
```

### `for` — laço com controle de iteração

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << " ";
}
```

### `while` — laço com condição

```cpp
int x = 0;
while (x < 5) {
    cout << x << " ";
    x++;
}
```

### `do while` — executa pelo menos uma vez

```cpp
int x = 0;
do {
    cout << x << " ";
    x++;
} while (x < 5);
```

## Laços de Repetição (Loops)

Em competições, é muito comum repetirmos operações: percorrer um array, somar valores, simular algo. Para isso, usamos os **laços de repetição**, também chamados de **loops**.

### 🔁 `for` – Laço com controle definido

É o mais usado quando sabemos quantas vezes queremos repetir algo.

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << " ";
}

```

> Saída: 0 1 2 3 4
> 

Partes do `for`:

- **inicialização**: `int i = 0`
- **condição**: `i < 5`
- **incremento**: `i++`

Também pode ser usado para percorrer arrays ou vetores:

```cpp
#include <vector>
vector<int> v = {10, 20, 30};
for (int i = 0; i < v.size(); i++) {
    cout << v[i] << " ";
}

```

---

### 🔄 `while` – Laço com condição

Ideal quando **não sabemos** quantas repetições serão necessárias de antemão.

```cpp
int x = 0;
while (x < 5) {
    cout << x << " ";
    x++;
}

```

Muito usado para ler entrada até o fim:

```cpp
int x;
while (cin >> x) {
    cout << "Lido: " << x << "\n";
}

```

---

### 🔁 `do while` – Executa ao menos uma vez

```cpp
int x = 0;
do {
    cout << x << " ";
    x++;
} while (x < 5);

```

---

## Funções

Funções permitem **quebrar o código em pedaços reutilizáveis**, facilitando testes, organização e clareza. Em problemas competitivos, isso ajuda a manter o raciocínio isolado e mais limpo.

### 📌 Como declarar uma função

```cpp
int soma(int a, int b) {
    return a + b;
}

```

Para usá-la:

```cpp
int x = soma(3, 4); // x vale 7

```

### 🛠️ Exemplo com verificação de número primo

```cpp
bool ehPrimo(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

```

Uso:

```cpp
int n;
cin >> n;
if (ehPrimo(n)) {
    cout << "É primo\n";
} else {
    cout << "Não é primo\n";
}

```

## Tente resolver esses problemas:

- [Olá Neps Academy](https://neps.academy/br/exercise/1)
- [Soma Fácil](https://neps.academy/br/exercise/134)
- [Par ou Ímpar](https://neps.academy/br/exercise/148)
- [Média Inteira](https://neps.academy/br/exercise/136)
- [Aprovado ou Reprovado](https://neps.academy/br/exercise/86)
