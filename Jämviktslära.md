# Jämviktlära

HEEEEJ
HALLLOOOOO!!

#### Frågeställning:

Skriv ett program där du går in med Delta H, \Delta S, T och därmed får ut jämviktskonstanten.

#### Kriterier för godkännande:

- En titel och en sammanfattande text av projektet
- Markdown-text där ni har någon ekvation, figur, tabell, animation, webbsida, eller - liknande.
- Förståelig så att någon annan lyckas köra den (med start från cell 1 och kärnan nollställd och vidare)
- Någon form av input i form av egen genererad data (t.ex. numpy) eller inläst (t.ex. pandas)
- Använda numpy, scipy eller pandas för att numeriskt manipulera datan
- Skapa minst en figur med flera delfigurer (antingen inset eller som subfigurer)
- Ha figurer färdiga för "tryck". Dvs. snygga och förklarande figurer, med beskrivna texter eller symboler på axlarna (med enheter). Ändra gärna figurstorlek och textstil (och storlek).

# Jämviktlära

#### Frågeställning:

Skriv ett program där du går in med Delta H, \Delta S, T och därmed får ut jämviktskonstanten.

#### Kriterier för godkännande:

- En titel och en sammanfattande text av projektet
- Markdown-text där ni har någon ekvation, figur, tabell, animation, webbsida, eller - liknande.
- Förståelig så att någon annan lyckas köra den (med start från cell 1 och kärnan nollställd och vidare)
- Någon form av input i form av egen genererad data (t.ex. numpy) eller inläst (t.ex. pandas)
- Använda numpy, scipy eller pandas för att numeriskt manipulera datan
- Skapa minst en figur med flera delfigurer (antingen inset eller som subfigurer)
- Ha figurer färdiga för "tryck". Dvs. snygga och förklarande figurer, med beskrivna texter eller symboler på axlarna (med enheter). Ändra gärna figurstorlek och textstil (och storlek).

## Introduktion - Förklaring av termodynamik, Titel, osv.

#### Sammanfattande text:

Programmet beräknar jämviktskonstanten K från ΔH, ΔS och temperaturen T, samt undersöker hur ΔH och ΔS ändras med temperaturen T. 


## Teori - Ekvationer som t.ex. Gibbs Free Energy
#### ΔGs relation med ΔH, ΔS och T:

$ \Delta G = \Delta H + T\Delta S $

#### ΔGs relation med jämviktskonstanten K:

$ \Delta G = \Delta G° + RT$ $ln(K) $

#### $ \rightarrow $ K relation med ΔH, ΔS och T 

$ K = e^{\Delta G / RT} $


Kanske lägga till något mer här som inkluderar någon figur, animation, websida av något slag

## Input - Data för någon reaktion ksk?

#### Någon termodynamisk reaktion*

T.ex. 
$H_2SO_4(l)+2NaOH\rightarrow2H_2O(l)+2Na^+(aq)+SO_4^{2-}(aq)$

#### Tabeller:
- En med data för reaktionen varifrån vi kan göra en mindre tabell som specifierar K, ΔH, ΔS, T. 
- Två kurvor med K värdet på y-axeln och ΔH, ΔS. på x-axeln som vi kan göra interaktiva genom att man kan hålla musen över curvan och se det förväntade K värdet eller nått.

Man kanske kan göra någon matris eller någon kod som kan beräkna K värdet för alla temperaturer, ΔH och ΔS, om vi inte hittar data någonstans eller vill använda Panda eller nått.

Numpy, scipy eller pandas + Snygga figurer

## Teori
Konstant temperatur.

Van't Hoff equation: 

$ K=e^{-{(\Delta H - T\Delta S)} /(RT)} $

    import matplotlib.pyplot as plt
    
    import numpy as np

    DH = np.linspace(-100000,100000,100) # J/mol
    DS = np.linspace(-300,300,100) # J/(mol* K)
    
    T = 298      # K
    R = 8.314    # J/(mol K)
    
    K = np.exp(-((DH-T*DS)/(R*T)))

    fig,(ax1, ax2) = plt.subplots(1, 2, figsize = (12,6))
    
    # plot 1: K vs DH
    DS_constant = 100 
    K_vs_DH = np.exp(-(DH - T*DS_constant)/(R*T))
    ax1.plot(DH/1000, np.log10(K_vs_DH))  # DH till kJ/mol
    ax1.set_xlabel('ΔH (kJ/mol)')
    ax1.set_ylabel('Log₁₀(K)')
    ax1.set_title(f'K vs ΔH (ΔS = {DS_constant} J/(mol·K))')
    ax1.grid(True)
    
    # plot 2: K vs DS
    DH_constant = -50000 # J/mol
    K_vs_DS = np.exp(-(DH_constant - T*DS)/(R*T))
    ax2.plot(DS, np.log10(K_vs_DS))
    ax2.set_xlabel('ΔS (J/(mol·K))')
    ax2.set_ylabel('Log₁₀(K)')
    ax2.set_title(f'K vs ΔS (ΔH = {DH_constant/1000} kJ/mol)')
    ax2.grid(True)
    
    plt.show()

$K$ vs $\Delta H$ under konstant entropi ($\Delta S = 100$ J/(mol K)): Negativ $\Delta H \rightarrow$ högre $K$

