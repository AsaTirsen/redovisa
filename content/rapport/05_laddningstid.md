kmom05 laddningsanalys
=======================

Analys av laddningstider för tre olika webbplatser och förslag till åtgärder för att minska denna. 

Urval
-----------------------

Jag använde webbläsaren safari och sökmotorn Google. Jag skrev sökordet barnskor. De tre första träffarna som inte var 
annonser valdes ut för analys. Det var Jollyroom.se/barnskor, footway.se/skor/barn och skoboo.se/sv/article/610/barn. 
Jag fick senare byta footway.se/skor/barn till 
zalando.se/barn-skor eftersom Googles verktyg PageSpeedInsights inte kunde analysera footway i desktop-läget.

Metod
-----------------------

Jag använde webbläsaren Chrome och Googles verktyg PageSpeedInsights i mobile läge respektive desktop läge. De värden jag
fick lade jag in i Google spreadsheets. 
Sedan tittade jag på respektive sidas laddningstid under Network på dev tools. Jag laddade varje sida tre gånger för att 
möta och vid varje laddning tömde jag cacheminnet och gjorde hård inläsning.

Resultat
-----------------------
Här finns rådatat för min analys: 
[Google spreadsheet](https://docs.google.com/spreadsheets/d/11k2rJqrAiwixylSpD20yuMgKlDUlCB7Zd9yj2vC36g4/edit?usp=sharing)


PageSpeedInsights (PSI) använder en skala för 0-100 för att åskådliggöra hur snabbt en hemsida laddar mobilt respektive på desktop. 
Skalan är:
90-100 (snabb) 
50-89 (medelomfång)
0-49 (långsam)


[FIGURE src="img/jollyroom.png" caption="Screenshot av jollyrooms hemsida"]

Jollyrooms hemsida fick en poäng på 65 på mobile-mätningen vilket motsvarar medel och 99 på desktop-mätningen vilket är snabbt. 
PSI värdet på First Contenful Paint i lab-miljön blev 1.8 s. 
Den genomsnittliga tiden till laddning av DOM content i dev tools för samma sida blev 1.45 s medan tiden till fullständig
laddnig var 2.47 s. 


[FIGURE src="img/Zalando.png" caption="Screenshot av zalandos hemsida"]
Zalandos hemsida fick en poäng på 39 på mobile-mätningen vilket räknas som långsamt och 99 på desktop-mätningen vilket är snabbt. 
PSI värdet på First Contenful Paint i lab-miljön blev 1.1 s. 
Den genomsnittliga tiden till laddning av DOM content i dev tools för samma sida blev 0.97 s medan tiden till fullständig
laddnig var 1.78 s. 
Snabbast i mina mätningar var Zalando, följt av skoboo och jollyroom. 

[FIGURE src="img/skoboo.png" caption="Screenshot av skoboos hemsida"]

Skoboos hemsida fick en poäng på 55 på mobile-mätningen vilket räknas som långsamt och 99 på desktop-mätningen vilket är snabbt. 
PSI värdet på First Contenful Paint i lab-miljön blev 2.9 s. 
Den genomsnittliga tiden till laddning av DOM content i dev tools för samma sida blev 1.47 s medan tiden till fullständig
laddnig var 1.80 s. 

Analys
-----------------------

Generellt är mobil-versionen av sidorna rejält mycket långsammare än desktop-versionerna som är snabba. Närmare 
undersökning av laddningsprocessen visar att Jollyroom klarar av sn DNS lookup, initial connection, SSL och TTFB 
(time to first byte) på 216 ms. Zalando klarar av samma process på 39 ms varav TTFB är 16 ms. För Skoboo är motsvarande 
värde 474 ms varav TTFB är 403 ms. Det som verkar ta tid är annonser som laddas från externa servrar, exempelvis Facebook.
Skoboo skulle tjäna på att snabba upp sin krypteringsprocess. 
Gemensamt för de här hemsidorna är att de har många bilder, något som ökar på laddningstiden. 

Jämfört med andra siter som har mycket bilder tex Aftonbladet (DOM content loaded 2.01 total load time: 7.39), 
Fredells (DOM content loaded 1.89 total load time: 3.22),  Åhléns (DOM content loaded 817ms total load time: 1.01) 
Granit.se (DOM content loaded 1.32 total load time: 3.41), blir väl slutsatsen att de ligger hyfsat till. De fick alla 
gott betyg på desktopladdning av PSI, och jämförbart med andra siter med mycket bilder och försäljning eller log-in så 
så ligger de bland de snabbare. 

Googles ananlys från 2017 visar följande:

[FIGURE src="img/mobilespeed.jpg" caption="Data över mobil laddtid"]

Alltså borde siter som laddar mobilt inom 3 s klara sig ganska bra. Närmare analys av PSI labdata för first meaningful paint 
mobilt klarar sig ingen av barnsko-siterna under 3 sekunder. Däremot är de snabba på desktop. 

Referenser
-----------------------
https://www.thinkwithgoogle.com/marketing-resources/data-measurement/mobile-page-speed-new-industry-benchmarks/
https://developers.google.com/speed/pagespeed/insights/
https://www.zalando.se/barn-home/
https://www.skoboo.se/sv/articles/610/barn

Övrigt
-----------------------

Den här rapporten är författad av Åsa Tirsén