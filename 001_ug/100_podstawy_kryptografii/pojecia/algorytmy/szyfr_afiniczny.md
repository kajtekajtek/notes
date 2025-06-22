# Szyfr Afiniczny

## Szyfrowanie
- `y = ax + b mod m`

## Odszyfrowywanie
- `x = (y - b) / a mod m`
- musi być określone dzielenie `1/a = a'` takie, że `a * a' = 1`
- jedno rozwiązanie istnieje wtedy i tylko wtedy gdy NWD(a, m) = 1

## Kryptoanaliza
- przestrzeń kluczy ma 312 elementów
- dwie litery tekstu jawnego i zaszyfrowanego często wystarczą; kilka par prawie napewno