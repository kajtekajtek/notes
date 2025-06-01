# Mikrokontroler
**Mikrokontroler** (MCU) to jednouchwytowe komputerowe **urządzenie scalone** zawierające wszystkie podstawowe komponenty komputera – **CPU, pamięć programową i danych oraz programowalne układy wejścia/wyjścia** – zintegrowane na jednym chipie. 
Mikrokontrolery są projektowane do zastosowań *embedded* (wbudowanych), dzięki czemu w odróżnieniu od typowych mikroprocesorów (stosowanych w PC, wymagających osobnych układów pamięci i peryferiów) tworzą kompletne, niewielkie i ekonomiczne rozwiązanie sterujące urządzeniem. 
**Program (firmware)** mikrokontrolera jest przechowywany w nieulotnej pamięci na chipie, a niewielka wbudowana pamięć RAM służy do bieżącego przetwarzania danych. Taka integracja zmniejsza koszt i rozmiar systemów sterowania, umożliwiając powszechne wykorzystanie mikrokontrolerów w urządzeniach codziennego użytku.

Mikrokontrolery znajdują zastosowanie w *automatycznie sterowanych* urządzeniach i systemach – od elektroniki konsumenckiej (pralki, telewizory, zabawki, aparaty fotograficzne), przez motoryzację (sterowniki silnika, ABS), sprzęt medyczny (np. implanty), aż po urządzenia IoT i przemysłowe systemy sterowania. Wiele nowoczesnych MCU to układy *mixed-signal*, integrujące poza blokami cyfrowymi także elementy analogowe (np. przetworniki ADC, komparatory) umożliwiające bezpośrednie podłączenie czujników analogowych.

## CPU
**CPU (Central Processing Unit)** to centralna jednostka przetwarzająca mikrokontrolera. Odpowiada za **wykonywanie instrukcji programu i obliczeń arytmetyczno-logicznych, a także za kontrolę pracy pozostałych komponentów**. 
- CPU **pobiera kolejne instrukcje** z pamięci programu (ROM/Flash) i **przetwarza dane** znajdujące się w pamięci operacyjnej (RAM) oraz rejestrach. 
- Typowy CPU mikrokontrolera **zawiera jednostkę arytmetyczno-logiczną (ALU)** do operacji na danych binarnych, **zestaw rejestrów** roboczych oraz **układy sterujące** przepływem programu. 
- Architektura CPU mikrokontrolera bywa 8-, 16- lub 32-bitowa – oznacza to, że przetwarza on liczby o danej szerokości bitowej jednocześnie. Przykładowo 8-bitowy CPU operuje na bajtach, podczas gdy 32-bitowy może jednorazowo operować na liczbach 32-bitowych. 
- CPU mikrokontrolera działa zwykle z stosunkowo niską częstotliwością taktowania (kilka MHz do kilkudziesięciu czy kilkuset MHz) w porównaniu z procesorami w PC, co jednak wystarcza do wbudowanych zadań i zmniejsza pobór mocy.

## RAM
**RAM (Random Access Memory)** to ulotna pamięć operacyjna mikrokontrolera. Służy do **przechowywania zmiennych i danych w czasie wykonywania programu** – są tu umieszczane np. bieżące wyniki obliczeń, dane wejściowe/wyjściowe, stos funkcji itp.. 
Pamięć RAM cechuje się *swobodnym dostępem* o szybkim czasie odczytu/zapisu i może być wielokrotnie zapisywana w trakcie pracy programu. Zawartość RAM jest jednak **ulotna** – wszystkie dane są tracone po wyłączeniu zasilania. Wielkość RAM w mikrokontrolerze jest zwykle ograniczona (rzędu od kilkuset bajtów do kilkudziesięciu kilobajtów w typowych 8-bitowych MCU) i programista musi gospodarować nią oszczędnie.

W praktyce RAM mikrokontrolera podzielony jest na kilka segmentów: 
- segment **danych statycznych** (inicjalizowane zmienne globalne)
- segment **stosu** (używany do przechowywania adresów powrotu i zmiennych lokalnych funkcji)
- obszar **heap** (dla dynamicznie alokowanych danych, jeśli system/program tego używa). 

