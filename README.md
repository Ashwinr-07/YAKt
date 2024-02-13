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

__API Endpoint that accesses the TopicRecord metadata record__


__Description:__
- Manages topics within the Kafka ecosystem.

__Functions:__
- `create_topic`: Creates a new topic.
- `get_topic_by_name`: Retrieves information about a specific topic by its name.

## PartitionRecord

### Description:
- Manages partitions within Kafka topics.

### Functions:
- `create_partition`: Creates a new partition.

## ProducerIdsRecord

### Description:
- Manages producer registrations from brokers.

### Functions:
- `register_producer_from_broker`: Registers a producer from a broker.

## BrokerRegistrationChangeBrokerRecord

### Description:
- Manages updates to brokers, including incrementing the epoch on changes and unregistering brokers.

## Functions:
- `update_broker`: Updates broker information and increments the epoch.
- `unregister_broker`: Unregisters a broker from the system.

## Broker Management (BrokerMgmt)

### Description:
- Provides management functions related to brokers.

### Functions:
- `get_metadata_updates_since`: Returns metadata updates since a specified offset/timestamp. If later than 10 minutes, sends the entire snapshot; otherwise, sends a diff of updated metadata.

## Client Management (ClientMgmt)

### Description:
- Provides management functions related to clients.

### Functions:
- `get_metadata_updates_since`: Returns metadata updates since a specified offset/timestamp. If later than 10 minutes, sends the entire snapshot; otherwise, sends updates for topics, partitions, and broker information only.


Content for subheading 3 goes here.

## Heading 4

Content for heading 4 goes here.

### Subheading 4

Content for subheading 4 goes here.

## Heading 5

Content for heading 5 goes here.

### Subheading 5

Content for subheading 5 goes here.

```bash
# Bash Console 1
$ command1

$ command2

