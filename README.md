# Sortowania

## InsertionSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: —
  - idea: przesuwaj kolejne elementy najdalej "w lewo" jak to możliwe respektując uporządkowanie z lewym sąsiadem
  - czas:
    - pesymistyczny: $O(n^2)$
    - rzeczywisty: $\Theta(n + Inv(a))$
  - pamięć: —
  - dodatkowe info:
    - stabilny
    - liczba porównań: $n-1 + Inv(a)$
    - liczba przesunięć: **$Inv(a)$**
    - złożoność zależna od liczby inwersji
    - PL: "sortowanie przez wstawianie"
  - Pseudokod:
    
    **Niezmiennik:** $a[1 \dots i-1]$ jest posortowana
    ```
    for i in [2..n]:
      cur := a[i]
      j := i-1

      while cur < a[j]:
        a[j+1] := a[j]
        j--
    
      a[j+1] := cur
    ```

## BubbleSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: —
  - idea: Porównuj sąsiednie elementy i zamieniaj je miejscami, jeśli są w złej kolejności
  - czas:
    - pesymistyczny: $O(n^2)$
    - rzeczywisty: $\Theta(n^2)$
  - pamięć: —
  - dodatkowe info:
    - stabilny
    - liczba porównań: $\frac{n * (n-1)}{2}$
    - **liczba zamian: $Inv(a)$**
    - PL: "sortowanie bąbelkowe"
  - Pseudokod:
    
    **Niezmiennik:** $a[i+1 \dots n]$ jest posortowana i zawiera $n-i$ największych elementów $a$.
    ```
    for i in [n..2]:
      for j in [1..i-1]:
        if a[j] > a[j+1]:
          a[j] :=: a[j+1]
    ```

## SelectionSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: —
  - idea: W każdej iteracji znajdź największy element w nieposortowanej części tablicy i zamień go z ostatnim elementem tej części
  - czas:
    - pesymistyczny: $O(n^2)$
    - rzeczywisty: $\Theta(n^2)$
  - pamięć: —
  - dodatkowe info:
    - nie-stabilny
    - liczba porównań: $\frac{n*(n-1)}{2}$
    - **liczba zamian: $n-1$**
    - PL: "sortowanie przez wybieranie"
  - Pseudokod:

    **Niezmiennik:** $a[i+1..n]$ jest posortowana i zawiera $n-i$ największych elementów $a$.
    ```
    for i in [n..2]:
      i_max := 1
      for j in [2..i]:
        if a[j] > a[i_max]:
          i_max := j
    
      a[i] :=: a[i_max]
    ```
    Zaś ogólniej
    ```
    for i in [n..2]:
      i_max := indeks taki, że a[i_max] = max(a[1..i])
    a[i] :=: a[i_max]
    ```

### k-sortowanie / KSort
  - wejście: tablica $a[1 \dots n]$, liczba $k$, algorytm $salg$ sortowania
  - wyjście: $k$-posortowana tablica $a$
  - założenia:
    - $k < n$
    - tablica $a$ jest $k$-posortowana, jeśli $\forall _{i \in [1 \dots n-k]} a[i] \leq a[i+k]$
  - idea:
      Niezależnie posortuj $k$ podciągów tablicy $a$ algorytmem $salg$: \
        $a[1, 1+k, 1+2k, \dots]$ \
        $a[2, 2+k, 2+2k, \dots]$ \
        ... \
        $a[k, 2k, 3k, \dots]$
  - czas:
    - zależy od $salg$: $k * T_{salg}(\frac{n}{k})$
  - pamięć: —
  - dodatkowe info:
    - Jeśli na $k$-posortowanej tablicy wykonamy $h$-sortowanie, to pozostanie ona nadal $k$-posortowana
    - Na wykładzie wykorzystywane tylko do _ShellSort_

