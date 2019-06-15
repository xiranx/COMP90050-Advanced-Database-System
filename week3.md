# Week 3

### Fault tolerance

the **failure is independent**.

Probability a particular module is not available: 

   = MTTR/(MTTF+MTTR)     ≅ MTTR/MTTF   if MTTF >> MTTR



![](pic/week3_1.png)



##### Software reliability

* design and coding faults
* N-version programming
* Bohrbugs  -> deterministic  bugs
* Heisenbugs -> software errors that only appear occasionally 
* Dense faults -> a system can tolerate up to N faults. more than N the system may be nterrupted.
* Byzantine faults -> the faults not part of the model and the design is not catered to tolerate such faults
######improve software reliability
* Periodic transfer of data: primary; The second backup.
* Checkpoint-restart: primary records its state on a duplexed storage module. the secondary starte reading the state of the primary from the duplexed storage.
* chekpoin message: primary send its state changes as messages to the backup.
* persistent: backup restarts in the null state and clean up all uncommitted transactions.
#######Highly available storage
* write to several storage module
* checksum
* disk mirroring
* shadowing
#######High available Process
* processpairing
* transaction based restart
* checkpoint restart

Summary

* Improving Hardware reliability that is CPUs, Memory and Storage Units. This can be done by employing lot of redundancy such as   N-plex systems. 
* Software reliability can be improved by employing process-pairing or transaction based recovery.









