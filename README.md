# A NodeSDK 1.2.x based sample with Fabric V1.2 software

Added the following functionality :

* Enabled Mutual TLS 
* Kafka based Orderering Service Node (OSN)
* 'AND' endorsement policy (Read a file pass it to the instantiate/upgrade request)
* Used REST based configtxlator for channel creation
* Upgrade chaincode
* Add private DB support + collections
* add support for couchdb Indexes
* Update Anchor peers using channel config update
* Revoke a user and Update the channel with revoked user (*** refer the note at the end)
* Service Discovery (Partial changes only)


**Terminal - 1** : 
Issue the following command
```
./bootstrap.sh
```

This does the following
* Clear the network if already launched.
* Launch network with the following topology.
  - Kafka based orderering service (3 orderers, 4 kafka brokerers, 3 zoo keepers).
  - Two orgs, each org has two peers + one CA.

**Terminal - 2** : Issue the following command to test fabric 1.2 features using REST calls with NodeSDK as the underlying client.

*ex:* 

  * Register/Enroll/Revoke user,

  * Create Channel/ Update Channel,

  * Join peers, 

  * Update Anchor peers , 

  * Install/Instantiate chaincode, 

  * Invoke & Query


ex:

`./end2end.sh -c testchain -l golang`

`./end2end.sh -c testchain`

`./end2end.sh -l node`


----
*note:* *** when user has been revoked and updated the channel with the CRL , the same user can't operate (ex: query/invoke) on the Blockchain any more.

Gist of **peer logs**

```
 2018-07-16 05:29:14.182 UTC [protoutils] ValidateProposalMessage -> WARN 051 channel [testchannel]: creator certificate is not valid: could not validate identity against certification chain: The certificate has been revoked
```


**Client (Node-sdk) err:**

```
Error: 2 UNKNOWN: access denied: channel [testchannel] creator org [Org1MSP]
```
----
