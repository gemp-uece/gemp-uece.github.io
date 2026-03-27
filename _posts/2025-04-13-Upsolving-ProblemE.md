---
title: Upsolving 'Bolsistas Can Code ?' ed. 1 - Problema E
description: Explicação e resolução do problema
author: felipessena
categories: [Upsolving]
---

# Upsolving 'Bolsistas Can Code ?' ed. 1 - Problema E

### Problema Geral
Um professor esqueceu o gabarito da prova na universidade e precisa reconstruí-lo usando as provas já corrigidas. Ele sabe que cada questão deve ter uma e apenas uma resposta correta e quer descobrir essa resposta com base nas opções marcadas pelo aluno. Entretanto, algumas respostas podem não ser identificadas.

### Restrições
- o aluno **só pode marcar as opções** A, B, C e D
- o aluno **só pode dá como resposta** T(correta) ou F(incorreta)

### Valores de Entrada
Um número inteiro T, representando o número de casos de teste. Para cada caso de teste:
- Dois inteiros separados por espaço: Q (número de questões) e M (número de provas corrigidas)
- M linhas contendo 2Q caracteres: a resposta do aluno para cada questão e o status indicando se a resposta está correta('T') ou incorreta('F')

### Solução
Para solucionar esse problema, pode-se utilizar um vetor `ans[q]` para armazenar as respostas corretas, inicialmente declaradas como '?', e uma matriz booleana `fs[q][4]` para marcar as opções identificadas como falsas. Então, com um loop `for(int i=0;i<m;i++)`, percorrer as provas corrigidas e para cada questão ler a resposta do aluno `option` e o status dela `answer`. Se o status for 'T', significa que a resposta do aluno está correta e ela é armazenada no vetor `ans[j] = option`. Senão, ela é marcada como falsa na matriz `fs[j][option-'A']=true`. Para o caso da resposta correta não ter sido identicada, se usa outro loop para percorrer as questões, e quando esse loop identificar uma questão ainda declarada como '?' ele vai percorrer um loop `for(int j=0;j<4;j++)` que vai identificar uma opção que não esteja marcada como falsa, guardar essa opção `option=j` e contar essa identificação `count++`. Se apenas uma opção for contada `if(count==1)`, ela é definida como correta `ans[i]='A' + option`.

### Código:
```cpp
#include <bits/stdc++.h>

using namespace std;

int main()
{
    
    int t;
    cin >> t;
    while(t--) {
        int q, m;
        cin >> q >> m;
        char ans[q];
        char option, answer;
        bool fs[q][4];
        for(int i=0;i<q;i++) {
            for(int j=0;j<4;j++) {
                fs[i][j]=false;
            }
        }
        for(int i=0;i<q;i++) {
            ans[i]='?';
        }
        for(int i=0;i<m;i++) {
            for(int j=0;j<q;j++) {
                cin >> option >> answer;
                if(answer=='T') {
                    ans[j] = option;
                } else {
                    fs[j][option-'A']=true;
                }
            }   
        }
        for(int i=0;i<q;i++) {
            int count = 0;
            int option;
            if(ans[i]=='?') {
                for(int j=0;j<4;j++) {
                    if(!fs[i][j]) {
                        option=j;
                        count++;
                    }
                }
                if(count==1) {
                    ans[i]='A' + option;
                }
            }
            if(i != q - 1) {
                cout << ans[i] << ' ';
            } else {
                cout << ans[i];
            }
        }
        cout << endl;
    }

    return 0;
}
```
