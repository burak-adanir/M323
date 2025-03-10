# Pure vs Impure Functions

## Aufgabe 1 - Beurteilung von Funktionen

| Aufgabe  | Nur ein Rückgabewert | Resultat nur abhängig von übergebenen Parametern | Verändert keine existierenden Werte | Pure oder Impure |
|----------|----------------------|--------------------------------|----------------------------|-----------------|
| 1.1      | Ja                   | Nein                           | Nein                       | **Impure**      |
| 1.2      | Ja                   | Ja                             | Ja                         | **Pure**        |
| 1.3      | Ja                   | Ja                             | Ja                         | **Pure**        |
| 1.4      | Ja                   | Nein                           | Ja                         | **Impure**      |
| 1.5      | Ja                   | Ja                             | Ja                         | **Pure**        |
| 1.6      | Ja                   | Ja                             | Nein                       | **Impure**      |

---

## Aufgabe 2 - Umschreiben von Impure Functions in Pure Functions

### Aufgabe 2.1 - `addToCart`
**Impure Function in Java:**
```java
import java.util.ArrayList;
import java.util.List;

public class ShoppingCart {
    private static List<String> cartItems = new ArrayList<>();

    public static List<String> addToCart(String item) {
        cartItems.add(item);
        return new ArrayList<>(cartItems);
    }
}
```

**Reine (Pure) Funktion:**
```java
import java.util.ArrayList;
import java.util.List;

public class ShoppingCart {
    public static List<String> addToCart(List<String> cartItems, String item) {
        List<String> newCart = new ArrayList<>(cartItems);
        newCart.add(item);
        return newCart;
    }
}
```

### Aufgabe 2.4 - multiplyWithRandom
**Impure Function in Java:**

```
import java.util.Random;

public class RandomMultiplier {
    public static double multiplyWithRandom(double number) {
        double randomValue = new Random().nextDouble();
        return number * randomValue;
    }
}
```

**Reine (Pure) Funktion:**

```java
public class RandomMultiplier {
    public static double multiplyWithRandom(double number, double randomValue) {
        return number * randomValue;
    }
}
```

Erkenntnis: Man kann die Zufälligkeit nicht in eine pure function umwandeln, ohne dass man die Zufallszahl als Parameter übergibt.

### Aufgabe 2.6 - printAndReturnString
**Impure Function in Java:**

```java
public class Printer {
    public static String printAndReturnString(String str) {
        System.out.println(str);
        return str;
    }
}
```

**Reine (Pure) Funktion:**

```java
public class Printer {
    public static String returnString(String str) {
        return str;
    }
}
```


## Aufgabe 3 - Eigene Pure Functions mit Rekursion

### Aufgabe 3.1 - Summe aller Listenelemente berechnen

```java
import java.util.List;

public class RecursiveSum {
    public static int sum(List<Integer> numbers) {
        if (numbers.isEmpty()) {
            return 0;
        }
        return numbers.get(0) + sum(numbers.subList(1, numbers.size()));
    }
}
```

## Aufgabe 3.2 - Mittelwert aller Listenelemente berechnen

```java
import java.util.List;

public class RecursiveAverage {
    public static double average(List<Integer> numbers) {
        if (numbers.isEmpty()) {
            throw new IllegalArgumentException("Liste darf nicht leer sein");
        }
        return (double) sum(numbers) / numbers.size();
    }

    private static int sum(List<Integer> numbers) {
        if (numbers.isEmpty()) {
            return 0;
        }
        return numbers.get(0) + sum(numbers.subList(1, numbers.size()));
    }
}
```

## Aufgabe 3.3 - Alphabetische Sortierung einer Liste von Strings

```java
import java.util.List;
import java.util.Collections;

public class RecursiveSort {
    public static List<String> sort(List<String> strings) {
        if (strings.size() <= 1) {
            return strings;
        }
        String pivot = strings.get(0);
        List<String> less = strings.stream().filter(s -> s.compareTo(pivot) < 0).toList();
        List<String> greater = strings.stream().filter(s -> s.compareTo(pivot) >= 0).skip(1).toList();
        return List.of(sort(less), List.of(pivot), sort(greater)).stream().flatMap(List::stream).toList();
    }
}
```

## Aufgabe 3.4 - Sortieren einer Liste von Objekten anhand Datum, Priorität und Titel

```java
import java.util.Comparator;
import java.util.List;

class Task {
    String title;
    String date;
    int priority;

    public Task(String title, String date, int priority) {
        this.title = title;
        this.date = date;
        this.priority = priority;
    }
}

public class TaskSorter {
    public static List<Task> sortTasks(List<Task> tasks) {
        return tasks.stream()
                .sorted(Comparator.comparing((Task t) -> t.date)
                        .thenComparing(t -> t.priority)
                        .thenComparing(t -> t.title))
                .toList();
    }
}

```

## Aufgabe 3.5 - Blätter aus einer Baumstruktur extrahieren


```java
import java.util.ArrayList;
import java.util.List;

class TreeNode {
    String value;
    List<TreeNode> children;

    public TreeNode(String value, List<TreeNode> children) {
        this.value = value;
        this.children = children;
    }
}

public class TreeLeaves {
    public static List<String> getLeaves(TreeNode node) {
        if (node.children.isEmpty()) {
            return List.of(node.value);
        }
        List<String> leaves = new ArrayList<>();
        for (TreeNode child : node.children) {
            leaves.addAll(getLeaves(child));
        }
        return leaves;
    }
}
```
