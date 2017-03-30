# Couchbase Development Workshop

This repository contains the material for a combined developer workshop. The following SDK-s are covered:

* C/C++
* Java

## Requirements

Each training computer should have at least the following HW configuration

* 4 CPU cores >=2GHz
* 8 GB RAM
* 50 GB free disk space

The following connectivity is expected:

* Internet access
* Access to Dropbox (alternatively the training material and environment can be provided on a network share in the LAN)

The following software needs to be installed on the attendee's computer:

* VirtualBox >= 4.3
* Putty and WinSCP (Windows only)
* A VNC Viewer (https://github.com/TigerVNC/tigervnc/releases)

The attendee should have all required permissions to create Virtual Machines and Virtual Machine networks on his box.


## VM Setup

Details regarding the setup of the workshop VM can be found here: 

* [VMSETUP](https://github.com/dmaier-couchbase/cb-workshop-dev/blob/master/VMSETUP.md)




## Agenda

* Day 1

| Time            | Title                                   | 
| --------------- |  ---------------------------------------|
| 09:00           | Introduction and Core Use Cases         |
|                 | Couchbase Server Architecture           |
|                 | Couchbase Server as a Distributed System|
| 10:30           | Coffee Break                            |
|                 | Working with Buckets                    |
|                 | Working with the Cluster                |
| 12:30           | Lunch                                   |
|                 | Security features                       |
|                 | Cross Data Center Replication explained |
|                 | Backup & Restore                        |
| 17:00           | Q&A and Summary                         |

* Day 2

| Time           | Topic                           |
| -------------- | ------------------------------- |
| 09:00          | Document Modelling Basics       |
|                | Data Access Paradigms & Index Structures |
| 10:30          | Coffee Break                    |
|                | Understanding Non-Blocking I/O, Callbacks & Reactive Programming|
|                | A short overview on the SDK API-s|
|                | Connection Management | 
|                | Error Handling and Logging |
| 12:30          | Lunch |
|                | Develop a Sample Application based on the 'travel-sample' data |
|                | Specific Use Case presentation |
|                | What's new in Couchbase 4.6 & Outlook|
| 17:00          | Q&A and Summary |

## Exercises

### Day 1: Couchbase Architecture and Administration Basics

| #               | Title                                  | Content                                      | 
| --------------- | -------------------------------------- | -------------------------------------------- |
| 1               | Installation and Configuration         | Disable Swappines | 
|                 |                                        | Disable the Linux Firewall |
|                 |                                        | Download and Install Couchbase |
|                 |                                        | Configure the Cluster |
| 2               | Testing the Installation               | List the nodes of your current cluster |
|                 |                                        | Investigate the data and index directory |
|                 |                                        | Get some data from a vBucket file |
|                 |                                        | Get some info about a vBucket file |
|                 |                                        | Install Telnet |
|                 |                                        | Retrieve some statistics via Telnet |
|                 |                                        | Set/get a value via Telnet |
|                 |                                        | Get details via the REST API |
| 3               | Working with Buckets                   | Create a Bucket via the UI |
|                 |                                        | Add a document to the Bucket |
|                 |                                        | Create a Bucket via the CLI|
|                 |                                        | Query a Bucket via the Query Workbench |
| 4               | Working with the Cluster               | Add/remove nodes via the UI|
|                 |                                        | Rebalance|
|                 |                                        | Add/remove nodes via the CLI |
| 5               | Backup/Restore                         | Use 'cbbackupmgr' to backup/restore a Bucket |
| 6               | XDCR                                   | Create an XDCR link via the UI |

### Day 2: Using the Couchbase Client Library

| #               | Title                                  | Content                                      | 
| --------------- | -------------------------------------- | -------------------------------------------- |
| 7               | Project Setup                          | Qt (C/C++) or Netbeans/Maven (Java) | 
| 8               | Connection Management                  | Implement a Data Source Factory |
| 9               | Create/Update Document                 | Implement the Upsert method of the Data Source class |
| 10              | Get Documents                          | Implement the Get method of the Data Source class |
| 11              | Delete Documents                       | Implement the Delete method of the Data Source class |
| 12              | Query a View                           | Create a View via the Admin UI, Implement the QueryView method in the Data Source class|
| 13              | Querying via N1QL                      | Inspect the Global Secondary Indexes, Simple queries, Join queries, Implement the QueryN1ql method in the DataSource class |
| 14              | Full Text Search                       | Implement  the FtSearch method in the DataSource class  |
| 15              | A Sample Application                   | Run and build the Travel-Sample application  |


