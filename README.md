# Sortowania

### InsertionSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: -
  - idea: przesuwaj kolejne elementy najdalej "w lewo" jak to możliwe respektując uporządkowanie z lewym sąsiadem
  - czas:
    - pesymistyczny: $O(n^2)$
    - rzeczywisty: $\Theta(n + Inv(a))$
  - pamięć: -
  - dodatkowe info:
    - stabilny
    - liczba porównań: $n-1 + Inv(a)$
    - liczba przesunięć: **$Inv(a)$**
    - złożoność zależna od liczby inwersji
    - PL: "sortowanie przez wstawianie"
  - Pseudokod:
    ```
    for i in [2..n]:
      cur := a[i]
      j := i-1

      while cur < a[j]:
        a[j+1] := a[j]
        j--
    
      a[j+1] := cur
    ```

### BubbleSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: -
  - idea: Porównuj sąsiednie elementy i zamieniaj je miejscami, jeśli są w złej kolejności
  - czas:
    - pesymistyczny: $O(n^2)$
    - rzeczywisty: $\Theta(n^2)$
  - pamięć: -
  - dodatkowe info:
    - stabilny
    - liczba porównań: $\frac{n * (n-1)}{2}$
    - **liczba zamian: $Inv(a)$**
    - PL: "sortowanie bąbelkowe"
  - Pseudokod:
    ```
    for i in [n..2]:
      for j in [1..i-1]:
        if a[j] > a[j+1]:
          a[j] :=: a[j+1]
    ```

### SelectionSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: -
  - idea: W każdej iteracji znajdź najmniejszy element w nieposortowanej części tablicy i zamień go z pierwszym elementem tej części
  - czas:
    - pesymistyczny: $O(n^2)$
    - rzeczywisty: $\Theta(n^2)$
  - pamięć: -
  - dodatkowe info:
    - nie-stabilny
    - liczba porównań: $\frac{n*(n-1)}{2}$
    - **liczba zamian: $n-1$**
    - PL: "sortowanie przez wybieranie"
  - Pseudokod:
    ```
    for i in [n..2]: // a[i+1..n] zawiera posortowane n-i największych elementów
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

#### k-sortowanie / KSort
  - wejście: tablica $a[1 \dots n]$, liczba $k$, algorytm $sort_alg$ sortowania
  - wyjście: $k$-posortowana tablica $a$
  - założenia:
    - $k < n$
    - tablica $a$ jest $k$-posortowana, jeśli $\forall _{i \in [1 \dots n-k]} a[i] \leq a[i+k]$
  - idea:
      Niezależnie posortuj $k$ podciągów tablicy $a$ algorytmem $sort_alg$: \
        $a[1, 1+k, 1+2k, \dots]$ \
        $a[2, 2+k, 2+2k, \dots]$ \
        ... \
        $a[k, 2k, 3k, \dots]$
  - czas:
    - zależy od $sort_alg$
  - pamięć: -
  - dodatkowe info:
    - Na wykładzie wykorzystywane tylko do Jeśli na $k$-posortowanej tablicy wykonamy $h$-sortowanie, to pozostanie ona nadal $k$-posortowana

### ShellSort
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
    - pesymistyczny: Pratt 1971: $O(nlog^2n)$ dzięki ciągowi skoków postaci $2^p3^q$: $1,2,3,4,6,8,9, \dots$
  - pamięć: -
  - dodatkowe info:
    - Algorytm Pratta:
      - długość ciągu skoków: $O(log^2n)
      - liczba inwersji w ciągu jednocześnie 2- i 3-posortowanym jest mniejsza od $n/2$
    - PL: "Metoda Shella"
  - Pseudokod:
    ```
    for i in [k..1]:
      h[i]-sortowanie metodą sortowania przez wstawianie
    ```

### Heap
  - operacje:
    - DownHeap
    - UpHeap
  - dodatkowe info: \
    warunek kopca: $heap(l,r) :: \forall _{l \leq i \leq r} lheap(i,r) \land rheap(i,r)$ \
    $lheap(i,r) :: 2i \leq r \Rightarrow a[i] \geq a[2i]$ - lewe poddrzewo zawiera elementy mniejsze \
    $rheap(i,r) :: 2i + 1 \leq r \Rightarrow a[i] \geq a[2i + 1]$ - prawe poddrzewo zawiera elementy większe
#### Heap.DownHeap
  - wynik: $heap(l,r)$
  - założenia: $heap(l+1,r)$
  - idea: opuszczaj element $a[r]$ w dół kopca, zamieniając go z większym z dzieci, dopóki nie zostanie spełniony warunek kopca
  - czas: $O(log\frac{r}{l})$
  - pamięć: -
    
#### Heap.UpHeap
  - wynik: $heap(l,r)$
  - założenia: $heap(l,r-1)$
  - idea: Wynoś element $a[l]$ w górę kopca, zamieniając go z rodzicem, dopóki nie zostanie spełniony warunek kopca
  - czas: $O(log\frac{r}{l})$
  - pamięć: -

### HeapSort
  - wejście: tablica $a[1 \dots n]$
  - wynik: tablica $a$ posortowana niemalejąco
  - założenia: -
  - idea:
    1. zbuduj kopiec w tablicy a
    2. 
  - czas: $O(nlogn)$
  - pamięć: -
  - dodatkowe info:
    - nie-stabilny
    - Tak naprawdę SelectionSort na sterydach
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
  
#### Merge
  - wejście: tablica $a$, liczby $l$, $r$, $s$
  - wynik: niemalejąco posortowana tablica $a$
  - założenia:
    - $1 \leq s < r \leq n$
    - $a[l \dots s]$ oraz $a[s+1 \dots r]$ są posortowane niemalejąco
  - idea: TODO 
  - czas:
    - pesymistyczny: TODO
    - amortyzowany: TODO
    - rzeczywisty: TODO
  - pamięć: TODO
  - dodatkowe info: TODO
  - Pseudokod:

### MergeSort
  - wejście: tablica $a[1 \dots n]$
  - wynik: tablica $a$ posortowana niemalejąco
  - założenia: TODO
  - idea: TODO
  - czas:
    - pesymistyczny: TODO
    - amortyzowany: TODO
    - rzeczywisty: TODO
  - pamięć: TODO
  - dodatkowe info: TODO
  - Pseudokod:

Algorytm - szablon
### Nazwa
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
