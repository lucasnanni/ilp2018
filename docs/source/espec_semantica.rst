Especificação Semântica
***********************

Programa
========

Um programa consiste de uma sequência de declarações. A última declaração deve ser obrigatoriamente a da rotina principal, pela qual se dará o início da execução do programa. Essa declaração deve ser de uma função chamada ``main`` com retorno do tipo ``int``. O valor retornado por essa função representa o resultado da execução do programa, onde ``0`` significa que a execução foi bem sucedida.

Todas as declarações realizadas no programa (fora de qualquer subprograma) estão dentro do escopo global.

Declaração
==========

Declaração de variáveis, funções e procedimentos são responsáveis por adicionar os símbolos envolvidos e suas vinculações na tabela de símbolos.

Caso a declaração de uma variável considere sua inicialização, o tipo da expressão de inicialização deve ser o mesmo declarado para a variável.

Comandos
========


If
--

* A expressão condicional do comando ``if`` deve resultar em um valor do tipo lógico.

While
-----

* A expressão condicional do comando ``while`` deve resultar em um valor do tipo lógico.

For
---

* As atribuições de inicialização e passo devem ser analisadas como um comando de atribuição normal.

* A expressão condicional deve resultar em um valor do tipo lógico.

Stop
----

* O comando ``stop`` deve estar cercado (diretamente ou indiretamente) por um comando de repetição (while ou for).

Skip
----

* O comando ``skip`` deve estar cercado (diretamente ou indiretamente) por um comando repetição (while ou for).

Return
------

* Caso apareça dentro de uma função, o tipo da expressão de retorno deve ser o mesmo do retorno declarado da função. Caso apareça dentro de um procedimento, o comando return não pode ter expressão.

Read
----

* A variável utilizada no comando read deve estar declarada e visível no escopo atual.

Write
-----

* Não há análise especial para o comando write.

Chamada de Procedimento
-----------------------

* O procedimento chamado deve estar declarado e visível no escopo atual.

* O número de argumentos fornecidos deve ser o mesmo da declaração do procedimento.

* Os argumentos fornecidos devem ter a mesma ordem de tipo utilizada na declaração do procedimento.

Atribuição
----------

* O lado esquerdo da atribuição deve ser uma variável declarada (simples ou acesso de arranjo) e visível no escopo atual.

* O lado direito deve ser uma expressão com tipo igual ao da variável do lado esquerdo da atribuição.

Bloco
-----

* Define um novo escopo estático. O escopo é criado no início do bloco e finalizado no término do bloco.

Expressões
==========

Aritmética (``+``, ``-``,  ``*``, ``/``, ``%``, ``neg``)
--------------------------------------------------------

* O(s) operando(s) devem ser do tipo inteiro. O tipo resultante é inteiro.

Relacional (``>``, ``>=``, ``<``, ``<=``)
-----------------------------------------

* Os operandos devem ser do tipo inteiro. O tipo resultante é lógico.

Igualdade (``==``, ``!=``)
--------------------------

* Os operandos devem ser do mesmo tipo primitivo. O tipo resultante é lógico.

Lógica (``&&``, ``||``, ``!``)
------------------------------

* O(s) operando(s) devem ser do tipo lógico. O tipo resultante é lógico.

Ternária
--------

* A expressão condicional deve resultar um valor do tipo lógico.

* As expressões então e senão devem possuir o mesmo tipo.

* O tipo resultante da expressão ternária é o mesmo tipo da expressão-então.

Uso de variável
---------------

* A variável deve estar declarada e visível no escopo atual. O tipo resultante é o tipo declarado da variável.

* Para variáveis agregadas, a expressão que resulta no índice a ser acessado deve ser do tipo inteiro.

Chamada de função
-----------------

* Análise análoga à chamada de procedimento.

* O tipo resultante é igual ao tipo declarado da função.