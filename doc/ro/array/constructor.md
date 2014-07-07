##Constructorul `Array`

Deoarece pentru constructorul `Array`  modul de folosire al parametrilor este ambiguu,
este recomandata folosirea notatiei literale - `[]` - pentru a crea un sir nou.

    
    [1, 2, 3]; // Rezultat: [1, 2, 3]
    new Array(1, 2, 3); // Rezultat: [1, 2, 3]

    [3]; // Rezulta: [3]
    new Array(3); // Rezultat: []
    new Array('3') // Rezultat: ['3']

In cazul in care constructorul `Array` este apelat cu un singur argument
si acel argument este de tip `Number`, contructorul va returna un sir *gol*
cu lungimea, proprietatea `length`, egala cu valoarea argumentului. Trebuie tinunt cont ca
**doar** proprietatea `length` va fi setata in acest fel; elementele din sir nu vor fi initializate.
 
    
    var arr = new Array(3);
    arr[1]; // undefined (nedefinit)
    1 in arr; // false, indexul nu a fost setat


Posibilitatea de a seta lungimea unui sir in avans este utila doar in cateva
cazuri, cum ar fi repetarea unui string, caz in care se evita folosirea unui loop.
  
    new Array(count + 1).join(stringToRepeat);

### Concluzii

Notatia literala este preferata in locul constructorului Array. Aceasta este mai scurta, sintaxa este mai clara,
si codul este mai usor de citit.