Dostęp do RAM odbywa się zazwyczaj poprzez architekturę *Harvarda* (oddzielną szynę danych) lub *von Neumanna* (wspólną szynę) – w wielu mikrokontrolerach (np. AVR, PIC) stosuje się architekturę Harvard, co oznacza oddzielenie magistrali pamięci danych od magistrali pamięci programu w celu przyspieszenia pracy CPU.

## ROM
**ROM (Read-Only Memory)** w kontekście mikrokontrolerów oznacza **nieulotną pamięć programu znajdującą się na chipie**. Współcześnie najczęściej jest to pamięć typu **Flash** (EEPROM flash), ewentualnie mask ROM w starszych/tańszych układach. 
- Pamięć ROM zawiera zapisany kod wykonywalny (**firmware**) oraz ewentualnie **stałe dane** wykorzystywane przez program. 
- Zawartość tej pamięci **nie ginie po odłączeniu zasilania** – dzięki temu mikrokontroler „pamięta” zaprogramowany algorytm nawet po wyłączeniu. 
- W normalnym trybie pracy zawartość ROM jest tylko **do odczytu dla CPU** (program nie może samowolnie nadpisać własnego kodu). 
- **Programowanie pamięci Flash** odbywa się za pomocą specjalnego programatora lub bootloadera, zazwyczaj przed umieszczeniem mikrokontrolera w urządzeniu lub podczas aktualizacji firmware.

Historycznie stosowano różne rodzaje pamięci programowej w mikrokontrolerach: OTP ROM (jednokrotnie programowalna), UV-EPROM (kasowalna ultrafioletem – miała okienko kwarcowe w obudowie) czy elektrycznie kasowalną EEPROM. Współczesne mikrokontrolery niemal zawsze używają pamięci Flash, która pozwala na wielokrotny elektryczny zapis/kasowanie i szybki odczyt. Pamięć programu bywa organizowana słowami o szerokości innej niż 8 bitów – np. w niektórych MCU jedna komórka Flash ma 16 bitów lub więcej (co często wynika z długości słów instrukcji danego procesora).

## EEPROM
**EEPROM (Electrically Erasable Programmable ROM)** to dodatkowa nieulotna pamięć danych, często występująca w mikrokontrolerach obok pamięci programu. Służy ona do **przechowywania niewielkiej ilości informacji, które muszą pozostać zachowane nawet po odcięciu zasilania** – np. ustawień kalibracyjnych, konfiguracji, liczników, wyników pomiarów itp. 
- EEPROM jest zorganizowana jako **oddzielna przestrzeń adresowa pamięci**, do której można zapisywać/odczytywać pojedyncze bajty podczas pracy programu. 
- Cechą EEPROM jest **możliwość elektrycznego kasowania i ponownego zapisu danych bez potrzeby specjalnego sprzętu** (w odróżnieniu od starszych UV-EPROM). 
- **Trwałość** komórek EEPROM jest ograniczona – typowo ok. 100 tysięcy cykli zapisu/kasowania danych, po którym komórki mogą ulec zużyciu. 
- Dostęp do EEPROM jest też **wolniejszy** niż do SRAM czy Flash, dlatego nie nadaje się ona do częstych zapisów dużych ilości danych w pętli programu.

W mikrokontrolerach EEPROM jest najczęściej wykorzystywana do sporadycznego zapisu ustawień użytkownika, stanów liczników, identyfikatorów itp. Mikrokontroler udostępnia specjalne rejestry lub procedury do zapisu/odczytu EEPROM (ponieważ CPU nie może bezpośrednio wykonywać instrukcji zapisu do pamięci programu w trakcie działania – wymagane jest angażowanie wewnętrznej logiki do zapisu Flash/EEPROM). Podczas programowania mikrokontrolera (np. poprzez programator) również istnieje możliwość odczytu/zapisu całej zawartości EEPROM, podobnie jak pamięci programu.

**Porównanie rodzajów pamięci mikrokontrolera:**