$K$ vs $\Delta S$ under konstant entalpi ($\Delta H = -50.0$ kJ/mol): Positiv $\Delta S \rightarrow$ högre $K$

    from ipywidgets import interact
    
    T = np.linspace(200,1000,100)
    
    def f(DH, DS):
    
        logK = -(DH - T*DS)/(R*T*np.log(10))
    
        plt.figure(figsize=(8,6))
        plt.plot(T, logK)
    
        plt.xlabel('Temperatur (K)')
        plt.ylabel('Log₁₀(K)')
        plt.title(
            f'ΔH = {DH/1000:.1f} kJ/mol, ΔS = {DS} J/(mol·K)')
    
        plt.grid(True)
        plt.show()
    
    interact(f, DH=(-100000, 100000, 5000),DS=(-300, 300, 10))


# Temperaturberoende jämviktskonstant



### I denna modell antas temperaturen variera inom ett intervall, vilket för att jämviktskonstantens temperaturberoende kan studeras. Därför används van't Hoffs ekvation:

![Formel](https://latex.codecogs.com/svg.image?(\partial(lnK)/\partial&space;T)_P=\Delta&space;H^0/RT^2&space;) 

För att bestämma hur jämviktskonstanten förändras mellan två temperaturer integreras uttrycket:

![Formel](https://latex.codecogs.com/svg.image?\partial(lnK)=\partial&space;T\times&space;\Delta&space;H^\circ&space;/RT^2)

![Formel](https://latex.codecogs.com/svg.image?\Leftrightarrow&space;)

![Formel](https://latex.codecogs.com/svg.image?\int_{T_1}^{T_2}d(lnK)=\Delta&space;H^\circ&space;/R\int_{T_1}^{T_2}1/T^2&space;dT)

![Formel](https://latex.codecogs.com/svg.image?\Leftrightarrow&space;)

![Formel](https://latex.codecogs.com/svg.image?ln(K)=-\Delta&space;H^\circ&space;/R(1/T_2-1/T_1))

Där:

K = jämviktskonstanten (enhetslös)  
T = temperatur (K)  
R = gaskonstanten (8.314 J/mol·K)  
 $\Delta H^\circ$ = reaktionens entalpiförändring (J/mol)
 
Exempel med reaktion:
 
 ![Formel](https://latex.codecogs.com/svg.image?HCI(aq)&plus;NaOH(aq)\rightleftharpoons&space;NaCl(aq)&plus;H_2O(l))
 
Standardbildningsentalpin kan hämtas från tabeller i kemiska databaser, exempelvis från Wikipedia.

I koden nedan visas en tabell över sådana värden:

```python
from IPython.display import IFrame
IFrame("https://en.wikipedia.org/wiki/Standard_enthalpy_of_formation", width=800, height=600)

### Sammanställning av standardbildningsentalpin för ämnena i reaktionen:

```python
import pandas as pd

data = {
    "Ämne": ["HCl(aq)", "NaOH(aq)", "NaCl(aq)", "H₂O(l)"],
    "ΔHf° (kJ/mol)": [-167.2, -469.15, -407.27, -285.8] 
}

df = pd.DataFrame(data)
df

### Temperaturintervall för reaktionen

Temperaturintervallen för reaktionen kan ändras i koden.

```python
import numpy as np
import matplotlib.pyplot as plt

# Konstanter
R = 8.314
delta_H = -57000
T0 = 298
K0 = 1

# Intervall
T1 = np.linspace(273, 800, 50)
T2 = np.linspace(300, 330, 50)
T3 = np.linspace(330, 373, 50)

def beräkna_K(T):
    ln_K = np.log(K0) - (delta_H / R) * (1/T - 1/T0)
    return np.exp(ln_K)

# Beräkna för varje intervall
K1 = beräkna_K(T1)
K2 = beräkna_K(T2)
K3 = beräkna_K(T3)

# Visa några värden
print(K1[:5]) #här kan antalet decimaler ändras

```python
import matplotlib.pyplot as plt

# Snyggare standardinställningar
plt.rcParams.update({'font.size': 12})

# Skapa delfigurer (1 rad, 2 kolumner)
fig, axs = plt.subplots(1, 2, figsize=(12, 4))

# --- Första delfiguren ---
axs[0].plot(T1, K1, label="273–800 K", color="blue")
axs[0].set_title("Stort temperaturintervall")
axs[0].set_xlabel("Temperatur (K)")
axs[0].set_ylabel("Jämviktskonstant K (-)")
axs[0].legend()
axs[0].grid()

# --- Andra delfiguren ---
axs[1].plot(T2, K2, label="300–330 K", color="orange")
axs[1].plot(T3, K3, label="330–373 K", color="green")
axs[1].set_title("Detaljerat intervall")
axs[1].set_xlabel("Temperatur (K)")
axs[1].set_ylabel("Jämviktskonstant K (-)")
axs[1].legend()
axs[1].grid()

# Justera layout
plt.tight_layout()

# Visa figuren
plt.show()

# Slutsats

Resultaten visar att jämviktskonstanten (K) minskar när temperaturen ökar. Detta beror på att reaktionen är exoterm (Delta H < 0). Enligt van’t Hoffs ekvation förskjuts jämvikten därför mot reaktanterna vid högre temperaturer, vilket ger ett lägre värde på (K).

