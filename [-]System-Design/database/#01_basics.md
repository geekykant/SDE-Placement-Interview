## Basics on Database

Ref: [What is Database Sharding?](https://www.youtube.com/watch?v=hdxdhCpgYo8)

#### Ways to improve DB performance:
- Scaling up horizontally (Hardware) - scaling is not linear, if 2x server specs we do NOT get "2x performance"
- Add replicas 
	- master node (for writes) and multiple read nodes (for reads)
	- eventual consistency as sync needs to happen from master to slaves
		- can cause stale/obsolete data
		- bad for banking software - write to master and in-between read happens on account balance


### Sharding
Sharding means splitting a database into multiple different databases, thus each having a subset of data.
- Thus creating multiple database instances.
- Each shard has a key - used as an input to the hashing function to locate the shard containing the data.

As an example, we have sharding based on 'customer_id':
- Shard 1 -> customer_id - 1, 2
- Shard 2 -> customer_id - 3, 4
- So we need to have a separate routing logic or a routing table - which adds additional dance to the requests coming in.
  
<img width="574" alt="Screenshot 2024-01-14 at 2 55 55 PM" src="https://github.com/geekykant/SDE-Placement-Interview/assets/27401142/3c23546b-e514-40e1-bc27-bb775e8f69c7">

Pros:
- Horizontal scalability (split into shards when performance seems huge for the DB instance)
- Availability, Fault tolerance - shard2 available (customer_id 3,4) even if shard1 fails (containing 1,2)

Cons:
- Complexity - partition mapping, routing, Non-uniformity (heavy customers can outgrow shard DB size and create a necessity to re-shard)
- Doing analytics over all shards together brings slight difficulty
