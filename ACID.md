## 🧩 ACID stands for:
test
A → Atomicity
C → Consistency
I → Isolation
D → Durability

এগুলো একসাথে একটা database transaction কে safe এবং reliable করে তোলে।


## 🔹 1️⃣ A – Atomicity (অ্যাটমিক বা অবিভাজ্যতা)

👉 “All or nothing” rule

মানে, একটি transaction-এর সব step পুরোপুরি সম্পন্ন হবে
না হলে একটাও হবে না।

🧠 Example:
```php
START TRANSACTION;

UPDATE accounts SET balance = balance - 1000 WHERE id = 1; -- send money
UPDATE accounts SET balance = balance + 1000 WHERE id = 2; -- receive money

COMMIT;
```

যদি মাঝপথে কোনো error হয় (যেমন 2nd query fail করে),
তাহলে পুরো transaction rollback হয়ে যাবে।

📘 অর্থাৎ —

টাকা কেটে গেলে অবশ্যই অন্য অ্যাকাউন্টে যাবে,
আর না গেলে আগের অবস্থায় ফিরে আসবে।

✅ Ensures data is not half updated.


## 🔹 2️⃣ C – Consistency (সঙ্গতি)

👉 Transaction-এর আগে এবং পরে database সবসময় valid state এ থাকতে হবে।

📘 Example:

যদি তোমার ব্যাংক balance negative না হতে পারে,
তাহলে transaction শেষে সেটা negative হবে না।

Database-এর rules (constraints, triggers, foreign keys, etc.)
transaction শেষে valid থাকতে হবে।

✅ Ensures data integrity.



## 🔹 3️⃣ I – Isolation (পৃথকতা)

👉 একাধিক transaction একসাথে চললেও একে অন্যকে interfere করবে না।

📘 Example:

দুইজন user একসাথে একই account থেকে টাকা তুলতে গেলে
একজনের কাজ শেষ না হওয়া পর্যন্ত অন্যজনের transaction “দেখবে না”।

এইটা dirty read, non-repeatable read, phantom read ইস্যুগুলা প্রতিরোধ করে।

✅ Ensures transactions don’t affect each other.



## 🔹 4️⃣ D – Durability (স্থিতিশীলতা)

👉 Once a transaction is committed, it’s permanent —
even if system crash হয়, power loss হয়, data lost হবে না।

📘 Database system committed data disk এ store করে রাখে (using logs, recovery systems)।

✅ Ensures data is never lost after commit.



