| Rodzaj pamięci         | Charakterystyka (ulotność, dostęp)                                                                                                             | Typowe zastosowanie                                                                                                               |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **RAM (SRAM)**         | Ulotna (traci zawartość po odłączeniu zasilania); bardzo szybki odczyt/zapis w czasie pracy programu                                           | Przechowywanie zmiennych podczas działania programu (dane tymczasowe), stos wywołań, bufory I/O                                   |
| **Programowa (Flash)** | Nieulotna (zachowuje dane bez zasilania); tylko do odczytu w trakcie pracy; zapis programatorem lub bootloaderem; umiarkowanie szybki odczyt   | Przechowywanie kodu programu (firmware) oraz stałych (konfiguracje, tablice) wykorzystywanych przez program                       |
| **EEPROM (dane)**      | Nieulotna; elektrycznie kasowalna/programowalna; ograniczona liczba zapisów (np. \~10<sup>5</sup> cykli); wolny zapis/odczyt (wymaga opóźnień) | Przechowywanie trwałych danych aplikacji: ustawień, kalibracji, liczników, które muszą przetrwać restart lub wyłączenie zasilania |

## Instrukcje
**Instrukcje** mikrokontrolera to elementarne rozkazy maszynowe, które **CPU** może wykonywać. Zestaw instrukcji (ISA – *Instruction Set Architecture*) określa, **jakie operacje potrafi wykonać dany procesor** – np. działania arytmetyczne na liczbach, operacje na bitach, załadowanie/zapis danych z/do pamięci, skoki warunkowe itp. 
- Mikrokontrolery często wykorzystują architekturę typu **RISC** (Reduced Instruction Set Computer), charakteryzującą się relatywnie niewielką liczbą prostych instrukcji o jednakowej długości słowa maszynowego. Dzięki temu wiele operacji wykonuje się w pojedynczym takcie zegara, co upraszcza sprzęt i przyspiesza działanie. 
- Przykładowo 8-bitowe mikrokontrolery AVR mają *zmodyfikowaną architekturę Harvard* i dysponują zestawem około 130 rozkazów, z których większość wykonuje się w 1 cyklu maszynowym. W architekturze Harvard rozdzielono magistrale pamięci programu i danych, co umożliwia jednoczesne pobieranie kolejnej instrukcji i odczyt/zapis danych w tym samym czasie – zwiększając efektywność przetwarzania. 
- Często słowo instrukcji ma inną szerokość niż standardowe 8 bitów – np. niektóre rodziny mikrokontrolerów PIC używają 12-bitowych lub 14-bitowych kodów instrukcji dla 8-bitowego CPU.

Mikrokontrolery są projektowane z myślą o sterowaniu urządzeniami, dlatego ich zestawy instrukcji zwykle zawierają udogodnienia do obsługi bitów i portów I/O. 
Powszechne są **instrukcje bitowe**, pozwalające np. sprawdzić i ustawić/skasować pojedynczy bit rejestru czy warunku – operacje tego typu mogą wykonać w jednym rozkazie to, co na procesorach ogólnego zastosowania wymagałoby kilku instrukcji. 
Większość mikrokontrolerów nie posiada sprzętowego wspomagania dla obliczeń zmiennoprzecinkowych (brak koprocesora arytmetycznego), choć nowsze 32-bitowe jednostki mogą mieć moduły DSP/FPU do szybszego przetwarzania sygnałów. 
W praktyce **programowanie mikrokontrolerów rzadko odbywa się bezpośrednio w asemblerze** – zamiast tego wykorzystuje się języki wyższego poziomu (np. C/C++), które za pomocą kompilatora przekładają kod na instrukcje maszynowe procesora. Mimo to rozumienie działania instrukcji (i architektury MCU) bywa istotne przy optymalizacji i debugowaniu programów w systemach wbudowanych.

## AVR
**AVR** to rodzina 8-bitowych mikrokontrolerów RISC opracowanych w latach 90. przez firmę Atmel (obecnie należących do Microchip Technology). 
Układy AVR wykorzystują **zmodyfikowaną architekturę Harvard** i były jednymi z pierwszych MCU wyposażonych w pamięć Flash do przechowywania programu zamiast jednokrotnie programowalnej pamięci OTP/EPROM. 
Procesory AVR **wykonują większość instrukcji w jednym cyklu**, co przekłada się na wysoką wydajność jak na 8-bitową architekturę. 
Rodzina AVR obejmuje m.in. serie: 
- **ATtiny** (układy o małej liczbie wyprowadzeń i ograniczonych zasobach)
- **ATmega** (bardziej rozbudowane mikrokontrolery o większej pamięci Flash/RAM i bogatszych peryferiach)
- nowsze **ATxmega** 
- 32-bitowe **AVR32**. 

