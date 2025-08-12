🚗 Vehicle Customization Shop (Java OOP Project)
📌 Overview
This project is a Java console-based application that allows users to select a vehicle type (Bike, Car, or Scooter), choose from a list of customizations, and generate a bill with GST and delivery details.
It demonstrates Object-Oriented Programming (OOP) concepts including:

Abstraction (Abstract class Vehicle)

Inheritance (Bike, Car, Scooter)

Polymorphism (Overridden methods)

Encapsulation (Customization handling)

Composition (Bill generation system)

🎯 Features
Select vehicle type and brand.

Choose custom features (Alloy Wheels, Touchscreen Display, Sunroof, etc.).

Choose color and sticker customizations.

Option to remove unwanted customizations before billing.

Automatic bill generation with:

Subtotal

GST (18%)

Final amount

Estimated delivery days

🛠 Technologies Used
Java (JDK 8+)

OOP Principles

Collections Framework (Map, List, LinkedHashMap, etc.)

Scanner for user input

📂 Project Structure
css
Copy
Edit
Main.java
├── Vehicle (Abstract Class)
│   ├── Bike
│   ├── Scooter
│   └── Car
├── Customization
├── BillGenerator
└── Main (Program Entry Point)
📖 How to Run
Clone or download the repository.

Open the project in any Java IDE (Eclipse, IntelliJ, NetBeans) or terminal.

Compile and run:

bash
Copy
Edit
javac Main.java
java Main
Follow the on-screen prompts.

💻 Sample Output
mathematica
Copy
Edit
🚗 Welcome to Vehicle Customization Shop!
Enter Vehicle Type (bike/car/scooter): car
Enter Vehicle Brand: Honda

🛠 Customization Options:
1. Leather Seats - ₹8000
2. Touchscreen Display - ₹12000
...
Enter options to add (space-separated): 1 3 5

🎨 Color Options:
1. Matte Black - ₹2500
...
Select color (0 to skip): 2

🔖 Sticker Options:
1. Flames - ₹1000
...
Select sticker (0 to skip): 1

🧹 Do you want to remove any selected customization?
...

-------- BILL --------
Vehicle Type : Car
Brand        : Honda
...
Total Amount : ₹XXXX.XX
Delivery in  : X days
-----------------------------------------------
Thank you for choosing us!
📚 OOP Concepts Used
Abstraction: Vehicle class defines a template for vehicles.

Inheritance: Bike, Car, and Scooter inherit from Vehicle.

Polymorphism: Overridden getCustomizations() and calculateDeliveryDays() methods.

Encapsulation: Customization class hides internal customization data.

Composition: BillGenerator works independently but is used inside Main.

📌 Future Enhancements
Save bills to a file.

Add more vehicle types.

Introduce multiple quantity orders.

Create a GUI version
