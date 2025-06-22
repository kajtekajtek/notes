# Podstawy kryptografii
## Działy
- **kryptografia**: nauka/sztuka szyfrowania ( i odszyfrowywania)
- **kryptoanaliza**: nauka/sztuka łamania szyfrów
- **kryptologia**: suma powyższych plus całościowe spojrzenie (właściwa nazwa przedmiotu)

## Cztery główne pojęcia

### Informacja
- tekst jawny – **wiadomość**
- tekst zaszyfrowany – **kryptogram**

### Uczestnik (entity)
- człowiek, komputer, urządzenie. . .
- Alicja, Bolek, Celina, Tadeusz, Pelagia, Wiktor (Alice, Bob, Cindy, Trent, Peggy, Victor)

### Przeciwnik
- Ewa, Mariola (Eve, Mallory)

### Klucz
znany **nie wszystkim**, **łatwo** zaszyfrować/odszyfrować z kluczem, **trudno** bez klucza

## Złożoność
parametr $n \rightarrow \infty$
- **liniowa**: n, żadna złożoność
- **wielomianowa**: np.: $n^2, n^3, n^{100}$
- **wykładnicza**: $2^n, n!, n^n$
- **ponadwielomianowa**, choć nie wykładnicza: $e^\sqrt{n}$
**Stała też się liczy**, np. n = 1024 bity i tylko ta wielkość nas
interesuje

## Założenia kryptografii
- przestrzeń tekstów jawnych **M**, kluczy **K** , kryptogramów **C**
    - algorytm generowania klucza $G: \rightarrow K$
    - algorytm szyfrowania $E: K \times M \rightarrow C$  (*czy jest deterministyczny?*)
    - algorytm odszyfrowywania $D: K \times C \rightarrow M$
- **zasada Kerckhoffsa** (1883):
    - przeciwnik zna szyfr (tzn. protokół/algorytmy)
    - przeciwnik ma duże zasoby obliczeniowe i duże umiejętności
    - przeciwnik NIE ZNA klucza
- dlaczego?
    - łatwiej utrzymać w tajemnicy klucz niż algorytm
    - nie da się opracować wielu (tajnych) algorytmów
- jedyny bezpieczny szyfr: **jednorazowy**
    - w zasadzie nie ma dowodów, że inne szyfry są bezpieczne

## Scenariusze ataków
- przeciwnik ma tylko tekst zaszyfrowany
- przeciwnik ma przykłady tekstów jawnych plus ich zaszyfrowane wersje
- przeciwnik może zaszyfrować żądaną wiadomość lub odszyfrować żądany tekst
- ataki pasywne vs. aktywne
- ilość: duża liczba tekstów lub par tekstów vs. pojedynczy tekst zaszyfrowany
- atak brutalny: przeszukiwanie całej przestrzeni kluczy K
    - aby zadziałał musi być metoda rozpoznania znalezienia klucza
    - przestrzeń kluczy musi być duża, np. > $2^{80}$ elementów

## Cele kryptografii
- **poufność** (tajność)
    - tylko uprawnieni uczestnicy mają dostęp do informacji, szyfrowanie, klucz
- **integralność danych**
    - dane są niezmienione (wykrycie zmiany, również/głównie celowej)
- **uwierzytelnianie**
    - w czasie rzeczywistym: identyfikacja uczestnika
    - odłożone w czasie: identyfikacja źródła dokumentu
- **niezaprzeczalność**
    - podpis: nie można się wyprzeć
    - niemożliwa w kryptografii klucza symetryczneg

## Kryptografia klasyczna vs. współczesna



# Kryptografia klasyczna
- tekst jawny $\rightarrow$ tekst zaszyfrowany $\rightarrow$ tekst jawny $M \rightarrow E_K M \rightarrow D_K E_K M$ (zawsze przekształcenie z kluczem)
- klasyczna kryptografia (do lat ’70): **ten sam klucz**
    - obie strony muszą wymienić klucz wspólny klucz
    - jak to zrobić?

