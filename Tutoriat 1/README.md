# Programarea Algoritmilor – Tutorial 1


## 1. Introducere în Python
 Ce este Python?

-Creat de Guido van Rossum (1991).

-Limbaj interpretat, multi-paradigmă (procedural, orientat obiect, funcțional).

-Popular pentru simplitate, citibilitate și suport extins de biblioteci.


## Instalare

🔗 [Python.org – Download](https://www.python.org/downloads/)


## 2. Tipuri de date fundamentale
| Tip de date | Clasă internă | Exemple | Descriere |
|--------------|----------------|-----------|------------|
| `NoneType` | `NoneType` | `None` | absența unei valori |
| `int` | `int` | `5`, `0b101`, `0x1F` | numere întregi |
| `float` | `float` | `3.14`, `-2.5e3` | numere reale |
| `complex` | `complex` | `2+3j` | numere complexe |
| `bool` | `bool` | `True`, `False` | valori logice |
| `str` | `str` | `'text'`, `"abc"` | șiruri de caractere |
| `list` | `list` | `[1, 2, 3]` | secvență mutabilă |
| `tuple` | `tuple` | `(1, 2, 3)` | secvență imutabilă |
| `set` | `set` | `{1, 2, 3}` | mulțime fără duplicate |
| `dict` | `dict` | `{"a": 1, "b": 2}` | perechi cheie: valoare |

## 3. Variabile și conversii

Python nu cere declararea tipului – tipul este determinat dinamic.

Poți folosi funcțiile type() și id() pentru a inspecta o variabilă.

a = 10
b = "10"
print(type(a), type(b))  # <class 'int'> <class 'str'>
print(int(b) + 5)        # conversie string -> int



## 4. Afișare și citire
### Afișare
print("Salut", "Python", sep=" | ", end="!!!\n")

### f-strings (format modern)
nume = "Ana"
varsta = 20
print(f"{nume} are {varsta} ani.")

### Citire
x= input("x= ")  //valoarea cititită este întodeauna un șir de caractere

###Pentru a transforma șirurile de caractere citite în valori de alte tipuri primitive se 
folosesc funcțiile de conversie int(șir), float(șir), complex(șir) sau bool(șir)

n = int(input("Introdu un număr: "))
print(f"Pătratul lui {n} este {n**2}")

## 5. Operatorii principali
### -Aritmetici

+ - * / // % **

a, b = 7, 2
print(a / b, a // b, a % b, a ** b)

### -Relaționali

< <= > >= == != is/is not   in/not in

print(3 in [1, 2, 3])     # True
print("a" is "a")         # True (aceeași referință)

### -Logici

not, and, or

x = 0
print(not x)  # True (0 e considerat False)

### -Pe biți

~, &, |, ^, <<, >>

print(5 & 3, 5 | 3, 5 ^ 3)

## 6. Instrucțiuni de control
### -Atribuire
x = 5
x += 3
a, b = 1, 2
a, b = b, a  # interschimbare

### -Condiționale (if, elif, else)
x = int(input("x = "))
if x < 0:
    print("Negativ")
elif x == 0:
    print("Zero")
else:
    print("Pozitiv")


🔸 Operator ternar:

paritate = "Par" if x % 2 == 0 else "Impar"

### -Repetiții (while, for)

### -Buclă while

n = 123
s = 0
while n > 0:
    s += n % 10
    n //= 10
print("Suma cifrelor =", s)


### -Buclă for

for i in range(5):
    print(i, end=" ")


### -Range personalizat

for i in range(2, 10, 2):  # start=2, stop=10, pas=2
    print(i)

## Alte instrucțiuni utile

continue → sare peste iterația curentă
break → oprește complet bucla
else → se execută doar dacă bucla s-a terminat natural
pass → “placeholder” fără acțiune

for i in range(10):
    if i == 3:
        continue
    if i == 8:
        break
    print(i)
else:
    print("Bucla s-a terminat normal.")

## 7. Funcții și expresii utile pentru începători
| Funcție | Descriere | Exemplu |
|----------|------------|----------|
| `len()` | lungimea unei secvențe | `len("abc") → 3` |
| `sum()` | suma elementelor numerice | `sum([1, 2, 3]) → 6` |
| `max()`, `min()` | maxim / minim | `max(4, 2, 7)` |
| `abs()` | valoare absolută | `abs(-5)` |
| `round()` | rotunjire | `round(3.14159, 2)` |
| `sorted()` | sortare | `sorted([3, 1, 2]) → [1, 2, 3]` |
| `type()`, `isinstance()` | verificare tip | `isinstance(3, int)` |



# Programarea Algoritmilor - Curs 03: Șiruri de Caractere și Fișiere Text în Python

Acest material conține o sinteză a conceptelor de bază legate de **șirurile de caractere (strings)** și **manipularea fișierelor text** în limbajul de programare Python.

## 1. Șiruri de Caractere (Strings)

În Python, un șir de caractere este o secvență de caractere indexată de la 0, stocată ca un obiect de tipul clasei `str`. Python utilizează setul de caractere **Unicode**.

### 1.1. Moduri de Reprezentare a Șirurilor

Constantele (literalii) de tip șir pot fi reprezentate în două moduri:

* **Pe o singură linie:** Folosind ghilimele simple (`'șir'`) sau duble (`"șir"`).
* **Pe mai multe linii:** Folosind trei ghilimele simple (`'''șir'''`) sau trei ghilimele duble (`"""șir"""`).

Se pot insera și **secvențe escape** (de exemplu, `\n` pentru linie nouă, `\t` pentru tab).

### 1.2. Imutabilitatea Șirurilor

O proprietate fundamentală este că șirurile de caractere sunt **imutabile**. Aceasta înseamnă că valoarea unui obiect de tip șir nu poate fi modificată după creare.

* Nicio metodă din clasa `str` nu modifică șirul curent, ci **creează un șir nou**.
* Pentru a "modifica" un șir, trebuie modificată referința variabilei la noul șir creat.
    * Exemplu: `s = s.upper()`

### 1.3. String Interning (Bazinul de Șiruri)

Python utilizează mecanismul de **string interning** pentru stocarea șirurilor, păstrând o singură copie a fiecărui șir distinct într-un **bazin de șiruri** (*string pool*).

* **Avantaje:** Reduce spațiul de memorie și crește viteza de comparare. Compararea `s == t` (valoare) poate fi înlocuită cu compararea `s is t` (referință/ID) care are complexitate $O(1)$ în loc de $O(len(s))$.
* **Se bazează pe imutabilitate**.
* **Internare Explicită:** Se poate folosi metoda `sys.intern(șir)` din modulul `sys` pentru a salva explicit un șir în bazin.

### 1.4. Accesarea Elementelor (Indexare și Slicing)

#### Indexare
Elementele se accesează prin indici.

* **Indici pozitivi:** De la $0$ la $n-1$ (de la stânga la dreapta).
* **Indici negativi:** De la $-n$ la $-1$ (de la stânga la dreapta).
* **Atenție:** Accesarea este de tip *read-only* (doar în citire) din cauza imutabilității.

#### Slicing
Se extrage un subșir folosind expresia `sir[st:dr]`.

* Extrage subșirul cuprins între pozițiile `st` (inclusiv) și `dr-1` (exclusiv).
* Se pot folosi indici pozitivi sau negativi.
* **Sintaxă completă:** `sir[start:stop:pas]`
    * `s[:]` returnează întregul șir.
    * `s[::-1]` returnează șirul oglindit (inversat).

### 1.5. Operatori Utili

| Operator | Descriere | Exemplu |
| :--- | :--- | :--- |
| `+` | Concatenare | `"un" + " exemplu"` = `"un exemplu"` |
| `*` | Multiplicare (concatenare repetată) | `"test" * 3` = `"testtesttest"` |
| `in`, `not in` | Testarea apartenenței unui subșir | `"est" in "atestat"` = `True` |
| `<`, `<=`, `>`, `>=`, `==`, `!=` | Comparări lexicografice (alfabetice) | `"POPA" == "Popa"` = `False` (depinde de implementare/locale) / **Atenție:** Literele mari sunt considerate "mai mici" lexicografic decât cele mici |

### 1.6. Metode Frecvente (Din Clasa `str`)

Metodele returnează un șir nou.

| Categorie | Metodă | Descriere |
| :--- | :--- | :--- |
| **Transformare** | `lower()`, `upper()`, `swapcase()`, `title()`, `capitalize()` | Transformări de litere (ex: mici în mari, prima literă a fiecărui cuvânt mare, etc.) |
| **Formatare** | `strip([caractere])` | Elimină prefixul și sufixul formate din caractere indicate (sau spații albe, implicit) |
| | `center(lățime, [caracter])` | Centrează șirul într-o lățime dată, folosind un caracter de umplere (sau spații, implicit) |
| | `format(...)` | Înlocuiește câmpurile variabile (`{}`) cu parametrii metodei (secvențial, pozițional sau cu nume) |
| **Clasificare** | `isspace()`, `islower()`, `isupper()`, `isalpha()`, `isdigit()`, `isalnum()`, etc. | Verifică dacă toate caracterele sunt de un anumit tip (returnează `True`/`False`) |
| **Căutare** | `count(subșir, [start], [stop])` | Numără aparițiile disjuncte ale unui subșir |
| | `find(subșir, [start], [stop])` | Furnizează cel mai mic indice la care începe subșirul (sau -1) |
| | `rfind(subșir, [start], [stop])` | Furnizează cel mai mare indice la care începe subșirul (sau -1) |
| | `startswith(prefix, [start], [stop])` | Verifică dacă șirul începe cu prefixul dat |
| | `endswith(sufix, [start], [stop])` | Verifică dacă șirul se termină cu sufixul dat |
| | `replace(subșir, subșir_nou, [max])` | Înlocuiește aparițiile subșirului |
| **Divizare/Construire** | `split(separator)` | Furnizează o listă de subșiruri folosind separatorul (implicit: spații albe) |
| | `join(listă_subșiruri)` | Concatenează șubșirurile dintr-o listă, folosind șirul curent ca separator |

---

## 2. Manipularea Fișierelor Text

Un fișier text este o secvență de caractere stocată pe linii în memoria externă, asigurând **persistența datelor**.

### 2.1. Deschiderea unui Fișier

Funcția `open("cale fișier", ["mod de deschidere"])` asociază fișierul fizic cu un obiect la nivel logic (de obicei, `io.TextIOWrapper`).

| Mod | Descriere | Acțiuni în caz de fișier inexistent |
| :--- | :--- | :--- |
| `"r"` | Citire (read) - **Mod implicit** | Generează `FileNotFoundError` |
| `"w"` | Scrierea (write) | Creează unul nou; dacă există, îl șterge automat și îl înlocuiește |
| `"x"` | Scrierea exclusivă (exclusive write) | Creează unul nou; dacă există, generează `FileExistsError` |
| `"a"` | Adăugare (append) | Creează unul nou; dacă există, scrie după ultimul caracter |

* **Tratarea excepțiilor:** Se folosește o structură `try...except` pentru a gestiona erorile de tip `FileNotFoundError` sau `FileExistsError`.

### 2.2. Citirea Datelor

Datele citite dintr-un fișier text sunt întotdeauna furnizate ca **șiruri de caractere**.

| Metodă | Descriere | Notă |
| :--- | :--- | :--- |
| `read()` | Furnizează **tot conținutul** fișierului text într-un singur șir de caractere. | Șirul returnat conține și caracterele de delimitare a liniilor (`\n`). |
| `readline()` | Furnizează conținutul **liniei curente** ca șir, sau un șir vid la sfârșitul fișierului. | Șirul returnat conține și caracterul de linie nouă (`\n`). |
| `readlines()` | Furnizează **toate liniile** într-o listă de șiruri de caractere. | Fiecare șir din listă conține și caracterul de linie nouă (`\n`). |

* **Citirea eficientă:** Pentru fișiere mari, se preferă citirea linie cu linie (iterarea directă a obiectului fișier) pentru a economisi memorie.
* **Conversia la Numere:** Dacă doriți să citiți numere, trebuie folosită o funcție de conversie, de exemplu `int()`.

### 2.3. Scrierea Datelor

Într-un fișier text se pot scrie **doar șiruri de caractere**.

| Metodă | Descriere |
| :--- | :--- |
| `write(șir)` | Scrie șirul în fișier, **fără a adăuga automat o linie nouă**. |
| `writelines(colecție de șiruri)` | Scrie toate șirurile din colecție, **fără a adăuga linii noi între ele**. |

### 2.4. Închiderea Fișierului

Fișierul trebuie închis explicit cu metoda `close()`.

* **Risc:** Dacă un fișier deschis pentru scriere nu este închis, ultimele informații scrise s-ar putea să nu fie salvate.
* **Instrucțiunea `with...as`:** Elimină necesitatea închiderii explicite, asigurând închiderea automată a fișierului chiar și în caz de erori.

```python
with open("exemplu.txt") as f:
    # Prelucrarea fișierului
    s = f.readlines()
# Aici fișierul f este deja închis automat
