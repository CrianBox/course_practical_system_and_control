# Structuur van de cursus

1. Introductie

    Hierin staat beschreven in welke situatie het overgrote deel van de industrie zich bevind en waar de algemene moeilijkheden zich precies bevinden. Dit hoofdstuk heeft als functie veelgebruikte begrippen en methodieken kort samen te vatten om zo verder cursusmateriaal in te leiden. Ervaren gebruikers van regelsystemen kunnen dit hoofdstuk overslaan. 

2.  Afstelregels

    ...

3. Systeemtheorie

    ...
   
4. Regeltechniek

    ...
   
5. Praktische aanpak

    ...
   
6. Theorievragen
    
    ...


# Situatie
Meer dan 80 $\%$ van de proces industrie maakt gebruik van PID regelaars waarbij de afstellen van de parameters naar sub-optimale waarden vaak genegeerd wordt. 
Om de juiste methodiek te verduidelijken moeten we overeenkomen over verschillende termen.   

# Probleem omschrijving
Het correct instellen van de parameters wordt vaak over het hoofd gezien. De reden hiervoor kan een gebrek in tijd of kennis zijn. Ook al krijgen de regelaars initieel de correcte parameters, het proces verandert contant door externe factoren. Parameters moeten dus continu bij geregeld worden (sterk afhankelijk van de omgeving). In onderhoud wordt het opnieuw afstellen van regelaars vaak over het hoofd gezien.  

# Oplossing
Voor veel toepassingen zijn standaard afstel regels een goed startpunt om betere proces resultaten te verkrijgen. 
Ziegler en Nichols (1942), de paper van Rivera, Morari en Skogestad (1986), het boek van Smith $\&$ Corripio (1985) en Astrom $\&$ Hagglund (1995) zijn fundamentele bronnen waarin afstel regels werden onderzocht en geformuleerd. Geen van deze regels garanderen een algemene verbetering van het controle proces. Afhankelijk van de soort situatie en vereisten kan een specifieke procedure de prestatie van de regelaar verbeteren. Deze cursus geeft een overzicht van verschillende populaire procedures samen met hun voor- en nadelen.

# Basis

## Termen en definities
Een proces refereert naar een systeem zonder controle. 
Een installatie (= 'plant') geeft het te controleren systeem weer waarvan het gecontroleerde proces een deel is.
Controle is de aanpassing van beschikbare manipuleerbare variabelen om de installatie op een acceptabele manier te laten werken.

De werking van het systeem is het gedrag dat zich voordoet wanneer het systeem inclusief regelsysteem is gemaakt. 
Operationaliteit is het potentieel dat het systeem bevat om aan acceptabele werking te bewerkstelligen. Operationaliteit houdt in: flexibiliteit, verwisselbaarheid, controleerbaarheid,etc. 
Flexibiliteit beschrijft de haalbare steady-state werking bij een gegeven set van werkingspunten. 

Schakelbaar slaat op de eigenschap om te veranderen naar een andere setpoint op een acceptabele manier. De haalbaarheid is hierbij van groot belang.
Optimale werking beschrijft de nominale optimale manier waarop de installatie werkt. Door steady-state en/of dynamische optimalisatie toe te voegen aan het model van de installatie. Hierbij streeft men naar het minimaliseren van een kostfunctie J. In werkelijkheid is de optimale werking niet realiseerbaar door het optreden van onzekerheid.

Onzekerheid kan men beschrijven vanuit twee bronnen. Signaal en bron onzekerheid. 
Robuustheid betekent het bestand zijn tegen onzekerheid. 
Robuuste optimale werking is de optimale werking waarin maatregelen voor onzekerheid zijn genomen.
Geïntegreerde optimalisatie en controle refereert naar een systeem waarin optimalisatie en zijn controle ingebouwd zijn. Dit is theoretisch mogelijk met hiërarchische decompositie.
Hiërarchische decompositie is het onderverdelen in verschillende lagen voor optimalisatie en controle.
Controleerbaarheid van een installatie is het tonen van acceptabele controle prestaties. Zoals controle variabelen (output) binnen bepaalde grenzen houden vanuit hun referentiepunten (ref). 
Zelfregelende installaties kunnen controle variabelen (output) binnen acceptabele grenzen houden met constante inputs.

