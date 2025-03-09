# Typy
Java jest językiem **silnie typowanym** - każda zmienna i każde wyrażenie posiada typ i każdy typ jest ściśle zdefiniowany.
## Typy proste
- Typy **całkowite**: byte, short, int i long
    Brak typów całkowitych bez znaku
- Typy **rzeczywiste**: float i double
- Typ **znakowy**: char;
    Reprezentuje znaki. Nie jest tym samym co typ znakowy języków C i C++ (8-bitowe liczby). Java reprezenuje znaki zgodnie ze standardem Unicode
- Typ **logiczny**: boolean;

## Zakres zmiennych
- global
- local

## Konwersje i rzutowania typów

### Automatyczne przekształcenia typów
- Oba typy są zgodne
- Typ docelowy jest większy niż typ źródłow

### Rzutowania typów niezgodnych (większego na mniejszy)
`(typ-docelowy) wartość`
Reguły konwersji zawężającej:
- Konwersja typów całkowitych: `(byte) i` dla `i = 257` to 1 (257 modulo byte)
- Konwersja typów rzeczywistych na całkowite: wartość typu rzeczywistego **traci część dziesiętną** i następnie **otrzymana wartość całkowita jest przekształcana jak liczby całkowite**

### Promocja typów w wyrażeniach
Przykład:
```
byte a, b, c;
a = 40; b = 50; c = 100;
int i = a * b / c;
```
Wynik wyrażenia a * b to **int**. Czasem Java promuje zbyt wiele. Np. program:
```
byte b;
b = b * 2;
```
Spowoduje błąd: **przypisanie int do byte**. Poprawnie:
```
byte b;
b = (byte) (b * 2);
```

## Tablice 
W Java wszystkie tablice są **dynamicznie alokowane**. Tablice są **implementowane jako obiekty**. Posiadają specjalny atrybut **length** reprezentujący liczbę elementów, które tablica może przechowywać (*a nie ich aktualną liczbę*).

### Jednowymiarowe
- Deklaracja zmiennej typu tablicoweggo: `typ zmienna[];`
- Alokacja pamięci do przechowywania elementów tablicy: `zmienna = new typ[rozmiar];`
- Deklaracja i alokacja w jednej linii: `typ zmienna[] = new typ[rozmiar];`
- `typ zmienna[] = { wart1, wart2, wart3, ... }`

### Wielowymiarowe
```
int twoD[][] = new int[3][4];
int a[] = new int[3];
int[] a = new int[3];
int b[][] = new int[3][4];
int[][] b = new int[3][4];
```

## String
W językach programowania zwykle z tablicami wiążą się typy napisowe, które są implementowane jako tablice znaków. **Typ String w Java nie jest typem prostym lecz klasą**, której instancje (obiekty) dopiero implementują napisy. **Obiekty klasy String są niezmienne**, tj. raz utworzone nie mogą zmieniać swojej zawartości. Klasa **StringBuffer** pozwalająca na dokonywanie zmian w przechowywanych napisach bez ich kopiowania.
Obiekty klasy String posiadają metody (m.in.):
- `boolean equals(String o)`:  równość dwóch napisów
- `int length()`: długość napisu
- `char charAt(int i)`: znak na pozycji i

## Pointer
Java **nie posiada typów wskaźnikowych.**

# Klasy
- W OOP **klasy służą do definiowania nowych typów danych** o znacznie większej sile wyrazu niż typy tradycyjne (np. język C).
- Mając definicję klasy możemy tworzyć obiekty typu danej klasy. **Klasa pełni rolę wzorca** (schematu budowy) obiektu.
- Obiekty danej klasy nazywamy **instancjami klasy**.
- Klasy pozwalają na zastosowanie **hermetyzacji**.
    Osiąga się to przez definiowanie danych i metod operujących na danych. Zwykle **użytkownik nie ma bezpośredniego dostępu do danych obiektu**, natomiast ma do dyspozycji **metody dostępu do danych**. Klasa definiuje więc interfejs do danych swoich instancji (właściwie: zmiennych instancji).
```
class NazwaKlasy {
    typ zmienna1;)
    typ zmienna2;

    typ metoda1(parametry) {
        ...
    }

    typ metoda2(parametry) {
        ...
    }
}
```

## Konstruowanie obiektu
1. Deklaracja zmiennej: `NazwaKlasy zmiennaKlasy;`
2. Utworzenie obiektu: `zmiennaKlasy = new NazwaKlasy();`
Nazwa klasy wraz z parametrami wyznacza **konstruktor klasy**. Konstruktor to metoda o nazwie takiej jak klasa. Definiuje on co trzeba zrobić by utworzyć obiekt danej klasy. **Konstruktory nie posiadają typu wynikowego**, nawet void. Niejawnym typem wynikowym każdego konstruktora jest klasa, której obiekt konstruktor tworzy. Prócz **powołania obiektu**, zadaniem konstruktora jest jego **inicjalizacja**, tak by po utworzeniu był w pełni sprawnym obiektem.

## Słowo kluczowe this
Wewnątrz metody **this** oznacza obiekt, na rzecz którego wywołano metodę.
```
Box (double width) {
    this.width = width;
}
```

