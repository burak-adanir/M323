# Autorennen - Berechnungen

## Aufgabenstellung

Wir möchten eine Anwendung, die:
- Die Gesamtzeit aller Runden ohne die erste Runde berechnet.
- Die Durchschnittszeit pro Runde (ohne Warm-up-Runde) ermittelt.

## Implementierung in Java

Die Implementierung erfolgt in Java und verwendet eine funktionale Programmierung mit Streams.

### Code

```java
import java.util.List;

public class RaceCalculator {
    
    /**
     * Berechnet die Gesamtzeit aller Runden ohne die erste (Warm-up-Runde).
     * @param lapTimes Liste mit Zeiten der einzelnen Runden in Sekunden.
     * @return Gesamtzeit ohne Warm-up-Runde.
     */
    public static double calculateTotalRaceTime(List<Double> lapTimes) {
        if (lapTimes.size() <= 1) {
            throw new IllegalArgumentException("Mindestens zwei Rundenzeiten sind erforderlich.");
        }
        return lapTimes.stream().skip(1).mapToDouble(Double::doubleValue).sum();
    }

    /**
     * Berechnet die Durchschnittszeit pro Runde ohne die erste Runde.
     * @param lapTimes Liste mit Zeiten der einzelnen Runden in Sekunden.
     * @return Durchschnittliche Rundenzeit ohne Warm-up-Runde.
     */
    public static double calculateAverageLapTime(List<Double> lapTimes) {
        if (lapTimes.size() <= 1) {
            throw new IllegalArgumentException("Mindestens zwei Rundenzeiten sind erforderlich.");
        }
        return calculateTotalRaceTime(lapTimes) / (lapTimes.size() - 1);
    }
    
    /**
     * Hauptmethode zum Testen der Funktionen.
     */
    public static void main(String[] args) {
        List<Double> lapTimes = List.of(62.5, 59.3, 58.7, 60.2, 57.5); // Beispielhafte Rundenzeiten
        
        double totalTime = calculateTotalRaceTime(lapTimes);
        double averageTime = calculateAverageLapTime(lapTimes);
        
        System.out.println("Gesamtzeit ohne Warm-up-Runde: " + totalTime + " Sekunden");
        System.out.println("Durchschnittliche Rundenzeit: " + averageTime + " Sekunden");
    }
}
```
