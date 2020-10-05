\chapter{Data-gedreven controle}
De voorgaande theorie is een goede basis in het begrijpen van de volgende procedure. Deze gaat over het bekomen van een controle systeem wanneer geen nauwkeurig model van het proces voorhanden is. Input-output data, die gerelateerd zijn aan het proces, bevat informatie die noodzakelijk is om het proces wiskundig te beschrijven. 

\section{Data captatie}

\section{Systeem identificatie}

\section{Controller ontwerp}

\section{Testen in de praktijk}
\

\chapter{Casestudies}
In dit hoofdstuk focussen we ons op het toepassen van de theorie op een aantal veelvoorkomende oefeningen met het doel om inzicht en vaardigheden te verwerven. Er bestaan verschillende schema's en stappenplannen om meer overzicht te creëren. Dit is echter geen garantie voor succes. Het is wel een goed begin bij complexe opgaven en het zal voorkomen dat er tijdrovende fouten worden gemaakt later in het proces.  

\begin{enumerate}
	\item Bekijk de verworven data.
	
	\item Schat de moeilijkheid in.
		\begin{itemize}
			\item Spectrale analyse benadering, ARX en state space model frequentie functies.
			\item Correlatie analyse benadering, ARX en state space model transiënte resultaten.
			\item Gemeten validatie output data, ARX en state space model gesimuleerde outputsignalen. Ookwel 'Model Output Plot' genaamd. 
		\end{itemize}
	
	\item Onderzoek de moeilijkheden.
		\begin{itemize}
			\item Onstabiele modelstructuur
			\item Feedback in de data
			\item Ruismodel
			\item Model orde
			\item Aanvullende ingangssignalen
			\item Niet lineaire effecten
			\item Rest
			Onvoldoende informatie, een slechte signaal/ruis verhouding, onbekende externe verstoringen en variërende systeem eigenschappen kunnen bijkomende verklaringen zijn van slechte validatie resultaten. Als deze voorkomen worden niet-lineaire black box modellen overwogen.
		\end{itemize}
	
	\item Verfijn het aantal ordes.
		\begin{itemize}
			\item De fit tussen gesimuleerde en gemeten data.
			\item Residu analyse 
			\item Polen en nullen elimineren
		\end{itemize}
	
	\item Aanvaard (tijdelijk) het bekomen model
	
\end{enumerate}

\begin{comment}
Betere controle ontwerpen zijn vaak het het resultaat van design of experiments (DOE), statistiek en optimalisatie. Kennis van aansluitende softwarepakketten vereenvoudigd het optimaliseren van het design wanneer meerdere objectieven van kracht zijn. (bv. Matlab, Simulink, ...)
https://nl.mathworks.com/discovery/design-optimization.html
\end{comment}



\section{Temperatuurregeling in een oven}
Het doel bestaat uit het regelen van de temperatuur in een oven waarbij de setpoint op 500°C ligt. De grenzen liggen op +- 2°C. Een chroom-aluminium thermokoppel wordt gebruikt met een sensitiviteit van 41 mV/°C en een bereik van -1890°C tot 1260°C. Hou rekening met de koude verbinding compensatie en het plaatsen van de nodige versterker.  
\cite{Instrumentation and control systems}

\section{Water niveau regeling}

\begin{figure}[H]
	\centering
	\captionbelow{Water niveau regelsysteem}
	\includegraphics{water level scheme}
\end{figure}

Door gebruik te maken van fysische wetten kan het systeem beschreven worden met enkele formules.

\[ Q = k_l H \]
Q: het steady-state debiet [$\frac{m}{s^3}$] \\
$k_l$: constante [$\frac{m}{s^2}$] \\
H: steady-state hoogte [m]

\[ R_l = \frac{dH}{dQ} = \frac{h}{q_o} \]
$R_l$: de weerstand 

\[ C = \frac{dV}{dH} \]
V: het opgeslagen volume \\
C: de capaciteit 

\[ \frac{dV}{dt} = q_i - q_o = C \frac{dh}{dt} \]

Door de formules te substitueren bekomt men één formule waarin zowel het manipuleerbare ($q_i$) als de te controleren variabele ($H$) zit. 
\[ C \frac{dh}{dt} = q_i - \frac{h}{R} \]
\[ RC \frac{dh}{dt} + h = R q_i \]
Om het oplossen van differentiaalvergelijkingen te omzeilen maken we gebruik van de Laplace transformatie.
\[ RCsH(s) + H(s) = R Q_i(s) \]
De transfer functie van het proces wordt bekomen door de manipuleerbare variabele in de teller en de te controleren variabele in de noemer te plaatsen. 
\[ \frac{H(s)}{Q_i(s)} = \frac{R}{(RCs + 1)} \]

Een veelvoorkomende opstelling in de industrie is een cascade van systemen. In dit voorbeeld staan twee watervaten na elkaar verbonden met een klep. De vaten hebben een invloed op het waterniveau van het tegenovergestelde vat.

\begin{figure}[H]
	\centering
	\caption{Cascade van twee watervaten}
	\includegraphics{cascade watervaten}
\end{figure}

