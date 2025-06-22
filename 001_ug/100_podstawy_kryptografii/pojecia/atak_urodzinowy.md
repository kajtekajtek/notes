# 🎂 Atak urodzinowy
- Celem ataku urodzinowego jest **znalezienie kolizji funkcji haszującej**.
- U jego podstaw leży paradoks dnia urodzin, który pozwala oczekiwać, że **kolizja zostanie znaleziona znacznie szybciej niż sugerowałby to rozmiar przeciwdziedziny funkcji haszującej**. Liczba potrzebnych do tego sprawdzeń rośnie bowiem proporcjonalnie do pierwiastka z liczby wszystkich możliwych wyników funkcji haszującej. 
- Dla funkcji generującej n-bitowe skróty, potrzebujemy `~√(2^n)` prób do znalezienia kolizji.
- **Przykład**: Algorytm haszujący *MD5* generuje 128-bitowe skróty. Daje nam to `2^128` różnych skrótów. Aby jednak trafić na dwa identyczne skróty z 50% prawdopodobieństwem, wystarczy wygenerować ok. `1,1774 ⋅ 2^64` skrótów. 
- Wniosek: funkcja skrótu powinna mieć co najmniej 160 bitów.