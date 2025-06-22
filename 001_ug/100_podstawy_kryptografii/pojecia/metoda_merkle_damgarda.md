# 🧱 Metoda Merkle-Damgarda

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