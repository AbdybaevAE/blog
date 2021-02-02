---
title: ACID
date: 2021-02-02 21:39:03
tags:
---

The safety guarantees provided by transactions are often know as acronym **ACID**, that stands for **Atomacity, Consistency, Isolation and Durabilty**. It's important to differentiate from **BASE** acronym which stands for Basically Available Soft State, Eventual consistency. ACID relates to transactions, while BASE it's more about system. Let's describe each letter sequentially.

**Atomacity**

​	Imagine situation where you wanna send a multiple write queries to database and unfortunately something bad happened between query processing. Process crashes or network interrrupt or someone unplug electrical cable. How you fix this situation? Send write queries again? This thing can happen everywhere and every time, that is why transcations provide such a good thing atomaticy. Something that you can't break into smaller parts and processed by database like a one query. By this property possible solution would be to abord all writes within this transaction. And if run your database after crash transation would be reject as not completed. This works by transcation journal.  

**Consistency**

​	Atomacity, durability, isolation - properties of database, while consistency - property of application. It's up to you to decided wether you application in consistent way or not. And you can relate to ACID properties as an ultimate truth to stay your data consistent. 

**Isolation**

​	Databases are concurrent. It's often happens when transactions processes concurently and if some transcation will see middle results of another transaction that could be aborted or commited we can get wrong results by condsidering not commited results. And for this case isolation make possible to run transaction like a single transcation in database at current time. It's like sequential running of transactions, while databases uses MVCC to bring isolation between transactions. 

**Durability**

​	This property ensures that once transcation was completed the data will be completely saved even if system crash happens. For single node database it would be a promise to write data for non volatile storage, in replicated database it could mean that the data was completely copied to all nodes. 
