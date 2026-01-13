# Tehnica de Programare Backtracking

## Cuprins
- [Prezentare Generală](#prezentare-generală)
- [Când se Utilizează Backtracking](#când-se-utilizează-backtracking)
- [Forma Generală a Algoritmului](#forma-generală-a-algoritmului)
- [Concepte Cheie](#concepte-cheie)
- [Probleme Clasice](#probleme-clasice)
- [Complexitate](#complexitate)
- [Optimizări Posibile](#optimizări-posibile)

## Prezentare Generală

Backtracking este o tehnică de programare utilizată pentru determinarea tuturor soluțiilor unei probleme într-un mod progresiv, evitând generarea întregului spațiu al soluțiilor. Soluțiile se construiesc componentă cu componentă, testându-se la fiecare pas validitatea lor.

### Principiul de Bază

- Soluțiile se construiesc **pas cu pas** (componentă cu componentă)
- La fiecare pas se verifică dacă soluția parțială este validă
- Dacă soluția parțială nu poate duce la o soluție completă, este **abandonată** (backtrack)
- Se evită astfel o rezolvare de tip **forță-brută**

### Exemplu Comparativ: Generarea Permutărilor pentru n=6

**Forță-Brută:**
- Generează toate tuplurile: 6⁶ = 46,656 tupluri
- Selectează doar permutările valide: 6! = 720
- Eficiență: ~1.5%

**Backtracking:**
- Generează doar soluții parțiale valide
- Abandonează imediat ramurile care nu pot duce la soluții
- Mult mai eficient, dar complexitatea rămâne mare

## Când se Utilizează Backtracking

Backtracking este ideal pentru probleme care pot fi formalizate astfel:

> Fie mulțimile nevide A₁, A₂, ..., Aₙ și un predicat P. Să se genereze toate tuplurile X = (x₁, x₂, ..., xₙ) pentru care xᵢ ∈ Aᵢ și P(x₁, x₂, ..., xₙ) = 1.

**Tipuri de probleme:**
- Generări combinatoriale (permutări, aranjamente, combinări)
- Probleme de decizie (există soluție?)
- Probleme de numărare (câte soluții există?)
- Probleme de optimizare (cea mai bună soluție)

## Forma Generală a Algoritmului

```python
def bkt(k):
    global s
    # Parcurgem toate valorile posibile v pentru s[k]
    for v in range(min_k, max_k + 1):
        # Atribuim componentei curente s[k] valoarea v
        s[k] = v
        
        # Verificăm dacă s[1],...,s[k] este soluție parțială
        if este_solutie_partiala(s, k):
            # Verificăm dacă este soluție completă
            if este_solutie_completa(s, k):
                # Prelucrăm soluția (afișare, salvare, etc.)
                prelucreaza_solutie(s, k)
            else:
                # Continuăm cu următoarea componentă
                bkt(k + 1)
```

### Observații Importante

- Bucățile de cod trebuie particularizate pentru fiecare problemă
- Tabloul `s` este indexat de la 1 (nu de la 0) pentru scriere naturală
- `min_k` și `max_k` se deduc din semnificația componentei `s[k]`
- Pentru testarea soluției complete nu retestăm condițiile de continuare
- Dacă `s[1],...,s[k]` nu este soluție parțială, nu se adaugă `s[k+1]`

## Concepte Cheie

### 1. Componenta Curentă
Componenta asupra căreia se acționează în momentul respectiv: `s[k]`

### 2. Soluție Parțială
Un tuplu `(x₁, ..., xₖ)` este soluție parțială dacă îndeplinește **condițiile de continuare** - există posibilitatea de a-l extinde până la o soluție completă.

### 3. Condițiile de Continuare
Condițiile pe care trebuie să le îndeplinească tuplul curent astfel încât să aibă sens extinderea sa. Acestea sunt:
- **Necesare** (deduse din predicatul P)
- **Nu întotdeauna suficiente**

### 4. Soluție Completă
O soluție parțială care îndeplinește și condițiile suplimentare specifice problemei.

## Probleme Clasice

### 1. Generarea Permutărilor

Generează toate permutările mulțimii {1, 2, ..., n}.

```python
def bkt(k):
    global s, n
    for v in range(1, n + 1):
        s[k] = v
        # Condiție de continuare: valoarea nu a fost folosită
        if s[k] not in s[:k]:
            # Condiție de soluție: avem n componente
            if k == n:
                print(*s[1:], sep=",")
            else:
                bkt(k + 1)

n = int(input("n = "))
s = [0] * (n + 1)
print("Toate permutările de lungime " + str(n) + ":")
bkt(1)
```

**Particularizări:**
- `min_k = 1`, `max_k = n`
- Soluție parțială: `s[k] ≠ s[i]` pentru orice `i ∈ {1,...,k-1}`
- Soluție completă: `k == n`
- Complexitate: **Ω(n!)**

### 2. Generarea Aranjamentelor

Aranjamente cu p elemente ale unei mulțimi cu n elemente (p ≤ n).

**Diferență față de permutări:** lungimea soluției este `p` în loc de `n`

**Număr de soluții:** Aⁿₚ = n!/(n-p)!

```python
def bkt(k):
    global s, n, p
    for v in range(1, n + 1):
        s[k] = v
        if s[k] not in s[:k]:
            if k == p:  # Diferență: p în loc de n
                print(*s[1:], sep=",")
            else:
                bkt(k + 1)

n = int(input("n = "))
p = int(input("p = "))
s = [0] * (p + 1)
print(f"Toate aranjamentele cu {p} elemente din {n}:")
bkt(1)
```

**Complexitate:** Ω(Aⁿₚ) = Ω(n!/(n-p)!)

### 3. Generarea Combinărilor

Submulțimi cu p elemente ale unei mulțimi cu n elemente.

**Observație importantă:** În submulțimi ordinea NU contează: {1,2,3} = {3,1,2}

**Soluție:** Generăm doar soluții cu elemente în ordine strict crescătoare.

```python
def bkt(k):
    global n, m, sol, cnt
    # Începem de la sol[k-1]+1 pentru ordine crescătoare
    for v in range(sol[k-1] + 1, n + 1):
        sol[k] = v
        if k == m:
            cnt += 1
            print(str(cnt).rjust(3) + ". ", end="")
            print(*sol[1:], sep=",")
        else:
            bkt(k + 1)

n = int(input("n = "))
m = int(input("m = "))
cnt = 0
sol = [0] * (m + 1)
print(f"Toate submulțimile cu {m} elemente ale unei mulțimi cu {n} elemente:")
bkt(1)
```

**Avantaje:**
- Nu mai verificăm condiții de continuare (elementele sunt automat distincte)
- Nu generăm duplicate
- Foarte eficient

**Număr de soluții:** Cⁿₚ = n!/(p!(n-p)!)

**Complexitate:** Ω(Cⁿₚ)

### 4. Generarea Anagramelor

Generează toate anagramele distincte ale unui cuvânt.

```python
def bkt(k):
    global s, n, cuv, cuv_dist
    for v in range(1, n + 1):
        s[k] = v
        if s[k] not in s[1:k]:
            if k == n:
                aux = "".join([cuv[s[i]-1] for i in range(1, n + 1)])
                cuv_dist.add(aux)
            else:
                bkt(k + 1)

cuv = input("Cuvantul: ")
n = len(cuv)
cuv_dist = set()
s = [0] * (n + 1)
bkt(1)
print("Anagramele distincte ale cuvântului " + cuv + ": ")
print(*cuv_dist, sep="\n")
```

### 5. Descompunerea unui Număr Natural

Descompune un număr natural n ca sumă de numere naturale nenule.

**Exemplu:** n=4 → 1+1+1+1, 1+1+2, 1+2+1, 1+3, 2+1+1, 2+2, 3+1, 4

```python
def bkt(k):
    global sol, n
    # max: n-k+1 (componentele anterioare au minim 1)
    for v in range(1, n - k + 2):
        sol[k] = v
        scrt = sum(sol[:k + 1])
        # Condiție de continuare: suma ≤ n
        if scrt <= n:
            # Soluție: suma == n
            if scrt == n:
                print(*sol[1:k + 1], sep="+")
            else:
                bkt(k + 1)

n = int(input("n = "))
sol = [0] * (n + 1)
bkt(1)
```

**Particularizări:**
- `min_k = 1`, `max_k = n - k + 1`
- Soluție parțială: `sum(s[1:k+1]) ≤ n`
- Soluție completă: `sum(s[1:k+1]) == n`
- Lungimi variabile (de la 1 la n)

**Variante:**
- Descompuneri distincte (fără duplicate în ordine)
- Descompuneri cu termeni distincți (fără numere egale)
- Descompuneri de lungime fixă
- Descompuneri cu termeni pari/impari

### 6. Problema celor N Regine

Plasează n regine pe o tablă n×n astfel încât nicio două să nu se atace.

**Reguli:** Două regine se atacă dacă sunt pe:
- Aceeași linie
- Aceeași coloană
- Aceeași diagonală

```python
def bkt(k):
    global s, n
    for v in range(1, n + 1):
        s[k] = v
        # Verificare coloană și diagonală
        if s[k] not in s[:k] and \
           True not in [abs(k - i) == abs(s[k] - s[i]) 
                        for i in range(1, k)]:
            if k == n:
                print(*s[1:], sep=",")
            else:
                bkt(k + 1)

n = int(input("n = "))
s = [0] * (n + 1)
print(f"Soluții pentru problema celor {n} regine:")
bkt(1)
```

**Particularizări:**
- `s[k]` = coloana pe care este regina de pe linia k
- Condiție coloană: `s[k] ≠ s[i]`
- Condiție diagonală: `|s[k] - s[i]| ≠ |k - i|`
- Pentru n=8: 92 soluții
- Pentru n≤3: nu există soluții

**Context istoric:**
- Formulată de Max Bezzel în 1848 (pentru n=8)
- Generalizată de Franz Nauck în 1850
- Studiată de matematicieni celebri (Gauss, Dijkstra)

### 7. Plata unei Sume cu Monede

Determină toate modalitățile de plată a unei sume P folosind monede cu valori date.

**Exemplu:** P=12$, monede=[2$, 3$, 5$] → 5 modalități

```python
def bkt(k):
    global s, P, v, n
    # s[k] = număr de monede cu valoarea v[k]
    for m in range(0, P // v[k] + 1):
        s[k] = m
        scrt = sum([s[i] * v[i] for i in range(k + 1)])
        if scrt <= P:
            if scrt == P and k == n:
                for i in range(1, n + 1):
                    if s[i] != 0:
                        print(s[i], "x", v[i], "$ + ", end="")
                print()
            else:
                if k < len(v[1:]):
                    bkt(k + 1)

P = int(input("Suma de plată: "))
aux = [int(x) for x in input("Valorile monedelor: ").split()]
v = [0]
v.extend(aux)
n = len(v[1:])
s = [0] * len(v)
print("Toate modalitățile de plată:")
bkt(1)
```

**Particularizări:**
- `s[k]` = număr de monede cu valoarea `v[k]`
- `min_k = 0`, `max_k = P / v[k]`
- Soluție parțială: `sum(s[i]*v[i]) ≤ P`
- Soluție completă: `sum(s[i]*v[i]) == P` și `k == n`
- Lungimi variabile

**⚠️ Atenție:** Limitare la `k < n` pentru a evita erori de memorie!

## Complexitate

### Complexitate Generală
Backtracking are complexitate **ridicată**, dar mai mică decât forța-brută:
- Depinde de numărul de soluții generate
- De obicei: **exponențială** sau **factorială**

### Complexități pentru Probleme Clasice

| Problemă | Complexitate Minimă | Nr. Soluții | Observații |
|----------|---------------------|-------------|------------|
| Permutări | Ω(n!) | n! | Factorial |
| Aranjamente | Ω(Aⁿₚ) | n!/(n-p)! | Factorial parțial |
| Combinări | Ω(Cⁿₚ) | n!/(p!(n-p)!) | Binomial |
| N Regine | Ω(n!) | Variabil | Bazat pe permutări |
| Descompuneri | Exponențială | p(n) | Funcție de partiție |
| Plata cu monede | O(2ⁿ) | Variabil | Aproximativ |

### Estimarea Complexității

> **Regulă generală:** Complexitatea ≥ Numărul de soluții afișate

Această euristică funcționează deoarece un algoritm nu poate avea complexitate mai mică decât afișarea output-ului.

**Exemplu:** Pentru n=1000, descompunerile distincte sunt aproximativ 2.4 × 10³¹!

## Optimizări Posibile

Deși complexitatea rămâne mare, există tehnici de optimizare:

### 1. Interval Minim pentru Componente
Alegerea intervalului `[min_k, max_k]` cât mai restrâns

**Exemplu:** În combinări, `min_k = s[k-1] + 1` elimină toate valorile inutile

### 2. Vectori de Marcaje
Pentru verificare rapidă a valorilor utilizate

```python
# În loc de: if s[k] not in s[:k]
# Folosim:
used = [False] * (n + 1)
if not used[v]:
    used[v] = True
    # ... proces backtracking
    used[v] = False  # reset la întoarcere
```

### 3. Actualizare Dinamică
A valorilor folosite în condiții (ex: suma curentă)

```python
# În loc de: scrt = sum(sol[:k+1])
# Actualizăm dinamic:
global suma_curenta
suma_curenta += sol[k]
# ... verificări
suma_curenta -= sol[k]  # la întoarcere
```

### 4. Structuri de Date Auxiliare
Pentru eficientizare verificări (hash sets, arrays de bool, etc.)

**⚠️ Notă:** Aceste optimizări complică codul și nu schimbă complexitatea asimptotică. Backtracking rămâne eficient doar pentru date mici.

## Variante ale Backtracking

### 1. Probleme de Numărare
**Scop:** Câte soluții există?

```python
count = 0

def bkt(k):
    global count
    # ... cod backtracking
    if este_solutie:
        count += 1  # În loc de print
```

**⚠️ Notă:** Adesea există formule matematice mai eficiente!

### 2. Probleme de Decizie
**Scop:** Există măcar o soluție?

```python
found = False

def bkt(k):
    global found
    if found:
        return  # Oprire la prima soluție
    # ... cod backtracking
    if este_solutie:
        found = True
        return
```

**⚠️ Notă:** Uneori există algoritmi specializați mai eficienți.

### 3. Probleme de Optimizare
**Scop:** Cea mai bună soluție (min/max)

```python
best_solution = None
best_value = float('inf')  # sau -inf pentru maximizare

def bkt(k):
    global best_solution, best_value
    # ... cod backtracking
    if este_solutie:
        value = calculeaza_valoare(s)
        if value < best_value:  # sau > pentru max
            best_value = value
            best_solution = s[1:k+1].copy()
```

**Alternative mai eficiente:**
- **Greedy** - pentru probleme cu structură specială
- **Programare Dinamică** - pentru probleme cu substructură optimă

## Concluzie

### ✅ Avantaje
- Mai eficient decât forța-brută
- Aplicabil la multe tipuri de probleme
- Implementare relativ simplă și intuitivă
- Generează TOATE soluțiile

### ❌ Dezavantaje
- Complexitate ridicată (exponențială/factorială)
- Timp de execuție acceptabil doar pentru date mici
- Există adesea metode mai eficiente pentru probleme specifice

### 🎯 Când să folosești Backtracking

**DA:**
- Când trebuie să generezi TOATE soluțiile
- Când datele de intrare sunt mici (n < 15-20)
- Când nu există o metodă mai eficientă cunoscută
- Pentru probleme de natură combinatorială

**NU:**
- Pentru date mari (n > 25)
- Când există algoritmi Greedy sau DP aplicabili
- Când există formule matematice directe
- Pentru probleme cu restricții de timp stricte

### 📚 Resurse Suplimentare

Pentru înțelegere mai profundă:
- Teoria numerelor (funcții de partiție)
- Analiza combinatorică
- Tehnici de pruning (tăiere ramuri)
- Branch and Bound (pentru optimizare)

---

**Autor:** Bazat pe cursul de Programarea Algoritmilor - Curs 14  
**Limbaj:** Python 3.x  
**Nivel:** Intermediar-Avansat