# midterm task.
public interface Coffee {
    double getCost();
    String getDescription();
}
//Espresso
public class Espresso implements Coffee {
    public double getCost() {
        return 2.0;
    }

    public String getDescription() {
        return "Espresso";
    }
}

// Cappuccino
public class Cappuccino implements Coffee {
    public double getCost() {
        return 3.0;
    }

    public String getDescription() {
        return "Cappuccino";
    }
}

// Latte
public class Latte implements Coffee {
    public double getCost() {
        return 2.5;
    }

    public String getDescription() {
        return "Latte";
    }
}
public class CoffeeFactory {
    public static Coffee createCoffee(String coffeeType) {
        switch (coffeeType) {
            case "Espresso":
                return new Espresso();
            case "Cappuccino":
                return new Cappuccino();
            case "Latte":
                return new Latte();
            default:
                throw new IllegalArgumentException("Unknown coffee type");
        }
    }
}
// Декоратор для добавления молока
public class MilkDecorator implements Coffee {
    private Coffee coffee;

    public MilkDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    public double getCost() {
        return coffee.getCost() + 0.5;
    }

    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }
}

// Декоратор для добавления карамельного сиропа
public class CaramelDecorator implements Coffee {
    private Coffee coffee;

    public CaramelDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    public double getCost() {
        return coffee.getCost() + 0.7;
    }

    public String getDescription() {
        return coffee.getDescription() + ", Caramel Syrup";
    }
}

// Декоратор для добавления взбитых сливок
public class WhippedCreamDecorator implements Coffee {
    private Coffee coffee;

    public WhippedCreamDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    public double getCost() {
        return coffee.getCost() + 0.8;
    }

    public String getDescription() {
        return coffee.getDescription() + ", Whipped Cream";
    }
}
import java.util.Scanner;

public class CoffeeShopSimulator {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Выбор кофе
        System.out.print("Select your coffee (Espresso, Cappuccino, Latte): ");
        String coffeeType = scanner.nextLine();
        Coffee coffee = CoffeeFactory.createCoffee(coffeeType);

        // Выбор ингредиентов
        System.out.print("Would you like to add Milk? (y/n): ");
        if (scanner.nextLine().equalsIgnoreCase("y")) {
            coffee = new MilkDecorator(coffee);
        }

        System.out.print("Would you like to add Caramel Syrup? (y/n): ");
        if (scanner.nextLine().equalsIgnoreCase("y")) {
            coffee = new CaramelDecorator(coffee);
        }

        System.out.print("Would you like to add Whipped Cream? (y/n): ");
        if (scanner.nextLine().equalsIgnoreCase("y")) {
            coffee = new WhippedCreamDecorator(coffee);
        }

        // Печать итогового описания и стоимости
        System.out.println("\nYour order:");
        System.out.println("Description: " + coffee.getDescription());
        System.out.println("Total cost: $" + String.format("%.2f", coffee.getCost()));
    }
}
