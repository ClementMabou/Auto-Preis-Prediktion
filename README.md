
# Datenanalyse & Machine Learning zur Preisprognose von Automobilen

## Überblick
Dieses Studienprojekt untersucht, welche Faktoren den Preis von Automobilen bestimmen und nutzt diese zur Prognose von Fahrzeugpreisen mittels Machine Learning.  Dazu wurde ein Datensatz mit über 200 Fahrzeugen und 25 Variablen analysiert, bereinigt und modelliert.

## Ziele
- Datenbereinigung und Datenaufbereitung 
- Identifikation der wichtigsten Einflussfaktoren auf Fahrzeugpreise    
- Aufbau von Regressionsmodellen zur Preisprognose  
- Evaluierung und Optimierung der Regressionsmodelle 

## Datengrundlage
- **Datensatz:** `autos.csv` mit >200 Fahrzeugen  
- **Prädiktoren :**  
  - 16 quantitative Prädiktoren: z. B. Motorgröße, Gewicht, PS, Verbrauch  
  - 8 qualitative Prädiktoren : z. B. Hersteller, Karosserieform, Kraftstoffart, Antriebstyp  
- **Zielvariable:** preis  

## Vorgehen
1. **Datenbereinigung**  
   - Entfernung von Duplikaten 
   - Ersetzung unlogischer Werte (z. B. ? → NA)  
   - Entfernung fehlender Werte  
   - Anpassung von Datentypen 
   - Ersetzung von Ausreißern nach der IQR-Regel durch die Werte des ersten bzw. dritten Quartils.  

2. **Univariate Datenanalyse**
    Sie ist wichtig um einzelne Variable zu verstehen (Wertebereiche, Skalierung, verteilung). Sie bildet eine wichtige Grundlage, um notwendige Transformationen in späteren Analyseschritten vorzunehmen. 
   - Descriptive Statistik, 
   - Histogramme, 
   - density plot  


3.**Multivariate Datenanalyse**
   Sie dient dazu, Zusammenhänge zwischen der Zielvariable und Prädiktoren zu erkennen.
   - Scatterplots
   - Korrelationsplot  
   - Boxplots    

3. **Feature Engineering**
   - Transformation von Merkmalen: Kategorien qualitativer Merkmale werden nach ihrer Einflussstärke auf die Zielvariable Preis     zusammengefasst (Binning), um die Anzahl der Kategorien zu reduzieren.
   - erste Merksmalauswahl:Prädiktoren mit schwacher Korrelation zur Zielvariable (r < 0,2) werden entfernt; bei stark korrelierten Prädiktoren untereinander (r ≥ 0,8) wird einer entfernt.
   - zweite Merkmalauswahl: Stepwise-Regression mit Forward- und Backward-Selection unter Verwendung des AIC-Kriteriums.

4. **Modellbildung**  
   - Multiple lineare Regression   
   - Überprüfung der Modellannahmen (Linearität, Homoskedastizität, Normalverteilung)  
   - Transformation der Zielvariablen (Box-Cox) zur verbesserung des Modells 

5. **Modellvalidierung**  
   - Trainings-/Testsplit (80/20)  
   - Performance-Bewertung: R2 auf train und Testdaten  

## Ergebnisse 
![alt text](image.png)

Die Zielvariable „Preis“ ist rechtsschief (Mittelwert 12.829 > Median 10.245), wobei 75 % der Autos unter 16.515 liegen. Einige teure Fahrzeuge erhöhen den Mittelwert. Eine Transformation (Logarithmus oder Quadratwurzel) kann die Schiefe reduzieren, während die hohe Standardabweichung (6.792,89) die große Preisspanne zeigt.

![alt text](image-1.png)

Das Bild zeigt Scatterplots, in denen der Autopreis mit verschiedenen quantitativen Merkmalen verglichen wird. Starke positive lineare Zusammenhänge zeigen Preis mit motor_groesse, gewicht , PS , anzahl_zylinder , laenge , radstand  und kolben_durchmesser; starke negative Zusammenhänge treten bei Verbrauch (Stadt/Autobahn) auf. Bei anderen Variablen wie maximale_drehzahl oder Kompressionsrate sind die Zusammenhänge schwach oder nichtlinear.

