# Week5

LectureSet5

---

### Isolation

**Guarantees consistency** ->  Isolation guarantees consistency provided each transaction itself is consistent.

**Achieve isolation by sequentially** (sometime sequentially much faster than parallel -> no need for locks) 

<br />

<br />

<br />



---



<br />

These two rules can guarantee isolation.

<br />

## Dependency property

In a history sequence H, consisting of tuples of the form (T, action, object).  e.g. 	(T1,a1,O)

<br />

**Lost update**: a transaction write is ignored by another transaction. (WRITE -> WRITE conflict)

**Dirty read**: a transaction reads an object written by another transaction which again modifies the object afterwards. (WRITE -> READ Conflict)

**Non repeatable read**: a transaction reads an object twice and gets different values. (READ->WRITE conflict)

<br />

##### Share lock

For read, cannot write. Also called read lock. If one source is locked by share lock, other transaction only can add share lock to it. The share lock can generate the value is not be modified.

<br />

##### Exclusive lock

For read&write. 

If one source is locked by exclusive lock, other transaction cannot add any lock on it. 

<br />

**Well-formed transactions**: A transaction is well formed if all READ, WRITE and UNLOCK operations are covered earlier by appropriate LOCK operations. 

**Two phase transactions**: A transaction is two phased if all LOCK operations precede all its UNLOCK operations. (if you lock then unlock, you cannot lock again)

**wormhole**: a history is isolated if and only if it has no wormholes. There is a cycle in the dependency graph.

**Rollback theorem**: an update transaction that does an UNLOCK and then does a ROLLBACK is not two phases.
**Locking Theorem**: if all transactions are well formed and two-phased, then any legal history will be isolated.

<br />

<br />

### Degree of isolation

The more locks you take, the poorer performance you have.  The degree of isolation is trying to increase parallel isolation and minimise waiting time.

#### Degree3:

* Perfect transaction model. Best isolation, true isolation. 
* Lock protocol is **two phase** and **well formed**.
* Two phase lock -> lock anything which you want to access, then do read and write.
* It is sensitive to the following conflicts:
  * write->write; write ->read; read->write限制的死死的Serialization

<br />

#### Degree2:

* no lost updates and no dirty reads. Response time lower than degree 3. Run much more parallel than degree 3
* Only apply phase 1 and phase 2 for XLCOKs.
* SLOCKs release immediately. XLOCKs no need to wait for a long time.
* Might Non repeatable reads
* It is sensitive to the following conflicts:
  * write->write; write ->read(解决了lost update和dirty read)读操作是slock加锁读完后迅速释放，因此可能读到不一样的值，但是读不到过程中修改的数因此可能有repeatable reads

<br />

#### Degree1:

* No SLOCK for reading. Reading no need for waiting.
* No two phase (two phase for exclusive locks), no well formed (well formed with respect to writes), no lock for reading
* Two phase for exclusive lock
* It is sensitive the following conflicts:
  * write->write;(解决了lost update),但是数据可以在修改的过程中随时被其他事物读（有dirty read）,同理也有repeatable read

<br />

#### Degree0:

* No two phase, no well formed, no lock for reading
* Write is well-formed, not two phase
* When writes, lock then and immediately release. High response.(写过的数据可能在提交之前被修改，所以有lost update)
* Ignores all conflicts.

<br />

![](pic/week5_4.png)

<br />

![](pic/week5_5.png)

<br />

<br />

<br />

---

END
