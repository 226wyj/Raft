# Raft 

## Introduction
This repository simulates a simple Raft algorithm application scenario based on Elixir, and it is the combination of Lab3 and Lab4 of NYU Distributed Systems Course(CSCI-GA 2621). In summary, it implements a replicated state machine using Raft as the underlying consensus protocol. The RSM models a queue supporting enqueue and dequeue operations. The RSM also provides a no-op operation that is used for testing and forcing commits.

**NOTE** Figure 2 in the [Raft paper](https://raft.github.io/raft.pdf) is exactly what I implemented. There are certain things that I did **not** implement:

* Snapshotting or anything else to reduce log sizes.
* Reconfiguration or mechanisms to change membership.

For this project it can be safely assumed that the network does not lose packets and that messages between pairs of processes are delivered in order.

## Part 1: Get the RSM Working without Leader Election (AppendEntries)

This project can be divided into two parts. For Part 1 it is to launch a cluster with a pre-appointed leader and allow clients to commit changes. In particular this requires

* Implementing AppendEntries so the leader can replicate log entries across the
  cluster.
* Making sure followers respond to AppendEntries appropriately.
* Making sure the leader can decide when an entry has been committed. The leader
  **should only** respond to the client once the appropriate operation has been
  applied to the queue, which of course requires that the corresponding log entry
  be committed. To help with this LogEntry's store information about the client
  that invoked a request.
* Making sure that followers apply committed log entries eventually.

You can start with the assumption that all processes are either leaders or followers, and hence not worry about candidates in this part.

### Testing Part 1
We have test cases for Lab 3 in [`test/lab3_test.exs`](apps/lab3/test/lab3_test.exs) which can be run using:

```
> mix test test/lab3_test.exs
```

## Lab 4: Get Leader Election Working
The second part is to complete the implementation so that leader election
works correctly. This requires implementing everything required to handle 
`RequestVote` calls correctly, and for getting logs to match.


### Testing Lab 4
There are test cases for Lab 4 in [`test/lab4test.exs`](apps/lab3/test/lab4_test.exs) which can be run using:

```
> mix test test/lab4_test.exs
```
