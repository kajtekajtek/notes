# MAC

## ✅ Integralność danych – MAC

- **MAC (Message Authentication Code)**:
  - Generuje się ze wspólnego klucza `k` i wiadomości `m`.
  - Funkcja: `t = MAC(k, m)`
  - Sprawdzenie: czy `t == MAC(k, m')`?
- **Protokół:**
  1. Alicja i Bolek ustalają klucz `k`.
  2. Alicja wysyła `m` i `t = MAC(k, m)`.
  3. Bolek sprawdza poprawność `t`.

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