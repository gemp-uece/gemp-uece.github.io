---
title: Upsolving 'Bolsistas Can Code ?' ed. 1 - Problema B
description: Passo a passo para a solução do problema.
author: joaom-marques
categories: [Upsolvings]
tags: [easy-level, string, substring]
---

# Upsolving 'Bolsistas Can Code ?' ed. 1 - Problema B

## Quebrando o problema em partes

### Parte 1 - Ideia geral

Ao ler o enunciado, podemos identificar que o elemento principal a ser trabalhado será uma string, ou array de caracteres. Também é evidente que estaremos abordando um problema de encriptação de strings.

### Parte 2 - Os requerimentos

O objetivo e a limitação apresentados no texto são claros. Devemos contar quantas vezes uma palavra (crib) encaixa em uma string provida no caso teste, sabendo que não é possível que um caractere seja igual à sua contraparte encriptada.

### Parte 3 - Reorganizando os requerimentos

Quando um problema parece complexo demais para ser escrito em código, geralmente é possível reinterpretá-lo, em busca de uma solução que seja mais abordável.
No caso desse problema, é importante identificar que é mais fácil verificar quando uma substring é inválida do que quando é válida, pois basta encontrar um único caractere na string que seja igual ao seu respectivo na crib provida.
Dessa forma: Iterativamente, quando encontrarmos uma situação `string[i] == crib[j]`, invalidaremos aquela posição de substring em potencial. Caso não haja tal ocorrência pela extensão da substring, ela será válida.

### Parte 4 - A solução

Como ficou evidente, a solução deve ser iterativa e verificaremos quantas substrings da string provida são válidas para a crib especificada.
Para cada começo de substring (percebe-se que são de tamanho fixo, o mesmo tamanho de crib) devemos iterar pelo tamanho de crib para verificar a sua validade:

```cpp

// Note o limite do loop. Precisamos apenas testar
// substrings de tamanho específico
for (int i = 0; i < string.size() - crib.size(); i++) {
    for (int j = i; j < crib.size(); j++) {
    // Comparamos cada char de crib com a substring
        if (string[i] == crib[j]) {
            match = true; // Match! substring inválida para essa posicao
            break; // Próxima substring
        }
    }
    if (!match) {
    count++; // Iteramos a substring sem matches? Contamos como válida
    }
}
```

- OBS: Essa solução terá pior caso de O(n²), mas será válida para o tamanho máximo da string provido (10⁴).
