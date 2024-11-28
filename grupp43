\documentclass{article}

\usepackage{graphicx} % Required for inserting images
\usepackage{amsmath}
\usepackage{hyperref}

\usepackage[utf8]{inputenc}
\usepackage[ngerman]{babel}
\usepackage[T1]{fontenc}

\usepackage{url} %URL Literaturverzeichnis

\usepackage{amssymb} % für das E von Erwartungswert

\usepackage{gensymb}


\title{Abgabe 1 für Computergestütze Methoden}
\author{Gruppe 43, Lea Brand, Lara Wagner}
\date{01.12.2024}

\begin{document}

\maketitle

\tableofcontents

\newpage

\section{Der zentrale Grenzwertsatz}

Der zentrale Grenzwertsatz (ZGS) ist ein fundamentales Resultat der Wahr-
scheinlichkeitstheorie, das die Verteilung von Summen unabh¨ angiger, identisch
verteilter $(i.i.d.)$ Zufallsvariablen (ZV) beschreibt. Er besagt, dass unter be-
stimmten Voraussetzungen die Summe einer großen Anzahl solcher ZV ann¨ ahernd
normalverteilt ist, unabh¨ angig von der Verteilung der einzelnen ZV. Dies ist be-
sonders n¨ utzlich, da die Normalverteilung gut untersucht und mathematisch
handhabbar ist. 


\subsection{Aussage}

Sei $X_1,X_2,...,X_n$ eine Folge von $i.i.d.$ ZV mit dem Erwartungswert $\mu=\mathbb{E}(X_i)$ und der Varianz $\sigma^2 = Var(X_i)$, wobei $0 < \sigma^2 < \infty$ gelte. Dann konvergiert die standardisierte Summe $Z_n$ dieser ZV für $n\to\infty$ in Verteilung gegen eine
Standardnormalverteilung:\footnote{Der zentrale Grenzwertsatz hat verschiedene Verallgemeinerungen. Eine davon ist der \textbf{Lindeberg-Feller-Zentrale-Grenzwertsatz} [\cite{Springer}, Seite 328], der schwächere Bedingungen an die Unabhängigkeit und die identische Verteilung der ZV stellt.}

\begin{equation}
    \label{eq:Normalverteilung1}
     Z_n= \frac{\sum_{i = 1}^nX_i-n\mu}{\sigma\sqrt{n}} 
\end{equation}

Das bedeutet, dass für große $n$ die Summe der ZV näherungsweise normalverteilt
ist mit Erwartungswert $n\mu$ und Varianz $n\sigma^2$:

\begin{equation}
    \label{eq:Normal2}
    \sum^n_{i=1}X_i\sim\mathbb{N}(n\mu,n\sigma^2).
\end{equation}

\subsection{Erklärung der Standardisierung}

Um die Summe der ZV in eine Standardnormalverteilung zu transformieren,
subtrahiert man den Erwartungswert $n\mu$ und teilt durch die Standardabwei-
chung $\sigma\sqrt{n}$. Dies führt zu der obigen Formel \eqref{eq:Normalverteilung1}. Die Darstellung \eqref{eq:Normal2} ist für
$n\to\infty$ nicht wohldefiniert.

\subsection{Anwendungen}

Der ZGS wird in vielen Bereichen der Statistik und der Wahrscheinlichkeits-
theorie angewendet. Typische Beispiele sind:
\begin{itemize}
    \item \textit{Hypothesentests}
    \item \textit{Stichprobenverteilung des Mittelwerts}
\end{itemize}


\newpage

\section{Bearbeitung zur Aufgabe 1}

\subsection{Berechnung der höchsten mittleren Temperatur}

Wir haben alle Datensätze von Gruppe 43 in eine neue Tabelle eingefügt, wobei uns aufgefallen ist, dass sich alle Daten eines Datums jeweils in einer Spalte befanden. Wir haben alle Zeilen ausgewählt und durch “Teilen in Spalten" die Daten, nach Kommas, in verschiedene Spalten aufteilen können. Dabei ist uns aufgefallen, dass viele Daten nicht vorhanden (NA), falsch (Windspeed=-1) oder in der falschen Spalte waren (Windspeed=Jun 49). Wir haben dann am Ende der Spalte \textit{average temperature} das Summenzeichen verwendet und dort \textit{max} ausgewählt und so den Wert $28,3{\degree}C$ Grad herausbekommen, als höchste mittlere Temperatur.

\subsection{Datenbankschema entwerfen}

1. Normalform: Durch 2.1. enthält jede Spalte einen atomaren Wert.
2. Normalform: Aufteilung in mehrere Tabellen abhängig vom Primärschlüssel.

Wir haben in 3 Tabellen aufgeteilt, in "group", "date" und "values".
In der Tabelle "group" haben wir die Spalten "group id" und "station", in "date id" haben wir die Spalten "date", "day of year", "day of week" und "month of year"  und in "values" haben wir "group id", "date id", "percipation", "windspeed", "min temperature", "average temperature", "max temperature" und "count".

\subsection{SQL und CSV}

Umsetzung des Schemas in SQL (DDL):

\begin{verbatim}
CREATE TABLE "group43" (
	id	INTEGER NOT NULL UNIQUE,
	name	TEXT NOT NULL UNIQUE,
	PRIMARY KEY("id")
);

CREATE TABLE "date43" (
	id	TEXT NOT NULL UNIQUE,
	day_of_year	INTEGER NOT NULL,
	day_of_week	INTEGER NOT NULL,
	month_of_year	INTEGER NOT NULL,
	PRIMARY KEY("id")
);

CREATE TABLE "values43" (
	group_id	TEXT NOT NULL,
	date_id	TEXT NOT NULL,
	precipitation	NUMERIC,
	windspeed	NUMERIC,
	min_temperature	NUMERIC,
	average_temperature	NUMERIC,
	max_temperature	NUMERIC,
	count	INTEGER,
	PRIMARY KEY("date_id","group_id"),
	FOREIGN KEY(date_id) REFERENCES date43(id),
	FOREIGN KEY(group_id) REFERENCES group43(id)
 );

\end{verbatim}

Import der zugeordneten Daten als CSV:

In der Excel-Datei haben wir unsere Gruppen-Tabelle abgespeichert als CSV-Datei. Dann haben wir den DB Browser für SQLite benutzt und die CSV-Datei importiert, indem wir im Menü "Importieren" ausgewählt haben und unsere vorbereitete Datei importiert. Wir haben den Feld-Seperator "," ausgewählt, String-Zeichen "`" und die Codierung "UTF-8".

\subsection{Formulierung der SQL-Abfrage, um höchste mittlere Temperatur zu ermitteln}

\begin{verbatim}

SELECT
max(average_temperature) as max_wert
FROM values43
WHERE average_temperature not in ('NA')
;
\end{verbatim}

\newpage


\bibliographystyle{plain}
\bibliography{references}


\end{document}

