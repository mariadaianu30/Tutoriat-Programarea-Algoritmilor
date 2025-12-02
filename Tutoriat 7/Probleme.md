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

## legaturi.in
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


## Iesire


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

## Iesire

```python
[(3, 8), (1, 3)]
```