## ShellSort
  - wejście:
    - tablica $a[1 \dots n]$
    - tablica $h[1 \dots k]$, elementy tej tablicy nazywami **skokami**
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia:
    - $h[1] = 1$ (1-sortowanie to zwykłe sortowanie)
    - $h$ jest uporządkowana ściśle rosnąco
  - idea:
    W każdej iteracji wykonaj $j$-sortowanie, gdzie $j$ to kolejna liczba z tablicy $h$, idąc od końca do początku.
    Z czasem liczba inwersji się zmniejsza, co sprzyja szybszemu wykonaniu się sortowania przez wstawianie, którego czas zależy wprost od liczby inwersji.
  - czas: **(zależy od doboru ciągu skoków!!!)**
    - pesymistyczny: Pratt 1971: $O(n\log^2n)$ dzięki ciągowi skoków postaci $2^p3^q$: $1,2,3,4,6,8,9, \dots$
  - pamięć: —
  - dodatkowe info:
    - Algorytm Pratta:
      - długość ciągu skoków: $O(\log^2n)$
      - liczba inwersji w ciągu jednocześnie 2- i 3-posortowanym jest mniejsza od $n/2$
    - PL: "Metoda Shella"
  - Pseudokod:
    ```
    for i in [k..1]:
      h[i]-sortowanie metodą sortowania przez wstawianie
    ```

## Heap
  - operacje:
    - DownHeap
    - UpHeap
  - dodatkowe info: \
    warunek kopca: $heap(l,r) :: \forall _{l \leq i \leq r} lheap(i,r) \land rheap(i,r)$ \
    $lheap(i,r) :: 2i \leq r \Rightarrow a[i] \geq a[2i]$ - lewe poddrzewo zawiera elementy nie-większe \
    $rheap(i,r) :: 2i + 1 \leq r \Rightarrow a[i] \geq a[2i + 1]$ - prawe poddrzewo zawiera elementy nie-większe
### Heap.DownHeap
  - wynik: $heap(l,r)$
  - założenia: $heap(l+1,r)$
  - idea: Opuszczaj element $a[l]$ w dół kopca, zamieniając go z większym z dzieci, dopóki nie zostanie spełniony warunek kopca
  - czas: $O(\log\frac{r}{l})$
  - pamięć: —
    
### Heap.UpHeap
  - wynik: $heap(l,r)$
  - założenia: $heap(l,r-1)$
  - idea: Wynoś element $a[r]$ w górę kopca, zamieniając go z rodzicem, dopóki nie zostanie spełniony warunek kopca
  - czas: $O(\log\frac{r}{l})$
  - pamięć: —

## HeapSort
  - wejście: tablica $a[1 \dots n]$
  - wynik: tablica $a$ posortowana niemalejąco
  - założenia: —
  - idea:
    1. zbuduj kopiec w tablicy a
    2. Przeprowadź _SelectionSort_
  - czas: $O(n \log n)$
  - pamięć: —
  - dodatkowe info:
    - nie-stabilny
    - Tak naprawdę _SelectionSort_ na sterydach
  - Pseudokod:
    ```
    // Zbuduj kopiec
    for i in [n/2 ... 1]:
      DownHeap(i,n)

    // Właściwe sortowanie
    for i in [n..2]:
      a[1] :=: a[i] // Wynieś największy element w kopcu na koniec tablicy
      DownHeap(1,i-1)
    ```
  
### Merge
  - wejście: tablica $a$, indeksy $l$, $r$, $s$, niech $n = r-l+1$
  - wynik: niemalejąco posortowana tablica $a[l \dots r]$
  - założenia:
    - $1 \leq s < r \leq n$
    - $a[l \dots s]$ oraz $a[s+1 \dots r]$ są posortowane niemalejąco
  - idea:
  Porównuj najmniejsze nieprzetworzone elementy z obu posortowanych części i przepisuj mniejszy do tablicy pomocniczej. Na końcu przepisz tablicę pomocniczą do oryginalnej.
  - czas: $\Theta(n)$
  - pamięć: $n$ na tablicę pomocniczą $b$
  - dodatkowe info:
    - liczba porównań $\leq n-1$
    - liczba przypisań na tablicach $\leq 2*(n-1) + 1$
  - Pseudokod: \
    **Niezmiennik:** $b[l \dots k]$ zawiera $k-l+1$ najmniejszych elementów z $a[l \dots r]$, posortowanych.
    ```
    i := l
    j := s+1
    k := l-1
    
    while (i ≤ s) AND (j ≤ r):
      k++
      if a[i] ≤ a[j]:
        b[k] := a[i]
        i++
      else:
        b[k] := a[j]
        j++
    
    if i ≤ s:
      a[k+1..r] := a[i..s]
    
    a[l..k] := b[l..k]
    ```

