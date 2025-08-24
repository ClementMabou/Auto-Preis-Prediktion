
# Datenanalyse & Machine Learning zur Preisprognose von Automobilen

## Überblick
Dieses Projekt untersucht, welche Faktoren den Preis von Automobilen bestimmen und wie diese mithilfe statistischer Methoden und Machine-Learning-Ansätzen modelliert werden können.  
Dazu wurde ein Datensatz mit über 200 Fahrzeugen und 25 Variablen analysiert, bereinigt und modelliert.

## Ziele
- Identifikation der wichtigsten Einflussfaktoren auf Fahrzeugpreise  
- Datenbereinigung und Transformation für robuste Analysen  
- Durchführung von explorativer und multivariater Datenanalyse  
- Aufbau von Regressionsmodellen zur Preisprognose  
- Evaluierung und Optimierung der Modellleistung  

## Datengrundlage
- **Datensatz:** `autos.csv` mit >200 Fahrzeugen  
- **Variablen:**  
  - Quantitativ: z. B. Motorgröße, Gewicht, PS, Verbrauch  
  - Qualitativ: z. B. Hersteller, Karosserieform, Kraftstoffart, Antriebstyp  
- **Zielvariable:** Fahrzeugpreis  

## Vorgehen
1. **Datenbereinigung**  
   - Entfernung von Duplikaten  
   - Behandlung fehlender Werte  
   - Anpassung von Datentypen  
   - Winsorisierung von Ausreißern  

2. **Explorative Datenanalyse (EDA)**  
   - Verteilungen, Histogramme, Scatterplots  
   - Korrelationsanalyse (z. B. Motorgröße ↔ Preis: r = 0,88)  
   - Boxplots für qualitative Merkmale (z. B. Herstellersegmente)  

3. **Feature Engineering & Binning**  
   - Gruppierung von Herstellern in Segmente (Luxus, Mittel, Niedrig)  
   - Vereinheitlichung von Antriebs- und Karosserieklassen  

4. **Modellbildung**  
   - Multiple lineare Regression  
   - Feature Selektion per Stepwise-Regression  
   - Überprüfung der Modellannahmen (Linearität, Homoskedastizität, Normalverteilung)  
   - Transformation der Zielvariablen (Box-Cox, √y)  

5. **Modellvalidierung**  
   - Trainings-/Testsplit (80/20)  
   - Performance-Bewertung: gute Generalisierung, keine Overfitting-Anzeichen  

## Ergebnisse
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



