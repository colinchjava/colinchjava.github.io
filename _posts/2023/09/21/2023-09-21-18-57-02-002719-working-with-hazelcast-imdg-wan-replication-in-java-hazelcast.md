---
layout: post
title: "Working with Hazelcast IMDG WAN replication in Java Hazelcast"
description: " "
date: 2023-09-21
tags: [hazelcast, wanreplication]
comments: true
share: true
---

Hazelcast IMDG (In-Memory Data Grid) is an open-source distributed computing platform that provides in-memory storage and processing of data. One of the key features of Hazelcast IMDG is its WAN (Wide Area Network) replication capability, which allows you to replicate data across different data centers or geographical regions.

In this blog post, we will explore how to configure and work with Hazelcast IMDG WAN replication in a Java environment.

## Setting up Hazelcast IMDG

Before we can start working with WAN replication, we need to set up Hazelcast IMDG in our Java application. To do this, we need to add the Hazelcast IMDG dependency to our project. 

### Maven Dependency
```xml
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
    <version>4.1</version>
</dependency>
```

### Configuring Hazelcast IMDG WAN Replication

To enable WAN replication, we need to configure two Hazelcast clusters - the source cluster and the target cluster. The source cluster contains the data that needs to be replicated, and the target cluster receives the replicated data.

#### Source Cluster Configuration
```java
Config config = new Config();
config.setClusterName("sourceCluster");

WanReplicationConfig wanConfig = new WanReplicationConfig();
wanConfig.setName("myWanReplication");
wanConfig.setTargetCluster("targetCluster");

config.addWanReplicationConfig(wanConfig);

HazelcastInstance hazelcastInstance = Hazelcast.newHazelcastInstance(config);
```

#### Target Cluster Configuration
```java
Config config = new Config();
config.setClusterName("targetCluster");

HazelcastInstance hazelcastInstance = Hazelcast.newHazelcastInstance(config);
```

In the above code, we configure the source cluster and target cluster with their respective cluster names. We then create a `WanReplicationConfig` object and set its name to "myWanReplication" and the target cluster name to "targetCluster". Finally, we add the `WanReplicationConfig` to the source cluster's `Config` object.

## Replicating Data

Once the source and target clusters are configured, we can start replicating data from the source cluster to the target cluster.

```java
IMap<String, String> sourceMap = hazelcastInstance.getMap("sourceMap");
IMap<String, String> targetMap = hazelcastInstance.getMap("targetMap");

sourceMap.put("key", "value");

// Wait for replication to complete
targetMap.addEntryListener(new EntryAdapter<String, String>() {
    @Override
    public void entryAdded(EntryEvent<String, String> event) {
        System.out.println("Replication complete");
    }
}, true);

```

In the above code, we retrieve the source map and target map objects from the Hazelcast instance. We then add an entry to the source map, and wait for the entry to be replicated to the target map. By adding an `EntryListener` to the target map, we can monitor when the replication is complete.

## Conclusion

Hazelcast IMDG WAN replication provides a powerful mechanism for replicating data across different clusters and geographical regions. In this blog post, we learned how to configure and use Hazelcast IMDG WAN replication in a Java application. With this knowledge, you can now leverage the benefits of WAN replication in your distributed computing scenarios.

#hazelcast #wanreplication