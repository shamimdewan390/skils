#SOLID principles

## Explain the SOLID principles in PHP.

SOLID stands for five design principles that improve software maintainability:

S - Single Responsibility Principle: A class should have only one reason to change.

O - Open/Closed Principle: Classes should be open for extension but closed for modification.

L - Liskov Substitution Principle: Subtypes must be replaceable with their parent class.

I - Interface Segregation Principle: Avoid forcing classes to implement unused methods.

D - Dependency Inversion Principle: Depend on abstractions, not concrete implementations.

## bed example
```
class User {
    public function saveToDatabase() {
        // Code to save user to DB
    }

    public function sendWelcomeEmail() {
        // Code to send email
    }
}
```
