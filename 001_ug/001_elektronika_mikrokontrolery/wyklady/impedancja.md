# Impedancja
Uogólnienie koncepcji oporu elektrycznego dla **obwodów okresowych**.
$$Z=R+j\cdot X$$
- R - **rezystancja** (rezystory)
- X - **reaktancja** (kondensatory, indukcyjności)
- $j = \sqrt{-1}$
![Opis w dziedzinie czasu i częstotliwości](../img/dziedzina_czasu_i_czestotliwosci.png)
(**układ RC** $\uparrow$)

## Kondensator
Układ gromadzący energię w polu elektrycznym. 
Budowa kondensatora:
- okładki
- dielektryk

Pojemność - zdolność do gromadzenia ładunku. (jednostka Farad)
- $C = \frac{Q}{U}$
- $C = \frac{dQ}{dU}$

### Napięcie, prąd, reaktancja pojemnościowa
**W dziedzinie czasu:**
- $i_c(t)=C\cdot\frac{d}{dt}u_c(t)$
- $u_c(t)=\frac{1}{C}\int_0^t i_c(t) \cdot dt + u_c(0)$

**Rachunek symboliczny:**
- $U(t)=U_o\cdot e^{j\omega t}$
- $I_c(t)=C\cdot\frac{dU(t)}{dt}=C\frac{d}{dt}(U_o e^{j\omega t}) = Cj\omega U_o e^{j\omega t}$
- $Z_c=\frac{1}{j\omega C}$ (patrz wyżej; *prąd proporcjonalny do napięcia*)

### Rodzaje
- ceramiczny
- elektrolityczny
- foliowy
- superkondensatory

### Ładowanie
Chwila t = 0
- $U_c=0$
- maksymalny prąd jest ograniczony przez rezystor. $I=\frac{U_z}{R}$

Chwila $t \rightarrow \infty$
- $U_c \rightarrow U_z$
- prąd nie płynie

### Sygnał sinusoidalny
$U_c(t) = U_c \cdot sin(\omega t)$
$I_c(t) = C \cdot \frac{du_c(t)}{dt}=U_c \cdot sin(\omega t + \frac{\pi}{2})$

## Cewka indukcyjna
**Cewka** – część obwodu elektrycznego, zaliczana do elementów biernych. Posiada uzwojenie, czyli nawinięte zwoje przewodnika. Wytwarzane przez nią **pole magnetyczne** może wpłynąć na prąd elektryczny płynący w obwodzie **zwiększając indukcyjność obwodu**. Wtedy jest nazywana **cewką indukcyjną**.
- $I(t)=I_o\cdot e^{j\omega t}$
- $U_L(t)=L\cdot\frac{dI(t)}{dt}=L\cdot\frac{d}{dt}(I_oe^{j\omega t})=Lj\omega I_oe^{j\omega t}$
- $Z_L = j\omega L$

## Impedancja rezystora, kondensatora i indukcyjności
$$Z_R = R$$
$$Z_C = \frac{1}{j\omega C}$$
$$Z_L = j\omega L$$
**Wartość reaktancji pojemnościowej i indukcyjnej zależy od częstotliwości.** Reaktancja wprowadza przesunięcie fazowe między napięciem a prądem.

## Łączenie impedancji

### Szeregowe
- $Z=\sum_i Z_i$ 
- $R=\sum_i R_i$, $C=\sum_i \frac{1}{C_i}$, $L=\sum_iL_i$

### Równoległe
- $\frac{1}{Z}=\sum_i\frac{1}{Z_i}$
- $Y=\sum_iY_i$
- $R=\sum_i\frac{1}{R_i}$, $C=\sum_iC_i$, $L=\sum_i\frac{1}{L_i}$

## Zależność od częstotliwości
Kondensator (pojemność)
- zwarcie dla sygnałów zmiennych AC ($\omega\rightarrow\infty$)
- rozwarcie dla sygnałów stałych DC ($\omega\rightarrow0$)
Cewka indukcyjna (indukcyjność)
- rozwarcie dla sygnałów zmiennych AC ($\omega\rightarrow\infty$)
- zwarcie dla sygnałów stałych DC ($\omega\rightarrow0$)