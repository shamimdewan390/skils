# SOLID principles

## Explain the SOLID principles in PHP.

SOLID stands for five design principles that improve software maintainability:

S - Single Responsibility Principle: A class should have only one reason to change.

O - Open/Closed Principle: Classes should be open for extension but closed for modification.

L - Liskov Substitution Principle: Subtypes must be replaceable with their parent class.

I - Interface Segregation Principle: Avoid forcing classes to implement unused methods.

D - Dependency Inversion Principle: Depend on abstractions, not concrete implementations.

# 1. Single Responsibility Principle (SRP)

## Bad Example (Violating SRP)

The User class handles both user data and email notifications.
```php
class User {
    public function saveToDatabase() {
        // Code to save user to DB
    }

    public function sendWelcomeEmail() {
        // Code to send email
    }
}
```
This violates SRP because the class has two responsibilities: handling user data and sending emails.

## Good Example (Following SRP)
Separate classes for each responsibility.
```php
class User {
    public function saveToDatabase() {
        // Code to save user to DB
    }
}

class EmailService {
    public function sendWelcomeEmail(User $user) {
        // Code to send email
    }
}
```


# 2. Open/Closed Principle (OCP)
A class should be open for extension but closed for modification.

## Bad Example (Violating OCP)
Every time a new payment method is added, we modify the Payment class.

```php
class Payment {
    public function process($type) {
        if ($type == 'paypal') {
            // Process PayPal
        } elseif ($type == 'stripe') {
            // Process Stripe
        }
    }
}
```

Good Example (Following OCP)

Use polymorphism to extend functionality without modifying existing code.
```php
interface PaymentMethod {
    public function pay();
}

// PayPal Implementation
class PayPal implements PaymentMethod {
    public function pay() {
        echo "Processing payment through PayPal...\n";
    }
}

// Stripe Implementation
class Stripe implements PaymentMethod {
    public function pay() {
        echo "Processing payment through Stripe...\n";
    }
}

// PaymentProcessor
class PaymentProcessor {
    public function process(PaymentMethod $paymentMethod) {
        $paymentMethod->pay();
    }
}

// Using PayPal
$paypal = new PayPal();
$processor = new PaymentProcessor();
$processor->process($paypal); // Output: Processing payment through PayPal...

// Using Stripe
$stripe = new Stripe();
$processor->process($stripe); // Output: Processing payment through Stripe...

```

# 3. Liskov Substitution Principle (LSP)

Derived classes should be substitutable for their base classes.

## Bad Example (Violating LSP) 

A Bird class assumes all birds can fly.
```php
class Bird {
    public function fly() {
        return "Flying";
    }
}

class Penguin extends Bird {
    public function fly() {
        throw new Exception("Penguins can't fly!");
    }
}
```
The Penguin class violates LSP because it breaks the expected behavior.

## Good Example (Following LSP)

Separate flying and non-flying birds.
```php
interface Bird {
    public function move();
}

class FlyingBird implements Bird {
    public function move() {
        return "Flying";
    }
}

class Penguin implements Bird {
    public function move() {
        return "Swimming";
    }
}
```

# 4. Interface Segregation Principle (ISP)

A class should not be forced to implement interfaces it does not use.

## Bad Example (Violating ISP)
The Worker interface forces Robot to implement eat(), which doesn’t make sense.

```php
interface Worker {
    public function work();
    public function eat();
}

class HumanWorker implements Worker {
    public function work() {
        return "Working";
    }

    public function eat() {
        return "Eating";
    }
}

class RobotWorker implements Worker {
    public function work() {
        return "Working";
    }

    public function eat() {
        throw new Exception("Robots don't eat!");
    }
}
```

## Good Example (Following ISP)
Split interfaces into smaller ones.

```php
interface Workable {
    public function work();
}

interface Eatable {
    public function eat();
}

class HumanWorker implements Workable, Eatable {
    public function work() {
        return "Working";
    }

    public function eat() {
        return "Eating";
    }
}

class RobotWorker implements Workable {
    public function work() {
        return "Working";
    }
}
```

# 5. Dependency Inversion Principle (DIP)
High-level modules should not depend on low-level modules. Both should depend on abstractions.

## Bad Example (Violating DIP)
The Order class is tightly coupled with MySQLDatabase.
```php
class MySQLDatabase {
    public function connect() {
        return "Connected to MySQL";
    }
}

class Order {
    private $db;

    public function __construct() {
        $this->db = new MySQLDatabase(); // Hard dependency
    }

    public function save() {
        return $this->db->connect();
    }
}
```

## Good Example (Following DIP)
Use dependency injection with an interface.

```php
interface Database {
    public function connect();
}

class MySQLDatabase implements Database {
    public function connect() {
        return "Connected to MySQL";
    }
}

class Order {
    private $db;

    public function __construct(Database $db) {
        $this->db = $db;
    }

    public function save() {
        return $this->db->connect();
    }
}

// Now we can easily switch databases
$database = new MySQLDatabase();
$order = new Order($database);
```





































