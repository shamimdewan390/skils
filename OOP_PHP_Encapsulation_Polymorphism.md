🧩 1. Encapsulation (এনক্যাপসুলেশন)

ধারণা:
Encapsulation মানে হচ্ছে একটি ক্লাসের ভেতরে ডেটা (property) এবং ফাংশন (method) একসাথে রাখা, এবং বাইরে থেকে সরাসরি সেই ডেটা অ্যাক্সেস করা বন্ধ রাখা।
এতে করে ডেটা সুরক্ষিত (protected) থাকে এবং ভুলভাবে পরিবর্তন হওয়ার সম্ভাবনা কমে যায়।

👉 সহজভাবে বললে:
“Data hide করে শুধুমাত্র দরকারি method দিয়েই access করার ব্যবস্থা করা।”

🔹 উদাহরণ:

bash```
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
