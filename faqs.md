# FAQs

## Architecture 

### In which language is Bondy implemented?

Bondy is implemented in Erlang, a wonderful programming language and platform for concurrent and \(soft\) real-time applications.

### Why does Bondy use an eventually consistent model?

Because we need Bondy to be scaleable and always-on either in the case of inter- or intra-datacentre clusters. We think it is really stupid to design super scaleable and fault-tolerant backend platforms using NoSQL databases, eventually consistency and more sophisticated techniques like CRDTs only to then define an API layer on top that relies on a strong consistency model. 

This problem usually happens when you use an API Gateway that relies on strong consistency for configuration and/or cluster state data replication,  in most cases by relying on a strong consistency database management system. All the hard work you've done in the backend to provide an always-on system is then hampered by an entry point which is not!

## License

### 

## Commercial Support

### Question?

Yes, after a few months we finally found the answer. Sadly, Mike is on vacations right now so I'm afraid we are not able to provide the answer at this point.



