---
title: Upsolving Contest- MFP Warmup [Unoficial]
date: 2025-04-25 00:38:00 -300
description: Upsolvingo do Contest promovido pelo GEMP, para alunas da universidade treinarem para a MFP.
author: buzz
categories: [Upsolving, MFP]
tags: [mfp, competicoes, upsolving]
pin: true
math: true
mermaid: true 
---

Link do contest : (Vjudge-Link)[https://vjudge.net/contest/712373]

### A : Fatigue-Fighting Vacation (Gym 104555F)

* Link do problema: (Fatigue-Fighting Vacation)[https://codeforces.com/gym/104555/problem/F]

O problema é: William tem uma energia inicial D, e faz C atividades que consomem energia e R atividades que dão energia pra ele quando ele realiza. Ele tem que executar as atividades de cada grupo em ordem, ou seja, ele nao pode realizar a C-esima atividade do grupo C antes da primeira atividade do grupo C. ( Isso vale para as atividades que dão energia, do grupo R).

Observação: As atividades do grupo podem ser intervaladas ou não, então podemos realizar, por exemplo : todas ativdades de um grupo primeiro e depois as outro em seguida. Isso irá servir de base pra ideia.

Ideia: Faça william realizar todas as atividades revigorantes primeiro, e em seguida ele começa a realizar todas atividades que ele conseguir que consome energia. Enquanto ele tiver capacidade de fazer uma atividade, ele faz.

Segue o código:

```cpp

#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

signed main() { _
    int d,c,r; cin >> d >> c >> r;
    vector<int> v(c);
    for(int i = 0; i < c; i++){
        cin >> v[i];
    }
    for(int i = 0; i < r; i++){
        int x; cin >> x;
        d += x; // ele sempre realiza todas as revigorantes no inicio
        // acumula energia, e realiza as que consomem energia
    }
    int ans = r; // guarda a quantidade de atividades no total
    // note que ele ja realizou as revigorantes.
    for(int i = 0; i < c;i++){
        if(v[i] > d) break; // ele nao consegue realizar mais atividades.
        d -= v[i]; // ele consome a energia da atividade i.
        ans++; // incremento na resposta.
    }
    cout << ans << endl;
    return 0;
}
```

### B : Playing 23 (Gym 103960J)

* Link do problema: (Playing 23)[https://codeforces.com/gym/103960/problem/J]

Problema: Assim como no jogo black-jack (21), você tera um jogo semelhante, mas com o objetivo de alcançar o mais proximo de 23, sem passar de 23. Na nossa simulação jogam 3 pessoas : Mesa, Maria e Joao. Basicamente iremos descrever os cenarios: as cartas que a mesa tem apos as N rodadas, as cartas que maria inicia e as cartas que joao inicia. O objetivo é tentar fazer maria ganhar na proxima rodada com a menor carta possivel.

Observação1: Maria ganha quando : (ela faz 23) ou (João faz mais que 23 e ela faz menos ou igual a 23)

Observação2: O deck é composto por 4 cartas de 1 até 13 (ignorando os naipes).

Observação3: As cartas da mesa valem para todos os jogadores.

Observação4: O valor das cartas 11,12,13 é 10. Lembre-se de tratar esse caso.

Ideia: Basta iterar sobre as cartas restantes, começando da menor até a maior, e achar a primeira carta que satisfaz a condição de vitória da Maria. Se ela nao ganhar depois de passar por todas as cartas disponíveis, retornamos -1.

```cpp

#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

// int cartas[14];

signed main() { _
    int n; cin >> n;
    int joao = 0, maria = 0, mesa = 0;
    map<int,int> cartas; 
    for(int i = 1; i <= 13;i++){
        cartas[i] = 4; // inicializo o baralho.
    }

    // Lendo o jogo:
    for(int i = 0; i < 2; i++){int x; cin >> x; cartas[x]--; x = x > 10 ? 10 : x; joao += x;} 
    for(int i = 0; i < 2; i++){int x; cin >> x; cartas[x]--; x = x > 10 ? 10 : x; maria += x;}
    for(int i = 0; i < n; i++){int x; cin >> x; cartas[x]--; x = x > 10 ? 10 : x; mesa += x;}  
    // Como as cartas jogadas ja nao podem ser mais utilizadas, removo elas nos loops acima.

    joao += mesa;
    maria += mesa;
    int ans = -1; 
    for(int i = 1; i <= 13; i++){
        if(cartas[i] == 0) continue; // nao tenho cartas desse valor no baralho.
        int valor = i > 10 ? 10 : i;

        if(valor + joao >= 24 && valor + maria <= 23){
            ans = i; 
            break;
        }

        if(maria + valor == 23){
            ans = i;
            break;
        }
    }
    cout << ans << endl;
    return 0;
}

```

### C : Multidimensional Hangman (Gym 103960F)

* Link do problema: (Multidimensional Hangman)[https://codeforces.com/gym/103960/problem/F]

Problema: Você recebe uma lista de palavras incompletas, faltando uma letra. Seu objetivo é gerar uma palavra completa, de modo que ela possa ser gerada por a maior quantidade de palavras incompletas da sua lista. Você deve printar a palavra e a quantidade de palavras da sua lista que podem gerar ela. 

Ideia: Vamos ler cada palavra. E para cada palavra identificamos a posição do '*', e geraremos todas as palavras possiveis. Ou seja, alteraremos o asterisco por letras de 'a' até 'z'. E enfim, armazenamos as palavras geradas em um hash map, para contar as ocorrencias de palavras geradas. Checando a condição de termos a maior quantidade de ocorrencias. 
```cpp

#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

signed main() { _
    int n, m; cin >> n >> m;
    vector<string> v(n);
    map<string,int> occurs;
    pair<string,int> ans = {"", -1};
    for(int i = 0; i < n; i++){
        cin >> v[i];
        int pos = 0;
        while(v[i][pos] != '*') pos++;
        for(int j = 'a'; j <= 'z'; j++){
            string gerada = v[i]; 
            gerada[pos] = j;

            if(occurs.find(gerada) == occurs.end()){
                occurs[gerada] = 1;
            } else {
                occurs[gerada]++;
                if(occurs[gerada] > ans.second){
                    ans = {gerada, occurs[gerada]};
                }
                else if(occurs[gerada] == ans.second){
                    ans.first = min(gerada, ans.first);
                }
            }
        }
    }
    cout << ans.first << " " << ans.second << endl;
    return 0;
}
```

### D : Eliminating Ballons (Gym 103960E)

* Link do problema: (Eliminating Ballons)[https://codeforces.com/gym/103960/problem/E]

Problema: Você recebe as posições do eixo x de uma lista de balões. e o objetivo é utilizar dardos para explodir o máximo de balões possivel com o mínimo de dardos.

Observação 1: Os dados são lançados seguindo uma linha horizontal de altura Y. se eles acertam uma balão, ele irá para o proximo balão na sequencia de altura Y-1. 

Observação 2: Esse problema é um problema de, dado um array de N números, quantos conjuntos consigo formar de tal modo que cada conjunto é decrescente, e a diferença entre elementos adjacentes é 1.
Exemplificando melhor essa obserção é:
Dado a sequencia: 3 2 1 3 2 1 5 4 3 3 1
Temos os conjuntos: {3,2,1}, {3,2,1}, {5,4,3}, {3,1}.

Ideia: Criar um vetor que guarda a posição do balão (y) x a quantidade de dardos na altura (y).
Quando tenho vis[y] = 0 => indica que nenhum dardo "caiu" de uma posicao acima e chegou em y. e então estourou o balão ali, e seguiu para a posição abaixo (y-1). 
Quando tenho vis[y] > 0 => algum dardo pode estourar aquele balão. ou seja, ele ira estourar, e seguir pro próximo => vis[y]-- e vis[y-1]++;

```cpp
/* Online C++ Compiler and Editor */
#include <bits/stdc++.h>

#define long long int

using namespace std;

const int maxn = 1e7+10;

int vis[maxn]; // vis[posicao do balao y] = quantidade de dardos em y.

signed main()
{
    int n; cin >> n;
    int ans = 0;
    for(int i = 0; i < n; i++){
        int aux; cin >> aux; // altura do balao. (y)
        if(vis[aux] == 0){ // nao tenho nenhum dardo nessa altura
            ans++; // tive que jogar um dardo.
        }
        else { // tenho um dardo.
            vis[aux]--; // removo o dardo dessa posicao, pq acertei um balao.
        }
        vis[aux-1]++; // meu dardo acertou um balao, logo ele desceu e esta em y-1.
    }
    cout << ans << endl;
   return 0;
}
```

### E : Buffoon (Gym 102346B)

* Link do problema: (Buffoon)[https://codeforces.com/gym/102346/problem/B]

Problema: Checar se o valor do primeiro elemento do array é o maior que ou igual a cada um dos outros elementos. Se sim, imprima S, se nao imprima N.

```cpp

#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

signed main() { _
    int n; cin >> n;
    int votos_carlos; cin >> votos_carlos;
    for(int i = 1; i < n; i++){
        int votos; cin >> votos;
        if(votos > votos_carlos){
            cout << "N" << endl;
            return 0;
        }
    }
    cout << "S" << endl;
    return 0;
}

```

### F : Battleship (Gym 102861B)

* Link do problema: [Battleship](https://codeforces.com/gym/102861/problem/B)

Problema: Você irá posicionar N navios horizontais ou verticais, seu objetivo é checar se eles estao se sobrepondo, ou se estão passando do limite do tabuleiro (10x10).

Ideia: Montar sequencialmente os navios no tabuleiro, seguindo as regras do problema.

```cpp

#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

bool check(int x,int y, vector<vector<int>> &grid){
    if(x > 10 || x < 0 || y > 10 || y < 0) return false;
    if(grid[x][y] == 1) return false;

    grid[x][y] = 1;
    return true;
}

signed main() { _
    int n; cin >> n;
    vector<vector<int>> grid(11, vector<int>(11, 0));
    for(int j = 0; j < n; j++){
        int d,l,r,c; cin >> d >> l >> r >> c;
        int x = c, y = r;
        if(d == 0) {
            for(int i = x; i <= c + l - 1; i++){
                if(!check(i,y,grid)){
                    cout << "N" << endl;
                    return 0;
                }
            }
        } else {
            for(int i = y; i <= r + l - 1; i++){
                if(!check(x,i,grid)){
                    cout << "N" << endl;
                    return 0;
                }
            }
        }
    }
    cout << "Y" << endl;
    return 0;
}

```
