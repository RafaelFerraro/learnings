# ACID in relational databases

ACID is a set of properties of a relational database that ensures a valid state of the data in a transaction. It is an acronym that stands fro Atomicity, Consistency, Isolation and Durability.

### Atomicity
<b>Atomicity</b> means that a database guarantees that all processes inside a transaction will either fail or succeed. If there is a single process that can't be committed inside a transaction, all other processes will not be committed as well, even if they already have been updated. In other words, the transaction only succeed if all processes are committed.

### Consistency
<b>Consistency</b> means that a database transaction ensures the integrity and consistency of the data. For example, if a database INSERT command is being executed inside a transaction, the transaction ensures that if there is any constraint in the table under the INSERT command and this constraint fails, the whole transaction will fail as well. It means that the data will only be committed if it is consistent againts database constraints.

### Isolation
<b>Isolation</b> means that if there are two transactions running at the same time, the data inside one transaction cannot be accessed by the another transaction. There are levels of isolation and not all of them ensures such level of isolation. We will see them later.

### Durability
<b>Durability</b> means that a database transaction ensures that if a row is committed, it doesn't matter if there is a power outage, or the system crashes, whatever. The data will be stored in a non-volatile place and then, when your systems recover, the data will be there available for you.