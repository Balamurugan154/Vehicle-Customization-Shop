import java.util.*;

// Abstract Base Class (Abstraction)
abstract class Vehicle {
    private String brand;

    public Vehicle(String brand) {
        this.brand = brand;
    }

    public String getBrand() {
        return brand;
    }

    // Abstract Method
    public abstract Map<String, Integer> getCustomizations();

    // Polymorphism: Can override in subclasses
    public int calculateDeliveryDays(int numCustomizations) {
        return 2 + numCustomizations;
    }
}

// Subclasses (Inheritance + Polymorphism)
class Bike extends Vehicle {
    public Bike(String brand) {
        super(brand);
    }

    @Override
    public Map<String, Integer> getCustomizations() {
        Map<String, Integer> options = new LinkedHashMap<>();
        options.put("Alloy Wheels", 3000);
        options.put("Custom Seat Cover", 1000);
        options.put("LED Headlights", 1500);
        options.put("Performance Exhaust", 4500);
        options.put("Mobile Holder", 300);
        options.put("Racing Graphics", 1200);
        return options;
    }
}

class Scooter extends Vehicle {
    public Scooter(String brand) {
        super(brand);
    }

    @Override
    public Map<String, Integer> getCustomizations() {
        Map<String, Integer> options = new LinkedHashMap<>();
        options.put("Mobile Charger", 500);
        options.put("Foot Mat", 300);
        options.put("Bluetooth Speakers", 1000);
        options.put("Side Stand Sensor", 700);
        options.put("Stylish Handle Grip", 400);
        options.put("Anti-Theft Lock", 900);
        return options;
    }
}

class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }

    @Override
    public Map<String, Integer> getCustomizations() {
        Map<String, Integer> options = new LinkedHashMap<>();
        options.put("Leather Seats", 8000);
        options.put("Touchscreen Display", 12000);
        options.put("Reverse Camera", 5000);
        options.put("Alloy Wheels", 7000);
        options.put("Sunroof Installation", 25000);
        options.put("Surround Sound System", 15000);
        options.put("Dash Cam", 4000);
        options.put("Ambient Interior Lighting", 3500);
        return options;
    }
}

// Encapsulation: Handles customization logic
class Customization {
    private static final Map<String, Integer> colorOptions = new LinkedHashMap<>();
    private static final Map<String, Integer> stickerOptions = new LinkedHashMap<>();

    static {
        colorOptions.put("Matte Black", 2500);
        colorOptions.put("Glossy Red", 2000);
        colorOptions.put("Pearl White", 2200);
        colorOptions.put("Metallic Blue", 2700);

        stickerOptions.put("Flames", 1000);
        stickerOptions.put("Racing Stripes", 1200);
        stickerOptions.put("Animal Print", 800);
        stickerOptions.put("Custom Name Sticker", 500);
    }

    public static Map<String, Integer> getColorOptions() {
        return colorOptions;
    }

    public static Map<String, Integer> getStickerOptions() {
        return stickerOptions;
    }
}

// Handles bill generation
class BillGenerator {
    private static final double GST = 0.18;

    public static void generateBill(Vehicle vehicle, Map<String, Integer> selected) {
        double total = 0;
        System.out.println("\n-------- BILL --------");
        System.out.println("Vehicle Type : " + vehicle.getClass().getSimpleName());
        System.out.println("Brand        : " + vehicle.getBrand());
        System.out.println("\nCustomizations:");
        System.out.printf("%-35s %10s\n", "Feature", "Cost (₹)");
        System.out.println("-----------------------------------------------");

        for (Map.Entry<String, Integer> entry : selected.entrySet()) {
            System.out.printf("%-35s %10d\n", entry.getKey(), entry.getValue());
            total += entry.getValue();
        }

        double gst = total * GST;
        double finalAmount = total + gst;
        int delivery = vehicle.calculateDeliveryDays(selected.size());

        System.out.println("-----------------------------------------------");
        System.out.printf("%-35s %10.2f\n", "Subtotal", total);
        System.out.printf("%-35s %10.2f\n", "GST (18%)", gst);
        System.out.printf("%-35s %10.2f\n", "Total Amount", finalAmount);
        System.out.printf("%-35s %10s\n", "Delivery in", delivery + " days");
        System.out.println("-----------------------------------------------");
        System.out.println("Thank you for choosing us!");
    }
}

