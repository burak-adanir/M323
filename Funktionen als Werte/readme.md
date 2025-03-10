# Aufgabe 1

```java
import java.util.*;
import java.util.stream.Collectors;

public class MapFunctionExercises {
    public static void main(String[] args) {
        // Übung 1: Jede Zahl verdoppeln
        List<Integer> zahlen = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> verdoppelt = zahlen.stream()
                .map(n -> n * 2)
                .collect(Collectors.toList());
        System.out.println(verdoppelt);  // Erwartete Ausgabe: [2, 4, 6, 8, 10]

        // Übung 2: Namen in Großbuchstaben umwandeln
        List<String> namen = Arrays.asList("Alice", "Bob", "Charlie");
        List<String> grossbuchstaben = namen.stream()
                .map(String::toUpperCase)
                .collect(Collectors.toList());
        System.out.println(grossbuchstaben);  // Erwartete Ausgabe: ["ALICE", "BOB", "CHARLIE"]

        // Übung 3: Hälfte jeder Zahl berechnen
        List<Integer> zahlen2 = Arrays.asList(12, 45, 68, 100);
        List<Double> halbiert = zahlen2.stream()
                .map(n -> n / 2.0)
                .collect(Collectors.toList());
        System.out.println(halbiert);  // Erwartete Ausgabe: [6.0, 22.5, 34.0, 50.0]

        // Übung 4: Adressliste formatieren
        class Adresse {
            String strasse;
            int hausnummer;
            String postleitzahl;
            String stadt;

            Adresse(String strasse, int hausnummer, String postleitzahl, String stadt) {
                this.strasse = strasse;
                this.hausnummer = hausnummer;
                this.postleitzahl = postleitzahl;
                this.stadt = stadt;
            }
        }

        List<Adresse> adressen = Arrays.asList(
                new Adresse("Hauptstrasse", 10, "12345", "Musterstadt"),
                new Adresse("Nebenstrasse", 5, "23456", "Beispielburg")
        );

        List<String> adressenFormatiert = adressen.stream()
                .map(a -> a.strasse + " " + a.hausnummer + ", " + a.postleitzahl + " " + a.stadt)
                .collect(Collectors.toList());
        System.out.println(adressenFormatiert);
        // Erwartete Ausgabe: ["Hauptstrasse 10, 12345 Musterstadt", "Nebenstrasse 5, 23456 Beispielburg"]

        // Übung 5: Vornamen in Großbuchstaben extrahieren
        List<String> personen = Arrays.asList("Max Mustermann", "Erika Mustermann");
        List<String> vornamenGross = personen.stream()
                .map(name -> name.split(" ")[0].toUpperCase())
                .collect(Collectors.toList());
        System.out.println(vornamenGross);  // Erwartete Ausgabe: ["MAX", "ERIKA"]
    }
}
```

# Aufgabe 2

```java
import java.util.*;
import java.util.stream.Collectors;

public class FilterFunctionExercises {
    public static void main(String[] args) {
        // Übung 1: Nur gerade Zahlen behalten
        List<Integer> zahlen = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> geradeZahlen = zahlen.stream()
                .filter(n -> n % 2 == 0)
                .collect(Collectors.toList());
        System.out.println(geradeZahlen);  // Erwartete Ausgabe: [2, 4]

        // Übung 2: Namen mit mehr als vier Buchstaben filtern
        List<String> namen = Arrays.asList("Alice", "Bob", "Charlie", "Diana");
        List<String> langeNamen = namen.stream()
                .filter(name -> name.length() > 4)
                .collect(Collectors.toList());
        System.out.println(langeNamen);  // Erwartete Ausgabe: ["Alice", "Charlie", "Diana"]

        // Übung 3: Zahlen größer als 50 filtern
        List<Integer> zahlen2 = Arrays.asList(12, 45, 68, 100);
        List<Integer> groessereZahlen = zahlen2.stream()
                .filter(n -> n > 50)
                .collect(Collectors.toList());
        System.out.println(groessereZahlen);  // Erwartete Ausgabe: [68, 100]

        // Übung 4: Wörter filtern, die mit "S" beginnen
        List<String> woerter = Arrays.asList("Scala", "ist", "fantastisch");
        List<String> mitS = woerter.stream()
                .filter(word -> word.startsWith("S"))
                .collect(Collectors.toList());
        System.out.println(mitS);  // Erwartete Ausgabe: ["Scala"]

        // Übung 5: Bücher vor 1950 filtern und nur die Titel ausgeben
        class Buch {
            String titel;
            String autor;
            int jahr;

            Buch(String titel, String autor, int jahr) {
                this.titel = titel;
                this.autor = autor;
                this.jahr = jahr;
            }
        }

        List<Buch> buecher = Arrays.asList(
                new Buch("1984", "George Orwell", 1949),
                new Buch("Brave New World", "Aldous Huxley", 1932),
                new Buch("Fahrenheit 451", "Ray Bradbury", 1953)
        );

        List<String> alteBuecher = buecher.stream()
                .filter(b -> b.jahr < 1950)
                .map(b -> b.titel)
                .collect(Collectors.toList());
        System.out.println(alteBuecher);  
        // Erwartete Ausgabe: ["1984", "Brave New World"]
    }
}
```