## MergeSort
  - wejście: tablica $a[1 \dots n]$
  - wynik: tablica $a$ posortowana niemalejąco
  - założenia: —
  - idea: Posortuj rekurencyjnie dwie połówki i scal je przy użyciu _Merge_.
  - czas:
    - pesymistyczny: $\Theta(n \log n)$
  - pamięć: $n$ na tablicę pomocniczą + $\log n$ na rekursję
  - dodatkowe info:
    - stabilny
    - liczba porównań $\leq n \lfloor \log n \rfloor + 2n - 2^{\lfloor \log n \rfloor + 1} = \Theta(n \lfloor \log n \rfloor)$
    - sporo przypisań
    - PL: Sortowanie przez scalanie
  - Pseudokod:
    ```
    if l < r:
      s = (l+r) / 2
      MergeSort(l,s)
      MergeSort(s+1,r)
      Merge(l,r,s)
    ```

<!-- TODO Merge Sort w miejscu? -->

## QuickSort abstrakcyjnie
  - wejście: $S$ - skończony podzbiór uniwersum z liniowym porządkiem
  - wynik: Uporządkowany rosnąco ciąg elementów
  - założenia: —
  - idea: Wybierz pivota z $S$ i podziel $S$ na zbiór elementów mniejszych od pivota i zbiór elementów większych od pivota. Posortuj rekurencyjnie te dwa zbiory, a między nie wstaw pivota.
  - czas:
    - pesymistyczny: $\Theta(n^2)$
    - oczekiwany: $O(n \log n)$
  - pamięć: Od $\Theta(\log n)$ do $\Theta(n)$ na rekursję
  - dodatkowe info:
    - liczba porównań: $\sum_{e \in S} d(e)$ gdzie $d(e)$ to głębokość poddrzewa w korzeniu (pivocie) $e$ w drzewie obliczeń _QS. \
    $n \log n + O(n) \leq$ liczba porównań $\leq \Theta(n^2)$
    - PL: Sortowanie szybkie
  - Pseudokod:
    ```
    if |S| <= 1:
      output S
    else:
      x := Pivot(S)
      S1 = {x1 in S : x1 < x}
      S2 = {x2 in S : x2 > x}

      QuickSort(S1)
      output x
      QuickSort(S2)
    ```

### Partition
  - wejście: Tablica $a$ rozmiaru $n$, jej indeksy $l$ i $r$
  - wynik: Indeks podziałowy $j$ tablicy $a$ taki, że $a[l \dots j-1] \leq a[j] \leq a[j+1 \dots r]$ przy czym nowa wartość $a[j]$ to stara wartość $a[l]$
  - założenia: $a[n+1] = +\infty$
  - idea: Przechodź tablicę od dwóch końców i zamieniaj pierwsze napotkane elementy, które są w złej relacji z wartością dzieląca $a[l]$
  - czas: $O(r-l)$: liniowy
  - pamięć: —
  - dodatkowe info:
    - liczba porównań: $r-l+1$ lub $r-l+2$
    - liczba zamian $\leq$ liczba porównań
  - Pseudokod:
    ```
    v := a[l]
    i := l
    j := r+1

    do {
      do i++ while a[i] < v
      do j-- while a[j] > v
      
      if i < j:
        a[i] :=: a[j]
    } while i < j

    a[l] :=: a[j]
    return j
    ```

