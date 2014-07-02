## The `Array` Constructor

Since the `Array` constructor is ambiguous in how it deals with its parameters,
it is highly recommended to use the array literal - `[]` notation - 
when creating new arrays.

##Constructorul `Array`  

Deoarece constructorul `Array`  este neclar in felul in care foloeste parametrii,
este recomandat sa fie folosita notarea array literal - `[]`
pentru a creea un array nouwhen creating new arrays.

    [1, 2, 3]; // Result: [1, 2, 3]
    new Array(1, 2, 3); // Result: [1, 2, 3]
    
    [3]; // Result: [3]
    new Array(3); // Result: []
    new Array('3') // Result: ['3']
    
    [1, 2, 3]; // Rezultat: [1, 2, 3]
    new Array(1, 2, 3); // Rezultat: [1, 2, 3]

    [3]; // Rezulta: [3]
    new Array(3); // Rezultat: []
    new Array('3') // Rezultat: ['3']

In cases when there is only one argument passed to the `Array` constructor
and when that argument is a `Number`, the constructor will return a new *sparse* 
array with the `length` property set to the value of the argument. It should be 
noted that **only** the `length` property of the new array will be set this way; 
the actual indexes of the array will not be initialized. 

In cazul in care constructorul `Array` este apelat cu un singur argument
si acel argument este un `Numar`, contructorul va returna un array *gol*
cu protietatea `length` - lungimea setata cu valoarea argumentului. Trebuie tinunt cont ca
**doar** lungimea `length` va fi setata in acest fel; index din array nu vor fi initializati.
 

    var arr = new Array(3);
    arr[1]; // undefined
    1 in arr; // false, the index was not set
    
    var arr = new Array(3);
    arr[1]; // undefined (nedefinit)
    1 in arr; // false, indexul nu a fost setat

Being able to set the length of the array in advance is only useful in a few
cases, like repeating a string, in which it avoids the use of a loop.

Posibilitatea de a seta lungimea unui array in avans este utila doar in cateva
cazuri, cum ar fi repetarea unui string, caz in care se evita folosirea unui loop.

    new Array(count + 1).join(stringToRepeat);
    
    new Array(count + 1).join(stringToRepeat);

### In Conclusion

Literals are preferred to the Array constructor. They are shorter, have a clearer syntax, and increase code
readability.

### Concluzii

Notarea literala este preferata in locul constructorului Array. Aceasta este mai scurta, sintaxa este mai clara,
si codul este mai usor de citit.