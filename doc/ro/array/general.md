## Array Iteration and Properties

## Parcurgerea si Proprietatile Sirurilor 

Although arrays in JavaScript are objects, there are no good reasons to use
the [`for in`](#object.forinloop) loop. In fact, there 
are a number of good reasons **against** the use of `for in` on arrays.

Desi in JavaScript sirurile sunt obiecte, nu exista nici un motiv sa folosim
instructiunea iterativa [`for in`](#object.forinloop). Din contra exista motive bune
**impotriva** folosirii lui `for in` pentru siruri.


> **Note:** JavaScript arrays are **not** *associative arrays*. JavaScript only 
> has [objects](#object.general) for mapping keys to values. And while associative 
> arrays **preserve** order, objects **do not**.

> **Nota:** Sirurile din JavaScript **nu sunt** *siruri asociative*. JavaScript are 
> doar [obiecte](#object.general) care permit maparea unor chei cu un set de valori. Si desi sirurile 
> asociative **pastreaza** ordinea, obiectele **nu o pastreaza**.

Because the `for in` loop enumerates all the properties that are on the prototype 
chain and because the only way to exclude those properties is to use 
[`hasOwnProperty`](#object.hasownproperty), it is already up to **twenty times** 
slower than a normal `for` loop.

Deoarece parcurgerea sirurilor cu `for in` itereaza prin toate proprietatile care sunt pe lantul
de prototipuri si singura cale de a le exclude este folosirea [`hasOwnProperty`](#object.hasownproperty),
aceasta este de pana la **20 de ori** mai lenta decat o instructiune clasica `for`. 

### Parcurgerea

In order to achieve the best performance when iterating over arrays, it is best
to use the classic `for` loop.

Pentru a obtine cea mai buna performanta in parcurgerea unui sir, este mai bine
sa folosim instructiunea clasica `for`.

    var list = [1, 2, 3, 4, 5, ...... 100000000];
    for(var i = 0, l = list.length; i < l; i++) {
        console.log(list[i]);
    }
    
    var list = [1, 2, 3, 4, 5, ...... 100000000];
    for(var i = 0, l = list.length; i < l; i++) {
        console.log(list[i]);
    }
    
There is one extra catch in the above example, which is the caching of the 
length of the array via `l = list.length`.

In varianta de mai sus mai exista o imbunatatire. Aceasta este memorarea
lungimii sirului cu ajutorul atribuirii `l = list.length`. 
There is one extra catch in the above example, which is the caching of the 
length of the array via `l = list.length`.

Although the `length` property is defined on the array itself, there is still an
overhead for doing the lookup on each iteration of the loop. And while recent 
JavaScript engines **may** apply optimization in this case, there is no way of
telling whether the code will run on one of these newer engines or not.
 
Desi proprietatea `length` este definita pe sir, exista un cost de performanta daca
aceasta este cautata la fiecare pas al parcurgerii. Desi motoarele
recente de JavaScript **ar putea** aplica optimizari in acest caz,
nu se poate sti daca codul va fi rulat pe un astfel de motor.

In fact, leaving out the caching may result in the loop being only **half as
fast** as with the cached length.

De fapt, daca nu se memoreaza lungimea, parcurgerea poate fi cu pana la
**jumatate mai lenta**.

### The `length` Property

### Proprietatea `length`

While the *getter* of the `length` property simply returns the number of
elements that are contained in the array, the *setter* can be used to 
**truncate** the array.

In timp ce *accesorul* proprietatii `length` returneaza numarul elementelor
din sir, *modificatorul* poate fi folosit pentru a **trunchia** sirul.

    var foo = [1, 2, 3, 4, 5, 6];
    foo.length = 3;
    foo; // [1, 2, 3]

    foo.length = 6;
    foo.push(4);
    foo; // [1, 2, 3, undefined, undefined, undefined, 4]
            

Assigning a smaller length truncates the array. Increasing it creates a sparse array.

Daca se seteaza o lungime mai mica, sirul este trunchiat. O valoare mai mare creaza un sir
cu elemente goale.

### In Conclusion

### Concluzii

For the best performance, it is recommended to always use the plain `for` loop
and cache the `length` property. The use of `for in` on an array is a sign of
badly written code that is prone to bugs and bad performance. 

Pentru cele mai bune performante, este recomandat ca intodeauna sa fie folosita
parcurgerea cu instructiunea `for` si memorarea proprietatii `length`. Parcurgerea cu
`for in` este un semn de cod scris gresit si poate duce la defecte si performante scazute.
