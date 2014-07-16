## Array Iteration and Properties

## Parcurgerea si Proprietatile Sirurilor 

Although arrays in JavaScript are objects, there are no good reasons to use
the [`for in`](#object.forinloop) loop. In fact, there 
are a number of good reasons **against** the use of `for in` on arrays.

Desi in JavaScript sirurile sunt obiecte, nu exista nici un motiv sa folosim
loop-ul [`for in`](#object.forinloop). Din contra exista motive bune
**impotriva** folosiri `for in` la siruri.


> **Note:** JavaScript arrays are **not** *associative arrays*. JavaScript only 
> has [objects](#object.general) for mapping keys to values. And while associative 
> arrays **preserve** order, objects **do not**.

> **Nota:** Sirurile din JavaScript **nu sunt** *siruri asociative*. JavaScript are 
> doar [objects](#object.general) care permit mapare valorilor cu chei. Si desi sirurile 
> asociative **pastreaza** ordinea, obiectele **nu o pastreaza**.

Because the `for in` loop enumerates all the properties that are on the prototype 
chain and because the only way to exclude those properties is to use 
[`hasOwnProperty`](#object.hasownproperty), it is already up to **twenty times** 
slower than a normal `for` loop.

Deoarece parcurgerea sirurilor cu `for in` enumera toate proprietatile care sunt pe prototype
chain si singura cale de a le execlude este folosirea [`hasOwnProperty`](#object.hasownproperty),
aceasta este de pana la **20 de ori** mai lenta decat un loop normal `for`. 

### Parcurgerea

In order to achieve the best performance when iterating over arrays, it is best
to use the classic `for` loop.

Pentru a avea cea mai buna performanta cand parcurgem sirurile este mai bine
sa folosim varianta clasica `for`.

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

In varianta de mai sus mai exista o imbunatatirea. Aceasta este memorarea
lungimi sirului cu ajutorul `l = list.length`. 
There is one extra catch in the above example, which is the caching of the 
length of the array via `l = list.length`.

Although the `length` property is defined on the array itself, there is still an
overhead for doing the lookup on each iteration of the loop. And while recent 
JavaScript engines **may** apply optimization in this case, there is no way of
telling whether the code will run on one of these newer engines or not.
 
Desi proprietatea `length` este definita pe sir, extista un cost daca
aceasta este cautata la fiecare pas al parcurgerii. Desi motoarele
recente de JavaScript **pot** aplica optimizari in acest caz
nu se poate stii daca codul va fi rulat pe astfel de motoare

In fact, leaving out the caching may result in the loop being only **half as
fast** as with the cached length.

In realitate, daca nu se foloseste memorarea parcurgerea poate fi cu pana la
**jumatate mai lenta** decat varianta cu memorare.

### The `length` Property

### Proprietatea `lenght

While the *getter* of the `length` property simply returns the number of
elements that are contained in the array, the *setter* can be used to 
**truncate** the array.

While the *getter* of the `length` property simply returns the number of
elements that are contained in the array, the *setter* can be used to 
**truncate** the array.

In timp ce *getter* proprietatii `length` returneaza numarul elementelor
din sir, *setterul* poate fi folosit pentru a **trunchia** sirul

    var foo = [1, 2, 3, 4, 5, 6];
    foo.length = 3;
    foo; // [1, 2, 3]

    foo.length = 6;
    foo.push(4);
    foo; // [1, 2, 3, undefined, undefined, undefined, 4]
            

Assigning a smaller length truncates the array. Increasing it creates a sparse array.

Daca se seteaza o valoare mai mica sirul este trunchiat. O valoare mai mare creaza un sir
cu elemente goale

### In Conclusion

### In Conclusion

### Concluzii

For the best performance, it is recommended to always use the plain `for` loop
and cache the `length` property. The use of `for in` on an array is a sign of
badly written code that is prone to bugs and bad performance. 

Pentru cele mai bune performate, este recomandat ca intodeauna sa fie folosit
parcurgerea cu `for` si memorarea proprietatii `length`. Parcurgerea cu
`for in` este un semn de cod scris gresit si poate duce la defecte  si preformanta scazuta
