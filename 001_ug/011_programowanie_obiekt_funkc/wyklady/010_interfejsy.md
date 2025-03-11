# Interfejsy
**Interfejs** specyfikuje **co klasa musi implementować, jednak nie specyfikuje jak**. Interfejsy są podobne do klas. Nie posiadają zmiennych instancyjnych, a ich metody nie posiadają ciała. Klasa może implementować dowolną liczbę interfejsów oraz dowolna liczba klas może implementować jeden interfejs. Interfejs nie zakłada sposobu implementacji swoich metod.
```
access interface INazwa {
    typ zmiennaFinalna1 = wartosc;
    typ nazwaMetody1(lista_param);
}
```
Jeżeli **access** jest **public**, to interfejs jest dostępny publicznie i jego elementy są także niejawnie publiczne. Jeżeli **access** nie występuje, to interfejs jest dostępny tylko wewnątrz pakietu. Zmienne występujące w interfejsie są niejawnie **final** i **static**

## Implementacja
**Implementacja interfejsu** polega na dodaniu słowa kluczowego implements z nazwą interfejsu do nagłówka klasy oraz na dodaniu implementacji metod zadeklarowanych w interfejsie. 
```
access class Klasa implements interfejs [,interfejs]] {
    // ciało klasy
}
```
Tutaj **access** jest **public** lub brak. Jeżeli dwa implementowane interfejsy deklarują tę samą metodę, to ta sama metoda będzie używana przez klientów obu interfejsów. Implementacje metod interfejsu muszą być zadeklarowane jako **public**.

Interfejsów można używać jak typów, zamiast klas. Wówczas odpowiednia implementacja interfejsu zostanie wybrana w trakcie wykonania programu. Interfejsy mogą być także implementowane przez klasy abstrakcyjne.

## Zastosowanie interfejsów
Istnieje **wiele możliwych implementacji** idei stosu. Można implementować stosy o stałej wielkości lub zmiennej, wybierając wewnętrzną implementację w postaci: tablic, list, drzew binarnych, itd.
Wspólną cechą wszystkich takich stosów będzie to, że możemy przy pomocy metody **push(e)** dodawać element **e** na wierzchołek stosu, a za pomocą metody **pop()** zdejmować element ze stosu.

## Interfejsy zmienne i rozszerzanie
Istnieje możliwość **wykorzystania interfejsu do importowania stałych** do wszystkich klas implementujących interfejs. Wewnątrz interfejsu **stałym powinna zostać nadana odpowiednia wartosc**. Wszystkie stałe zaimportowane do klasy w taki sposób są niejawnie traktowane jak zmienne **final**.

Interfejs może rozszerzać inny interfejs.Składnia takiego rozszerzenia jest podobna do rozszerzania klas. Klasa implementująca interfejs musi implementować wszystkie metody tego interfejsu oraz wszystkie metody dziedziczone przez ten interfejs.