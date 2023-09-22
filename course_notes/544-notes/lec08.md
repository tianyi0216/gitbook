# Lec08

A section of code we don't want interrupted by certain other code is a "critical section".&#x20;

Want atomicity and consistency.



Lock:

Lock rules: acquire and release.

Between acquire and release, a lock is held by the thread that acquire it.

A lock may only be held by one thread at a time.

If T2 wants to acquire a lock held by T1, T2 blocks until T1 release it.



Def: fine-grained locking - only hold the lock for a small piece of work

coarse-grained locking.&#x20;

(don't release if you immediately want to require)



Deadlock: exception, no release. Try to acquire lock but the other was not released.



with staement calls (to avoid exception not release lock)

with lock:
