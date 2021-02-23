---
title: Isolation levels 
date: 2021-02-03 22:24:34
tags:
---
In this article we will talk about **isolation levels** in RDBMS

​	If multiple transactions do not process the same data, they can run safely in parallel. Race conditions becomes inevitable when one transaction process data that is modyfied by another transaction. 

​	That is why it's important to deal properly in this situation. The strongest level of consistency that could provide database - **serializable isolation level.** It's like sequential running transactions if they share some data in database. How we can  achieve that level? Just simply put locks on data that we have read or write. And no one can access data while we unlock that data. It means no one can access data and there are a wait look on it, after data was unlocked transation take process data. If we use such approach for every transcations that we run in database we get big performance issue. And for this purposes there are exists  another weak levels of isolations that could give guarantes with conditions to process transactions.  

**Read commited**

​	The default level in many databases that gives you two guarantees. Transaction reads only commit data. It's impossible to read data that was uncommit. For example in case when you some transaction start modifying data and at some moment of time get aborted. There is no middle time transaction that was read uncommited data that was never existed. Another synonym for this - **no dirty reads**. The same works for writes. You never write data that wasn't commited, **no drity writes.** Implementing no dirty writes like putting lock on data before modyfing data. It must wait until lock asquired before modifying data. Most databases stores old and new value of data to prevent dirty writes. 

**Repeatable read**

​	Suppose you two have account in bank with 500$ on each. And you wanna get total sum of your money. You read first accont and get 500$. At this point of time another transactions start transfer 100$ from one account to another. Transaction increments first account by 100$ and decrements by 100$ on second account and commited succefully. You continue reading second account money and get 400$ in it. So totally you get 900$, but in fact it must be 1000$. This phenomenon names non repeatable read. And Repeatable read isolation level guarantees to you to escape **non repeatable read**. To implement this behaviour you need to keep snapshot isolation in your database, that also relates to storing different versions of your data**(MVCC)** while transactions are running under this level. Every transaction has it's own auto incrementing id. And transactions can differentiate data by applying knowledge from this ids. 

​	Both levels don't prevent from **lost update,** that happens when you need read value, modify it and save back. If two transcation do this concurenly you will probably lose one of the modification, because some transaction don't consider first modification and rewrite value. For this problem there are several solutions: 

**Atomic write**

```sql
 UPDATE counters SET value = value + 1 WHERE key = 'foo';
```

In given query database setup exclusive lock on value, so that no one can access value while it inrements it. 

Another way to use **explicit lock**: 

```sql
BEGIN TRANSACTION;
SELECT * FROM figures
WHERE name = 'robot' AND game_id = 222
FOR UPDATE;
-- Check whether move is valid, then update the position
-- of the piece that was returned by the previous SELECT.
UPDATE figures SET position = 'c4' WHERE id = 1234;
COMMIT;
```

The key for lock is `FOR UPDATE` statements, that locks rows and other transactions considering this rows waits until lock is released. 

**Automatically detecting lost update** is one of the the way to deal situation. In this case database automatically find losted updates and abort transaction or give another try again. 

If you don't use transactions it's possible to prevent lost update by doing **compare and set**: 

```sql
UPDATE wiki_pages SET content = 'new content'
WHERE id = 1234 AND content = 'old content';
```

Keep in mind to handle situation when you need to try again if no updates happened. 

**Phantoms** phenomena can't also be preveneted by applying given isolation levels. Phantoms happens when you consider data that can't be attached to some lock in database, for example while registering in service, you select accounts with given username and if there is no accounts you create account and concurrent transaction could also successfully repeat actions. 

**Serializable isolation**

The strongest form of guarantee. There are 3 ways to implement this:

1. Serial processing of transactions 
2. Two phase locking 
3. Optimistic concurrency control 