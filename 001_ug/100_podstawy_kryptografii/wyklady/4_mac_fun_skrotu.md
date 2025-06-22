
# Integralność danych: MAC i funkcje skrótu 

## 🔐 Integralność a prywatność

- **Prywatność**: Ewa nie może odczytać wiadomości `m` z zaszyfrowanej postaci `c`.
- **Integralność**: Czy Ewa może złośliwie zmodyfikować `c` tak, aby zmienić treść `m`?

### Tryby szyfrowania:
- **Strumieniowy**: `c = m ⊕ G(k)` – zmiana bitu w `c` wpływa na ten sam bit w `m`.
- **Blokowy:**
  - **OFB / CTR**: podobne właściwości jak szyfr strumieniowy.
  - **ECB**: zmiana bitu wpływa na cały blok, możliwa zmiana kolejności bloków.
  - **CBC**: zmiana bitu w IV wpływa na pierwszy blok; nagłówki mogą być krytyczne.

---

## ✅ Integralność danych – MAC

- **MAC (Message Authentication Code)**:
  - Generuje się ze wspólnego klucza `k` i wiadomości `m`.
  - Funkcja: `t = MAC(k, m)`
  - Sprawdzenie: czy `t == MAC(k, m')`?
- **Protokół:**
  1. Alicja i Bolek ustalają klucz `k`.
  2. Alicja wysyła `m` i `t = MAC(k, m)`.
  3. Bolek sprawdza poprawność `t`.

---

## 🔁 Funkcje skrótu (Hash Functions)

- **Definicja**: Dowolna funkcja `h: [*] -> [n]`
  - **dziedzina**: ciąg bitów o dowolnej długości
  - **przeciwdziedzina**: ciąg bitów długości ustalonej i niedużej
- **Własności:**
  - Łatwe do obliczenia.
  - Trudne do odtworzenia wiadomości (`preimage resistance`).
  - Trudne do znalezienia dwóch wiadomości z tym samym skrótem (`collision resistance`).

---

## 📄 Zastosowania funkcji skrótu

### Nie kryptograficzne:
- **znajdowanie indeksów tablic** dla argumentów ze zbioru [∗] albo zbioru [N] dla dużego N (tablice mieszające)
- **wykrywanie przypadkowych błędów transmisji**: przesyłane
są wiadomość m oraz skrót h(m), odczytywane są m1 oraz h1, jeśli h(m1) =/= h1, to znaczy, że wystąpił błąd

### Kryptograficzne:
- wykrywanie celowych i złośliwych zmian dokumentów
- w szczególności zobowiązanie bitowe
- skrócenie wiadomości dla kryptografii asymetrycznej (podpis)

### Inne nazwy:
- hash, odcisk palca (fingerprint), message digest
- MAC (dla funkcji z hasłem)

---

## 🔐 Właściwości kryptograficzne funkcji skrótu

- **Łatwo obliczyć**
- **Jednokierunkowość**: trudność w odtworzeniu `m` z `h(m)`.
- **Słaba bezkolizyjność**: trudność w znalezieniu `m'` dla danego `m` z `h(m) = h(m')`.
- **Silna bezkolizyjność**: trudność w znalezieniu dwóch różnych `m, m'` z `h(m) = h(m')`.

---

## 🎂 Atak urodzinowy
- Celem ataku urodzinowego jest **znalezienie kolizji funkcji haszującej**.
- U jego podstaw leży paradoks dnia urodzin, który pozwala oczekiwać, że **kolizja zostanie znaleziona znacznie szybciej niż sugerowałby to rozmiar przeciwdziedziny funkcji haszującej**. Liczba potrzebnych do tego sprawdzeń rośnie bowiem proporcjonalnie do pierwiastka z liczby wszystkich możliwych wyników funkcji haszującej. 
- Dla funkcji generującej n-bitowe skróty, potrzebujemy `~√(2^n)` prób do znalezienia kolizji.
- **Przykład**: Algorytm haszujący *MD5* generuje 128-bitowe skróty. Daje nam to `2^128` różnych skrótów. Aby jednak trafić na dwa identyczne skróty z 50% prawdopodobieństwem, wystarczy wygenerować ok. `1,1774 ⋅ 2^64` skrótów. 
- Wniosek: funkcja skrótu powinna mieć co najmniej 160 bitów.

---

## 🧪 Model losowej wyroczni – atak egzystencjalny

- Zakładamy idealną funkcję skrótu `h`.
- Przeciwnik (Ewa) wygrywa, jeśli znajdzie `m'`, dla którego `MAC(k, m')` jest akceptowalny, mimo że `m'` nie było wcześniej przesyłane.

---

## 🔁 Funkcja pseudolosowa jako MAC

- Dana funkcja pseudolosowa: `F: [n] x [n] -> [n]`
- `MAC(k, m) = F(k, m)`
- **Weryfikacja**: porównanie wartości `MAC(k, m)` z oczekiwaną.
- Twierdzenie: jest to bezpieczny algorytm uwierzytelniania **dla ciągów ustalonej długości**
  - dla funkcji losowej wartości f (x) oraz f (y) są niezależne,
  - funkcja pseudolosowa jest PPT nieodróżnialna od losowej
  - więc znajomość wielu wartości nie pomaga w znalezieniu nowej
Problemem jest nadal funkcja MAC : [n] × [∗] → [∗] dla
ciągów dowolnej długości
– a w praktyce będziemy żądać by MAC : [n] × [∗] → [ℓ],
stała długoś
- Problem: rozciągnięcie działania na wiadomości o zmiennej długości.
  - `MAC: [n] x [*] -> [*]`

---

## 📏 MAC dla wiadomości o dowolnej długości

