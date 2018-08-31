Especificação Sintática
***********************

Programa
========

Um programa consiste de uma sequência não vazia de declarações de variáveis e subprogramas.  

::

    programa ::= dec {dec}

Variáveis
========= 

Existem dois tipos de variáveis: as simples e as agregadas. Variáveis simples suportam apenas um único valor de um determinado tipo primitivo em um determinado momento. Variáveis agregadas são de tipos agregados (arranjos) e suportam mais de um valor de um mesmo tipo em um determinado momento. 

Declaração de Variáveis
----------------------- 

::

    decVar ::= 'var' listaSpecVars ':' tipo ';'
    listaSpecVars ::= specVar {',' specVar} 
    specVar ::= specVarSimples | specVarSimplesIni |  
                specVarArranjo | specVarArranjoIni 

**Exemplo:**

::

    var a, b = 3, c = 2 + b: int; 
    var str1, str2 = "String 2": string; 
    var i, j = true: bool; 
    var x, v[10], z[3] = {1, 5, 8}: int; 

Observe que a declaração de variáveis é indicada pela palavra reservada var. Observe também que múltiplas variáveis podem ser declaradas de uma vez e que elas podem ser inicializadas durante a declaração.  

Na declaração de arranjos, o tamanho da estrutura deve ser especificada como um literal numérico.

Subprogramas (procedimentos e funções) 
======================================

A definição de procedimentos e funções possui uma sintaxe comum, exceto pela ausência do tipo de retorno para procedimentos. Não há separação entre declaração e definição de subprogramas, isto é, o subprograma deve ser definido durante sua própria declaração. 

Declaração de Subprogramas
--------------------------

::

    decSub ::= decProc | decFunc 

Declaração de Procedimento
~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    decProc ::= 'def' id '(' [listaParâmetros] ')' bloco 

**Exemplo**

::

    def proc(y: int) { 
        if (y < 0) { 
            return;
        } 
        x = 2 * y; // x é global! 
    }

Declaração de Função
~~~~~~~~~~~~~~~~~~~~

::

    decFunc ::= 'def' id '(' [listaParâmetros] ')' ':' tipo bloco

**Exemplo**

::

    def func(x[], y: int; z: bool): int { 
        a = x[y-1]: int; 
        return a + 1; 
    }

Lista de Parâmetros
~~~~~~~~~~~~~~~~~~~

::

    listaParâmetros ::= specParams {';' specParams}
    specParams ::= param {',' param} ':' tipo
    param ::= id | id '[]'

Parâmetros de tipo inteiro ou lógico são passados naturalmente por cópia e parâmetros de tipo arranjo ou string são passados naturalmente por referência. 

Comandos
========

Existem duas classes de comandos: os comandos simples e os blocos de comando.

::

    comando ::= cmdSimples | bloco 

A seguir são especificados os comandos simples: 

Atribuição
----------

::

    cmdAtrib ::= atrib ';' 
    atrib ::= variável ('='|'+='|'-='|'*='|'/='|'%=') expressão 

O comando de atribuição avalia o valor da expressão e o armazena na variável.

As atribuições compostas devem ser traduzidas da seguinte maneira:  

::

    var X= expressão -> var = var X expressão 

Condicional If
--------------

::

    cmdIf ::= 'if' '(' expressão ')' comando ['else' comando] 

A estrutura condicional if é executada verificando o resultado da expressão de teste. Se ela resultar no valor true, apenas o primeiro comando será executado. Se a expressão resultar no valor false, caso a estrutura else esteja presente, apenas o segundo comando será executado. 

Laço While
----------

::

    cmdWhile ::= 'while' '(' expressão ')' comando 

O laço while inicia verificando o resultado da expressão de teste. Caso o valor seja true, o comando do seu corpo é executado e o laço volta a testar o valor da expressão de teste para a próxima iteração. Caso o valor seja false, a execução do laço é interrompida. 

Laço For
--------

::

    cmdFor ::= 'for' '(' atrib-ini ';' expressão ';' atrib-passo ')' comando 

O laço for inicia executando a atribuição de inicialização. A partir daí, antes de cada iteração, o resultado da expressão de teste é verificado. Se ele for true, o comando corpo é executado e a atribuição de passo é executada em seguida, reiniciando o processo. Se antes de qualquer iteração o valor resultado pela expressão de teste for false, a execução do laço é interrompida. 

Interrupção do laço
-------------------

::

    cmdStop ::= 'stop' ';' 

O comando stop interrompe o laço mais próximo que o cerca. Ele só pode aparecer dentro do corpo de comandos de repetição while e for.  

