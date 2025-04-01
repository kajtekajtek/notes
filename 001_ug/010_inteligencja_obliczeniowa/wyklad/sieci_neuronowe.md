# Sieci neuronowe
Sztuczne sieci neuronowe bazują na biologicznych odpowiednikach: **neuronach** i **mózgach**.
![Budowa neuronu](../img/budowa_neuronu.png)
1. Neuron otrzymuje dostatecznie **silny bodziec** na dendrytach.
2. Dochodzi do wytworzenia potencjału czynnościowego (polaryzacja błony neuronu)
3. Potencjał czynnościowy jest stały dla neuronu (nie może wytwarzać silniejszych potencjałów).
4. Impuls dociera do zakończeń aksonu.
5. **Sygnał elektryczny pobudza wydzielanie neuroprzekaźników w synapsie.** One wywołują **sygnał elektryczny w kolejnym neuronie.**

## Sztuczna sieć neuronowa
Sztuczna sieć neuronowa, w ujęciu matematyczno-informatycznym, to **graf skierowany, z wagami na krawędziach i o specyficznej warstwowej strukturze.** 
- **Warstwa wejściowa** (Input layer) zawiera neurony, które pobierają sygnały/bodźce/dane z zewnątrz.
- **Warstwy ukryte** (hidden layers) przetwarzają te sygnały.
- **Warstwa wyjściowa** (output layer) zwraca dane wyjściowe/wyniki.
![Podobienstwo](../img/podobienstwo.png)
1. Neuron **dostaje dane liczbowe** (imitacja sygnałów elektrycznych), **mnoży** przez wagi na krawędziach i **sumuje**.
2. Następnie suma przetwarzana jest przez tzw. **funkcję aktywacji** f(n)
3. Tak obliczona liczba jest **przekazywana** do kolejnej warstwy (propagowanie sygnału, forward propagation)
Potencjał czynnościowy neuronu biologicznego jest ograniczony przez pewien zakres. **Funkcja aktywacji** f(n) to **”ogranicznik”** dla modelu matematycznego. Jej wartości są z wąskiego zakresu, często [−1, 1] lub [0, 1].
![Funkcje aktywacji](../img/funkcje_aktywacji.png)

### Schemat działania
Sieci neuronowe w praktyce **same konstruują potrzebne użytkownikowi modele**, ponieważ automatycznie uczą się na podanych przez niego przykładach. 
1. użytkownik sieci gromadzi **reprezentatywne dane** 
2. uruchamia **algorytm uczenia**, który ma na celu wytworzenie w pamięci sieci potrzebnej struktury (modelu) 
3. wyuczona sieć realizuje wszystkie potrzebne funkcje związane z eksploatacją wytworzonego modelu

### Zalety sieci neuronowych
- Potrafią odpowiadać w warunkach informacji niepełnej
- Nie wymagają znajomości algorytmu rozwiązania zadania (automatyczne uczenie)
- Przetwarzają informację w sposób wysoce równoległy
- Potrafią generalizować (uogólniać na przypadki nieznane)
- Są odporne na częściowe uszkodzenia
- Potrafią realizować pamięć asocjacyjną (skojarzeniową – podobnie jak działa pamięć u ludzi) w przeciwieństwie do pamięci adresowanej (charakterystycznej dla klasycznych komputerów)
- Duża moc (nieliniowych charakter)

### Rodzaje sieci neuronowych
- perceptron - sieć z jednym neuronem
- klasyczna sieć jednokierunkowa (ta, której dotyczy ta definicja)
- sieć rekurencyjna
- sieć modularna

### Zastosowania
- Rozpoznawanie twarzy, obiektów (rozpoznawanie wzorców).
- Dane medyczne: stawianie diagnozy.
- Prognozowanie: giełda, sprzedaż.
- Aproksymacje funkcji.
- Rozpoznawanie pisma (OCR), mowy, gestów.
- Gry i rozwiązanie problemów (szachy).

## Uczenie sieci: algorytm wstecznej propagacji