- Naiwna metoda: sumowanie MAC-ów dla bloków — nie działa, umożliwia manipulacje.
- **Rozwiązanie**: każdy blok zawiera:
  - numer bloku (uniemożliwia przestawienie)
  - długość pliku (np. liczbę bloków, uniemożliwia ucięcie)
  - liczbę jednorazową (uniemożliwia sklejanie wiadomości)
  - oraz fragment wiadomości
  - MAC jest zestawem: liczba jednorazowa i ciąg MAC bloków
- Rozwiązanie to jest całkowicie niepraktyczne
  - numer bloku i długość pliku zajmą co najmniej po 32 bity lub więcej
  - liczba jednorazowa nawet 64 bitowa może być niewystarczająca
  - bloku musiałby być wielkości znacznie większej niż 128 bitów
  - MAC byłby co najmniej dwa razy dłuższy niż sama wiadomość

---

## 🔄 CBC-MAC

- MAC działa jak szyfrowanie w trybie CBC, ale tylko ostatni blok jest wynikiem.
- Wektor IV i długość wiadomości muszą być zakodowane i znane.

---

## 🧱 Metoda Merkle-Damgarda

- **Dana funkcja**: `hs : [n + n] → [n]` (funkcja kompresji)
  - (może zależna od dodatkowego parametru s)
  - iteracja dla ciągów dowolnej długości: `H(x, ⟨y , Z ⟩) = H(hs (x, y ), Z)`
  - dla dowolnego ciągu bitów trzeba jeszcze uzupełnić ostatni, niepełny blok ciągu
  - na końcu blok kodujący długość pliku
  - wektor początkowy jest ustalony
- **Twierdzenie**: jeśli funkcja kompresji hs ma własność
bezkolizyjności, to funkcja H też ma taką własność
  - dw. gdyby dwie wiadomości miały ten sam skrót H
  - to albo będą się różnić wielkością (ostatni blok da kontrprzykład dla hs )
  - albo będą się różnić wcześniej, wcześniejszy blok da kontrprzykład dla hs 
- MAC w algorytmie Merkle-Damgarda
  - NMAC (nested MAC): dla klucza k dodatkowy blok na końcu hs (k, H(m))

---

## 🔐 Standard SHA-1

- Opracowany przez NIST.
- Produkuje skrót 160-bitowy.
- Obecnie niezalecany – znaleziono kolizje.
- Standard określa funkcję kompresji, jest ona iterowana
  - `m = {m0, m1, m2, . . .}`, `X0` początkowa wartość rejestru, `Xj+1 = h(Xj , mj)`, `h(m)` jest równe ostatniej wartości rejestru
  - standard określa też początkową wartość rejestru oraz sposób wypełnienia ostatniego bloku: ostatnie 64 bity określają długość m, brakujące są uzupełnione zerami

---

## 🔑 MD5

- Autor: Rivest
- Skrót 128 bitowy
  - 4 rejestry 32 bitowe
  - 64 rundy (4 cykle po 16)
  - w każdym cyklu inna funkcja nieliniowa z efektem lawinowym, przesunięcia bitów, dodawanie z bieżącymi danymi
- MD2, inna funkcja
  - bardzo wolna
  - ale chyba bezpieczniejsza
  - jest używana w protokole PEM, bezpiecznej poczty elektronicznej
- Wiele znanych kolizji.
- Obecnie niezalecany w zastosowaniach bezpieczeństwa.

---

## 🔬 Nowoczesne funkcje skrótu

- SHA-3: wykorzystuje tzw. **metodę gąbki** (sponge construction).
- Bezpieczniejsze od SHA-1 i MD5.
- Umożliwiają elastyczne długości wyjściowe.

---

## 🔐 Funkcja skrótu za pomocą szyfrowania
- Dana funkcja szyfrująca `E : [ℓ+n] → [n]`, n długość szyfrowanych bloków, ℓ długość klucza
  - można przerobić ją na funkcję skrótu na wiele sposobów:
    - h(k, m) = E (k, m) ⊕ m
    - E (k, m) ⊕ m ⊕ k
    - E (k, k ⊕ m) ⊕ m
    - ...
  - i dalej iterować użycie dla większej liczby bloków
  - jest to równoważne zastosowaniu szyfru symetrycznego w wersji blokowej i przyjęciu ostatniego bloku jako skrótu
- Możliwość ataku urodzinowego wyklucza szyfry o kluczu mniejszym niż np. 128 bitów
  - np. klasyczny DES

## Szyfrowanie za pomocą funkcji skrótu
Funkcja skrótu h pozwala wygenerować ciąg pseudolosowy
  - x0 musi być losowe i przesłane niezależnie jako IV
  - xj = 8 bitów z h(k, xj–1), k jest kluczem, jest użyte jako ciąg pseudolosowy
  - tzn. cj = mj ⊕ xj , ciąg xj jest dodawany do wiadomości w celu zaszyfrowania/odszyfrowania

## Szyfrowanie i uwierzytelnianie
- Dane dwa klucze, jak zapewnić poufność i integralność?
- przesłać Enc(k1, m) oraz MAC(k2, m)
  - ale MAC może ujawnić całą wiadomość
  - a praktycznie zawsze jest deterministyczny: ŹLE
- przesłać Enc(k1, m||MAC (k2, m))
  - szyfr nie musi być odporny na atak z wybranym kryptogramem
  - być może nawet da się odtworzyć cały tekst jawny: ŹLE
- **Prawidłowe rozwiązanie**: przesłać Enc(k1, m) oraz MAC(k2, Enc(k1, m))
  - uniemożliwia atak przez modyfikację kryptogramu
  - bezpieczeństwo takie same jak dla Enc
  - UWAGA: MAC i Enc mogą być funkcjami wzajemnie
  odwrotnymi (szyfry blokowe itp), klucze muszą być różne