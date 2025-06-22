# Funkcje skrótu

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