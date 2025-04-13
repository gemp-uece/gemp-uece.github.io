---
title: Upsolving 'Bolsistas Can Code ?' ed. 1 - Problema F
date: 2025-04-12 12:40:00 -0300
categories: [Competitive Programming, Upsolving]
description: Resolução do problema "Kefa and Park" do Codeforces.
tags: [tree, dfs]    
author: <ian_domingos>
---

# Upsolving 'Bolsistas Can Code ?' ed. 1 - Problema F

### Estratégia

Ao ler o enunciado do problema, foi percebido que para seria preciso contabilizar os caminhos que, partindo do vértice 1, terminassem em um vértice folha, desde que o caminho nao apresente mais de m gatos consecutivos em nenhum momento. Tendo isso em vista, é preciso criar uma arvore que será percorrida por todos os caminhos possíveis a partir do vértice 1, usando um DFS.

### Representação da arvore

A estrutura escolhida para representação da árvore foi um vetor de vetores dinamicos "graph", no qual cada elemento graph[i] apresentava todos os vértices ligados ao vértice i.

```c++ 
vector graph[100007]; 
```

### Presença dos gatos

Além da arvore, foi criado o vetor de inteiros "hascat", para consultar a presença de gatos em um determinado vértice. Para isso, temos hascat[i] = 1 significando que há um gato no vértice i.

```c++ 
int hascat[100007]; 
```

### Resolução

Após a criação das estruturas, foi criada a função solve, responsável por retornar o número de caminhos possíveis a partir de um vértice. A função recebe os seguintes parámetros:

* curr: vértice atual

* parent: vértice pai do atual

* cats: número de gatos consecutivos acumulados até o vértice atual

* m: número máximo de gatos consecutivos permitidos

Primeiramente, ela verifica se há um gato no vértice atual e ,se sim, incrementa a variável cats, se não, zera a variável, indicando a quebra da sequeência de gatos. Após isso, há a verificação se o limite de m gatos foi ultrapassado. Se isso ocorrer, a função retorna 0, sinalizando que não é possível seguir caminho por aquele vértice. Se o limite foi respeitado, iteramos sobre os vértices ligados ao atual, chamando solve recursivamente para os que são diferentes de seu pai, para dar continuidade ao caminho, ademais, é adicionado o número de caminhos possíveis a partir de cada vértice seguinte em uma variável de soma(sum). Durante essa iteração, também há a verificação de que o vértice seja uma folha, ou seja é o final de um caminho, utilizando o booleano leaf. Por fim, se o vértice atual for uma folha, a função retorna 1, indicando que um caminho possível foi finalizado, se não, a função retorna a variável de soma, indicando o número de caminhos possíveis a partir do vértice atual.

```c++ 
ll solve(int curr, int parent, int cats, int m)
{
    if (hascat[curr] == 1)
        cats++;
    else
        cats = 0;
    if (cats > m)
        return 0;
    bool leaf = true;
    ll sum = 0;
    for (auto next : graph[curr])
    {
        if (next != parent)
        {
            leaf = false;
            sum += solve(next, curr, cats, m);
        }
    }
    if (leaf)
        return 1;
    return sum;
}
```

### Implementação 

Por fim, após toda a lógica de resolução estar pronta, a função main é responsável por:

* Ler os valores de entrada;

* Marcar os vértices com gatos;

 * Conectar os vértices vizinhos;

* Inicializar a chamada da função solve a partir do vértice 1.

```c++ 
int main()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        cin >> hascat[i];
    }
    for (int i = 0; i < n - 1; i++)
    {
        int x, y;
        cin >> x >> y;
        graph[x].push_back(y);
        graph[y].push_back(x);
    }
    ll ans = solve(1, 0, 0, m);
    cout << ans << endl;
    return 0;
}
```


