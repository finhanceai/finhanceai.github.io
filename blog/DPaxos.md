# DPaxos

- Introduction
    - Need for edge datacenters
        - With rise of IoT, AR/VR, latency cannot be tolerated thus stores should come closer to the user, i.e., on the edge
    - State Machine Replication
        - A general method of replicating servers to ensure fault-tolerance
        - Principle of independent failures
    - Design principles: local access, mobility, fault-tolerance
    - Operations like transaction management, atomic broadcast and stream processing are most common. RDBMS type databases are good for these operations. Paxos is a protocol of SMR designed for RDBMS.
    - Challenges
        - Existing research is only on data-centers and not on the edge
        - Paxos is consensus algorithm which requires participation of majority nodes which in edge nodes will be very huge. Vanilla paxos would incur two communication bottlenecks:
            - Replication overhead
            - Leader Election overhead
        - Goal: To minimize the replication and leader election communication while ensuring all the nice properties of Paxos
    - **Base idea:** Zone-centric Quorums
        - Two processes: Leader Election and Replication
    - Howard et al. showed in Flexible Paxos that replication quorum can be small as long as **all** **leader election quorums** intersect these replication quorums across zones.
    - How to get around this problem? - **Contribution**
        - Expanding Leader Election Quorums: LE quorums initially do not intersect all replication quorums. Later on when replication quorums increase they merge with other LEs but only in these used replication quorums
        - Leader Handoff: lightweight leader election process , typically single message to pass on the leadership
- Design Principles
    - Distributed Edge Datacenter Topology - Includes datacenters, edge nodes (if available)
    - Mobility
    - Fault tolerance
- DPaxos Overview
    - Zone-centric Quorums proposed by Heidi et al. - inter-intersection condition
        - Replication quorums are kept small but to do this we need leader election quorums to intersect with all replication quorums.
        - Topology - Grid-like, for $f_d$ nodes failures in a zone and $f_z$ zone failures.
        - Bottleneck 1 busted: Replication quorums are small now
    - Mitigating the problem of large LE quorums: Expanding quorums
        - only concurrent replication quorums
        - aspiring leaders detect which are these concurrent replication quorum and expand to intersect with them
        - Delegate Quorum → Majority of zones participate, Leader Zone Quorums→ One zone participates
        - Leader Zone Quorum → First nodes participate to decide a leader zone; then nodes in that zone contend for election. since all nodes participate, the intersection condition is fulfilled.
        - If workload moves then aspiring leaders and current leader zone gets far, hence leader zone needs to migrate - refer algorithm 2
        - Garbage collection to shrink the leader quorum, otherwise it just keeps growing monotonically.
    - Fast Leader Handoff— typically a single message
        - Stems by the idea that this was not triggered by a failure but user's behavior.
        - the idea of leader is a logical one; don't confuse with physical leader
- Evaluation
    - By how much has the replication overhead decreased?
        - Expectation: Similar to Flexible Paxos
        - Holds True
    
    - By how much has the leader election overhead decreased for the 2 variants?
        - Leader Zone and Handoff are function of distance
        - Multi Paxos and Delegate are pretty much similar and consistent
        - Flexible paxos is worse
    - Are leaderless paxos any good than dPaxos? Simulating some cases

### Discussion

- Isn't the failure assumption too simple? We don't know $f_d , f_z$ precisely?
- What's stopping from making it implementable?
- Are there simple insights about workload that can be used to trim the complexity of the system?
- How realistic it is/ Is it even possible for big companies like Google, Microsoft to start migrating their services to a geo-replicated DB like this one? Other aspects like security, availability etc are important too?

[https://www.youtube.com/watch?v=s8JqcZtvnsM](https://www.youtube.com/watch?v=s8JqcZtvnsM)

[https://www.youtube.com/watch?v=SRsK-ZXTeZ0](https://www.youtube.com/watch?v=SRsK-ZXTeZ0)

[https://www.youtube.com/watch?v=fYfX9IGUiVw&list=PLNPUF5QyWU8PydLG2cIJrCvnn5I_exhYx&index=11](https://www.youtube.com/watch?v=fYfX9IGUiVw&list=PLNPUF5QyWU8PydLG2cIJrCvnn5I_exhYx&index=11)