Beschrijf opnieuw de verschillende onderdelen van het proces in een formule vorm met de hulp van fysische wetten.
De eerste tank:
\[ C_1 \frac{dh_1}{dt} = q - \frac{h_1 - h_2}{R_1}\]
De tweede tank:
\[ C_2 \frac{dh_2}{dt} = \frac{h_1 - h_2}{R_1} - \frac{h_2}{R_2} \]
Leiding 1 beschrijven we als volgt. 
\[ q_1 = \frac{h_1 - h_2}{R_1}\]
Leiding 2:
\[ q_2 = \frac{h_2}{R_2}\]
Let op het verschil tussen de formules. 
\[ C_1 \frac{dh_1}{dt} + \frac{h_1}{R_1} = q + \frac{h_2}{R_1} \]
\[ C_2 \frac{dh_2}{dt} + \frac{h_2}{R_1} + \frac{h_2}{R_2} = \frac{h_1}{R_1} \]
De initiële conditie zal voor de eenvoud gelijk gesteld worden aan nul. ($h_1(0) = 0, h_2(0) = 0$)
De differentiaalvergelijking wordt opnieuw met Laplace getransformeerd. 
\[ (C_1s + \frac{1}{R_1}) H_1(s) = Q(s) + \frac{1}{R_1} H_2(s) \]
\[ (C_2s + \frac{1}{R_1} + \frac{1}{R_2}) H_2(s) = \frac{1}{R_1} H_1(s) \]
Uit de eerste vergelijking bekomen we:
\[ H_1(s) = \frac{R_1Q(s) + H_2(s)}{R_1C_1s +1} \]
Door deze vergelijking de substitueren in de tweede formule bekomen we:
\[ (C_2s + \frac{1}{R_1} + \frac{1}{R_2}) H_2(s) = \frac{1}{R_1} \frac{R_1Q(s) + H_2(s)}{R_1C_1s +1} \]
We weten dat:
\[ H_2(s) = R_2Q_2(s) \]
Hieruit leiden we de volgende formule af:
\[ \frac{Q_2(s)}{Q(s)} = \frac{1}{R_2C_1R_1C_2s^2 + (R_1C_1 + R_2C_2 + R_2C_1)s + 1} \]
Deze vergelijking geeft de verhouding weer tussen het ingaande debiet en het debiet dat in het tweede vat binnenstroomt. Het model, welke de werkelijkheid representeert, wordt verder ingevuld met de werkelijke parameters.

\begin{figure}[H]
	\centering
	\caption{stap impulse tf1 tf2}
	\includegraphics{stap impuls tf1 tf2}
	\label{fig:stapimpuls}
\end{figure}

Via het software pakket 'Matlab' is het mogelijk om waardevolle tijdsdomeinkarakteristieken weer te geven zoals risetime, settlingtime, overshoot en piekwaarde.
De transferfunctie voor een systeem met één vat zal sneller reageren dan twee vaten in serie. 

\begin{itemize}
	\item risetime: 22
	\item settlingtime: 39
	\item overshoot: 0
	\item piek: 2
\end{itemize}

Dit is merkbaar wanneer we de risetime en settlingtime met elkaar vergelijken. 

\begin{itemize}
	\item risetime: 38.5
	\item settlingtime: 70
	\item overshoot: 0
	\item piek: 2
\end{itemize}

Met behulp van de cursus kunnen sufficiënte P, I en D parameterwaarden berekend worden om een robuust en efficiënt systeem te bouwen. 

\begin{figure}[H]
	\centering
	\caption{Simulink schema}
	\includegraphics{simulink schema TF1}
	\label{fig:SimTF1}
\end{figure}

\begin{comment}
https://www.slideshare.net/shekharanku/water-level-controller-42584772

https://nl.mathworks.com/help/slcontrol/ug/passive-control-of-water-tank-level.html
\end{comment}


\section{Vloeistof verwarmer}

\begin{figure}[H]
	\centering
	\caption{Illustratie vloeistof verwarmer}
	\includegraphics[scale=0.5]{vloeistofverwarmer}
\end{figure}

\begin{comment}
cursus Frederik
\end{comment}

\begin{comment}
\section{Stuuroppervlak van een vliegtuig}

\begin{figure}[H]
	\centering
	\caption{Cascade meervoudige lus feedback 
		\cite{https://nl.mathworks.com/help/slcontrol/ug/cascaded-multi-loopmulti-compensator-feedback-design.html}}
	\includegraphics{CascadedMultiloopFeedbackDesignExample}
\end{figure}

\end{comment}

\section{Continuous Stirred Tank Reactor (CSTR)}
Dit is een mooi voorbeeld om gain-scheduled PID control uit te werken. 
https://nl.mathworks.com/videos/gain-scheduling-of-pid-controllers-68883.html

\section{Servomotor sturing}
Stel met behulp van 'First principals' de differentiaalvergelijkingen op en reken deze om naar het frequentiedomein met Laplace. 
Bestudeer de polen en nullen.
Hoe zal het systeem reageren in het frequentiedomein bij een stap, impuls en sinusoïdaal ingangssignaal. 

\section{Hydraulische kleppen}
Hier letten we op het niet-lineair gedrag van de kleppen. Is het mogelijk om een robuuste lineaire regelkring te maken door de niet-lineaire kenmerken rond het werkingspunt te lineariseren?