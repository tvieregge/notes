source: https://www.2ndquadrant.com/en/blog/postgresql-anti-patterns-read-modify-write-cycles/

[[postgress]] has a bunch of [[concurrency]] options

Easiest option is to push the work into PG
```
SELECT balance FROM accounts WHERE user_id = 1; (returns 300)
UPDATE balance SET balance = 200 WHERE user_id = 1; (300 – 100 = 200)
COMMIT;
```
Turns into
```
UPDATE accounts SET balance = balance - 100 WHERE user_id = 1; (sets balance=200)
```
Tada!

Row level locking is usually the easiest to apply to an existing solution

SERIALIZABLE transactions and Optimistic concurrency control are two other options