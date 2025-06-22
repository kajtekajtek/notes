# Szyfr jednorazowy

## Klucz
- generowany losow ciąg znaków     
    - długości tekstu jawnego
    - każdy fragment używany tylko raz
    - znany wyłącznie nadawcy i odbiorcy

## Szyfrowanie
- `c = m ⊕ k`
    - gdzie `m, k, c ∈ {0, 1}^ℓ`, tzn. ciągi bitów długości ℓ
- inaczej: dla każdego i:
    - `Ci = (Mi + Ki) mod N`
    - gdzie N = rozmiar alfabetu

## Odszyfrowanie
- dla każdego i:
    - `Pi = (Ci - Ki) mod N`

## Kryptoanaliza
- Jeśli klucz jest naprawdę losowy, użyty tylko raz, i utrzymany w tajemnicy, szyfr jednorazowy oferuje niezłomną ochronę: **szyfrogram nie daje żadnej statystycznej informacji o tekście jawnym** (Shannon, 1949).