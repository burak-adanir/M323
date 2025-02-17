# Einführung - Aufgaben

## Aufgabe 1 - Imperativ vs. Deklarativ

### Imperativ:

```
public static int calculateScore(String word) {
    int score = 0;
    for (char c : word.toCharArray()) {
        if (c != 'a') {
            score++;
        }
    }
    return score;
}
```

### Deklarativ:

```
import java.util.stream.Collectors;

public static int wordScore(String word) {
    return (int) word.chars()
                     .filter(c -> c != 'a')
                     .count();
}
```

## Aufgabe 2 - Shopping Cart

### Imperativ:

```
import java.util.ArrayList;
import java.util.List;

class ShoppingCart {
    private List<String> cartItems;
    private boolean bookAdded;

    public ShoppingCart() {
        this.cartItems = new ArrayList<>();
        this.bookAdded = false;
    }

    public void addItem(String item) {
        cartItems.add(item);
        if (item.toLowerCase().contains("book")) { 
            bookAdded = true;
        }
    }

    public void removeItem(String item) {
        cartItems.remove(item);
        if (!cartItems.stream().anyMatch(i -> i.toLowerCase().contains("book"))) {
            bookAdded = false;
        }
    }

    public List<String> getItems() {
        return new ArrayList<>(cartItems);
    }

    public double getDiscountPercentage() {
        return bookAdded ? 5.0 : 0.0;
    }
}

public class Main {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        
        cart.addItem("Laptop");
        cart.addItem("Book - Java");

        System.out.println("ShoppingCart: " + cart.getItems()); 
        System.out.println("Rabatt: " + cart.getDiscountPercentage() + "%"); 

        cart.removeItem("Book - Java");

        System.out.println("ShoppingCart after removing: " + cart.getItems()); 
        System.out.println("Discount: " + cart.getDiscountPercentage() + "%"); 
    }
}
```

### Deklarativ:

```
import java.util.List;

public class Main {
    public static double getDiscountPercentage(List<String> cartItems) {
        return cartItems.stream().anyMatch(item -> item.toLowerCase().contains("book")) ? 5.0 : 0.0;
    }

    public static void main(String[] args) {
        List<String> cart1 = List.of("Laptop", "Book - Java");
        List<String> cart2 = List.of("Laptop", "Phone");

        System.out.println("Discount for cart1: " + getDiscountPercentage(cart1) + "%");
        System.out.println("Discount for cart2: " + getDiscountPercentage(cart2) + "%");
    }
}
```

## Aufgabe 3 - TipCalculator, Pure Function

```
import java.util.List;

public class Main {
    public static int calculateTipPercentage(List<String> names) {
        if (names.isEmpty()) {
            return 0;  // Keine Personen -> 0% Trinkgeld
        } else if (names.size() > 5) {
            return 20; // Mehr als 5 Personen -> 20% Trinkgeld
        } else {
            return 10; // 1-5 Personen -> 10% Trinkgeld
        }
    }

    public static void main(String[] args) {
        List<String> group1 = List.of();  // Keine Personen
        List<String> group2 = List.of("Michael", "Jackson");  // 2 Personen
        List<String> group3 = List.of("Tom", "Jerry", "Mickey", "Donald", "Goofy", "Döner");  // 6 Personen

        System.out.println("Tip for Group 1: " + calculateTipPercentage(group1) + "%"); // 0%
        System.out.println("Tip for Group 2: " + calculateTipPercentage(group2) + "%"); // 10%
        System.out.println("Tip for Group 3: " + calculateTipPercentage(group3) + "%"); // 20%
    }
}
```
