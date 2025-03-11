# Dziedziczenie

## Podstawy
**Dziedziczenie** jest jedną z podstawowych cech OOP ponieważ umożliwia łatwe implementowanie **klasyfikacji hierarchicznych**. W OOP klasę dziedziczoną nazywamy **klasą nadrzędną (superclass)**, natomiast klasę dziedziczącą **klasą podrzędną (subclass)**. 
**Klasa podrzędna jest wyspecjalizowaną wersją klasy nadrzędnej.** Dziedziczy ona wszystkie zmienne instancyjne i metody zdefiniowane w klasie nadrzędnej oraz dodaje swoje specyficzne elementy.
```
class nazwaPodklasy extends nazwaNadklasy {
}
```
**W Java można dziedziczyć po jednej klasie**. Niektóre języki dopuszczają dziedziczenie wielokrotne. Klasa nie może być klasą nadrzędną dla samej siebie.

## Referencje do klas
**Zmienna referencyjna** do klasy nadrzędnej może **wskazywać na obiekt dowolnej klasy podrzędnej**.
Przykład: 
```
A obA = new A();
B obB = new B(); 
obA = obB;
```
Typ zmiennej referencyjnej wyznacza, które elementy wskazywanego obiektu będą dostępne.
W powyższym przykładzie zakładamy, że klasa **B** dziedziczy po klasie **A**. Zmienna referencyjna **obA**, wskazująca na obiekt klasy **A**, będzie miała dostęp tylko do tych elementów wskazywanego obiektu, które są dziedziczone z klasy **A**.

## Zmienna super
Zmienna **super** służy do **odwoływania się do elementów klasy będącej bezpośrednim poprzednikiem klasy obiektu, w którym występuje**. **super** może być używana na dwa sposoby:
- **Odwołanie do konstruktora klasy nadrzędnej** klasy rozpatrywanego obiektu: służy zwykle do inicjalizacji danych prywatnych klasy nadrzędnej. Odwołanie takie musi odbywać się w konstruktorze jako pierwsza instrukcja.
- **Odwołanie do zmiennej lub metody**: to zastosowanie jest podobne do użycia zmiennej this, z tym, że odwołuje się do klasy nadrzędnej. Stosuje się, gdy klasa podrzędna definiuje element o takiej samej nazwie jak klasa nadrzędna.
**Konstruktory zawsze są wywoływane w kolejności od klasy nadrzędnej do podrzędnej** nawet, gdy nie używamy odwołania do konstruktora przez **super**.

## Nadpisywanie metod
Jeżeli metoda w klasie podrzędnej **posiada tę samą nazwę i sygnaturę** co metoda w klasie nadrzędnej, wówczas mówimy, że metoda z klasy podrzędnej **nadpisuje** metodę klasy nadrzędnej.

Wywołanie nadpisanej metody z klasy podrzędnej zawsze spowoduje wykonanie kodu metody z klasy podrzędnej. **Wersja metody z klasy nadrzędnej będzie przesłonięta wersją z klasy podrzędnej, dostępną wciąż przez zmienną super.**

Z nadpisywaniem metod mamy do czynienia **tylko wtedy, gdy nazwy i sygnatury dwóch metod są identyczne**. Jeżeli metody mają takie same nazwy lecz różne sygnatury, to mamy do czynienia z **przeciążaniem metod**, omówionym już wcześniej.

## Klasy abstrakcyjne
Abstrakcja polega na niedopowiedzeniach. W programowaniu obiektowym dotyczy to metod. **Klasa abstrakcyjna powinna nadawać kształt (sygnaturę) wybranych metod w klasach potomnych lecz sama o niczym nie przesądzać** (np.: ToolsTest.java).
Metody takie mają następującą postać:
```
abstract typ nazwa(lista-parametrów);
```
Każda **klasa, która posiada chociaż jedną metodę abstrakcyjną, musi także być zadeklarowana jako abstrakcyjna** (**abstract** przed słowem class).
**Nie można tworzyć instancji klas abstrakcyjnych**, chociaż można deklarować zmienne referencyjne klas abstrakcyjnych i wskazywać nimi obiekty klas pochodnych.

## Słowo final
Słowo kluczowe final posiada trzy zastosowania:
- Niezmienne zmienne instancyjne czyli **stałe**
- **Metody nienadpisywalne**: metody posiadające słowo kluczowe **final** w nagłówku nie mogą być nadpisane w klasach pochodnych; są niezmienne w klasach pochodnych
- **Klasy nie dające się dziedziczyć**: klasy takie nie mogą być dziedziczone do klas potomnych; wszystkie metody takiej klasy niejawnie są zadeklarowane jako **final**; jak można się domyślać błędem jest deklarowanie klasy jako abstract i final
Kompilatory Javy często, dla wygenerowania efektywniejszego kodu, wpisują kod metody finalnej w miejsce jej wywołania. Oszczędza to czas potrzebny na wywołanie metody. Taki sposób kompilacji nazywamy **wczesnym wiązaniem**, tj. wiązaniem kodu metody z jej wywołaniem w trakcie kompilacji

## Klasa Object
**Object** jest specjalną klasą języka Java. Wszystkie klasy języka Java są jej podklasami. Oznacza to, że zmienna referencyjna typu **Object** może wskazywać na obiekt dowolnej klasy.
Klasa Object definiuje następujące metody:
- **Object clone()** tworzy obiekt taki sam, jak obiekt wywołujący
- **boolean equals(Object o)** sprawdza równość obiektów
wywołującego i o
- **void finalize()** wywoływana przed odzyskaniem pamięci obiektu przez zbieracz śmieci
- **Class getClass()** oddaje klasę obiektu wywołującego
- **int hashCode()** oddaje hash code obiektu
- **String toString()** oddaje napis opisujący obiekt wywołujący

## Dokumentacja klas
W skład SDK wchodzi program javadoc, służący do generowania
dokumentacji klasy na podstawie pliku źródłowego oraz
specjalnych znaczników:
- /** ..* /: komentarz będący jednocześnie dokumentacją komentowanego elementu
- **@autor**: autor klasy lub komentowanego elementu
- **{@link}**: link do dodatkowej informacji
- **@param**: parametry metody
- **@return**: opis wartości zwracanej przez metodę
- **@see**: link do tematu pokrewnego
- **@exception** wyjątki generowane przez metodę
- **@version**: wersja klas