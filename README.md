Keďže som v Unreal engine nikdy nepracoval väšľinu času som strávil učením sa čo ako funguje alebo hľadaním prečo niečo nefunguje. 
Zadanie bolo fajn, voxeli sú veľmi zaujímavá téma s kopou možností na optimalizácie, na koľko je toto moja unreal premiéra od začiatku
som tušil, že za k nejakým extra optimalizáciám za týždeň nedostyanem ale predsa len som niečo stihol.

Zadnie nieje kompletné, keďže deadline je dnes do polnoci v maine je mergnute zadanie v aktualnom stave pred deadlinom.

Rozhodol som sa ho robiť pomocou blueprintov a táto verzia obsahuje:
- generovanie terénu z perlin noise, nastaviteľný seed a frekvencia
- dynamické načítavanie chunkov, nastaviteľná vykresľovacia vzdialenosť aj rozmery chunkov
- len 1 typ bloku, tráva
- stavanie (right click), ničenie (left click) blokov

Implementované optimalizácie:
- pamäť: pre každý voxel v chunku ukladám iba jeho typ + chunk obsahuje map s indexami inštancií (voxelmi ktoré sú aktuálne vykreslené)
- rendering: na bloky som použil instancovanie, na začiatku sú instancované len najvyššie časti terénu, ak hráč nejak upravý terén
  (pridá/zničí blok) susedńe bloky sa "reloadnu", skontroluje sa či sa odobraním bloku nestal ďalší viditeľný a je potom instancovaný alebo
  pridaním prestal byť viditeľný a jeho instancia sa zničí).

Neimplementované možné optiomalizácie:
- aktuálne instancujem celé bloky ktoré sú viditeľné (susedia aspoň s jedným prázdnym voxelom), ďalší level tejto optimalizácie je instancovať
  koonkrétne faces voxelov ktoré sú viditeľné
- pre ešte väčšiu redukciu faces ktoré je nutné vykresliť sa môžu rovnaké voxely spojiť do jednej meshe ako to robí minecraft
- údaje o voxeloch a instanciách by sa dali samozrejme ukladať aj kompaktnejšie ako len integery
- načítavanie chunkov v samostatnom vlákne

Známe bugy: 
- ak ste šikovný je možné vypadnúť zo sveta ak sa vám podarí vojsť diagonálne do dvoch chunkov zároveň, je tam rpoblém s procesovaním dvoch
  kolízií naraznestihol som to už opraviť
- ak to výrazne preženiete s frekvenciou šumu môžu sa objaviť trhliny v teréne keďže instancujem iba vrchnú časť

Zo zadanie už nechýba až tak veľa a chcem si ho dokončiť, keďže deadline je do dnes v zadaní budem pokračovať vo vetve post-deadline aby to 
bolo oddelené.
    
