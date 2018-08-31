Especificação Léxica
********************

Identificadores
===============

Chamamos de identificador qualquer nome criado pelo usuário da linguagem. Os identificadores seguem a mesma regra de formação da linguagem C: 

Devem iniciar com uma letra (minúscula ou maiúscula) ou um subtraço seguido de letras, subtraços ou dígitos entre 0 e 9. 

Um identificador será expresso pelo símbolo id nas especificações sintáticas. 

Literais
========

Daremos o nome de literal a todo valor fixado no código. A linguagem possui representação de literais para seus três tipos primitivos. 

Números
-------

Os literais numéricos devem ser representados na base decimal e podem conter qualquer combinação de dígitos entre 0 e 9. Os números negativos não serão processados na fase léxica, mas sim na sintática e semântica. Dessa forma, o número -42, por exemplo, consiste de dois lexemas: "-" e "42", e serão tratados como uma operação aritmética nas análises sintática e semântica. 

Strings
------- 

Os literais string possuem a mesma regra de formação definida pela linguagem C. 

*Exemplo:* ``"isso é \"uma\" string!\n"``

Lógicos
-------

Os literais lógicos verdadeiro e falso são representados pelos lexemas ``true`` e ``false`` respectivamente. 

Comentários
-----------

A linguagem possui apenas comentários de linha:  

* Começam com ``//`` e seguem até o final da linha. 

De forma geral, os comentários podem conter qualquer tipo de símbolo, inclusive os não permitidos pela linguagem. Os comentários devem ser processados corretamente pelo analisador léxico e em seguida descartados. 

Palavras reservadas e símbolos
------------------------------

As palavras reservadas e símbolos da linguagem são:

``bool else false for if int read return skip stop string true var while write``

``( ) [ ] { } , ; + - * / % == != > >= < <= || && ! = += -= *= /= %= ? :``