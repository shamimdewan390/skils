## 🧩 1. Encapsulation (এনক্যাপসুলেশন)

ধারণা:
Encapsulation মানে হচ্ছে একটি ক্লাসের ভেতরে ডেটা (property) এবং ফাংশন (method) একসাথে রাখা, এবং বাইরে থেকে সরাসরি সেই ডেটা অ্যাক্সেস করা বন্ধ রাখা।
এতে করে ডেটা সুরক্ষিত (protected) থাকে এবং ভুলভাবে পরিবর্তন হওয়ার সম্ভাবনা কমে যায়।

👉 সহজভাবে বললে:
“Data hide করে শুধুমাত্র দরকারি method দিয়েই access করার ব্যবস্থা করা।”

🔹 উদাহরণ:

```php
<?php
class BankAccount {
    private $balance; // সরাসরি বাইরে থেকে অ্যাক্সেস করা যাবে না

    public function __construct($balance) {
        $this->balance = $balance;
    }

    // balance বের করার জন্য getter
    public function getBalance() {
        return $this->balance;
    }

    // balance বাড়ানোর জন্য setter
    public function deposit($amount) {
        if ($amount > 0) {
            $this->balance += $amount;
        }
    }
}

$account = new BankAccount(5000);
$account->deposit(1500);
echo $account->getBalance(); // Output: 6500
?>

```

🗣️ বাংলায় ব্যাখ্যা:
এখানে $balance প্রপার্টি private দেওয়া আছে, তাই বাইরে থেকে $account->balance লেখা যাবে না।
শুধুমাত্র deposit() এবং getBalance() মেথডের মাধ্যমে ব্যালান্স দেখা ও পরিবর্তন করা যাবে।
এটাই encapsulation — ডেটাকে নিরাপদ রাখা এবং কন্ট্রোলড এক্সেস দেওয়া।

🔹 উদাহরণ:


```php
<?php
class Student {
    private $name;
    private $grade;

    // কনস্ট্রাক্টর দিয়ে ডেটা সেট করা
    public function __construct($name, $grade) {
        $this->name = $name;
        $this->grade = $grade;
    }

    // নাম বের করার জন্য getter
    public function getName() {
        return $this->name;
    }

    // গ্রেড বের করার জন্য getter
    public function getGrade() {
        return $this->grade;
    }

    // গ্রেড আপডেট করার জন্য setter
    public function setGrade($grade) {
        if ($grade >= 0 && $grade <= 100) {
            $this->grade = $grade;
        } else {
            echo "Invalid grade value!";
        }
    }
}

// অবজেক্ট তৈরি করা
$student = new Student("Samreen", 85);

// গ্রেড দেখা
echo $student->getName() . "'s grade is: " . $student->getGrade() . "<br>";

// গ্রেড আপডেট করা (setter দিয়ে)
$student->setGrade(90);
echo "Updated grade: " . $student->getGrade();
?>

```

🗣️ বাংলায় ব্যাখ্যা:

এখানে আমরা $name এবং $grade — এই দুইটা property private রেখেছি।
অর্থাৎ, ক্লাসের বাইরে থেকে এগুলো সরাসরি পরিবর্তন বা পড়া যাবে না।

👉 যদি তুমি ক্লাসের বাইরে থেকে $student->grade = 60; লিখতে চাও, সেটা কাজ করবে না।
তুমি কেবল setGrade() মেথডের মাধ্যমে নিরাপদভাবে পরিবর্তন করতে পারবে।
এইভাবে ডেটা লুকিয়ে রাখা (data hiding) এবং নিয়ন্ত্রিত অ্যাক্সেস দেওয়া (controlled access) — এটিই Encapsulation।


