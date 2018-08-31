Exemplos
********

Bubble-Sort
===========

::

    var v[10]: int; 

    // Procedimento de ordenação por troca 
    // Observe como um parâmetro de arranjo é declarado 

    def bubblesort(v[]: int; n: int) { 
        var i=0, j: int; 
        var trocou = true: bool; 
        
        while (i < n-1 && trocou) { 
            trocou = false; 
            for (j=0; j<(n-i-1); j+=1) { 
                if (v[j] > v[j+1]) { 
                    var aux = v[j]: int; 
                    v[j] = v[j+1]; 
                    v[j+1] = aux; 
                    trocou = true; 
                } 
            } 
            i += 1;
        }
    } 

    def main(): int { 
        var i: int; 
        
        write "Digite os valores do arranjo:\n"; 
        
        for (i=0; i<10; i+=1) { 
            write "A[", i, "] = "; 
            read v[i]; 
        } 

        bubblesort(v, 10); 

        write "Arranjo ordenado:\nA = "; 

        for (i=0; i<10; i+=1) { 
            write v[i], " "; 
        } 

    } 
