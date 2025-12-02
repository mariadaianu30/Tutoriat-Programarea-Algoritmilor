## Problema 1
Se consideră o rețea în plan formată din puncte unite prin linii numite legături (muchii).
Fiecare punct are coordonatele întregi, iar o legătură are asociată o culoare (un șir de
caractere fără spații reprezentând numele culorii, de exemplu: roșu, verde, albastru) și o
etichetă (un șir care poate conține spații). Un punct cu coordonatele x și y va fi notat (x,y). Se
consideră fișierul text legaturi.in care conține informații despre o astfel de rețea, fiecare linie
conținând informații despre o legătură sub forma:
[x1,y1] [x2,y2] culoare eticheta
unde [x1,y1] și [x2,y2] sunt punctele între care există legătură, iar culoare și etichetă
reprezintă culoarea și eticheta asociate legăturii. Vom spune că legătura este între punctele
[x1,y1] și [x2,y2], vom numi punctele [x1,y1] și [x2,y2] capetele legăturii (legătura este
neorientată și bidirecțională) și cele două puncte sunt vecine. Un exemplu de fișier de acest
tip este următorul:

### legaturi.in
```python

[1,2] [1,3] rosu legatura 1
[1,2] [1,4] albastru legatura 2
[1,3] [2,6] rosu legatura 3
[2,6] [2,7] albastru legatura 4
[2,7] [3,8] rosu legatura 5
```

a) [2 p.] Să se memoreze datele din fișier într-o singură structură astfel încât să se răspundă
eficient la cerințele de la punctele următoare (interogarea și modificarea informațiilor
despre o legătură dintre două puncte date, determinarea vecinilor unui punct).
b) [1 p.] Scrieți o funcție insereaza_legatura care primește 5 parametri:
● în primul parametru se transmite structura în care s-au memorat datele la cerința a)
● următorii 2 parametri sunt tupluri cu 2 elemente reprezentând capetele unei legături
● ultimii 2 parametri sunt șiruri de caractere reprezentând culoarea și eticheta unei
legături.
Dacă există deja o legătură în rețea între punctele primite ca parametru funcția va returna
False, altfel funcția va adăuga această legătură în rețea (modificând structura trimisă ca
parametru) și va returna True. Să se apeleze funcția pentru punctele (1,3) și (2,7), culoarea
negru și eticheta "legatura noua" și să se afișeze legăturile memorate în structura obținută
în același format în care s-au dat și datele în fișier (nu contează ordinea în care se vor afișa
legăturile).


### Iesire


```python

[1,2] [1,3] rosu legatura 1
[1,2] [1,4] albastru legatura 2
[1,3] [2,6] rosu legatura 3
[2,6] [2,7] albastru legatura 4
[2,7] [3,8] rosu legatura 5
[1,3] [2,7] negru legatura noua
```

c) [1 p.] Scrieți o funcție vecini care primește ca parametri (în această ordine): structura în
care s-au memorat datele la cerința a) și un număr variabil de tupluri cu 2 elemente
reprezentând puncte din rețea. Funcția va returna o listă cu acele puncte p din rețea cu
proprietatea că există legătură de la p la orice punct primit ca parametru (vecinii comuni
pentru punctele primite ca parametru). Punctele din lista returnată vor fi ordonate
descrescător după a doua coordonată. Apelați funcția pentru punctele (2,7) și (1,2) și afișați
rezultatul obținut.

### Iesire

```python
[(3, 8), (1, 3)]
```

## Problema 2

. Se dă fișierul “autori.in” cu următoarea structură:
• Pe prima linie sunt două numere naturale m și n separate printr-un spațiu.
• Pe următoarele m linii sunt câte 3 valori separate prin spațiu reprezentând
informații despre un autor: codul (număr natural), numele și prenumele unui autor.
• Pe următoarele n linii sunt valori separate prin spațiu reprezentând 5
informații despre cărți scrise de autorii dați anterior (o carte are un unic autor): codul
unui autor (număr natural, dintre codurile date pe liniile 2, …, m+1), codul cărții (număr
natural), an apariție, număr de pagini, numele cărții (șir ce poate conține spații).

### autori.in

```python
3 7
11 Ionescu Ion
20 Popescu Marin
17 Georgescu Oana
11 131 2010 30 Despre algoritmi
11 101 1990 70 Bazele Informaticii
20 213 2012 80 Introducere in C/C++
11 141 2010 100 Complexitatea algoritmilor
11 121 2010 100 Tehnici de programare
17 214 2018 150 Introducere in Python
20 111 2017 50 Initiere in programare
```

