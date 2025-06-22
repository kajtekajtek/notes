# 🔐 Standard SHA-1
- Opracowany przez NIST.
- Produkuje skrót 160-bitowy.
- Obecnie niezalecany – znaleziono kolizje.
- Standard określa funkcję kompresji, jest ona iterowana
  - `m = {m0, m1, m2, . . .}`, `X0` początkowa wartość rejestru, `Xj+1 = h(Xj , mj)`, `h(m)` jest równe ostatniej wartości rejestru
  - standard określa też początkową wartość rejestru oraz sposób wypełnienia ostatniego bloku: ostatnie 64 bity określają długość m, brakujące są uzupełnione zerami