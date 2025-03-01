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


#2. Open/Closed Principle (OCP)
A class should be open for extension but closed for modification.

##Bad Example (Violating OCP)
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





