Mikrokontrolery AVR zyskały ogromną popularność w hobbystycznych i edukacyjnych zastosowaniach embedded, m.in. dzięki wykorzystaniu w wielu otwartych platformach **Arduino**. Przykładowo **ATmega328P** (8-bitowy AVR z 32 KB Flash) jest mikrokontrolerem stanowiącym „serce” popularnej płytki Arduino Uno. Platforma Arduino udostępnia wygodne środowisko do programowania mikrokontrolerów AVR i to właśnie na bazie Arduino często prowadzi się dydaktykę systemów embedded.

## Microchip
**Microchip PIC** – rodzinę mikrokontrolerów PIC (*Peripheral Interface Controller*) – zapoczątkowano w latach 80. XX w. w firmie Microchip Technology (pierwotnie jako produkt firmy General Instrument).
- PIC to **jedne z najpopularniejszych 8-bitowych mikrokontrolerów** stosowanych w przemyśle i hobbystycznie, cenione za prostotę i niską cenę.
- Architektura klasycznych PIC jest Harvardzka i oparta na rdzeniu typu **accumulator** – posiada **pojedynczy główny rejestr roboczy** (akumulator W) i operuje na nim oraz niewielkiej liczbie rejestrów pamięci danych. 
- Zestaw rozkazów PIC jest zbliżony do RISC: składa się z niewielkiej liczby instrukcji o stałej długości słowa maszynowego, wykonywanych zazwyczaj w 2 cyklach zegara (lub 4 cyklach, zależnie od rodziny). 

Charakterystyczne dla PIC są różne długości słowa instrukcji w zależności od rodziny – najprostsze mają 12-bitowe instrukcje (PIC10/12), bardziej rozbudowane 14-bitowe (PIC16), a zaawansowane 8-bitowe PIC18 stosują 16-bitowe słowa rozkazów; 16-bitowe mikrokontrolery PIC24/dsPIC mają 24-bitowe instrukcje. Baseline i mid-range (niższe rodziny PIC) używają 8-bitowej magistrali danych i oferują tylko kilkadziesiąt bajtów do kilku kB RAM, podczas gdy high-end (PIC18) rozszerzono do 16-bitowej przestrzeni danych i większych pamięci. Microchip rozwinął również 32-bitowe mikrokontrolery **PIC32**, początkowo oparte o architekturę MIPS (seria PIC32MX/MZ), a także linię **PIC32C** wykorzystującą rdzenie ARM Cortex-M (współdzieloną z nabytą rodziną SAM z Atmela). 
Dzięki mnogości wariantów (od 6-pinowych miniaturowych MCU po 100-pinowe układy z USB, CAN itp.) rodzina PIC znajduje zastosowanie w niezliczonych aplikacjach – od prostych zabawek i modułów sensorowych, po motoryzację i zastosowania przemysłowe. W 2013 r. firma Microchip dostarczała już ponad miliard mikrokontrolerów PIC rocznie, co świadczy o ich popularności.

## Układy wejścia/wyjścia
Mikrokontroler posiada wbudowane **układy wejścia-wyjścia** (*peryferia*), pozwalające na interakcję z otoczeniem – pomiar sygnałów, sterowanie elementami wykonawczymi oraz komunikację z innymi układami. Do standardowych peryferiów należą m.in. programowalne **timery/liczniki**, przetworniki analogowo-cyfrowe **ADC**, interfejsy komunikacyjne **USART/UART**, linie **GPIO** (cyfrowe wejścia/wyjścia) i wiele innych specjalizowanych modułów.