* $K_p$ : de versterker (gain) van de controller
* $T_i$ : de integratietijd (integrator) van de controller
* $T_d$ : de afgeleide tijd (derivative) van de controller
* $T_u$ : de periode van de oscillatiefrequentie tijdens de stabiliteitslimiet (in een gesloten lus)
* $K_u$ : de versterkingsmarge voor stabiliteit (in een gesloten lus)

1. Controle structuur design

	Structurele beslissingen zoals de selectie van: controle variabelen (outputs), manipuleerbare variabelen (inputs), meetbare variabelen, controle configuratie (lokale blokken) en controller type. 

2. Controller design

    Parametrische beslissingen

3. Implementatie

## Regelaar

Een PID regelaar heeft slechts drie parameters maar deze juist instellen is geen gemakkelijke klus. Een duidelijk stappenplan bijgestaan door gemakkelijke formules zijn een goed startpunt om tot betere performantie te komen.

Een eerste orde systeem is de eerste keuze om het proces te representeren, nadien wordt een tweede orde systeem geopteerd. Wanneer ook dit geen bevredigende resultaten geeft wordt er gekeken naar meer geavanceerde technieken.
We bespreken later verschillende instelregels die van toepassing zijn als er een model van het proces gekend is. Dit model is het product van 'first principals' en/of 'system identification'. Beide krijgen nog verdere uitleg.

Klassieke PID instelregels werden in 1942 door Ziegler en Nichols opgesteld. In hun originele vorm geven ze een goed resultaat als er aan een aantal criteria wordt voldaan. Daarom bestaan er ook gemodificeerde algoritmes die voor een betere set-point respons zullen zorgen. Het SIMC algoritme van S. Skogestad is een voorbeeld van een instel algoritme gebaseerd op de Ziegler-Nichols regels. Sigurd Skogestad is een Professor in Chemical Engineering met een focus op proces controle. Hij is de auteur van menige boeken en papers over controle, van multivariabele feedback controle tot simple PID tuning. Over dit laatste bestaan er enkele goed beschreven systematische aanpakken die in deze cursus aan bod zullen komen.

## Controle structuur ontwerp
Het definiëren van de verschillende variabelen en begrijpen waarom deze worden gekozen is de eerste stap in het ontwerpen van de controle structuur.
De **te controleren variabele** moet volgens Skogestad (2000) aan vier eigenschappen voldoen.

1. De optimale waarde is ongevoelig voor storingen.
2. Het is gemakkelijk om nauwkeurig te meten en controleren.
3. De waarde is gevoelig voor veranderingen van de manipuleerbare variabelen.
4. Voor situaties met twee (of meer) te controleren variabelen, de geselecteerde variabelen mogen niet sterk afhankelijk van elkaar zijn.
   
De **manipuleerbare variabelen** zijn de fysieke vrijheidsgraden. Voorbeelden hiervan zijn: de elektrische stroom door warmte elementen, de hoek van een klep, etc.
De selectie van de **te meten variabelen** hangt af van de resultaten vanuit een controleerbaarheidsanalyse. Het aantal, de locatie en de nauwkeurigheid van de sensoren zijn vaak een afweging tussen de kost en de verbetering in controle.  
De selectie van de **controle configuratie** is de beschrijving van de structuur van de controller dat de metingen, de setpoints en de manipuleerbare variabelen verbindt. Een controller kan gestructureerd worden in verschillende (horizontale of verticale) blokken. Dit heeft verschillende voordelen zoals: het minder gevoelig zijn voor modelonzekerheid, het verlagen van de kost om het controle probleem te definiëren, grotere fout tolerantie, etc.

## Stabiliteit en robuustheid

Het is belangrijk om te weten dat systemen met grote dode tijd en/of grote vertraging (lag) slechte robuustheid vertonen. 
Meer marge uit veiligheidsredenen betekend een tragere respons. Een snel reagerend controle systeem zal kleinere robuustheidsmarges hebben.

<!--
  todo: grafiek open/gesloten en tijdsdomein/frequentie
-->