## QuickSort implementacja tablicowa
  - wejście: Tablica $a$ rozmiaru $n$
  - wynik: Uporządkowana tablica $a$
  - założenia: Niech $QS(l,r)$ to sortowanie tym algorytmem podtablicy $a[l \dots r]$. Wtedy sortowanie całej tablicy to po prostu $QS(1,n)$
  - idea: Wybierz pivota z $S$ i podziel $S$ na zbiór elementów mniejszych od pivota i zbiór elementów większych od pivota. Posortuj rekurencyjnie te dwa zbiory, a między nie wstaw pivota.
  - czas:
    - pesymistyczny: $\Theta(n^2)$
    - oczekiwany: $O(n \log n)$
  - pamięć: $\Theta(\log n)$ na rekursję ($\Theta(n)$ w prymitywnej wersji)
  - Dodatkowe info:
    - **Żeby uniknąć liniowej głębokości stosu należy zawsze schodzić do krótszego przedziału. Wtedy:**
    - prawie w miejscu
    - nie-stabliny
    - Można też starać się unikać czasu kwadratowego poprzez heurystykę wyboru elementu dzielącego w *Partition*: brać medianę podtablicy $a[l \dots r]$ jako element dzielący
  - Pseudokod: \
    **Wersja prymitywna:**
    ```
    QS(l,r)::
      if l < r:
        j := Partition(l,r)
        QS(l,j)
        QS(j+1,r)
    ```

    **Wersja z logarytmiczną głębokością stosu:**
    ```
    S := [(1,n)]

    do {
      (l,r) := S.Pop()
      
      while l < r:
        j := Partition(l,r)

        if r-j >= j-l:
          S.Push(j+1,r)
          r := j-1
        else:
          S.Push(l,j-1)
          l = j+1
    } until Empty(S)
    ```

## CountSort
  - wejście: Tablica $a$ rozmiaru $n$ o wartościach z przedziału $[0 \dots m-1]$
  - wynik: Posortowana tablica $a$
  - założenia: —
  - idea: Zliczanie wystąpień poszczególnych elementów w $a[1 \dots n]$
  - czas:
    - pesymistyczny: $\Theta(n+m)$ - liniowo dla $m = O(n)$
  - pamięć: $O(m)$
  - dodatkowe info:
    - stabilny
  - Pseudokod:
    ```
    // Zliczanie wystąpień poszczególnych elementów w a[1..n]
    for i in [0..m-1] do b[i] := 0
    for i in [1..n] do ++b[a[i]]

    // Dla każdej wartości pojawiającej się w a[1..n] wyznaczamy
    // ostatnią pozycję dla elementu o tej wartości w tablicy posortowanej
    for i in [1..m-1] do b[i] += b[i-1]

    // Właściwe sortowanie
    for i in [n..1]:
      last_encounter := &b[a[i]]
      t[*last_encounter] := a[i]
      *last_encounter--

    a := t
    ```

<!-- TODO Sortowanie kubełkowe -->

<!-- TODO ## Partition 3-way
  - wejście: Tablica $a[1..n]$, liczba $k$
  - wynik: $v \in a$ t. że $|\text{elementy }  a \text{ mniejsze od } v| < k$
  - założenia: $k \leq n$, $a[n+1] = +\infty$
  - idea: Wyznaczyć $v$ w czasie $O(\log n)$
  - czas:
    - pesymistyczny: TODO
    - amortyzowany: TODO
    - rzeczywisty: TODO
  - pamięć: TODO
  - dodatkowe info: TODO
  - Pseudokod: -->

# Szablony
## Algorytm
  - wejście: TODO
  - wynik: TODO
  - założenia: TODO
  - idea: TODO
  - czas:
    - pesymistyczny: TODO
    - amortyzowany: TODO
    - rzeczywisty: TODO
  - pamięć: TODO
  - dodatkowe info: TODO
  - Pseudokod:

# Randomowe fakty

## Algorytmiczne
Optymalna liczba porównań w algorytmie sortującym n elementów: $\lceil \log n! \rceil$ - bierze się z wysokości drzewa decyzyjnego. \
Sortowanie $k$ posortowanych ciągów sumarycznej długości $n$: $O(n \log k)$ \
Każdy algorytm sortujący przez porównania wykonuje średnio $\geq n \log n - 1.45n$ porównań \
Dla ciągu $a$ rozmiaru $n$ oczekiwana liczba inwersji wynosi $\Theta(n^2)$

## Matematyczne
$\log \sqrt n = \frac{1}{2} \log n$ \
$\sum_{i = 1}^{n} i^k = \Theta(n^{k+1})$