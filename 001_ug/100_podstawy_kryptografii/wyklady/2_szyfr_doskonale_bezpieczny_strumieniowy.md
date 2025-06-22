# Szyfr doskonale bezpieczny
Przestrzeń **wiadomości M, kluczy K i kryptogramów C**

Funkcje szyfrowania i odszyfrowywania:
- **Enc** : `M × K → C` , być **może niedeterministyczna**
- **Dec** : `C × K → M`, `Dec(Enc(m, k), k) = m` **deterministyczna**
- `m1 =/= m2 -> Enc(m1, k) =/= Enc(m2, k)`
- `P(m = m0), m0 ∈ M`, `P(k = k0), k0 ∈ K` to **niezależne rozkłady**
- System jest **doskonale bezpieczny**, jeśli `P(m = m0) = P(m = m0|c = c0), c0 ∈ C`
    - tzn.: **po poznaniu kryptogramu wiedza na temat tekstu jawnego jest taka sama jak przedtem**
    - inaczej, zdarzenia `m = m0` oraz `c = c0` są niezależne
- problemik techniczny: P(c = c0) > 0

### Wniosek 1:
System jest doskonale bezpieczny wtt. gdy
- `P(c = c0|m = m0) = P(c = c0)`
- W kryptografii asymetrycznej jest wprost przeciwnie

### Wniosek 2:
System jest doskonale bezpieczny wtt. gdy
- `P(c = c0|m = m0) = P(c = c0|m = m1)` dla `m0, m1 ∈ M`

### Wersja z grą:
- Ewa wybiera dwa teksty jawne: m0, m1
- Tadeusz losuje klucz k, losuje bit b ∈ {0, 1}, ogłasza Enc(mb, k)
- Ewa stara się odgadnąć bit b, wygrywa jeśli odgadnie
- **system jest doskonale bezpieczny wtt. gdy Ewa odnosi sukces z prawdopodobieństwem 1/2**

## Złożoność obliczeniowa

### System **doskonale bezpieczny** (perfect security)
- **klucz** musi być co najmniej tak **długi jak tekst jawny** i użyty tylko jeden raz
- założenia zbyt ograniczające praktyczne zastosowania

### Bezpieczeństwo obliczeniowe (computational security)
- system musi być **bezpieczny wobec obliczeń możliwych do**
**wykonania w rozsądnym czasie**
- bezpieczny z prawdopodobieństwem bliskim 1
    - tzn. dopuszczamy możliwość złamania szyfru mało prawdopodobnym przypadkiem albo wskutek długich obliczeń
- Założenia: złożoność szyfru mierzona jest parametrem n, przeciwnik działa w czasie wielomianowym (C · nc dla pewnych C i c)
- system jest bezpieczny jeśli prawdopodobieństwo złamania **jest mniejsze niż** $\frac{1}{c^n}$ dla dowolnego c
- Algorytm działa **w czasie wielomianowym (na wejściu x)**
    - wynik jest wyprodukowany po **p(|x|)** krokach, p – pewien wielomian
- **Algorytm probabilistyczny** działa w czasie wielomianowym jeśli dodatkowo odczytuje co najwyżej **p(|x|) losowych bitów**
    - oznaczenie **PPT**
    Obie klasy algorytmów są zamknięte na złożenia i inne operacje
    Funkcja f jest **zaniedbywalnie mała**
    - jeśli ∀p ∈ PPT . ∃N ∈ N. ∀n > N. f (n) < $\frac{1}{p(n)}$
    - np. 2−n, 2−√n, n− log n
    - Funkcje zaniedbywalnie małe są zamknięte na dodawanie i mnożenie przez wielomian

## Dwa rodzaje ataków
*Dec* : `K × C → M`
- **|K | <= |M| ≈ |C |**, dużo mniejsza przestrzeń kluczy

### Atak brutalny
- wypróbowanie każdego możliwego klucza
- Dec(K , c0) ⊆ M
- albo atak z parą ⟨m0, c0⟩ i wówczas znajdujemy Dec(k0, c0) = m0
- albo trzeba jakoś wiedzieć, że k0 jest kluczem
- prawdopodobieństwo znalezienia klucza = 1

### Zgadywanie
- testujemy tylko jeden klucz, Dec(k0, c0)
- prawdopodobieństwo znalezienia = $\frac{1}{|K|}$
Czyli przestrzeń klucza musi być ponadwielomianowa dla parametru szyfru

