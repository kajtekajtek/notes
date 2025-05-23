# Tranzystor
**Tranzystor** - układ aktywny mogący **wzmacniać sygnał** elektryczny.
- wymaga **dodatkowego źródła zasilania** ($U_{cc}$)
- **Przełącznik**
- Model Ebersa-Molla
- Model małosygnałowy

## Rodzaje tranzystorów
- **Bipolarne**
	- npn
	- pnp
- **Polowe** (FET)
	- MOSFET
	- NMOS
	- PMOS
	- ...

## Wyprowadzenia

### Tranzystory bipolarne
- B - **baza**
- E - **emiter**
- C - **kolektor**

![Tranzystor NPN i PNP](../img/npn_pnp_transistors.png)

### Tranzystory unipolarne (polowe)
- S - **źródło**
- D - **dren**
- G - **bramka**

# Tranzystor Bipolarny
Struktura półprzewodnikowa złożona z dwóch złącz p-n.
![Tranzystor bipolarny](../img/bipolar_transistor.jpg)

## Zasada działania
Przy odpowiedniej polaryzacji złącz **BE**, **CE** i **CB** prąd **kolektora** ($I_C$) jest **proporcjonalny** do prądu **bazy** ($I_B$).
- $I_C=\beta\cdot I_B$
- $\beta \sim 100A/A$

**Niewielki prąd** płynący pomiędzy **bazą i emiterem** **steruje większym prądem** płynącym między **kolektorem i emiterem.**
W przypadku tranzystorów polowych, napięcie przyłożone do bramki zmienia przewodnictwo kanału, wpływając w ten sposób na płynący prąd.
## Złącza
![Tranzystor złącza](../img/zlacza.png)

## Model małosygnałowy
![Model małosygnałowy](../img/model_malosygnalowy.png)

## Tranzystor jako przełącznik
![Tranzystor jako przełącznik](../img/transistor_as_switch.png)

## Polaryzacja tranzystora npn
![Polaryzacja tranzystora npn](../img/transistor_polarity.png)

## Obszary pracy tranzystora
- Odcięcie
- Obszar aktywny
- Nasycenie

### Obszar aktywny
Tranzystor działa jak **wzmacniacz**. $I_C=\beta \cdot I_B$
- **Złącze B-E**
	- kierunek przewodzenia
	- $U_{BE} = 0.6V$
- **Złącze B-C**
	- kierunek zaporowy
- Prąd C jest proporcjonalny do prądu B
- Wzmacniacze liniowe

### Odcięcie
Tranzystor jest całkowicie **wyłączony**. (przełącznik)
- $U_{BE}=0V$
- $I_B=0$
- $I_C=0$
- $U_{CE}=U_{CC}$

### Nasycenie
Tranzystor jest w pełni **włączony**. (przełącznik)
- $U_{BE}=0.6V$
- $I_B = \text{odp. duży}$
- $I_C = \text{max, niezależny od }I_B$
- $U_{CE} \sim 0$

## Zależności prądowe (obszar aktywny)
- $I_E=I_C + I_B$
- $I_C = \beta\cdot I_B$
- $I_E = \alpha\cdot I_C$
- $\beta > 100$, $\alpha \sim 1$

![Zależności prądowe](../img/transfer_characteristics_transistor.png)
$V_O=V_C$, $V_{i} \sim V_B$

## Ograniczenia
W praktyce parametry tranzystora zależą między innymi od temperatury.

## Podstawowy układ pracy
Tranzystor bipolarny npn, obszar aktywny, DC.
![Podstawowy układ pracy](../img/uklad_pracy.png)
- $U_{in} = U_{RB} + U_{BE} \text{, } U_{RB}=I_B \cdot R_B \text{, } U_{BE} = 0.6V$
- $U_{CC}=U_{RC}+U_{CE} \text{, } U_{RC}=I_C\cdot R_C$
- $I_C=\beta\cdot I_B$
- $U_{out} = U_{CC} - I_C \cdot R_C$
- $I_C = \beta\cdot I_B$
- $I_B = \frac{U_{in} - 0.6}{R_B}$
- $U_{out} = U_{CC} - \beta\cdot\frac{R_C}{R_B}\cdot(U_{in} - 0.6)$
## Punkt pracy
Przez punkt pracy tranzystora rozumie się **wartości prądów i napięć, które występują na tranzystorze przy braku zewnętrznego sygnału sterującego**. Zewnętrzny sygnał moduluje prąd i napięcie kolektora wokół punktu pracy.
Stałe (DC) wartości napięć $U_B, U_C, U_E$. (oznaczane dużymi literami)
Wejściowy sygnał zmienny moduluje punkt pracy. (oznaczane małymi literami)

## Równanie oczkowe DC i AC
- $U_{CE}=U_{CC}-\beta\cdot(\frac{U_{in}-0.6}{R_B})\cdot R_C \leftarrow DC$ 
- $u_{CE}=\Delta U_{CE}=-\beta\cdot\frac{R_C}{R_B}\cdot u_{in} \leftarrow AC$
## Układy cyfrowe

### Inwerter tranzystorowy
Dobieramy $R_C$ i $R_B$ tak aby tranzystor pracował albo w nasyceniu albo w odcięciu.
- $R_B$  małe
- $R_C$ duże
![Inwerter](../img/inverter.png)
- $U_{in} < 1V \rightarrow V_{out} = 5V$
- $U_{in} > 1V \rightarrow V_{out} = 0V$

### NOR
![NOR](../img/nor.png)

### NAND
![NAND](../img/nand.png)

### Źródło prądowe
![Źródło prądowe](../img/zrodlo_pradowe.png)
- $I_C=\frac{U_{ref}-0.6}{R_E}$

### Sterowanie LED
![Sterowanie LED](../img/sterowanie_led.png)

### Sterowanie przekaźnikiem
![Sterowanie przekaźnikiem](../img/sterowanie_przekaznikiem.png)

### Mostek H
![Mostek H](../img/H-bridge.png)
Sterowanie silnikiem.
- zmiana kierunku obrotu
- silnik DC
Zwykle tranzystory MOSFET.

## Układy analogowe

### Wtórnik emiterowy
![Wtórnik emiterowy](../img/wtornik_emiterowy.png)
- $U_{out}=U_{in}-0.6$
- $u_{out}=u_{in}$
- $u_{in}=\frac{i_E \cdot R_E}{\frac{i_E}{\beta + 1}}=(\beta + 1) \cdot R_E$

### Dioda Zenera i wtórnik w zasilaczu

### Układ wspólny emitera (koncepcja)

### Klucz analogowy

### Konwerter 5V <-> 3.3V