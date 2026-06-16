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
ax1.plot(DH/1000, np.log10(K_vs_DH))  # Convert DH to kJ/mol for x-axis
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