## Definicja bezpieczeństwa szyfru
**Doskonałe bezpieczeństwo**
1. Ewa wybiera dwa teksty jawne: m0, m1
2. Tadeusz losuje klucz k, losuje bit b ∈ {0, 1}, ogłasza Enc(k, mb)
3. Ewa stara się odgadnąć bit b, wygrywa jeśli odgadnie
4. system jest doskonale bezpieczny wtt. gdy Ewa odnosi sukces z prawdopodobieństwem $\frac{1}{2}$
**Bezpieczeństwo obliczeniowe** (atak tylko z kryptogramem)
- parametr n
- Ewa używa algorytmu PPT
- teksty jawne mają tę samą długość (wielomianową od n)
- klucz jest losowany dla tego parametru n
- system jest bezpieczny, jeśli prawdopodobieństwo sukcesu Ewy < $\frac{1}{2}$ + zaniedbywalnie mała

# Szyfr Strumieniowy

## Liczby losowe i  pseudolosowe
- **Liczby losowe** pochodzą z obserwacji zjawisk fizycznych/przyrodniczych.
- **Liczby pseudolosowe** generowane są przez _algorytm_ (tzw. generator) z pewnym ziarnem (seed).
- Ciąg pseudolosowy **wygląda** na losowy (trudny do przewidzenia), choć tak naprawdę jest w pełni zdeterminowany przez algorytm i klucz/ziarno.

### Cechy generatorów pseudolosowych
1. **Trudne do odróżnienia od losowego** – prawdopodobieństwo skutecznego rozróżnienia ciągu pseudolosowego od prawdziwego ciągu losowego przez efektywny (w sensie obliczeniowym) algorytm ma być _zaniedbywalnie małe_.
2. **Długość ciągów** – generator może wytwarzać ciągi o praktycznie dowolnej długości (o ile starczy mocy obliczeniowej).
3. **Kontrola przez klucz/ziarno** – przy znajomości klucza (ziarna) cały ciąg jest w pełni odtwarzalny.

## Przykładowe generatory pseudolosowe
- **Generator liniowy**: $x[n]=a⋅x[n−1]⊕b(\bmod k)$. Prosty, ale mało bezpieczny kryptograficznie.
- **Blum–Blum–Shub**: $x[n]=x[n−1]^2\bmod k$. Wolniejszy, ale zapewnia znacznie wyższy poziom bezpieczeństwa.

## Rejestry przesuwne (LFSR)
- **LFSR** (Linear Feedback Shift Register) to popularna konstrukcja sprzętowa/algorytmiczna do generacji ciągów bitowych.
- Polega na przesuwaniu bitów i wprowadzaniu nowego bitu obliczanego jako funkcja liniowa kilku poprzednich bitów.
- **Zalety**: prosta implementacja, duże szybkości generacji.
- **Wady**: w wersji czysto liniowej – niewystarczające bezpieczeństwo (łatwo odtworzyć klucz po przechwyceniu dostatecznej liczby bitów).

### Ulepszenia rejestrów przesuwnych
- **Generator redukujący**: łączy wyniki z kilku rejestrów, by wygenerować jeden bit wyjściowy (np. wybór bitu z innego rejestru).
- **Generator kombinacji**: stosuje nieliniową funkcję na bitach z kilku rejestrów.

## Szyfr strumieniowy – ogólna idea
- Zbliżony w założeniu do **szyfru jednorazowego (one-time pad)**, ale klucz jest krótszy.
- Generowanie klucza: **losowy długości n**
- **Szyfrowanie**: $Enc⁡(k,m)=G(k)⊕m$ 
- **Odszyfrowanie**: $Dec⁡(k,c)=G(k)⊕c$
- Bezpieczeństwo opiera się na jakości generatora G. Jeśli ciąg nie da się odróżnić od losowego, szyfr jest (w dużym uproszczeniu) bezpieczny.

### Przykłady w praktyce
- **RC4** – dawniej popularny, ale ma ograniczenia (ujawnienie wzorców w początkowych bitach).
- **Rejestry przesuwne** – proste rozwiązania często nie spełniają wymagań bezpieczeństwa; stosuje się więc rozbudowane funkcje nieliniowe.

## Szyfrowanie wielu wiadomości (wielokrotne użycie szyfru strumieniowego)
- Ważne jest, by **nigdy nie używać dwa razy tego samego strumienia** G(k) do szyfrowania różnych wiadomości. Prowadzi to do ujawnienia informacji o obu tekstach jawnych.
- Jeśli atakujący zna oba szyfrogramy zaszyfrowane tym samym strumieniem, to:
    $c0⊕c1=(m0⊕G(k))⊕(m1⊕G(k))=m0⊕m1$
    co ujawnia związek między tekstami jawnymi.
- Aby _uniknąć powtórnego użycia_ strumienia, stosuje się:
    1. **Tryb synchronizowany**: każda nowa sesja/wiadomość dostaje inny segment ciągu, a stan generatora jest zapamiętywany.
    2. **Tryb asynchroniczny**: wprowadza się **wektor inicjalizujący (IV)** i traktuje (k,IV)) łącznie jako ziarno; każdy IV musi być unikatowy.