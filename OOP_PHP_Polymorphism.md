
## 🧬 2. Polymorphism (পলিমরফিজম)

ধারণা:
Polymorphism মানে “বিভিন্ন রূপ”।
একই মেথড নাম ব্যবহার করে আলাদা ক্লাসে ভিন্ন ভিন্ন কাজ করা যায়।

👉 সহজভাবে বললে:
“একই নামের মেথড, কিন্তু বিভিন্ন ক্লাসে আলাদা আচরণ।”

🔹 উদাহরণ:
```php
<?php
interface Animal {
    public function makeSound();
}

class Dog implements Animal {
    public function makeSound() {
        echo "Bark! 🐶";
    }
}

class Cat implements Animal {
    public function makeSound() {
        echo "Meow! 🐱";
    }
}

// একই মেথড নাম, কিন্তু আলাদা ক্লাসে ভিন্ন কাজ
$animals = [new Dog(), new Cat()];

foreach ($animals as $animal) {
    $animal->makeSound(); 
    echo "<br>";
}
?>

```

### Output:
```php
Bark! 🐶  
Meow! 🐱
```

🗣️ বাংলায় ব্যাখ্যা:
এখানে makeSound() মেথডটা সব ক্লাসেই আছে, কিন্তু Dog ক্লাসে এটা “Bark!” বলে আর Cat ক্লাসে এটা “Meow!” বলে।
এইভাবে একই নামের মেথড বিভিন্ন রকমভাবে কাজ করছে — এটাকেই বলে Polymorphism।

🔹 উদাহরণ:

```php
<?php
// Parent Class
class Human {
    public function introduce() {
        echo "Hi, I am a human.<br>";
    }
}

// Child Class 1
class Student extends Human {
    public function introduce() {
        echo "Hi, I am a student. I love learning! 📚<br>";
    }
}

// Child Class 2
class Teacher extends Human {
    public function introduce() {
        echo "Hi, I am a teacher. I love teaching! 👩‍🏫<br>";
    }
}

// Child Class 3
class Doctor extends Human {
    public function introduce() {
        echo "Hi, I am a doctor. I save lives! 🩺<br>";
    }
}

// একই মেথড নাম, কিন্তু ভিন্ন ক্লাসে ভিন্ন কাজ
$people = [new Human(), new Student(), new Teacher(), new Doctor()];

foreach ($people as $person) {
    $person->introduce();
}
?>

```



### 🧠 Output:
```php
Hi, I am a human.
Hi, I am a student. I love learning! 📚
Hi, I am a teacher. I love teaching! 👩‍🏫
Hi, I am a doctor. I save lives! 🩺
```


🗣️ বাংলায় ব্যাখ্যা:

এখানে introduce() নামের মেথডটা সবার জন্য একই,
কিন্তু Student, Teacher, এবং Doctor ক্লাসে এটা ভিন্ন ভিন্নভাবে কাজ করছে।

👉 অর্থাৎ,

Student বলছে “I love learning!”

Teacher বলছে “I love teaching!”

Doctor বলছে “I save lives!”

একই মেথড নাম — কিন্তু বিভিন্ন রূপে আচরণ করছে।
এটাই Polymorphism (বহুরূপিতা)।