### TIMER
**Timer/Counter** to **programowalny licznik sprzętowy, taktowany sygnałem zegarowym** (wewnętrznym lub zewnętrznym). 
- Jego podstawową funkcją jest **odliczanie upływu czasu lub zliczanie impulsów** – timer zwiększa (lub zmniejsza) swoją wartość w każdym kroku zegara, a po osiągnięciu określonej wartości może generować zdarzenie (np. **przerwanie** informujące CPU o przepełnieniu lub o osiągnięciu wartości porównania). 
- Timery pozwalają mikrokontrolerowi na realizację działań takich jak odmierzanie opóźnień czasowych, pomiar długości impulsów/częstotliwości sygnałów, generowanie sygnałów o zadanym przebiegu (np. **PWM** do sterowania jasnością LED czy położeniem serwomechanizmu) oraz zliczanie zdarzeń zewnętrznych (tryb licznika). 
- Typowy mikrokontroler posiada kilka niezależnych timerów – np. 8-bitowych oraz 16-bitowych – co umożliwia jednoczesne realizowanie różnych zadań. 
- Rozdzielczość timera (np. 8-bit = zliczanie 0–255) wpływa na maksymalny odliczany czas przy danej częstotliwości zegara; timery 16-bitowe mogą odmierzać dłuższe okresy lub wyższą rozdzielczość czasową niż 8-bitowe.

Aby elastycznie zarządzać zakresem odliczania, timery wyposażone są w **preskalery**, czyli dzielniki częstotliwości zegara. Preskaler pozwala spowolnić efektywne taktowanie licznika – np. preskaler = 64 spowoduje, że licznik zwiększa się co 64 takty bazowego zegara zamiast co każdy takt. Dzięki temu można generować dłuższe opóźnienia lub precyzyjnie dostroić częstotliwość generowanych sygnałów. 
Timer zazwyczaj posiada również rejestry porównania (ang. *compare registers*), za pomocą których można wygenerować zdarzenie (np. zmienić stan pinu wyjściowego lub wywołać przerwanie) w momencie, gdy licznik doliczy do zaprogramowanej wartości – mechanizm ten jest wykorzystywany przy generowaniu sygnałów PWM i precyzyjnych częstotliwości sygnałów wyjściowych. 
Podsumowując, timery/liczniki to uniwersalne peryferia do odmierzania czasu i zliczania zdarzeń, szeroko wykorzystywane we wszelkiego rodzaju aplikacjach mikroprocesorowych (od migania diodą co 1 sekundę, poprzez pomiar czasu trwania sygnału z czujnika ultradźwiękowego, aż po realizację protokołów komunikacyjnych wymagających precyzyjnego taktowania).

### ADC
**ADC (Analog-to-Digital Converter)** to przetwornik analogowo-cyfrowy – układ peryferyjny pozwalający na **pomiar analogowego sygnału (napięcia) i przekształcenie go na reprezentację cyfrową (liczbową)** zrozumiałą dla mikrokontrolera. 
- Przetwornik dokonuje okresowych *próbek* napięcia wejściowego i każdej próbce przypisuje najbliższą wartość dyskretną spośród ograniczonego zbioru poziomów – proces ten nazywa się **kwantyzacją** i wprowadza drobny błąd (błąd kwantyzacji), zależny od rozdzielczości ADC. 
- Rozdzielczość ADC określa, z ilu bitów składa się wynik pomiaru – np. typowy wbudowany ADC w  mikrokontrolerach AVR ma rozdzielczość **10-bit**, co oznacza $2^{10}=1024$ możliwych kodów wyjściowych (od 0 do 1023). Taka rozdzielczość przy zakresie napięcia wejściowego 0–5V daje **rozdzielczość napięciową** ok. 4,88 mV na jeden poziom (tzw. *LSB*, najmłodszy bit reprezentuje ok. 4,9 mV). Niektóre mikrokontrolery oferują 12-bitowe ADC (4096 poziomów) lub inne rozdzielczości – wyższa rozdzielczość pozwala mierzyć mniejsze zmiany sygnału, ale zazwyczaj kosztem szybkości konwersji.

Ważnym parametrem ADC jest także **częstotliwość (częstość) próbkowania**, czyli maksymalna liczba pomiarów analogowych jaką może wykonać w ciągu sekundy. Określa ona pasmo sygnałów, jakie możemy wiarygodnie przetwarzać (zgodnie z twierdzeniem Nyquista – częstotliwość próbkowania musi być co najmniej dwa razy większa od najwyższej częstotliwości składowej sygnału analogowego, aby uniknąć aliasingu). Wbudowane ADC w mikrokontrolerach mają typowe częstotliwości próbkowania rzędu kilkudziesięciu do kilkuset tysięcy próbek na sekundę, co jest wystarczające dla pomiarów wolnozmiennych (np. temperatury, oświetlenia, napięcia baterii itp.), ale niewystarczające do bezpośredniej akwizycji np. sygnału audio o wysokiej jakości.