# Aufgabe 3

```java
import java.util.*;
import java.util.stream.Collectors;

public class MapFilterExercises {
    public static void main(String[] args) {
        // Übung 1: Filterung von Mitarbeiterdaten
        class Mitarbeiter {
            String name;
            String abteilung;
            int gehalt;

            Mitarbeiter(String name, String abteilung, int gehalt) {
                this.name = name;
                this.abteilung = abteilung;
                this.gehalt = gehalt;
            }
        }

        List<Mitarbeiter> mitarbeiter = Arrays.asList(
                new Mitarbeiter("Max Mustermann", "IT", 50000),
                new Mitarbeiter("Erika Musterfrau", "Marketing", 45000),
                new Mitarbeiter("Klaus Klein", "IT", 55000),
                new Mitarbeiter("Julia Gross", "HR", 40000)
        );

        List<String> gefilterteMitarbeiter = mitarbeiter.stream()
                .filter(m -> m.abteilung.equals("IT") && m.gehalt >= 50000)
                .map(m -> m.name.split(" ")[0].toUpperCase())
                .collect(Collectors.toList());
        System.out.println(gefilterteMitarbeiter);  
        // Erwartete Ausgabe: ["MAX", "KLAUS"]

        // Übung 2: Kursnamen formatieren und sortieren
        List<String> kurse = Arrays.asList(
                "Programmierung in Scala",
                "Datenbanken",
                "Webentwicklung mit JavaScript",
                "Algorithmen und Datenstrukturen"
        );

        // Filtern: Behalte nur die Kursnamen, die "Daten" enthalten
        List<String> datenKurse = kurse.stream()
                .filter(kurs -> kurs.contains("Daten"))
                .map(kurs -> kurs.replace(" ", "")) // Entferne alle Leerzeichen
                .collect(Collectors.toList());

        // Alphabetisch sortieren
        List<String> datenKurseSortiert = new ArrayList<>(datenKurse);
        Collections.sort(datenKurseSortiert);

        // Umgekehrt alphabetisch sortieren
        List<String> datenKurseUmgekehrtSortiert = new ArrayList<>(datenKurse);
        datenKurseUmgekehrtSortiert.sort(Collections.reverseOrder());

        System.out.println(datenKurse);  
        // Erwartete Ausgabe: ["Datenbanken", "Algorithmen und Datenstrukturen" -> "AlgorithmenundDatenstrukturen"]

        System.out.println(datenKurseSortiert);  
        // Erwartete Ausgabe: ["AlgorithmenundDatenstrukturen", "Datenbanken"]

        System.out.println(datenKurseUmgekehrtSortiert);  
        // Erwartete Ausgabe: ["Datenbanken", "AlgorithmenundDatenstrukturen"]
    }
}
```

# Aufgabe 4

```java
import java.util.*;
import java.util.stream.Collectors;

public class FoldLeftExercises {
    public static void main(String[] args) {
        // Übung 1: Summe aller Zahlen berechnen
        List<Integer> zahlen = Arrays.asList(1, 2, 3, 4, 5);
        int summe = zahlen.stream()
                .reduce(0, Integer::sum); // FoldLeft durch reduce() in Java
        System.out.println(summe);  // Erwartete Ausgabe: 15

        // Übung 2: Strings zu einem einzigen String kombinieren
        List<String> texte = Arrays.asList("Hallo", " ", "Welt", "!");
        String gesamterText = texte.stream()
                .reduce("", String::concat);
        System.out.println(gesamterText);  // Erwartete Ausgabe: "Hallo Welt!"

        // Übung 3: Schwerpunkt (durchschnittlichen Punkt) berechnen
        List<int[]> points = Arrays.asList(
                new int[]{1, 3},
                new int[]{2, 5},
                new int[]{4, 8},
                new int[]{6, 2}
        );

        // FoldLeft zur Berechnung der Summe der x- und y-Werte
        int[] summeXY = points.stream()
                .reduce(new int[]{0, 0}, (acc, point) -> new int[]{acc[0] + point[0], acc[1] + point[1]});

        int anzahl = points.size();
        int xMittelwert = summeXY[0] / anzahl;
        int yMittelwert = summeXY[1] / anzahl;

        System.out.println("(" + xMittelwert + ", " + yMittelwert + ")");  
        // Erwartete Ausgabe: (3, 4)
    }
}
```
# Aufgabe 5