## Zbieracz śmieci
Operator **new** dynamicznie rezerwuje pamięć na tworzony obiekt. Można się zastanowić jak obiekty są niszczone a ich pamięć zwalniana. W niektórych językach obiekty zarezerwowane dynamicznie muszą być zwalniane ręcznie. W Java przyjęto inne rozwiązanie. **JVM** posiada mechanizm zwany **zbieraczem śmieci (ang.: garbage collection)**, który automatycznie zwalnia pamięć przydzieloną obiektom. Zbieracz śmieci **włącza się sam**, gdy jest co posprzątać. Nie ma jednej reguły jego włączania się. Różne JVM posiadają różne algorytmy zbierania śmieci, lecz mają jedną wspólną cechę: *programista nie musi pamiętać o zwalnianiu pamięci, jak i o samym zbieraczu śmieci*.

## Metoda finalize
Zbieracz śmieci zaraz przed zwolnieniem obiektu uruchamia metodę **finalize** zwalnianego obiektu. Metoda ta jest stosowana, gdy obiekt rezerwuje pewne nie-Javowe zasoby, które muszą być zwolnione w specjalny sposób. Na metodzie tej nie możemy opierać poprawności programu, ponieważ nie wiemy, kiedy zostanie wywołana przez zbieracz śmieci.
```
protected void finalize() {
    ...
}
```

## Przeciążanie metod
Można definiować wiele metod o tej samej nazwie w jednej klasie. Metody takie nazywamy **przeciążonymi**. Muszą one **różnić się typami lub liczbą argumentów**. Mogą także różnić się typami wynikowymi ale nie wystarcza to by metody były różne. Metody przeciążone wspierają **polimorfizm**.

## Przekazywanie parametrów
Sposób przekazywania parametrów do metody zależy od ich typu. **Parametry typów prostych zawsze są przekazywane przez**
**wartość, natomiast obiekty zawsze przez zmienną**.
- Przekazywanie przez **wartość**: przekazywane wartości nie ulegają trwałym zmianom
- Przekazywanie przez **zmienną**: przekazywane wartości ulegają trwałym zmianom

## Kontrola dostępu
Java pozwala na kontrolę dostępu na poziomie **pakietu, klasy i**
**komponentu klasy**. Słowa kluczowe:
- **public**: elementy są dostępne dla dowolnego innego kodu
- **private**: dla elementu klasy sprawia, że jest on dostępny tylko dla innych elementów tej samej klasy
- **protected**: ma zastosowanie w procesie dziedziczenia klas
Domyślną specyfikacją kontroli dostępu, tj. brak słowa kluczowego jest zasięg pakietowy.

## Elementy static
Zwykłe komponenty klasy są dostępne po utworzeniu obiektu. Istnieje jednak możliwość zdefiniowania elementów, do których nie musimy się odwoływać za pośrednictwem obiektów. Służy do tego słowo kluczowe **static**. Może być stosowane do:
- **Zmiennych instancji**: są one wówczas zmiennymi globalnymi wszystkich obiektów danej klasy. **Utworzenie obiektu danej klasy nie powoduje powstania instancji statycznej zmiennej**.
- **Metod**: podlegają one następującym restrykcjom:
    - Mogą wywoływać tylko inne metody statyczne
    - Mogą korzystać wyłącznie ze zmiennych statycznych
    - Nie mogą odwoływać się do zmiennych this i super
Blok static służy do inicjalizacji zmiennych statycznych. Będzie on wykonany tylko raz, gdy klasa jest po raz pierwszy załadowana

## Elementy final
Słowo kuczowe **final** służy do oznaczenia zmiennych, których wartość ma być niezmienna we wszystkich instancjach. Pełnią one **rolę stałych** i muszą być inicjalizowane przy deklaracji:
```
final int FILE_NEW = 1;
final int FILE_OPEN = 2;
final int FILE_SAVE = 3;
final int FILE_QUIT = 4;
```
Nie zajmują one miejsca w instancjach klasy. Przyjętą konwencją jest pisanie zmiennych **final** dużymi literami. **final** może również być zastosowane do metod

## Klasy wewnętrzne
Istnieje możliwość definiowania **klasy wewnątrz innej klasy**. Klasy takie nazywa się **klasami zagnieżdżonymi**. Zakres klasy wewnętrznej jest ograniczony klasą zewnętrzną, tj.:
> Jeżeli klasa **B** jest zdefiniowana wewnątrz klasy **A**, wówczas B jest znana wewnątrz **A**, natomiast nie jest poza **A**.

Klasa wewnętrzna **posiada dostęp** do wszystkich elementów klasy zewnętrznej (*nawet prywatnych*), natomiast klasa zewnętrzna **nie posiada dostępu** do elementów klasy wewnętrznej.
Istnieją dwa rodzaje klas wewnętrznych:
- **Statyczne**: zdefiniowane ze słowem kluczowym static. Nie mogą odwoływać się one do elementów klasy zewnętrznej wprost. Muszą zdefiniować obiekt klasy zewnętrznej i odwoływać się za jego pośrednictwem.
- **Niestatyczne**: najczęściej używane. Mają dostęp do wszystkich elementów klasy zewnętrznej tak jak jej metody niestatyczne

## Parametry linii komend
W Java istnieje możliwość przekazania parametrów wywołania programu do metody **main()**. Parametry te są przekazane do programu jako tablica elementów typu **String**. 
Następujący program wypisuje wszystkie argumenty, z którymi został wywołany:
```
class CommandLine {
    public static void main(String args[]) {
        for(int i = 0; i < args.length; i++)
            System.out.println(“arg[“ + i +“] =” + args[i]);
    }
}
```
Przykładowe wywołanie: `java CommandLine to tylko test`