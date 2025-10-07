# SOLID principles

## Explain the SOLID principles in PHP.

SOLID stands for five design principles that improve software maintainability:

S - Single Responsibility Principle: A class should have only one reason to change.

O - Open/Closed Principle: Classes should be open for extension but closed for modification.

L - Liskov Substitution Principle: Subtypes must be replaceable with their parent class.

I - Interface Segregation Principle: Avoid forcing classes to implement unused methods.

D - Dependency Inversion Principle: Depend on abstractions, not concrete implementations.

# 1. Single Responsibility Principle (SRP)

👉 একটি ক্লাসের শুধু একটাই কাজ থাকা উচিত।

অর্থাৎ, এক ক্লাস একাধিক দায়িত্ব নেবে না।
যদি এক ক্লাসে অনেক কাজ রাখো (যেমন: ডাটাবেজ, ইমেইল, লগ সব একসাথে), তাহলে কোড মেইনটেইন করা কঠিন হয়।

## Bad Example (Violating SRP)

The User class handles both user data and email notifications.
```php
<?php
// ❌ খারাপ উদাহরণ
class User {
    public function createUser($data) {
        // ইউজার তৈরি
    }

    public function sendWelcomeEmail($email) {
        // ইমেইল পাঠানো
    }
}

```
```php
✅ ভালো উদাহরণ:
class User {
    public function createUser($data) {
        // ইউজার তৈরি
    }
}

class EmailService {
    public function sendWelcomeEmail($email) {
        // ইমেইল পাঠানো
    }
}
```
Another example:
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

এটা মানে হলো:

Open for Extension (এক্সটেনশন)

নতুন ফিচার যোগ করা যাবে।

পুরনো কোডকে চেঞ্জ না করেই নতুন ফাংশনালিটি যোগ করা যায়।

Closed for Modification (মডিফিকেশন)

বিদ্যমান কোড পরিবর্তন করা যাবে না।

কারণ যদি পরিবর্তন করা হয়, তাহলে পুরনো ফিচার ভেঙে যেতে পারে।

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

কথায় সংজ্ঞা:

“যে কোনো child class, তার parent class-এর জায়গায় ব্যবহার করা যায় এবং কোড ঠিকভাবে কাজ করবে।”

অর্থাৎ: Parent class-এর behaviour child class-এর মাধ্যমে ভাঙা যাবে না।
এই principle Barbara Liskov নামের বিজ্ঞানীর নামে নামকরণ করা হয়েছে।

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

👉 বড় ইন্টারফেসকে ছোট ছোট নির্দিষ্ট ইন্টারফেসে ভাগ করা উচিত।

অর্থাৎ, ক্লাসকে এমন ইন্টারফেস implement করতে বাধ্য কোরো না যার কিছু মেথড তার দরকারই নেই।

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
## another example


## Bad Example (Violating DIP)
The Order class is tightly coupled with MySQLDatabase.
```php
class EmailService {
    public function sendEmail($message) {
        echo "Sending Email: $message\n";
    }
}

class Notification {
    private $emailService;

    public function __construct() {
        $this->emailService = new EmailService(); // Direct dependency (Bad)
    }

    public function send($message) {
        $this->emailService->sendEmail($message);
    }
}

// Usage
$notification = new Notification();
$notification->send("Hello, this is an email notification!");

```

## Good Example (Following DIP)
Use dependency injection with an interface.

```php
// Step 1: Define an abstraction (interface)
interface Notifier {
    public function send($message);
}

// Step 2: Create concrete implementations
class EmailService implements Notifier {
    public function send($message) {
        echo "Sending Email: $message\n";
    }
}

class SMSService implements Notifier {
    public function send($message) {
        echo "Sending SMS: $message\n";
    }
}

// Step 3: Notification class depends on abstraction
class Notification {
    private $notifier;

    public function __construct(Notifier $notifier) {
        $this->notifier = $notifier; // Inject dependency
    }

    public function send($message) {
        $this->notifier->send($message);
    }
}

// Usage
$emailNotification = new Notification(new EmailService());
$emailNotification->send("Hello via Email!");

$smsNotification = new Notification(new SMSService());
$smsNotification->send("Hello via SMS!");

```
```php
class WhatsAppService implements Notifier {
    public function send($message) {
        echo "Sending WhatsApp Message: $message\n";
    }
}

// Using WhatsApp notification
$whatsappNotification = new Notification(new WhatsAppService());
$whatsappNotification->send("Hello via WhatsApp!");
```

### Another example

```php
<?php

// Interface (Contract)
interface MessageService {
    public function sendMessage($msg);
}

// EmailService implements the interface
class EmailService implements MessageService {
    public function sendMessage($msg) {
        echo "Email sent: $msg<br>";
    }
}

// SMSService implements the interface
class SMSService implements MessageService {
    public function sendMessage($msg) {
        echo "SMS sent: $msg<br>";
    }
}

// User class depends on interface, not concrete class
class User {
    private $messageService;

    // Dependency Injection
    public function __construct(MessageService $messageService) {
        $this->messageService = $messageService;
    }

    public function notify($msg) {
        $this->messageService->sendMessage($msg);
    }
}

// =======================
// Usage Examples
// =======================

// 1️⃣ Email Notification
$emailService = new EmailService();
$user1 = new User($emailService);
$user1->notify("Hello via Email!"); // Output: Email sent: Hello via Email!

// 2️⃣ SMS Notification
$smsService = new SMSService();
$user2 = new User($smsService);
$user2->notify("Hello via SMS!"); // Output: SMS sent: Hello via SMS!
?>

```

































