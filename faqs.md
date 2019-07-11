# FAQs

## Architecture 

### In which language is Bondy implemented?

Bondy is implemented in Erlang, a wonderful programming language and platform for concurrent and \(soft\) real-time applications.

### Why does Bondy use an eventually consistent model?

Because we need Bondy to be scaleable and always-on either in the case of inter- or intra-datacentre clusters. 

We think it is really stupid to design super scaleable and fault-tolerant backend platforms using NoSQL databases, eventually consistency and more sophisticated techniques like CRDTs only to then define an API layer on top that relies on a strong consistency model. 

This problem usually happens when you use an API Gateway that relies on strong consistency for configuration and/or cluster state data replication,  in most cases by relying on a strong consistency database management system. All the hard work you've done in the backend to provide an always-on system is then hampered by an entry point which is not!

### How is Bondy or a WAMP Router different than other messaging technologies?

For a comparison with other products and technologies review the [WAMP Compared article](https://wamp-proto.org/comparison.html) in the protocol specification website.

## License

### How is Bondy licensed?

Leapsight Bondy is licensed under the Apache License 2.0, review a copy of the license [here](https://gitlab.com/leapsight/bondy/blob/develop/LICENSE).

### How is this documentation licensed?

You can find the answer in the [Documentation License](documentation-license.md) page.

## Commercial Support

### Do you provide Commercial Support?

Yes, please contact us to understand the options.