## Szyfr Cezara
- **szyfrowanie**: y = x + k mod 26, x = 0, 1, . . . , 25
- **kryptoanaliza**: wypróbowanie 25 przesunięć. Jedna litera pary tekst jawny+zaszyfrowany wystarczy by odgadnac klucz.

## Szyfr  afiniczny
- **szyfrowanie**: y = ax + b mod 26
- **odszyfrowywanie**: x = ((y - b) / a) mod 26
- musi być określone dzielenie 1/a = a′ t.ż. a · a′ = 1 mod 26. Istnieje w.t.w. gdy **NWD(a, 26) = 1**
- dla klucza (13, 4) „input” i „alter” szyfrują się do „ERRER”
- **kryptoanaliza**: przestrzeń kluczy ma 312 elementów. Dwie litery tekstu jawnego+zaszyfrowanego często wystarczą, kilka par prawie na pewno

## Szyfr monoalfabetyczny
Szyfr, w którym jednej literze alfabetu tajnego odpowiada dokładnie jedna litera alfabetu jawnego.

## Szyfr podstawieniowy
Szyfr, w którym każdy znak tekstu jawnego zastępowany jest przez inny znak lub znaki szyfrogramu.

## Szyfr Vigenere’a
- **klucz**: wektor liczb nieznanej długości np. (k1, k2, . . . , kn)
- **szyfrowanie**: y1 = x1 + k1, y2 = x2 + k2, . . ., yn = xn + kn, 
- **odszyfrowywanie**: analogicznie
- **kryptoanaliza**: przeszukiwanie wyczerpujące jest nierealne, kluczy jest 26 · 26 · . . ., dla n = 9 jest ich 5·1012 
- para tekst jawny+zaszyfrowany, długości klucza, definiuje
klucz
- gdy znany jest tylko szyfrogram oraz długość klucza, to można przeprowadzić analizę częstotliwości dla fragmentów szyfrogramu, dla zestawów {y1, y10, y19, . . .} itd.
- analiza częstotliwości oznacza przybliżenie wektora częstotliwości wystąpień liter w szyfrogramie z częstotliwościami języka naturalnego

# Kryptografia nowoczesna
- współczesna kryptografia: **para kluczy** (kryptografia *asymetryczna*, PKC),
    - idea: Diffie, Hellman (1976)
    - implementacja: RSA (Rivest, Shamir, Adleman) (1977)
    - wada: słaba wydajność
    - zaleta: nie trzeba przedtem przekazywać klucza

## Kryptografia klucza asymetrycznego
### Przykład zastosowania
1. Alicja prosi Bolka o **przekazanie klucza publicznego** B, albo odczytuje z ogłoszenia, albo od wspólnego znajomego
2. Alicja **szyfruje wiadomość kluczem publicznym** Bolka
3. Alicja przekazuje wiadomość $E_B M$
4. Bolek **odszyfrowuje wiadomość swoim kluczem prywatnym** $D_B E_B M = M$
- **Nikt** nie przesyła tajnego klucza
- **problem**: czy to naprawdę Bolek przekazał klucz publiczny?

## Zasady nowoczesnej kryptografii
- Precyzyjne definicje
- Jawne założenia systemu
- Dowody poprawności

## Atak z wybranym tekstem jawnym
- Bezpieczeństwo przeciwko atakowi z kryptogramem
    - Ewa **nie jest w stanie zgadnąć, która wiadomość jest zaszyfrowana na podstawie znajomości kryptogramu**
- Bezpieczeństwo szyfrowania wielokrotnego
    - Ewa nie potrafi odgadnąć, który zestaw wiadomości jest szyfrowany
    - Twierdzenie: **szyfr bezpieczny przeciwko atakowi z wybranym tekstem jawnym musi być niedeterministyczny**
- Bezpieczeństwo przeciwko atakowi z wybranym tekstem jawnym – CPA
    - założenie: Ewa ma dostęp do maszyny szyfrującej (wyrocznia – daje kryptogram dowolnej wiadomości)
    - Ewa nie potrafi odgadnąć, która wiadomość jest zaszyfrowana