a. [1,25p] Să se memoreze datele din fișier într-o singură structură astfel încât să se
răspundă cât mai eficient la cerințele b) (ștergerea unei cărți având dat codul cărții și aflarea
numelui unicului său autor) și c) (accesarea numelui unui autor și a informațiilor despre toate
cărțile sale, având dat codul autorului).
b. [0,75p] Să se scrie o funcție sterge_carte cu 2 parametri: în primul parametru se
transmite structura în care s-au memorat datele la cerința a), iar al doilea este codul unei
cărți, care șterge din structura de date primită toate informațiile legate de cartea cu codul
dat ca parametru. Funcția returnează numele unicului autor al cărții cu codul dat,
sau None dacă acea carte nu s-a găsit.
Să se apeleze funcția pentru un cod de carte citit de la tastatură și să se afișeze pe
ecran mesajul “Cartea a fost scrisa de … .”, sau
mesajul “Cartea nu exista.”. Apoi să se afișeze pe ecran toată structura rămasă după ștergere.

| Intrare de la tastatură | Ieșire pe ecran                           |
|------------------------|------------------------------------------|
| 111                    | Cartea a fost scrisa de Popescu Marin.   |
|                        | ...structura de date afisata             |
| 333                    | Cartea nu exista.                        |


c. [1p] Să se scrie o funcție carti_autor cu 2 parametri: în primul parametru se
transmite structura în care s-au memorat datele la cerința a), iar al doilea este codul
unui autor. Funcția returnează numele autorului și o listă cu informații despre cărțile sale (un
element al listei fiind un tuplu ce conține: numele cărții, anul apariției, numărul de pagini),
lista fiind sortată crescător după anul apariției, în caz de egalitate descrescător după numărul
de pagini, iar în caz de egalitate crescător după numele cărții. Funcția va returna o listă vidă
dacă nu există un autor cu codul primit ca parametru.
Să se apeleze funcția pentru un cod de autor citit de la tastatură și să se afișeze
rezultatul returnat ca în exemplul de mai jos.

| Intrare de la tastatură | Ieșire pe ecran                         |
|------------------------|------------------------------------------|
| 11                     | Ionescu Ion                              |
|                        | Bazele Informaticii 1990 70              |
|                        | Complexitatea algoritmilor 2010 100      |
|                        | Tehnici de programare 2010 100           |
|                        | Despre algoritmi 2010 30                 |
| 10                     | cod incorect                             |


## Problema 3

Se consideră fișierul text catalog.in cu următoarea structură:
• pe prima linie apare numărul n reprezentând numărul de elevi dintr-o clasă a unui liceu
• pe următoarele linii avem informații despre cei n elevi, respectiv pentru fiecare elev
informațiile sunt structurate astfel:
▪ linie de forma <șir de caractere> <m>, unde șirul de caractere este numele elevului (acesta
este unic), iar m este un număr natural reprezentând numărul de materii
▪ urmată de m linii care conțin notele elevului (numere naturale) la m materii, fiecare având
următoarea structură:
<nume_materie>,<nota_1>,<nota_2>,...,<nota_k>
Observație: Orice elev are la fiecare materie cel puțin o notă, iar denumirile materiilor nu conțin
caracterul ',' (virgula).

### Exemplu de fișier de intrare:


```python
5
Ana Maria Pop 3
Matematica,10,9,9,10,10
Limba romana,8,9,9,8
Fizica,10,9,7,10,10
Mihai Popescu 3
Matematica,9,7,10,10
Limba romana,8,3,5,10
Fizica,10,10
Andrei Mincu 2
Matematica,10,9,2
Fizica,3,7,9
Ioana Matei 3
Fizica,10,10
Matematica,10,10,10,9
Limba romana,9,9,10,10
Alin Enache 3
Limba romana,10,10,10
Matematica,10,10,10,10
Fizica,10
```


Cerințe:
a) [2 p.] Scrieți o funcție care citește datele din fișierul catalog.in și returnează o structură de
date cu informațiile din fișier. Folosiți o structură de date convenabilă pentru a rezolva
eficient subpunctele următoare.
b) [1 p.] Scrieți o funcție detalii_elev care primește ca parametri structura în care s-au memorat
datele la cerința a) și un șir de caractere reprezentând numele unui elev și returnează mediile
la toate materiile elevului cu numele primit ca parametru, memorate sub formă de listă de
tupluri de tipul (nume_materie, medie). Dacă un elev are o singură notă la o materie sau
media este mai mică strict decât 5, acesta va avea media egală cu 0 și va rămâne corigent. Să
se citească de la tastatură numele unui elev și să se afișeze pe ecran mediile acestuia
(rotunjite cu două zecimale) la fiecare materie (sortate lexicografic) folosind această funcție.
### Exemplu:
### Intrare tastatură: 

```python
Ana Maria Pop
```

### Afișare pe ecran:

