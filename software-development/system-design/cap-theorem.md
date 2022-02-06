# CAP Theorem

> The CAP theorem states that any _**distributed** data store_ can only provide two of the following three guarantees:
>
> **Consistency**
>
> Every read receives the most recent write or an error.
>
> **Availability**
>
> Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
>
> **Partition Tolerance**
>
> The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network
> between nodes.
>
> \- [Wikipedia](https://en.wikipedia.org/wiki/CAP_theorem)

The theorem is applicable ONLY WHEN a network partition happens. Since _partition tolerance_ is a must to keep the
system running, the actual trade-off is between _consistency_ and _availability_.

**CP = Consistency + Partition Tolerance**

The data store will cancel the operation and thus decrease availability.

**AP = Availability + Partition Tolerance**

The data store will proceed with the operation and thus risk inconsistency.

## Special Notes

Think of the CAP theorem as a dimension to understand the design of the distributed data store, instead of a strict rule
that the data store must follow.

In reality, most distributed data stores behave as a mix of `CP` and `AP` in case of a network partitioning. For example,
the read operations are available but the write operations are aborted.

Here's a good read from Eric Brewer, the author of the CAP theorem:
[CAP Twelve Years Later: How the "Rules" Have Changed](https://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed/)
