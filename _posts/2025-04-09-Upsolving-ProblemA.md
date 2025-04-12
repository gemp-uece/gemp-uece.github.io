---
title: TITLE
description: Short summary of the post.
date: YYYY-MM-DD HH:MM:SS +/-TTTT
author: author_id
categories:
  - Blogging
tags: 
pin: "true"
math: "true"
mermaid: "true"
---
# # Upsolving 'Bolsistas Can Code ?' ed. 1 - Problema A
##### Conhecimentos necessários: #ControleDeFluxo #IfElse
### Problema Geral
Um jogador está participando de um programa de auditório que consiste em escolher, entre 3 portas fechadas, sendo duas com uma cabra e outra com um carro, a porta que tem o carro. 
### Restrições
Sabemos que, pelas restrições ditas no problema:
- o jogador **sempre vai escolher a primeira porta**
- o anfitrião sempre vai escolher a outra porta que tiver a cabra, restando apenas a primeira porta do jogador e a outra porta restante. 
- **o jogador sempre troca** de porta depois que o apresentador abre a outra porta com a cabra.
### Solução
Como o jogador sempre troca de porta após o apresentador revelar a primeira cabra, podemos perceber que sempre que o carro estiver na porta de número 1, o jogador irá perder, pois ele trocará essa porta por outra com a cabra.
Percebe-se também, que independente se o carro estiver nas portas 2 ou 3, ele sempre vai ganhar pois, irá trocar a sua, que contém a última cabra, pela a que contém o carro. 
E para satisfazer essas condições, podemos usar as funções if-else, conferindo se a váriavel que chamaremos de ```car``` é igual a 2 ou a 3, então aumentando 1 na quantidade de vezes que o jogador ganha.

### Código:
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
	ios_base::sync_with_stdio(0);
	cin.tie(0);
	cout.tie(0);
	
	int n; 
	cin>>n;
	int resposta = 0;
	while(n--){
		int car;
		cin>>car;
		
		if(car == 2 || car == 3){
			resposta++;
		}
	}
	cout << resposta << "\n";
	
	return 0;
}
```