```java
import java.util.*;
import java.util.stream.Collectors;

public class FlatMapExercises {
    public static void main(String[] args) {
        // Übung 1: Liste von Listen flach machen und Zahlen verdoppeln
        List<List<Integer>> listenVonZahlen = Arrays.asList(
                Arrays.asList(1, 2),
                Arrays.asList(3, 4),
                Arrays.asList(5, 6)
        );

        List<Integer> verdoppelteZahlen = listenVonZahlen.stream()
                .flatMap(List::stream) // Flache Liste erstellen
                .map(n -> n * 2) // Jede Zahl verdoppeln
                .collect(Collectors.toList());

        System.out.println(verdoppelteZahlen);
        // Erwartete Ausgabe: [2, 4, 6, 8, 10, 12]

        // Übung 2: Liste aller einzigartigen Farben extrahieren
        List<Person> personen = Arrays.asList(
                new Person("Max", Arrays.asList("Blau", "Grün")),
                new Person("Anna", Arrays.asList("Rot")),
                new Person("Julia", Arrays.asList("Gelb", "Blau", "Grün"))
        );

        List<String> einzigartigeFarben = personen.stream()
                .flatMap(p -> p.farben.stream()) // Farben aus der Liste extrahieren
                .distinct() // Doppelte Farben entfernen
                .collect(Collectors.toList());

        System.out.println(einzigartigeFarben);
        // Erwartete Ausgabe: ["Blau", "Grün", "Rot", "Gelb"]
    }

    // Hilfsklasse für die Personen mit Namen und Lieblingsfarben
    static class Person {
        String name;
        List<String> farben;

        Person(String name, List<String> farben) {
            this.name = name;
            this.farben = farben;
        }
    }
}
```

# Aufgabe 6

```java
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class ForComprehensionExercises {
    public static void main(String[] args) {
        // Übung 1: Zahlen von 1 bis 10 quadrieren
        List<Integer> quadrate = IntStream.rangeClosed(1, 10)
                .map(n -> n * n)
                .boxed()
                .collect(Collectors.toList());

        System.out.println(quadrate);
        // Erwartete Ausgabe: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

        // Übung 2: Nur gerade Zahlen von 1 bis 20 auswählen
        List<Integer> geradeZahlen = IntStream.rangeClosed(1, 20)
                .filter(n -> n % 2 == 0)
                .boxed()
                .collect(Collectors.toList());

        System.out.println(geradeZahlen);
        // Erwartete Ausgabe: [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

        // Übung 3: Alle möglichen Farbstoff-Kombinationen erzeugen
        List<String> colors = Arrays.asList("Red", "Green", "Blue");
        List<String> fruits = Arrays.asList("Apple", "Banana", "Orange");

        List<String> farbFruchtKombinationen = colors.stream()
                .flatMap(color -> fruits.stream().map(fruit -> color + " " + fruit))
                .collect(Collectors.toList());

        System.out.println(farbFruchtKombinationen);
        // Erwartete Ausgabe: ["Red Apple", "Red Banana", "Red Orange", "Green Apple", "Green Banana", ...]

        // Übung 4: Benutzer und unerledigte Aufgaben finden
        class User {
            String name;
            List<String> tasks;

            User(String name, List<String> tasks) {
                this.name = name;
                this.tasks = tasks;
            }
        }

        List<User> users = Arrays.asList(
                new User("Alice", Arrays.asList("Task 1", "Task 2", "Task 3")),
                new User("Bob", Arrays.asList("Task 1", "Task 4", "Task 5")),
                new User("Charlie", Arrays.asList("Task 2", "Task 3", "Task 6"))
        );

        List<String> tasksCompleted = Arrays.asList("Task 1", "Task 3", "Task 5");

        List<String> unerledigteAufgaben = users.stream()
                .flatMap(user -> user.tasks.stream()
                        .filter(task -> !tasksCompleted.contains(task))
                        .map(task -> user.name + " - " + task))
                .collect(Collectors.toList());

        System.out.println(unerledigteAufgaben);
        // Erwartete Ausgabe: ["Alice - Task 2", "Bob - Task 4", "Charlie - Task 2", "Charlie - Task 6"]
    }
}
```