Przetwornik ADC wymaga odniesienia do **napięcia referencyjnego** – jest to ustalony poziom napięcia odpowiadający najwyższemu kodowi cyfrowemu. Napięcie to może być podawane z zewnątrz lub generowane wewnętrznie (np. popularne wartości to **5V, 3.3V, 2.56V** lub inne). Wejście analogowe jest następnie mierzone w skali od 0 do Vref. Dla przykładu, przy Vref = 5V i 10-bit ADC: odczyt 0 oznacza \~0V na wejściu, odczyt 1023 oznacza napięcie \~5V, a wartość \~512 odpowiada \~2.5V.

Wykorzystanie ADC w mikrokontrolerze pozwala na podłączenie do niego różnego rodzaju **czujników analogowych** – np. termistora (czujnik temperatury analogowej), fotorezystora (czujnik światła), mikrofonu, potencjometru itp. Sygnał z takiego czujnika (np. napięcie zależne od temperatury) można w regularnych odstępach czasu próbkować i zamieniać na postać cyfrową do dalszej obróbki w programie (np. przeliczenie temperatury, podjęcie decyzji sterujących). Wiele mikrokontrolerów posiada *wielokanałowe* ADC – oznacza to, że jeden moduł ADC jest przełączany wewnętrznym multiplekserem między kilkunastoma pinami analogowymi, co umożliwia pomiar wielu różnych sygnałów (kolejno, nie jednocześnie). Po zakończeniu konwersji ADC zwykle ustawia flagę lub wywołuje przerwanie, informując CPU o gotowości wyniku do odczytu.

### USART
**USART (Universal Synchronous/Asynchronous Receiver/Transmitter)** to uniwersalny sprzętowy interfejs szeregowy służący do komunikacji danych między mikrokontrolerem a innymi układami. USART może pracować w trybie asynchronicznym (*UART*) lub synchronicznym, w zależności od potrzeb. 
- W **trybie asynchronicznym (UART)** transmisja danych odbywa się bit po bicie bez osobnego sygnału zegarowego – ustalony jest tylko *baud rate* (częstość bitów), a ramka danych zawiera bity synchronizujące początek i koniec bajtu. Każdy bajt wysyłany przez UART jest opakowany w jeden bit **startu** (logiczne *0* sygnalizujące początek ramki), następnie wysyłane jest 5–8 bitów danych (zwykle 8 bitów), opcjonalnie bit **parzystości** (do kontroli błędów), i na koniec 1 lub 2 bity **stopu** (logiczne *1* oznaczające koniec ramki). Taka struktura ramki pozwala odbiornikowi wykryć początek i koniec nadawanego bajtu bez wspólnego zegara – synchronizacja odbywa się na podstawie wykrycia bitu start. UART jest **asynchroniczny**, co upraszcza okablowanie (wymagane są tylko linia TX, linia RX oraz masa wspólna do dwukierunkowej komunikacji). Warunkiem poprawnej komunikacji jest jednak ustawienie tego samego baud rate po stronie nadajnika i odbiornika (np. standardowe prędkości to 9600, 115200 bit/s itp.).
- USART w trybie **synchronicznym** wykorzystuje dodatkowy sygnał zegarowy – jeden z urządzeń (master) generuje takt, a drugi (slave) korzysta z tego zegara do próbkowania danych. Tryb synchroniczny bywa użyteczny przy komunikacji pomiędzy mikrokontrolerami lub z peryferiami wymagającymi precyzyjnej synchronizacji (podobnie do interfejsu SPI, choć SPI jest osobnym, prostszym protokołem). W praktyce wiele mikrokontrolerów oferuje sprzęt UART, który może opcjonalnie pracować jako pełny USART (czyli z trybem synchronicznym).