// Main Application
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Vehicle vehicle = null;

        System.out.println("🚗 Welcome to Vehicle Customization Shop!");
        System.out.print("Enter Vehicle Type (bike/car/scooter): ");
        String type = sc.nextLine().trim().toLowerCase();

        System.out.print("Enter Vehicle Brand: ");
        String brand = sc.nextLine().trim();

        switch (type) {
            case "bike":
                vehicle = new Bike(brand);
                break;
            case "car":
                vehicle = new Car(brand);
                break;
            case "scooter":
                vehicle = new Scooter(brand);
                break;
            default:
                System.out.println("Invalid vehicle type.");
                return;
        }

        Map<String, Integer> selectedCustomizations = new LinkedHashMap<>();
        Map<String, Integer> options = vehicle.getCustomizations();
        List<String> keys = new ArrayList<>(options.keySet());

        System.out.println("\n🛠 Customization Options:");
        for (int i = 0; i < keys.size(); i++) {
            System.out.println((i + 1) + ". " + keys.get(i) + " - ₹" + options.get(keys.get(i)));
        }

        System.out.print("Enter options to add (space-separated): ");
        String[] selected = sc.nextLine().split(" ");
        for (String s : selected) {
            try {
                int idx = Integer.parseInt(s) - 1;
                if (idx >= 0 && idx < keys.size()) {
                    String feat = keys.get(idx);
                    selectedCustomizations.put(feat, options.get(feat));
                }
            } catch (Exception e) {
                System.out.println("Invalid input: " + s);
            }
        }

        // Color Option
        List<String> colorList = new ArrayList<>(Customization.getColorOptions().keySet());
        System.out.println("\n🎨 Color Options:");
        for (int i = 0; i < colorList.size(); i++)
            System.out.println((i + 1) + ". " + colorList.get(i) + " - ₹" + Customization.getColorOptions().get(colorList.get(i)));
        System.out.print("Select color (0 to skip): ");
        int color = sc.nextInt();
        sc.nextLine();
        if (color > 0 && color <= colorList.size()) {
            String choice = colorList.get(color - 1);
            selectedCustomizations.put("Color: " + choice, Customization.getColorOptions().get(choice));
        }

        // Sticker Option
        List<String> stickerList = new ArrayList<>(Customization.getStickerOptions().keySet());
        System.out.println("\n🔖 Sticker Options:");
        for (int i = 0; i < stickerList.size(); i++)
            System.out.println((i + 1) + ". " + stickerList.get(i) + " - ₹" + Customization.getStickerOptions().get(stickerList.get(i)));
        System.out.print("Select sticker (0 to skip): ");
        int sticker = sc.nextInt();
        sc.nextLine();
        if (sticker > 0 && sticker <= stickerList.size()) {
            String choice = stickerList.get(sticker - 1);
            selectedCustomizations.put("Sticker: " + choice, Customization.getStickerOptions().get(choice));
        }

        // Ask if user wants to remove any selected customization
        if (!selectedCustomizations.isEmpty()) {
            System.out.println("\n🧹 Do you want to remove any selected customization?");
            System.out.println("Selected Customizations:");
            List<String> selectedKeys = new ArrayList<>(selectedCustomizations.keySet());
            for (int i = 0; i < selectedKeys.size(); i++) {
                System.out.println((i + 1) + ". " + selectedKeys.get(i) + " - ₹" + selectedCustomizations.get(selectedKeys.get(i)));
            }

            System.out.print("Enter numbers to remove (space-separated, 0 to skip): ");
            String[] toRemove = sc.nextLine().split(" ");
            for (String s : toRemove) {
                try {
                    int idx = Integer.parseInt(s) - 1;
                    if (idx >= 0 && idx < selectedKeys.size()) {
                        String keyToRemove = selectedKeys.get(idx);
                        selectedCustomizations.remove(keyToRemove);
                        System.out.println("Removed: " + keyToRemove);
                    }
                } catch (Exception e) {
                    System.out.println("Invalid input: " + s);
                }
            }
        }

        // Generate Bill
        BillGenerator.generateBill(vehicle, selectedCustomizations);
        System.out.println("\n🎉 Visit us again for more customizations! 🎉");
    }
}