![alt text](image-8.png)

Der Korrelationsplot zeigt Stärke und Richtung linearer Zusammenhänge. Die Zielvariable „Preis“ korreliert stark positiv mit Motorgröße (0,88), Gewicht (0,88), PS (0,82) usw., und stark negativ mit Verbrauch auf Autobahn (-0,74) und in der Stadt (-0,76). Hohe Korrelationen zwischen Prädiktoren, z. B. Gewicht und Motorgröße (0,88) oder Verbrauchsvariablen (0,97), weisen auf Multikollinearität hin, die bei linearen Modellen berücksichtigt werden muss.

![alt text](image-9.png)

Die Boxplots zeigen, dass der Autopreis stark von Merkmalen wie Hersteller, Karosserieform, Antriebstyp und Motorsteuerungabhängt. teurere Autos stammen meist von renommierten Marken (z. B. Jaguar, Mercedes-Benz, Porsche), nutzen häufig Diesel, haben Karosserien wie Hardtop oder convertible, verfügen über Heckantrieb, Turbolader und moderne Motorsteuerung, während günstigere Fahrzeuge meist Kleinwagen  mit einfacheren Antriebs- und Motorkonfigurationen sind. Insgesamt spiegeln höhere Preise sowohl technische Leistungsfähigkeit als auch Luxus wider. 

Viele qualitativen Variablen weisen zahlreiche Ausprägungen auf. Um die Anzahl der Dummy-Variablen in späteren Modellen zu reduzieren, wurden ähnliche Ausprägungen  pro qualitative Variablen (solche mit vergleichbarer Erklärungsstärke für den Preis) per Binning zu Gruppen zusammengefasst.

![alt text](image-10.png)

Die Boxplots nach dem Binning zeigen, dass die Erklärungsstärke der neuen Ausprägungen qualitativer Prädiktoren verbessert wurde und die Datenstruktur für nachfolgende Analysen übersichtlicher ist.

![alt text](image-11.png)
Dieses Modell basiert auf der Quadratwurzel-Transformation der Zielvariable (Preis) aus einem ersten Modell, um die Voraussetzungen der multiplen linearen Regression zu verbessern. Es umfasst deutlich weniger Merkmale als die ursprüngliche Menge potenzieller Prädiktoren, was die Interpretierbarkeit erhöht, und weist gleichzeitig eine sehr hohe Güte auf: Mit einem R² von 0,9249 (angepasst 0,9202) erklärt es über 92 % der Varianz. Variablen wie Motoraufladung (Turbo), Antriebstyp (rwd), Motorposition (rear), Breite, Zylinderzahl und Motorgröße wirken positiv auf die Autopreise, während eine höhere Kraftstoffeffizienz (Autobahn-mpg) sowie bestimmte Hersteller-Dummies (MS: Marken im mittleren Preissegment, NS: Marken im niedrigen Preissegment) negative Effekte zeigen.

![alt text](image-12.png)
![alt text](image-6.png)
![alt text](image-13.png)

- **Starke Einflussfaktoren:** Motorgröße, Gewicht, PS, Verbrauch, Herstellersegment  
- **Negativer Zusammenhang:** Höherer Preis ↔ schlechtere Kraftstoffeffizienz  
- **Bestes Modell:** Transformierte multiple Regression mit hoher Prognosegüte  

## Ausblick
- Erweiterung um nichtlineare Modelle (z. B. Random Forest, Gradient Boosting)  
- Einbezug größerer und aktuellerer Fahrzeugdatensätze  
- Anwendung für Preisprognosen in Echtzeit (z. B. Gebrauchtwagenportale)  

## Technologien
- **Programmiersprache:** R / Python (abhängig von Umsetzung)  
- **Methoden:** Explorative Datenanalyse, Korrelationsanalyse, multiple lineare Regression, Modellvalidierung  
- **Bibliotheken:** pandas, numpy, matplotlib, seaborn, scikit-learn (bei Python)  