Typowe zastosowanie UART/USART to komunikacja z komputerem PC lub innym systemem – np. klasyczny port szeregowy RS-232 (wymagany jest konwerter poziomów napięć, np. układ MAX232, ponieważ UART w mikrokontrolerze pracuje na logice TTL 0–5V lub 0–3.3V), komunikacja z modułami bezprzewodowymi (Bluetooth, WiFi – wiele z nich używa UART jako interfejsu komend AT), z odbiornikami GPS, układami GSM itp. USART może też służyć do wymiany danych między dwoma mikrokontrolerami. Sprzętowy moduł UART odciąża CPU – posiada bufor rejestrów nadawczych i odbiorczych (dane są wysyłane/odbierane w tle, a procesor może zostać przerwaniem powiadomiony o nadejściu danych). Dzięki temu komunikacja szeregowa może odbywać się *w tle* pracy programu.

### GPIO i inne
**GPIO (General Purpose Input/Output)** to uniwersalne **cyfrowe piny wejścia/wyjścia dostępne w mikrokontrolerze**.  Typowy MCU posiada od kilku do kilkudziesięciu pinów GPIO, zorganizowanych często w porty (np. Port A, Port B itp.), które programowo **można konfigurować indywidualnie jako wejście lub wyjście**. 
- Gdy pin GPIO jest skonfigurowany jako **wejście**, mikrokontroler może odczytywać stan logiczny sygnału z zewnątrz (np. stan przycisku, czujnika cyfrowego, odbiornika IR itp.). Wejścia mogą być wyposażone w wewnętrzne **rezystory podciągające** do dodatniego napięcia, aby zapewnić stabilny stan logiczny `1` przy braku sygnału (tzw. *pull-up*). 
- Gdy pin jest ustawiony jako **wyjście**, MCU może ustawiać na nim stan wysoki lub niski (logiczne `1`/`0`), służący do sterowania podłączonymi urządzeniami – diodami LED, buzzerami, tranzystorami mocy, silnikami (przez sterowniki) itp.. Wyjścia GPIO dostarczają ograniczony prąd (zwykle kilkanaście mA), dlatego bezpośrednio mogą zasilać tylko niewielkie elementy (LED z rezystorem, itp.), a do sterowania większymi obciążeniami stosuje się tranzystory lub drivery.

Poza podstawowymi interfejsami omówionymi wyżej, mikrokontrolery często zawierają również wiele **innych peryferiów** rozszerzających ich możliwości.  Poniżej wymieniono kilka przykładów:

* **SPI (Serial Peripheral Interface)** – synchroniczny interfejs szeregowy typu master-slave, wykorzystujący linie: zegara (SCLK), danych wyjściowych master (MOSI) i danych wyjściowych slave (MISO) oraz sygnały wyboru układu (SS). Umożliwia bardzo szybkie przesyłanie danych między mikrokontrolerem a urządzeniami peryferyjnymi takimi jak pamięci Flash, przetworniki DAC/ADC, czujniki itp. SPI nie wymaga adresowania urządzeń na magistrali (każdy slave ma osobny sygnał SS) i umożliwia pełny dupleks.
* **I²C (Inter-Integrated Circuit)** – dwuprzewodowa magistrala szeregowa (linie SDA – dane, SCL – zegar) typu multi-master, multi-slave. Wykorzystywana do komunikacji z różnymi podzespołami na krótkie odległości (np. czujniki temperatury, ekspandery I/O, wyświetlacze itp.). I2C używa adresowania urządzeń na wspólnej magistrali i protokołu ramek ze start/stop bitami – jest wolniejsza od SPI, ale wymaga tylko dwóch linii i pozwala podłączyć wiele urządzeń.
* **Watchdog timer** – wewnętrzny *pies stróżujący*, specjalny timer, który resetuje mikrokontroler, jeśli program przestanie prawidłowo pracować (np. zawiesi się w nieskończonej pętli). Program musi okresowo zerować (przeładowywać) licznik watchdog, co jest gwarancją, że system działa poprawnie. W przeciwnym razie, po upływie ustalonego czasu, watchdog spowoduje reset – to zabezpiecza urządzenie przed utknięciem w błędnym stanie.
* **Układy analogowe** – wiele MCU ma wbudowane *komparatory analogowe* (do porównywania dwóch napięć i generowania sygnału logicznego, gdy jedno jest wyższe) przydatne np. do wykrywania przekroczenia progu napięcia. Coraz częściej spotyka się także wbudowane **DAC** (Digital-to-Analog Converter), czyli przetworniki cyfrowo-analogowe, pozwalające generować analogowe napięcie wyjściowe (np. do sterowania głośnością audio, generowania przebiegów analogowych) – choć DAC występują głównie w wyższych i specjalizowanych modelach MCU.

