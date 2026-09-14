# Aula 02 — Notas de Aula: Linguagens Formais e Gramáticas

> Anotações da Unidade 1, escritas do meu jeito depois da aula.
> Segue o formato pedido: sumário, objetivos, conteúdo, exemplos, exercícios e revisão para prova.

## Sumário

- [Objetivos](#objetivos)
- [1. Alfabeto — Σ](#1-alfabeto--σ)
- [2. Cadeia e comprimento](#2-cadeia-e-comprimento)
- [3. Palavra vazia — ε](#3-palavra-vazia--ε)
- [4. Σ* — todas as cadeias possíveis](#4-σ--todas-as-cadeias-possíveis)
- [5. Linguagem formal — L ⊆ Σ*](#5-linguagem-formal--l--σ)
- [6. Prefixos e sufixos](#6-prefixos-e-sufixos)
- [7. Gramática formal](#7-gramática-formal)
- [8. Regras de produção e os símbolos → e |](#8-regras-de-produção-e-os-símbolos--e-)
- [9. Derivação de palavras](#9-derivação-de-palavras)
- [10. Linguagem gerada — L(G)](#10-linguagem-gerada--lg)
- [11. Operadores lógicos](#11-operadores-lógicos)
- [12. Exemplos resolvidos](#12-exemplos-resolvidos)
- [13. Exercícios](#13-exercícios)
- [14. Revisão para prova](#14-revisão-para-prova)
- [15. Mapa mental](#15-mapa-mental)
- [Checklist](#checklist)

---

## Objetivos

Transformei os objetivos da aula em perguntas — se eu respondo todas sem consultar, fechei a unidade:

- O que é um alfabeto Σ?
- O que é uma cadeia, e como se mede o tamanho dela?
- O que significa ε, e por que `|ε| = 0`?
- Como identificar prefixos e sufixos de uma palavra?
- O que é uma linguagem formal, e como se lê `L ⊆ Σ*`?
- Σ* tem limite de tamanho?
- Como funciona uma gramática formal, e quais são as suas quatro partes?
- Como interpretar uma regra de produção?
- Como gerar palavras a partir de uma gramática?

---

## 1. Alfabeto — Σ

Alfabeto é um **conjunto finito de símbolos**, representado pela letra grega sigma:

```
Σ
```

Exemplo da aula:

```
Σ = {a, b}
```

Com esses dois símbolos eu consigo montar palavras como:

```
a     b     aa     ab     ba     bb     aaa     aab     aba     ...
```

O que anotei: **finito** é exigência do alfabeto. A lista de símbolos tem que terminar. A
quantidade de *palavras* que dá pra montar com eles é outra história — essa pode ser infinita.

---

## 2. Cadeia e comprimento

Cadeia (ou palavra) é uma sequência de símbolos do alfabeto. O comprimento é a contagem de
símbolos, escrita entre barras:

```
|abc| = 3
|ab|  = 2
|a|   = 1
```

Detalhe: a **ordem importa**. `ab` e `ba` são cadeias diferentes, mesmo usando os mesmos símbolos.

---

## 3. Palavra vazia — ε

Se escreve `ε` e se lê **épsilon**. É a cadeia que não possui nenhum símbolo:

```
|ε| = 0
```

O aviso mais importante da seção: **ε não é espaço em branco**. Espaço seria um símbolo e
contaria no comprimento. ε significa que **não existe nenhum símbolo** na cadeia.

O jeito que memorizei: ε funciona como o **zero da concatenação**. Assim como `5 + 0 = 5`, vale
`aε = a`. Grudar ε numa palavra não muda nada — isso vai aparecer direto nas derivações da seção 9.

---

## 4. Σ* — todas as cadeias possíveis

`Σ*` é o conjunto de **todas as cadeias finitas** que dá pra formar com os símbolos de Σ,
**incluindo ε**. Com `Σ = {a, b}`:

```
Σ* = {ε, a, b, aa, ab, ba, bb, aaa, ...}
```

### Existe limite?

Não existe limite máximo para o tamanho das palavras. Sempre dá pra alongar mais:

```
ε     a     aa     aaa     aaaa     aaaaa     ...
```

Para um alfabeto com 2 símbolos, a quantidade de cadeias de tamanho `n` é `2ⁿ`:

| Tamanho | Quantidade |
|:-:|:-:|
| 0 | 1 |
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 4 | 16 |
| 5 | 32 |
| … | … |

A linha do tamanho 0 dá 1, e essa única cadeia é o ε.

>  **Conclusão que cai na prova:** Σ* é **infinito**, mas cada cadeia dentro dele tem tamanho
> **finito**. "Sem limite de tamanho" não é a mesma coisa que "palavra infinita".

---

## 5. Linguagem formal — L ⊆ Σ*

Linguagem formal é um **conjunto de palavras** construídas a partir do alfabeto:

```
L ⊆ Σ*
```

Lê-se: *L é um subconjunto de sigma estrela*. Ou, do jeito que eu leio: *toda palavra de L é uma
das palavras que dá pra montar com Σ*.

As três peças, lado a lado:

| Peça | O que é |
|:-:|---|
| `Σ` | o alfabeto — os símbolos disponíveis |
| `Σ*` | todas as palavras possíveis com esses símbolos |
| `L` | as palavras que eu escolhi de Σ* |

### Exemplo

Com `Σ = {a, b}`, posso definir:

```
L = {a, ab, abb, abbb}
```

Todas essas palavras usam só `a` e `b`, então `L ⊆ Σ*`.

### Finita × infinita

```
L = {ε, a, ab}                  →  finita, dá pra listar por completo
L = {a, aa, aaa, aaaa, ...}     →  infinita, a lista nunca acaba
```

É justamente o caso infinito que justifica a próxima seção: se não dá pra listar as palavras, eu
preciso de **regras** que as gerem.

---

## 6. Prefixos e sufixos

Usando a palavra `ab`:

**Prefixo** é o pedaço que começa **no início**:

```
Prefixos(ab) = {ε, a, ab}
```

**Sufixo** é o pedaço que termina **no final**:

```
Sufixos(ab) = {ε, b, ab}
```

| Palavra | Prefixos | Sufixos |
|:-:|---|---|
| `ab` | ε, a, ab | ε, b, ab |

As dicas que anotei: *prefixo começa no começo, sufixo termina no final*.

### O macete que uso pra não esquecer nenhum

Imagino uma tesoura passeando pela palavra. Ela tem uma posição de corte antes do primeiro símbolo,
uma entre cada par e uma depois do último:

```
 │ a │ b │
 ↑   ↑   ↑
 0   1   2
```

Em cada posição, o pedaço da **esquerda** é prefixo e o da **direita** é sufixo:

| Corte | Prefixo | Sufixo |
|:-:|:-:|:-:|
| 0 | `ε` | `ab` |
| 1 | `a` | `b` |
| 2 | `ab` | `ε` |

Assim eu nunca esqueço os dois que sempre escapam: o `ε` e a **palavra inteira**. Os dois contam
como prefixo **e** como sufixo.

---

## 7. Gramática formal

A gramática fornece **regras para gerar palavras**. A forma geral é:

```
G = (N, Σ, P, S)
```

| Elemento | Significado |
|:-:|---|
| `N` | não terminais |
| `Σ` | terminais |
| `P` | produções |
| `S` | símbolo inicial |

A gramática usada na aula:

```
G = ({S}, {a}, {S → aS | ε}, S)
```

Destrinchando as quatro partes:

| Parte | Valor |
|---|---|
| Não terminais | `{S}` |
| Terminais | `{a}` |
| Produções | `S → aS \| ε` |
| Símbolo inicial | `S` |

O que fixei sobre terminal × não terminal: **não terminal** é a variável que ainda vai ser
substituída (aparece em maiúscula); **terminal** é o símbolo definitivo, que fica na palavra
(minúscula). Enquanto sobrar maiúscula, a derivação ainda não acabou.

---

## 8. Regras de produção e os símbolos → e |

A regra:

```
S → aS | ε
```

é uma forma compacta de escrever **duas regras**:

```
S → aS          ou          S → ε
```

Porque o símbolo `|` significa **OU**.

### Como ler o →

O mesmo desenho muda de significado conforme o contexto — e essa é a pegadinha da aula:

| Contexto | Leitura | Exemplo |
|---|---|---|
| **Gramáticas** | produz / gera / deriva em | `S → aS` = *S produz aS* |
| **Lógica** | implica / se... então | `p → q` = *se p, então q* |

Na hora de derivar, eu **escolho** qual das alternativas aplicar. É essa liberdade de escolha que
faz uma gramática só gerar palavras de tamanhos diferentes.

---

## 9. Derivação de palavras

Derivar é aplicar as regras, uma por vez, começando **sempre** pelo símbolo inicial `S`, até não
sobrar nenhum não terminal. Com `G = ({S}, {a}, {S → aS | ε}, S)`:

**Gerando ε** — aplico direto a regra de parada:

```
S → ε
```

**Gerando `a`** — uma vez `S → aS`, depois `S → ε`:

```
S → aS → aε → a
```

**Gerando `aa`** — duas vezes `S → aS`:

```
S → aS
  → aaS
  → aaε
  → aa
```

**Gerando `aaa`** — três vezes `S → aS`:

```
S → aS
  → aaS
  → aaaS
  → aaaε
  → aaa
```

Dois pontos que anotei:

- o passo `aaε → aa` só funciona porque ε não ocupa espaço (é o zero da concatenação, seção 3);
- cada aplicação de `S → aS` **fixa um `a`** e empurra o `S` para a direita, como um cursor.
  A regra `S → ε` é o que encerra — sem ela a derivação nunca terminaria.

---

## 10. Linguagem gerada — L(G)

Juntando tudo que `G = ({S}, {a}, {S → aS | ε}, S)` produz:

```
L(G) = {ε, a, aa, aaa, aaaa, ...}
```

Que também se escreve:

```
L(G) = {aⁿ | n ≥ 0}
```

Lê-se: *n letras `a`, para qualquer n maior ou igual a zero*. O caso `n = 0` é justamente o `ε`.

---

## 11. Operadores lógicos

A revisão de lógica que abriu a aula:

| Símbolo | Nome | Leitura |
|:-:|---|---|
| `¬` | Negação | não |
| `∧` | E | e |
| `∨` | OU | ou |
| `→` | Implicação | implica / se... então |

Refiz o exemplo com as proposições da aula:

```
p = "Está chovendo."
q = "Eu levo um guarda-chuva."
```

| Fórmula | Leitura |
|:-:|---|
| `¬p` | Não está chovendo. |
| `p ∧ q` | Está chovendo **e** eu levo um guarda-chuva. |
| `p ∨ q` | Está chovendo **ou** eu levo um guarda-chuva. |
| `p → q` | **Se** está chovendo, **então** eu levo um guarda-chuva. |

O motivo de isso vir logo no começo da unidade é o aviso do `→`: aqui ele é implicação, na
gramática é produção. Trocar os dois na prova é erro fácil de cometer.

---

## 12. Exemplos resolvidos

Montei mais alguns casos pra treinar, todos usando os conceitos acima.

### Exemplo A — comprimento

```
|ab|   = 2
|aaa|  = 3
|ε|    = 0
```

### Exemplo B — pertence ou não a Σ*

Com `Σ = {a, b}`:

| Cadeia | Está em Σ*? | Por quê |
|:-:|:-:|---|
| `abba` | sim | só usa `a` e `b` |
| `ε` | sim | Σ* inclui a palavra vazia |
| `abc` | não | `c` não pertence ao alfabeto |

### Exemplo C — prefixos e sufixos de `aab`

Aplicando a tesoura da seção 6:

| Corte | Prefixo | Sufixo |
|:-:|:-:|:-:|
| 0 | `ε` | `aab` |
| 1 | `a` | `ab` |
| 2 | `aa` | `b` |
| 3 | `aab` | `ε` |

```
Prefixos(aab) = {ε, a, aa, aab}
Sufixos(aab)  = {ε, b, ab, aab}
```

### Exemplo D — a mesma gramática, com uma produção trocada

E se em vez de `S → aS | ε` a gramática fosse `S → aS | a`?

```
S → aS → aa        (parando com a regra S → a)
S → a              (usando S → a de cara)
```

Aí a menor palavra passa a ser `a`, e o `ε` **não** é mais gerado:

```
L(G) = {a, aa, aaa, ...} = {aⁿ | n ≥ 1}
```

Uma produção trocada, e a linguagem muda. Isso me ajudou a entender o papel do `S → ε`.

---

## 13. Exercícios

As duas atividades pedidas na aula, resolvidas. Deixei o gabarito escondido pra eu conseguir
refazer sem ver a resposta quando for revisar.

### Atividade 1 — Prefixos e sufixos

**Enunciado:** considere a palavra `ab`. Liste os prefixos e sufixos.

Minha resposta:

Usando a tesoura da seção 6:

| Corte | Prefixo | Sufixo |
|:-:|:-:|:-:|
| 0 | `ε` | `ab` |
| 1 | `a` | `b` |
| 2 | `ab` | `ε` |

**Resposta:**

```
Prefixos(ab) = {ε, a, ab}
Sufixos(ab)  = {ε, b, ab}
```

Reparar que o `ε` e a palavra inteira entram nas duas listas.

O que **não** entra: `ba` (mudou a ordem, não é pedaço da palavra) e o `b` na lista de prefixos —
`b` está no fim, então é sufixo, não prefixo.

---

### Atividade 2 — Gramática

**Enunciado:** considere a gramática

```
G = ({S}, {a}, {S → aS | ε}, S)
```

Liste 3 palavras geradas.

Minha resposta:

Escolhi as três palavras mais curtas e derivei cada uma:

| Palavra | Derivação | Regras usadas |
|:-:|---|---|
| `ε` | `S → ε` | só a de parada |
| `a` | `S → aS → aε → a` | `aS` uma vez, depois `ε` |
| `aa` | `S → aS → aaS → aaε → aa` | `aS` duas vezes, depois `ε` |

**Resposta:** `ε`, `a` e `aa`.

Outras respostas também valeriam — `aaa`, `aaaa`, `aaaaa`, … — porque a linguagem completa é:

```
L(G) = {aⁿ | n ≥ 0}
```

ou seja, qualquer quantidade de `a`, incluindo zero.

O que eu **não** poderia responder:

- `b` — não é terminal desta gramática, nenhuma regra produz `b`;
- `aS` — ainda tem não terminal, então a derivação não terminou e isso não é palavra.

---

## 14. Revisão para prova

O mínimo que quero ter na cabeça no dia da prova:

| Conceito | Notação | Exemplo |
|---|:-:|---|
| Alfabeto (finito) | `Σ` | `Σ = {a, b}` |
| Cadeia / palavra | — | `ab` |
| Comprimento | `\|w\|` | `\|ab\| = 2` |
| Palavra vazia | `ε` | `\|ε\| = 0` |
| Todas as cadeias | `Σ*` | `{ε, a, b, aa, ab, ba, bb, ...}` |
| Linguagem | `L ⊆ Σ*` | `L = {a, ab, abb}` |
| Prefixo | — | `Prefixos(ab) = {ε, a, ab}` |
| Sufixo | — | `Sufixos(ab) = {ε, b, ab}` |
| Gramática | `G = (N, Σ, P, S)` | `({S}, {a}, {S → aS \| ε}, S)` |
| Produz | `→` | `S → aS` |
| Ou | `\|` | `S → aS \| ε` |
| Linguagem gerada | `L(G)` | `{aⁿ \| n ≥ 0}` |

E os pontos onde eu mais escorrego:

1. `ε` **não** é espaço em branco — é ausência de símbolo, e `|ε| = 0`;
2. Σ* é infinito, **mas** toda cadeia dentro dele é finita;
3. `→` é *produz* em gramática e *implica* em lógica;
4. `|` numa produção significa **ou**;
5. prefixos e sufixos incluem sempre `ε` **e** a palavra inteira;
6. começar a derivação por qualquer coisa que não seja `S` — sempre parte do símbolo inicial.

---

## 15.  Mapa mental

Desenhei seguindo o caminho da aula: dos símbolos até as palavras geradas.

```
                    ┌──────────────────┐
                    │   Σ  ALFABETO    │   conjunto FINITO de símbolos
                    │     {a, b}       │
                    └────────┬─────────┘
                             │  junto símbolos em sequência
                             ▼
                    ┌──────────────────┐
                    │     CADEIAS      │   |ab| = 2
                    │   ab, aa, bba    │   caso especial: ε , com |ε| = 0
                    └────────┬─────────┘
              ┌──────────────┴──────────────┐
              ▼                             ▼
   ┌─────────────────────┐      ┌────────────────────────┐
   │  Σ*  TODAS AS       │      │  PEDAÇOS DA CADEIA     │
   │  CADEIAS POSSÍVEIS  │      │  prefixo → do começo   │
   │  infinito, mas cada │      │  sufixo  → até o fim   │
   │  palavra é finita   │      │  ε entra nos dois      │
   └──────────┬──────────┘      └────────────────────────┘
              │  escolho um subconjunto
              ▼
      ┌────────────────┐
      │  L ⊆ Σ*        │   pode ser finita ou infinita
      │   LINGUAGEM    │
      └───────┬────────┘
              │  se é infinita, não dá pra listar → preciso de regras
              ▼
   ┌────────────────────────┐
   │ GRAMÁTICA G=(N,Σ,P,S)  │   N = não terminais (maiúsculas)
   │      S → aS | ε        │   Σ = terminais (minúsculas)
   └───────────┬────────────┘
               │  aplico as produções a partir de S
               ▼
        DERIVAÇÃO   S → aS → aaS → aaε → aa
               │
               │  paro quando não sobra não terminal
               ▼
        L(G) = {ε, a, aa, aaa, ...} = {aⁿ | n ≥ 0}
```

---

## Checklist

Marco o que já consigo explicar em voz alta, sem consultar:

- O que é um alfabeto Σ;
- O que é uma cadeia;
- O que significa ε;
- Por que `|ε| = 0`;
- Por que ε não é espaço em branco;
- O que é um prefixo;
- O que é um sufixo;
- O que significa Σ*;
- Se Σ* possui limite de tamanho;
- Quantas cadeias de tamanho `n` existem sobre um alfabeto de 2 símbolos;
- O que é uma linguagem formal L;
- O que significa `L ⊆ Σ*`;
- A diferença entre linguagem finita e infinita;
- O que é uma gramática formal e quais são as suas quatro partes;
- O que são terminais e não terminais;
- O que é uma regra de produção;
- Como ler `S → aS | ε`;
- As duas leituras do símbolo `→`;
- Como gerar palavras usando uma gramática.

---

## Conceito-chave

Se eu tiver que resumir a unidade inteira em cinco linhas:

> O alfabeto dá os símbolos.
> As cadeias são as sequências formadas com esses símbolos.
> Σ* reúne todas as cadeias possíveis.
> Uma linguagem escolhe algumas delas.
> E a gramática é o conjunto de regras que gera exatamente essas escolhidas.
