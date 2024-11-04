## 1. Vehicle Management System - Inappropriate Use of Inheritance

**Scenario and UML:**

A system for managing vehicles uses a class structure where `Car`, `Motorcycle`, and `Bicycle` all inherit from `Vehicle`, which includes an attribute `fuelType`. However, `Bicycle` inherits `fuelType` even though it doesn’t use fuel, leading to irrelevant properties.

```plaintext
Vehicle
├── make: String
├── model: String
├── fuelType: String
├── mileage: double

Car (inherits Vehicle)
├── seatingCapacity: int

Motorcycle (inherits Vehicle)
├── hasSidecar: boolean

Bicycle (inherits Vehicle)
└── gearCount: int
```

**Solution and Explanation:**  
The `fuelType` attribute doesn’t apply to `Bicycle`, which causes irrelevant properties to exist in some subclasses. A better approach could be to split `Vehicle` into `PoweredVehicle` (with `fuelType`) and `NonPoweredVehicle` (without `fuelType`). `Car` and `Motorcycle` would inherit from `PoweredVehicle`, while `Bicycle` would inherit from `NonPoweredVehicle`.

```plaintext
PoweredVehicle
├── make: String
├── model: String
├── mileage: double
├── fuelType: String

Car (inherits PoweredVehicle)
├── seatingCapacity: int

Motorcycle (inherits PoweredVehicle)
└── hasSidecar: boolean

NonPoweredVehicle
├── make: String
├── model: String
├── mileage: double

Bicycle (inherits NonPoweredVehicle)
└── gearCount: int
```

Or, another possible implementation:

```plaintext
Vehicle
├── make: String
├── model: String
├── mileage: double

PoweredVehicle (inherits Vehicle)
└── fuelType: String

Car (inherits PoweredVehicle)
└── seatingCapacity: int

Motorcycle (inherits PoweredVehicle)
└── hasSidecar: boolean

Bicycle (inherits Vehicle)
└── gearCount: int
```

<br><br>

## 2. E-Commerce Product Catalog - Violation of Single Responsibility Principle

**Scenario and UML:**

The e-commerce system has a `Product` class responsible for managing product details, calculating discounts, and handling inventory updates. This makes the `Product` class overly complex.

```plaintext
Product
├── name: String
├── price: double
├── inventory: int
├── calculateDiscount(): double
└── updateInventory(): void
```

**Solution and Explanation:**  
This design is trying to do too much with the `Product` class. (In OOP design, one of the foundational rules is called the Single Responsibility Principle or SRP.) It is better to split responsibilities into separate classes: `Product` for product details, `DiscountCalculator` for discount-related operations, and `InventoryManager` for inventory updates. This reduces complexity and makes each class easier to maintain and extend.

```plaintext
Product
├── name: String
├── price: double
├── inventory: int
├── setInventory(int): void
├── getInventory(): int
├── setPrice(double): void
└── getPrice(): double

DiscountCalculator
└── applyDiscount(double, Product): void (static method)

InventoryManager
└── updateInventory(int, Product): void (static method)
```

<br><br>


## 3. Employee Management System - Redundant Class Structure

**Scenario and UML:**

An employee management system has separate classes for `FullTimeEmployee`, `PartTimeEmployee`, and `Intern`, with duplicated properties (`name`, `ID`, `email`) and methods (`calculateSalary()`).

```plaintext
FullTimeEmployee
├── name: String
├── ID: int
├── email: String
└── calculateSalary(): double

PartTimeEmployee
├── name: String
├── ID: int
├── email: String
└── calculateSalary(): double

Intern
├── name: String
├── ID: int
├── email: String
└── calculateSalary(): double
```

**Solution and Explanation:**  
The current design duplicates common properties and methods. Instead, an `Employee` base class could be created with shared attributes (`name`, `ID`, `email`) and methods (`calculateSalary()`). `FullTimeEmployee`, `PartTimeEmployee`, and `Intern` would inherit from `Employee`, allowing specialization where needed.

```plaintext
Employee
├── name: String
├── ID: int
├── email: String
├── calculateSalary(): double

FullTimeEmployee (inherits Employee)
└── specializedMethod(): void

PartTimeEmployee (inherits Employee)
└── specializedMethod(): void

Intern
└── specializedMethod(): void
```

<br><br>

## 4. Online Learning Platform - Poor Use of Inheritance and Composition

**Scenario and UML:**

An online learning platform has classes `Course`, `Student`, `Instructor`, and `CourseMaterial`. The `CourseMaterial` class is unnecessarily divided into multiple subclasses for different types of materials, such as `Video`, `TextDocument`, and `Quiz`, each with a `content` attribute, leading to a bloated hierarchy.

```plaintext
CourseMaterial
└── content: String

Video (inherits CourseMaterial)
└── content: String

TextDocument (inherits CourseMaterial)
└── content: String

Quiz (inherits CourseMaterial)
└── content: String
```

**Solution and Explanation:**  
Since `Video`, `TextDocument`, and `Quiz` only differ in content type but have identical structures, a single `CourseMaterial` class with a `type` attribute (e.g., "video", "text", "quiz") would be more efficient. This design reduces the need for multiple subclasses and keeps the codebase simpler.


```plaintext
CourseMaterial
├── type: String
└── content: String
```

<br><br>

## 5. Banking System - Poor Encapsulation

**Scenario and UML:**

In a banking system, the `BankAccount` class directly exposes its balance as a public field, and methods like `withdraw` and `deposit` directly modify this field without validation.

```plaintext
BankAccount
├── accountID: int
├── balance: double (public)
├── withdraw(amount: double): void
└── deposit(amount: double): void
```

**Solution and Explanation:**  
Exposing `balance` as a public field violates encapsulation and allows unauthorized modification. A better approach would be to make `balance` private and access it through `getBalance()`. The `withdraw` and `deposit` methods should include validation checks to prevent invalid transactions (e.g., withdrawing more than the available balance). This design ensures that data is accessed safely and only modified through controlled methods.

```plaintext
BankAccount
├── accountID: int
├── private balance: double
├── withdraw(amount: double): void
└── deposit(amount: double): void
```

<br><br>