```python
Fizica 9.20
Limba romana 8.50
Matematica 9.60

```

c) [1 p.] Scrieți o funcție clasament care primește structura de date în care s-au memorat datele
la cerința a) și un număr variabil de parametri de tip șir de caractere reprezentând nume de
elevi. Funcția returnează o listă de tupluri de tipul (nume_elev, medie_generala) cu mediile
generale ale elevilor ale căror nume au fost primite ca parametru ordonată descrescător după
medii. Media generală a unui elev este egală cu media aritmetică a mediilor de la fiecare
materie, dacă acesta nu este corigent, altfel media este 0.

### Exemplu: 

Dacă se apelează funcția pentru elevii Alin Enache și Ioana Matei se va returna lista
[(Ioana Matei,9.75), (Alin Enache,0)], deoarece Alin Enache are o singură notă la
fizică, deci este corigent.

## Problema 4

Fișierul text cinema.in conține programul dintr-o zi al unui lanț de cinematografe. Fiecare linie
din fișier are următoarea structură:
nume_cinematograf % nume_film % ore_de_difuzare
unde nume_cinematograf este un șir de caractere reprezentând numele unui cinematograf,
nume_film este numele unui film (numele cinematografului și al filmuluisunt formate din cuvinte
separate prin câte un spațiu și nu conțin caracterul '%'), iar ore_de_difuzare este un șir de
caractere conținând orele (sub forma hh:mm) la care este programat filmul în cinematograf, orele
fiind separate prin câte un spațiu. Un exemplu de astfel de fișier este:


### cinema.in

```python
Cinema 1 % Minionii 2 % 12:30 18:30
Cinema 3 % Elfii cofetari % 10:30 12:30
Cinema 2 % Minionii 2 % 15:00 18:30 20:30
Cinema 1 % Elfii cofetari % 10:00 12:30
Cinema 2 % Gasca Animalutelor % 15:00 18:30 20:00
Cinema 4 % Minionii 2 % 16:00 18:30 20:30
Cinema 1 % Buna dimineata % 09:30

```

a) [2,5 p.] Să se memoreze datele din fișier într-o singură structură de date astfel încât să se
răspundă cât mai eficient la cerințele de la punctele următoare.

b) [1 p.] Scrieți o funcție sterge_ore care are următorii parametri (în această ordine):
• structura în care s-au memorat datele la cerința a)
• un șir de caractere cinema reprezentând numele unui cinematograf
• un șir de caractere film reprezentând numele unui film
• mulțime ore având ca elemente șiruri de caractere de forma hh:mm
Funcția va șterge din programul cinematografului cinema programările filmului film de la
orele din mulțimea ore și va returna o listă cu filmele programate la cinematograful cinema după
această actualizare. Se citesc de la tastatură un nume de film f, un nume de cinematograf c și un
șir de caractere o de forma hh:mm reprezentând o oră. Să se apeleze funcția sterge_ore pentru
a șterge programarea filmului f la cinematograful c la ora o și să se afișeze lista returnată; după
apelul funcției să se afișeze și structura în care s-au memorat datele.

c) [1,5 p.] Scrieți o funcție cinema_film care primește următorii parametri: structura în care sau memorat datele la cerința a), un număr variabil de șiruri de caractere reprezentând nume
de cinematografe și doi parametri ora_minima și ora_maxima șiruri de caractere de forma
“hh:mm” reprezentând ore. Funcția returnează o listă de tupluri cu elementele de tip
(nume_film, nume_cinema, lista_de_ore) cu filmele care rulează (încep) la cel puțin unul
dintre cinematografele primite ca parametru între orele ora_minima și ora_maxima, unde:
• nume_film este numele unui astfel de film
• nume_cinema este un nume de cinema dintre cele primite ca parametru la care rulează
filmul nume_film
• lista_de_ore este lista orelor la care este programat filmul nume_film la cinematograful
nume_cinema între orele ora_minima și ora_maxima, ordonată crescător


Lista returnată va fi ordonată crescător după numele filmului, apoi, în caz de egalitate,
descrescător după numărul de elemente din lista_de_ore. Să se apeleze funcția pentru
cinematografele ‘Cinema 1’ și ‘Cinema 2’, ora_minima "14:00" și ora_maxima "22:00" și să se afișeze lista returnată. 
### Explicații: 
pentru datele din fișier lista returnată va fi:

[('GascaAnimalutelor', 'Cinema 2', ['15:00', '18:30', '20:00']), ('Minionii 2', 'Cinema 2', ['15:00', '18:30', '20:30']), ('Minionii 2', 'Cinema 1', ['18:30'])];

-filmul ‘Elfii cofetari’ nu apare în listă deoarece este programat mai devreme de ora “14:00

