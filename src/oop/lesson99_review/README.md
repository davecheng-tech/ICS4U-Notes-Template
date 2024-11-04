
# Identifying Flaws in Object-Oriented Design

Below are five examples of flawed OOP designs. Each example presents a scenario with common OOP mistakes such as poor class hierarchy, inappropriate use of inheritance, inefficient data handling, and other design issues. 

Identify the flaw, explain the problem, and propose a corrected design.

## 1. Vehicle Management System

**Scenario and UML:**

A system for managing vehicles uses a class structure where `Car`, `Motorcycle`, and `Bicycle` all inherit from `Vehicle`, which includes an attribute `fuelType`. 

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

**Question:**  
What is the issue with having `fuelType` in the `Vehicle` class? How could you redesign the hierarchy to address this issue?

<br><br>

## 2. E-Commerce Product Catalog

**Scenario and UML:**

The e-commerce system has a `Product` class responsible for managing product details, calculating discounts, and handling inventory updates.

```plaintext
Product
├── name: String
├── price: double
├── inventory: int
├── calculateDiscount(): double
├── updateInventory(): void
```

**Question:**  
Identify the design issue in having `Product` manage both inventory and discount calculations. How would you improve this design?

<br><br>

## 3. Employee Management System

**Scenario and UML:**

An employee management system has separate classes for `FullTimeEmployee`, `PartTimeEmployee`, and `Intern`.

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

**Question:**  
Identify the redundancy in the current design and explain how it could be improved to avoid duplication.

<br><br>

## 4. Online Learning Platform

**Scenario and UML:**

An online learning platform has classes `Course`, `Student`, `Instructor`, and `CourseMaterial`. The `CourseMaterial` class is divided into multiple subclasses for different types of materials, such as `Video`, `TextDocument`, and `Quiz`, each with a `content` attribute.

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

**Question:**  
Explain the choice of using `Video`, `TextDocument`, and `Quiz` as subclasses of `CourseMaterial`. How could this design be simplified?

<br><br>

## 5. Banking System

**Scenario and UML:**

In a banking system, the `BankAccount` class directly exposes its balance as a public field, and methods like `withdraw` and `deposit` directly modify this field.

```plaintext
BankAccount
├── accountID: int
├── balance: double (public)
├── withdraw(amount: double): void
└── deposit(amount: double): void
```

**Question:**  
What’s wrong with exposing the `balance` field directly and allowing direct modification? How would you redesign this to ensure better encapsulation and data integrity?

<br><br>

# Example Assessment Rubric 

| Criteria                 | 4 - Excellent                                | 3 - Good                                      | 2 - Satisfactory                              | 1 - Needs Improvement                         |
|--------------------------|----------------------------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Identification of Flaws** | Clearly identifies the main flaw(s) in the design with logical reasoning | Identifies most flaws with reasonable explanations | Identifies some flaws but lacks detailed reasoning | Fails to identify major flaws or gives weak reasoning |
| **Explanation of Flaws**  | Provides a thorough, logical explanation of why the flaws are inefficient | Provides a reasonable explanation, missing minor details | Explanation is partial or lacks clarity | Little to no explanation or unclear reasoning |
| **Redesign Proposal**     | Suggests an effective redesign that fully addresses flaws and enhances efficiency | Redesign is mostly effective with minor gaps in efficiency | Redesign partially addresses flaws but leaves some inefficiencies | Redesign is ineffective or introduces new issues |
| **Use of OOP Principles** | Correctly applies OOP principles like inheritance, composition, and encapsulation in redesign | Mostly correct application with minor missteps | Partially correct application with several missteps | Misuse or lack of OOP principles in the redesign |
| **Clarity and Coherence** | Redesign and explanation are clear, well-structured, and coherent | Redesign is mostly clear, with minor coherence issues | Explanation is partially clear but lacks structure | Explanation and redesign are unclear or poorly structured |

