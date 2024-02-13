# YAKt
### Yet Another KRAFT

## About KRAFT
- KRaft is a event based, distributed metadata management system that was written to replace Zookeeper in the ecosystem of Kafka.
- It uses Raft as an underlying consensus algorithm to do log replication and manage consistency of state.

## Languages / libraries Used:
Language Used : Python 

### Libraries:
- Flask - HTTP Server
- Pyraft - Raft Consensus Library
- Telnetlib - a Python library that provides Telnet client functionality for communicating with remote devices over the Telnet protocol.
- Threading Library

### Testing:
- Postman for API Testing.



## Raft Architecture
<img width="511" alt="image" src="https://github.com/Ashwinr-07/YAKt/assets/105007681/4173e06f-746c-4d40-9fec-6b5b6e2c6619">



### Raft Functionalities
- Raft handles __leader elections__ within the KRaft cluster.
- Implements an __event-driven architecture__ to facilitate communication and coordination.
- Ensures eventual __consistency across the cluster__.
- Manages failover by providing standard Raft failover guarantees; for instance, this is a 3 Node Cluster and handles a single cluster failiure can be scaled up to (2n + 1) Node Clusters,
- Maintains an __event log__ of all changes made, allowing for the reconstruction of the metadata store if necessary.
- Supports __snapshotting__ functionality, including the creation and retrieval of snapshots.
- Takes periodic snapshots of the event log at the leader node to enhance fault tolerance.



## Metadata Storage

There are 5 record types : 
1) RegisterBrokerRecord
2) TopicRecord
3) PartitionRecord
4) ProducerIdsRecord
5) BrokerRegistrationChangeBrokerRecord


## HTTP Server APIs

The APIs are of 2 broad categories
1) Broker Management API
2) Client Management API

In total there are 12 API Endpoints



__API Endpoint that accesses the RegisterBrokerRecord metadata record__

__Description:__
- Handles registration of brokers in the Kafka ecosystem.

__Functions:__
- `register`: Registers a broker.
- `get_all_active_brokers`: Retrieves information about all active brokers.
- `get_broker_by_id`: Retrieves information about a specific broker by its ID.

__API Endpoints that access/modify the TopicRecord metadata record__


__Description:__
- Manages topics within the Kafka ecosystem.

__Functions:__
- `create_topic`: Creates a new topic.
- `get_topic_by_name`: Retrieves information about a specific topic by its name.

__API Endpoints that access/modify the PartitionRecord metadata record__

__Description:__
- Manages partitions within Kafka topics.

__Functions:__
- `create_partition`: Creates a new partition.

__API Endpoints that access/modify the ProducerIdsRecord metadata record__

__Description:__
- Manages producer registrations from brokers.

__Functions:__
- `register_producer_from_broker`: Registers a producer from a broker.

__API Endpoints that access/modify the BrokerRegistrationChangeBrokerRecord metadata record__

__Description:__
- Manages updates to brokers, including incrementing the epoch on changes and unregistering brokers.

__Functions:__
- `update_broker`: Updates broker information and increments the epoch.
- `unregister_broker`: Unregisters a broker from the system.

### Broker Management (BrokerMgmt)

__Description:__
- Provides management functions related to brokers.

__Functions:__
- `get_metadata_updates_since`: Returns metadata updates since a specified offset/timestamp. If later than 10 minutes, sends the entire snapshot; otherwise, sends a diff of updated metadata.

### Client Management (ClientMgmt)

__Description:__
- Provides management functions related to clients.

__Functions:__
- `get_metadata_updates_since`: Returns metadata updates since a specified offset/timestamp. If later than 10 minutes, sends the entire snapshot; otherwise, sends updates for topics, partitions, and broker information only.

```bash
# Start Raft Node 1
$ python3 raft_http1.py -a 127.0.0.1:5010 -i 1 -e 2/127.0.0.1:5020,3/127.0.0.1:5030

# Start Raft Node 2
$ python3 raft_http2.py -a 127.0.0.1:5020 -i 2 -e 1/127.0.0.1:5010,3/127.0.0.1:5030

# Start Raft Node 3
$ python3 raft_http3.py -a 127.0.0.1:5030 -i 3 -e 2/127.0.0.1:5020,1/127.0.0