### Gradient
Gradient to **pole wektorowe dla funkcji liczbowej.** W każdym punkcie dziedziny funkcji zaczepiamy strzałkę wskazującą, w którą stronę funkcja rośnie/maleje i jak szybko się to dzieje. Matematycznie można go rozumieć jako **zestaw pochodnych cząstkowych.**
- Przykład: dla funkcji $f(x, y, z)=2x-3y^2-sinz$ jest $\nabla f=[\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z}] = [2, -6y, -cosz$

### Funkcja straty
W przypadku sieci, funkcja f , którą chcemy zminimalizować (patrząc na jej gradient), to **funkcja błędu / straty** (ang. loss function). Zwykle wybiera się funkcję **MSE** (Mean Squared Error) lub **Cross Entropy**.
Funkcja MSE porównuje przewidywany output z prawdziwym outputem dla jednej próbki (te dwa wektory są jej argumentami).
- $MSE(output_{pred}, output_{real}) = \sum_i \frac{(output_{pred}^i - output_{real}^i)^2}{n}$

W trenowaniu sieci poprawiamy jednak wagi W w sieci. Należy zdefiniować więc funkcję straty następująco, z innym argumentem:
- $Loss_{input}(W)=MSE(ForwardProop_w(input), output_{real})$

dla pewnej próbki input.
W praktyce bierzemy też często większy zestaw próbek (tzw. batch, ale o tym później) i obliczamy średnią funkcję:
- $Loss_{batch}(W)=\sum_{input\in batch}\frac{MSE(ForwardProp_w(input), output_{real}}{|batch|}$

### Spadek (wzdłuż) gradientu
Jak szukać minimum dla funkcji straty? Trzeba poruszać się w kierunku minimum, patrząc na pochodne cząstkowe (czyli gradient funkcji). Służy do tego procedura zwana **spadkiem (wzdłuż) gradientu** (ang. **gradient descent**). Algorytm działa w krokach -iteracjach.

### Wsteczna propagacja
Wsteczna propagacja (ang. back propagation) to **sposób uczenia sieci**, który idzie **od warstwy wyjściowej, ”w lewo”, do warstwy wejściowej poprawiając wagi**. Poprawianie każdej z wagi następuje poprzez **spadek gradientu** dla niej.
Algorytm dąży do minimalizacji błędu popełnianego przez sieć (minimalizacja funkcji straty, loss function). Ogólny schemat:
1. Zainicjalizuj sieć z losowymi wagami (random **W** )
2. Wybierz próbkę (lub batch) danych ze zbioru treningowego. Oblicz wartości wyjściowe sieci dla próbki (dla **input** obliczamy $output_{pred}$ )
3. Oblicz błąd sieci (np. **MSE** porównujące $output_{pred}$ i $output_{real}$)
4. Popraw wagi W poprzez propagację wsteczną błędu (minimalizujemy **Loss(W)**)
5. Czy sieć nauczona? Czy upłynęło max epok?
	- TAK – KONIEC
	- NIE – wróć do punktu 2

## Uczenie sieci: konfiguracja, hiperparametry, ocenianie

### Współczynnik uczenia się 
(ang. **learning rate, gain**) to **hiperparametr** regulujący szybkość uczenia się, często oznaczany jako $\eta$ (eta). **Hiperparametr** to parametr regulujący cały proces uczenia się. Zwykłe parametry (np. wagi w SSN), podlegają zmianom podczas uczenia się.
Jeśli jest mały, to proces uczenia się jest wolny, ale stabilny. Jesli jest duży, to proces jest szybki, ale wykonuje duże ”kroki” i może przeoczyć dobre rozwiązanie.
Współczynnik uczenia się może być stały lub może być zmieniany w czasie uczenia (iteracje, epoki) wg jakiegoś wzoru. We wzorach często używane sa inne hiperparametry np. **decay** (zanik) d lub **momentum** (pęd). Przykładowy wzór na zmianę η pomiędzy (n + 1) a n iteracją (zwany: time-based schedule):
- $\eta_{n+1}=\frac{\eta_n}{1+d\cdot n}$

To jak będziemy manipulować współczynnikiem uczenia się oraz wzorem na poprawianie wag może prowadzić do zauważalnych zmian w wydajności i szybkości uczenia się sieci. Na przestrzeni lat powstało wiele optimizerów np.
- **SGD** (Stochastic Gradient Descent)
- **Adam**
- **RMSProp**

### Epoki
**Epoka** (ang. epoch, czytaj: ’ipok) to fragment procesu uczenia, w którym **przeszliśmy dokładnie jeden raz przez każdą próbkę ze zbioru treningowego ucząc się na niej**. Algorytm uczący ma zadaną pewną **liczbę epok** - hiperparametr mówiący, ile razy musimy przejść przez każdą próbkę w training set (ile razy powtórzyć pojedynczą epokę). Liczba epok musi być dopasowana do skomplikowania problemu i sieci. Może wynosić 10, 100 lub nawet 1000. Jeśli wielkość zbioru treningowego to **7000**, a liczba epok to **100**, to wówczas algorytmu wstecznej propagacji uruchomi się **700 000** razy.

### Batch
**Batch**, lub **partia**, to fragment epoki. To część procesu uczenia, w którym przeszliśmy przez **pewną liczbę próbek ze zbioru treningowego**, po czym aktualizujemy wagi w sieci neuronowej. **Wag w sieci neuronowej nie aktualizujemy po każdej próbce, tylko po każdym batchu**. Każda waga jest średnią z wag obliczonych z próbek batcha.
**Wielkość batcha** (ang. batch size) to kolejny hiperparametr, który silnie oddziałowuje na proces uczenia się.
- Duże batche powodują, że uczenie się jest wolniejsze, ale droga do celu jest prostsza.
- Dobór najlepszej wielkości batcha może wymagać kilku eksperymentów i porównywania wyników (np. na krzywej uczenia się).
- Typowe wielkości są potęgami dwójki (ze względu na architekturę komputera), czyli np.: 1, 2, 4, 8, 32, 64, 128, albo nawet wielkość całego zbioru treningowego.
- Wielu badaczy twierdzi, że małe batche (do 32) działają najefektywniej.

### Iteracje
Parametrem, który automatycznie powstaje po wybraniu wielkości batcha jest **liczba iteracji** wynosząca $\frac{\text{wielkość zbioru treningowego}}{\text{wielkość batcha}}$. Uwaga: gdy zbiór treningowy nie dzieli się równo na batche, można go zmniejszyć (dopasować) lub po prostu zaakceptować, że ostatni batch będzie mniejszy

### Zbiór walidacyjny
- **Zbiór treningowy** (ang. training set) - używany w procesie uczenia do poprawiania wag sieci.
- **Zbiór testowy** (ang. test set) - używany po zakończeniu procesu uczenia, do sprawdzenia dokładności sieci.
- **Zbiór walidacyjny** (ang. validation set) - zbiór do testowania w trakcie uczenia. Pomaga odpowiedzieć na pytanie: czy uczymy się dalej ze zbioru treningowego, czy już mamy dobrą wydajność i kończymy.

### Krzywa uczenia się
**Krzywa uczenia się** (ang. learning curve) - wykres przedstawiający jaka jest wydajność sieci neuronowej (oś Y) w czasie uczenia, liczbie epok (oś X). 
- Właściwie najczęściej mamy do czynienia z dwiema krzywymi na jednym wykresie: dla zbioru treningowego i zbioru walidacyjnego.
- Przez wydajność możemy rozumieć dokładność sieci jako klasyfikatora (performance, accuracy) lub odstępstwo wyników sieci od tych prawdziwych, funkcja straty (loss, optimization

![Learning curves](../img/learning_curves.png)

### Niedouczenie się
Gdy model sieci neuronowej jest zbyt prosty, nie uda jej się dobrze wyuczyć z danych. Mowa wówczas o niedouczeniu się (underfitting).

### Przeuczenie się
Sieć przeuczona zbyt dokładnie nauczyła się zbioru treningowego, co może spowodować, że w zbiorze walidacyjnym będzie popełniała więcej błędów.