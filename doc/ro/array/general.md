## Parcurgerea si Proprietatile Sirurilor 

Desi in JavaScript sirurile sunt obiecte, nu exista nici un motiv sa folosim
instructiunea iterativa [`for in`](#object.forinloop). Din contra exista motive bune
**impotriva** folosirii lui `for in` pentru siruri.


> **Nota:** Sirurile din JavaScript **nu sunt** *siruri asociative*. JavaScript are 
> doar [obiecte](#object.general) care permit maparea unor chei cu un set de valori. Si desi sirurile 
> asociative **pastreaza** ordinea, obiectele **nu o pastreaza**.


Deoarece parcurgerea sirurilor cu `for in` itereaza prin toate proprietatile care sunt pe lantul
de prototipuri si singura cale de a le exclude este folosirea [`hasOwnProperty`](#object.hasownproperty),
aceasta este de pana la **20 de ori** mai lenta decat o instructiune clasica `for`. 

### Parcurgerea


Pentru a obtine cea mai buna performanta in parcurgerea unui sir, este mai bine
sa folosim instructiunea clasica `for`.
  
    var list = [1, 2, 3, 4, 5, ...... 100000000];
    for(var i = 0, l = list.length; i < l; i++) {
        console.log(list[i]);
    }
    
In varianta de mai sus mai exista o imbunatatire. Aceasta este memorarea
lungimii sirului cu ajutorul atribuirii `l = list.length`. 

Desi proprietatea `length` este definita pe sir, exista un cost de performanta daca
aceasta este cautata la fiecare pas al parcurgerii. Desi motoarele
recente de JavaScript **ar putea** aplica optimizari in acest caz,
nu se poate sti daca codul va fi rulat pe un astfel de motor.

De fapt, daca nu se memoreaza lungimea, parcurgerea poate fi cu pana la
**jumatate mai lenta**.

### Proprietatea `length`

In timp ce *accesorul* proprietatii `length` returneaza numarul elementelor
din sir, *modificatorul* poate fi folosit pentru a **trunchia** sirul.

    var foo = [1, 2, 3, 4, 5, 6];
    foo.length = 3;
    foo; // [1, 2, 3]

    foo.length = 6;
    foo.push(4);
    foo; // [1, 2, 3, undefined, undefined, undefined, 4]
            

Daca se seteaza o lungime mai mica, sirul este trunchiat. O valoare mai mare creaza un sir
cu elemente goale.

### Concluzii

Pentru cele mai bune performante, este recomandat ca intodeauna sa fie folosita
parcurgerea cu instructiunea `for` si memorarea proprietatii `length`. Parcurgerea cu
`for in` este un semn de cod scris gresit si poate duce la defecte si performante scazute.
