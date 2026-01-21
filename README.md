Algorytm - szablon
Nazwa
  - wejście: TODO
  - wyjście: TODO
  - założenia: TODO
  - idea: TODO
  - czas:
    - pesymistyczny: TODO
    - amortyzowany: TODO
    - rzeczywisty: TODO
  - pamięć: TODO
  - dodatkowe info: TODO
  - Pseudokod:

Struktura danych - szablon
Nazwa
  - operacje: TODO
  - wykorzystania: TODO

# Sortowania

InsertionSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: -
  - idea: przesuwaj kolejne elementy najdalej "w lewo" jak to możliwe respektując uporządkowanie z lewym sąsiadem
  - czas:
    - pesymistyczny: $O(n^2)$
    - amortyzowany: -
    - rzeczywisty: $\Theta(n + Inv(a))$
  - pamięć: -
  - dodatkowe info:
    - stabilny
    - liczba porównań: $n-1 + Inv(a)$
    - liczba przesunięć: $Inv(a)$
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

BubbleSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: -
  - idea: Porównuj sąsiednie elementy i zamieniaj je miejscami, jeśli są w złej kolejności
  - czas:
    - pesymistyczny: $O(n^2)$
    - amortyzowany: -
    - rzeczywisty: $\Theta(n^2)$
  - pamięć: -
  - dodatkowe info:
    - stabilny
    - liczba porównań: $\frac{n * (n-1)}{2}$
    - liczba zamian: $Inv(a)$
    - PL: "sortowanie bąbelkowe"
  - Pseudokod:
    ```
    for i in [n..2]:
      for j in [1..i-1]:
        if a[j] > a[j+1]:
          a[j] :=: a[j+1]
    ```

SelectionSort
  - wejście: tablica $a[1 \dots n]$
  - wyjście: tablica $a$ posortowana niemalejąco
  - założenia: -
  - idea: W każdej iteracji znajdź najmniejszy element w nieposortowanej części tablicy i zamień go z pierwszym elementem tej części
  - czas:
    - pesymistyczny: $O(n^2)$
    - amortyzowany: -
    - rzeczywisty: $\Theta(n^2)$
  - pamięć: -
  - dodatkowe info:
    - nie-stabilny
    - liczba porównań: $\frac{n*(n-1)}{2}$
    - liczba zamian: $n-1$
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

k-sortowanie
  - wejście: tablica $a[1 \dots n]$, liczba $k$
  - wyjście: $k$-posortowana tablica $a$
  - założenia:
    - $k < n$
    - tablica $a$ jest $k$-posortowana, jeśli $\forall _{i \in [1 \dots n-k]} a[i] \leq a[i+k]$
  - idea:
      Niezależnie posortuj $k$ podciągów tablicy $a$: \
        $a[1, 1+k, 1+2k, \dots]$ \
        $a[2, 2+k, 2+2k, \dots]$ \
        ... \
        $a[k, 2k, 3k, \dots]$
  - czas:
    - pesymistyczny: TODO
    - amortyzowany: TODO
    - rzeczywisty: TODO
  - pamięć: TODO
  - dodatkowe info: Jeśli na $k$-posortowanej tablicy wykonamy $h$-sortowanie, to pozostanie ona nadal $k$-posortowana
  - Pseudokod:

Struktura danych - szablon
Nazwa
  - operacje: TODO
  - wykorzystania: TODO
