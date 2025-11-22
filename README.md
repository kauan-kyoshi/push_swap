# push_swap

Projeto `push_swap` — solução para o projeto 42 que implementa um gerador
de operações para ordenar uma pilha de inteiros usando apenas operações
pré-definidas. Este repositório serve como portfólio e contém a versão
desenvolvida por Kyoshi Lima.



**Tecnologias:** C, Makefile, biblioteca auxiliar `libft` (incluída).

**Estrutura do repositório**
- `src/`: código-fonte do `push_swap` e do `checker`.
- `includes/`: cabeçalhos públicos, principalmente `push_swap.h`.
- `libft/`: implementação da biblioteca utilitária utilizada no projeto.
- `makefile`: regras de compilação (alvo padrão gera o binário `push_swap`).
- `obj/`: objetos gerados pela compilação.

**Principais arquivos**
- `src/main.c` — ponto de entrada do `push_swap`.
- `src/checker.c` — utilitário `checker` que valida uma sequência de operações.
- `src/sort_small.c` — tratamento ótimo para 2 e 3 elementos (e casos 4/5).
- `src/sort_many.c` — algoritmo com divisão em "chunks" para entradas grandes.
- `src/ops_*.c` — implementação das operações: `sa, sb, ss, pa, pb, ra, rb, rr, rra, rrb, rrr`.
- `includes/push_swap.h` — definições principais e assinaturas de funções.

**Recursos implementados**
- Parsing de argumentos simples e de strings contendo múltiplos números.
- Validação de números, limites de `int` e checagem de duplicatas.
- Indexação dos valores (atribuição de rótulos 0..n-1) antes da ordenação.
- Operações exigidas pelo projeto: `sa, sb, ss, pa, pb, ra, rb, rr, rra, rrb, rrr`.
- Programa auxiliar `checker` que lê operações pela entrada padrão e verifica
  se a pilha resultante fica ordenada.

Como funciona (resumo técnico)
- Os valores lidos são armazenados em uma lista dupla fornecida pela `libft`.
- Antes de ordenar, a função `ps_index_stack` constroi um array ordenado
  (bubble sort) e substitui cada valor pelo seu índice — isso facilita
  comparações e redução do espaço de valores.
- Para n <= 3 existem rotinas ótimas (`sort_2`, `sort_3`). Para n = 4 ou 5
  é aplicada uma estratégia mista (trazer mínimos para `b`, ordenar os 3
  restantes e recolocar).
- Para entradas maiores é usado um algoritmo baseado em "chunks". A pilha `a`
  é particionada por blocos/limiares; valores são empurrados para `b` por
  fases e depois recolocados na ordem correta puxando os maiores de `b`.

Complexidade (observações)
- Indexação atual utiliza `bubble_sort` e tem custo O(n^2) no pré-processo.
- O algoritmo de movimentação com chunks tem comportamento prático eficiente
  para reduzir número de operações, porém o custo teórico pode ser O(n^2)
  no pior caso. Uso de chunks (5 para até 100, 11 para >100) melhora resultados.

Como compilar
- Gere o binário principal (`push_swap`):

```bash
make
```

- Gere o utilitário `checker` (opcional):

```bash
make checker
```

Como usar
- Exemplo simples:

```bash
./push_swap 3 2 1
```

- Aceita também uma única string com múltiplos números:

```bash
./push_swap "3 2 1"
```

- Validar a sequência de operações com o `checker` (pipe):

```bash
./push_swap 3 2 1 | ./checker 3 2 1
# Deve imprimir: OK (ops=<numero>)
```

Exemplos
- Ordenar 3 elementos:

```bash
./push_swap 2 1 3
# saída possível:
# sa
```

- Teste com entrada maior:

```bash
./push_swap 5 2 3 1 4 | ./checker 5 2 3 1 4
```

Dependências
- Compilador C compatível com as flags `-Wall -Wextra -Werror`.
- Cabeçalhos da `libft` já incluídos na pasta `libft/` — o `make` invoca sua
  própria regra para compilar `libft.a`.



# push_swap