Salto de iteração do laço
-------------------------

::
    
    cmdSkip ::= 'skip' ';'

O comando skip salta para a próxima iteração do laço mais próximo que o cerca, ignorando a execução dos comandos que o seguem dentro deste laço. Ele só pode aparecer dentro do corpo de comandos de repetição while e for. 

Retorno de subprograma
----------------------

::

    cmdReturn ::= 'return' [expressão] ';' 

O comando return encerra a execução do subprograma que o cerca retornando o valor resultado pela expressão. A expressão de retorno de uma função deve resultar em um valor do mesmo tipo para o qual a função foi definida.  Funções devem obrigatoriamente conter pelo menos um comando return. Já procedimentos podem ou não conter comandos return. Caso o tenham, eles devem retornar nada: return; Como o programa principal é definido por meio de uma função, ele deve conter pelo menos um comando return e o valor retornado deve ser um número inteiro.  

Chamada de procedimento
-----------------------

::

    cmdChamadaProc ::= id '(' [expressão {',' expressão}] ')' ';' 

Como a chamada de procedimentos não resulta em um valor, é necessário um comando para sua execução. A chamada de funções possui sintaxe semelhante, exceto por não ser um comando, e sim uma expressão. 

Entrada Read
------------

::

    cmdRead ::= 'read' variável ';' 

Saída Write
-----------

::

    cmdWrite ::= 'write' expressão {',' expressão} ';' 

Bloco de Comandos
-----------------

Um bloco é uma sequência de (nenhuma ou várias) declarações de subprogramas e variáveis seguida de uma sequência de (nenhum ou vários) comandos. Um bloco é circundado por chaves ``{`` ``}``.

::

    bloco ::= '{' {dec} {comando} '}'

Expressão
=========

Uma expressão pode conter valores dos três tipos definidos (inteiros, lógicos e strings), uso de variáveis, chamadas de função e outras expressões. Uma expressão pode estar cercada por parênteses e se relacionar a outras expressões por meio dos seguintes operadores:

.. table:: Tabela de Operadores

    +-------------+---------------------+------------------------------------------------------+-----------------+
    | Precedência | Operador            | Descrição                                            | Associatividade |
    +=============+=====================+======================================================+=================+
    | 1           | ``-``               | Negativo Unário                                      | À direita       |
    +-------------+---------------------+------------------------------------------------------+-----------------+
    | 2           | ``*``, ``/``, ``%`` | Multiplicação, divisão e resto                       |                 |
    +-------------+---------------------+------------------------------------------------------+                 |
    | 3           | ``+``, ``-``        | Adição e subtração                                   |                 |
    +-------------+---------------------+------------------------------------------------------+                 |
    |             | ``<``, ``<=``       | Operadores relacionais ``<`` e ``≤`` respectivamente |                 |
    | 4           +---------------------+------------------------------------------------------+ À esquerda      |
    |             | ``>``, ``>=``       | Operadores relacionais ``>`` e ``≥`` respectivamente |                 |
    +-------------+---------------------+------------------------------------------------------+                 |
    | 5           | ``==``, ``!=``      | Operadores relacionais ``=`` e ``≠`` respectivamente |                 |
    +-------------+---------------------+------------------------------------------------------+                 |
    | 6           | ``&&``              | E lógico                                             |                 |
    +-------------+---------------------+------------------------------------------------------+                 |
    | 7           | ``||``              | OU lógico                                            |                 |
    +-------------+---------------------+------------------------------------------------------+-----------------+
    | 8           | ``? :``             | Condicional ternário                                 | À direita       |
    +-------------+---------------------+------------------------------------------------------+-----------------+

O operador condicional ternário é formado da seguinte maneira:  

::

    opTern ::= expressão-teste '?' expressão-então ':' expressão-senão 

A expressão teste é avaliada. Se o resultado for true a expressão então é resultada, caso contrário, a expressão senão é resultada. Dessa forma, o resultado desse operador é sempre uma expressão. O operador pode ser utilizado assim: 

::

    x = a > 0 ? a * 2 : a + 1;

Uso de variável
---------------

Como o uso de uma variável resulta no valor armazenado pela variável, todo uso de variável é uma expressão. Variáveis simples são usadas por meio do identificador (nome) associado a ela e variáveis compostas (arranjo) são usadas por meio do identificador e a posição numérica do elemento acessado. 

::

    variável ::= id | id '[' expressão ']' 

Observe que a sintaxe do uso de variável não impede que uma variável simples seja utilizada como arranjo. Essa associação deve ser verificada na etapa de análise semântica.