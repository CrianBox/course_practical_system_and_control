\chapter{Regeltechniek}
Regeltechniek omvat hoofdzakelijk de volgende onderwerpen:
\begin{itemize}
	\item regelaarontwerp
	\item inzicht van systeemtheorie gebruiken
	\item inzicht van de performantiecriteria voor het gesloten lus gedrag gebruiken
	\item verschillende ontwerpmethodes 
\end{itemize}

\section{basis}

\subsection{Voorwaardse koppeling (feedforward)}


\subsection{Achterwaardse koppeling (feedback)}

%\begin{comment}
\subsection{Weerstand tegen storing}
Storing kunnen zowel ruis als externe krachten zijn. 

\begin{figure}[H]
\centering
\caption{Model van een voeding \cite{Control system design guide book}}
\includegraphics{powersupply_model}
\end{figure}

\[ \frac{U_F(s)}{I_{LOAD}(s)}$ = $\frac{1/Cs}{1+(1/Cs) (1+K_I/s) K_P LPF(s)} \] 

In het mid-frequent domein is de weerstand tegen storing het slechtste.

\begin{figure}[H]
\centering
\caption{Transferfunctie van verstoringsignaal \cite{Control system design guide book}}
\includegraphics{disturbance_rejection}
\end{figure}

\begin{figure}[H]
\centering
\caption{Invloed van parametervariatie op het verstoringssignaal \cite{Control system design guide book}}
\includegraphics{disturbance_rejection}
\end{figure}

%\end{comment}
 
 

\section{PID architecturen}

\begin{comment}
\section{anti-aliasing}
\section{integrator anti-windup}
\section{derivative filtering}
\section{digital implementation}
\section{energie-verbruik}
\section{prefiltering}
\section{notch filtering}
\section{dode tijd compensatie}
\end{comment}