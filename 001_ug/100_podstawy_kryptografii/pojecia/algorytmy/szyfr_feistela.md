# Szyfr Feistela

## Sieci Feistela
- Konstrukcja szyfru, w której blok (o długości 2n) dzielony jest na dwie części: **L** i **R** (po **n bitów**).
- Runda sieci Feistela: 
    - $F(k, \langle L, R \rangle) = \langle R, L \oplus f(k, R)\rangle$
    - gdzie f to dowolna funkcja (nie musi być bijekcją!).
- Główna zaleta: odwracalność – wystarczy zastosować tę samą funkcję F dwa razy, by uzyskać pierwotny blok (lub identyczną konstrukcję w odwrotnym porządku).

## Szyfr Feistela w praktyce
- Dany blok ($L_0, R_0$) przechodzi przez kolejne rundy:
    - $L_i = R_{i-1}, R_i = L_{i-1}\oplus f(k_i, R_{i-1})$
    - gdzie $k_i$ to klucze rundowe (zależne od klucza głównego).
- Po ostatniej rundzie można (lub nie) zamienić miejscami $L_n$ i $R_n$​ – zależy to od definicji szyfru.
- **Odszyfrowywanie** wygląda podobnie, ale używa kluczy w odwrotnej kolejności.

## Funkcja f
- Może być praktycznie dowolna, byle była dobrze mieszająca. 
- Jest to często miejsce, gdzie umieszcza się S-boksy, permutacje, rozszerzenia bitów itp. 
- Sieci Feistela są bardzo popularne m.in. w DES i wielu innych szyfrach.