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


