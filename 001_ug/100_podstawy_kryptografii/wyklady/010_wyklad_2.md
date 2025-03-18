# Szyfr doskonale bezpieczny
Przestrzeń **wiadomości M, kluczy K i kryptogramów C**
Funkcje szyfrowania i odszyfrowywania
- **Enc** : M × K → C , być **może niedeterministyczna**
- **Dec** : C × K → M, Dec(Enc(m, k), k) = m **deterministycznie**
- na pewno **m1 =/= m2 implikuje Enc(m1, k)̸ = Enc(m2, k)**
Rozkłady prawdopodobieństwa:
- P(m = m0), m0 ∈ M, P(k = k0), k0 ∈ K , **niezależne rozkłady**
System jest **doskonale bezpieczny**, jeśli
- P(m = m0) = P(m = m0|c = c0), c0 ∈ C
- tzn.: **po poznaniu kryptogramu wiedza na temat tekstu jawnego jest taka sama jak przedtem**
- inaczej, zdarzenia m = m0 oraz c = c0 są niezależne
problemik techniczny: P(c = c0) > 0

### Wniosek 1:
System jest doskonale bezpieczny wtt. gdy
- P(c = c0|m = m0) = P(c = c0)
W kryptografii asymetrycznej jest wprost przeciwnie

### Wniosek 2:
System jest doskonale bezpieczny wtt. gdy
- P(c = c0|m = m0) = P(c = c0|m = m1) dla m0, m1 ∈ M

### Wersja z grą:
- Ewa wybiera dwa teksty jawne: m0, m1
- Tadeusz losuje klucz k, losuje bit b ∈ {0, 1}, ogłasza Enc(mb, k)
- Ewa stara się odgadnąć bit b, wygrywa jeśli odgadnie
- **system jest doskonale bezpieczny wtt. gdy Ewa odnosi sukces z prawdopodobieństwem 1/2**

## Złożoność obliczeniowa
System **doskonale bezpieczny** (perfect security):
- **klucz** musi być co najmniej tak **długi jak tekst jawny** i użyty tylko jeden raz
- założenia zbyt ograniczające praktyczne zastosowania
**Bezpieczeństwo obliczeniowe** (computational security):
- system musi być **bezpieczny wobec obliczeń możliwych do**
**wykonania w rozsądnym czasie**
- bezpieczny z prawdopodobieństwem bliskim 1
- tzn. dopuszczamy możliwość złamania szyfru mało prawdopodobnym przypadkiem albo wskutek długich obliczeń
Założenia: złożoność szyfru mierzona jest parametrem n, przeciwnik działa w czasie wielomianowym (C · nc dla pewnych C i c)
- system jest bezpieczny jeśli prawdopodobieństwo złamania **jest mniejsze niż** $\frac{1}{c^n}$ dla dowolnego c