Oprócz powyższych, bardziej zaawansowane mikrokontrolery mogą posiadać kontrolery komunikacji **USB**, interfejsy sieci **CAN**, multipleksowane przetworniki **DAC/ADC** wysokiej rozdzielczości, moduły kryptograficzne, kontrolery LCD, a nawet wbudowane transceivery radiowe – wybór peryferiów zależy od przeznaczenia danej rodziny MCU. Producent mikrokontrolera w dokumentacji dostarcza szczegółowy opis wszystkich bloków peryferyjnych oraz sposobu ich konfiguracji i użycia w aplikacji.

## Przerwania
**Przerwania (interrupts)** to mechanizm pozwalający mikrokontrolerowi reagować natychmiast na istotne zdarzenia, **przerywając** normalne wykonywanie programu. 
- Gdy wystąpi określone zdarzenie w systemie (np. nadejdzie sygnał na pin, upłynie czas w timerze lub pojawią się dane z interfejsu komunikacyjnego), odpowiedni **układ peryferyjny generuje sygnał przerwania do CPU**. Mikroprocesor kończy wtedy wykonywanie bieżącej instrukcji i automatycznie **zawiesza główny program**, po czym przechodzi do wykonania specjalnej procedury obsługi przerwania – **ISR** (Interrupt Service Routine). 
- ISR to krótka funkcja (napisana przez programistę) przypisana do danego źródła przerwania, która **wykonuje niezbędne czynności w reakcji na zdarzenie** (np. odczytuje otrzymany bajt danych, zmienia stan jakiegoś wyjścia, zwiększa licznik itp.). 
- Po zakończeniu ISR mikrokontroler **powraca do przerwanego miejsca** w głównym programie i kontynuuje jego wykonywanie od punktu, w którym został przerwany.

Źródła przerwań w mikrokontrolerze zależą od jego wyposażenia – najczęściej spotykane to: 
- *przerwania timerów* (np. przepełnienie licznika lub osiągnięcie wartości porównania)
- *przerwania zewnętrzne* od pinów (zmiana stanu logicznego na wybranym wejściu, np. naciśnięcie przycisku)
- *przerwanie od zakończenia konwersji ADC* (gotowość nowego wyniku pomiaru)
- *przerwanie od interfejsu komunikacyjnego* (odebrano nowy bajt przez UART/SPI/I2C)

Przerwania **mogą mieć przypisane priorytety oraz wektory (adresy) obsługi** – dzięki temu gdy wystąpi wiele różnych zdarzeń, każde zostanie obsłużone we właściwej kolejności przez odrębną procedurę. 
Mechanizm przerwań sprawia, że mikrokontroler może **realizować reakcję w niemal rzeczywistym czasie** – nie musi ciągle *pollingować* (sprawdzać w pętli) statusu urządzeń, tylko zajmuje się nimi wtedy, gdy tego wymagają, co jest bardziej efektywne i szybkie.

W kontekście energooszczędnej pracy, przerwania odgrywają kluczową rolę – mikrokontroler można wprowadzić w tryb **uśpienia** (wyłącza wtedy CPU i większość układów, redukując pobór mocy do mikroamperów), oczekując na zdarzenie. Gdy nastąpi ustalone zdarzenie (np. stan pinu zmieni się lub upłynie czas timera watchdog), wygenerowane przerwanie *wybudzi* procesor ze stanu uśpienia i natychmiast zostanie obsłużone. Pozwala to budować systemy zasilane bateryjnie, które przez większość czasu pozostają w uśpieniu, a aktywują się tylko w razie potrzeby (sterowane właśnie przerwaniami).

Przerwania, choć bardzo użyteczne, wprowadzają pewne wyzwania – przede wszystkim konieczność ochrony współdzielonych zasobów (dane, urządzenia) przed równoczesnym dostępem z kodu głównego i ISR (problem synchronizacji) oraz zapewnienie, że rutyny obsługi są krótkie i wydajne (długotrwałe przebywanie w ISR opóźnia obsługę innych przerwań i zatrzymuje główny program). Mimo to właściwe użycie przerwań jest fundamentem projektowania responsywnych i efektywnych systemów wbudowanych.