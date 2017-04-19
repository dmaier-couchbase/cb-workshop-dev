### TOC

   * [Couchbase Development Workshop](#couchbase-development-workshop)
      * [Requirements](#requirements)
      * [VM Setup](#vm-setup)
      * [Downloads](#downloads)
      * [Agenda](#agenda)
      * [Exercises](#exercises)
         * [Day 1: Couchbase Architecture and Administration Basics](#day-1-couchbase-architecture-and-administration-basics)
         * [Day 2: Using the Couchbase Client Library](#day-2-using-the-couchbase-client-library)


# Couchbase Development Workshop

Couchbase Server is an open source, distributed, NoSQL document-oriented database. It exposes a fast key-value store with managed cache for submillisecond data operations, purpose-built indexers for fast queries and a query engine for executing SQL-like queries. Couchbase Server was designed to satisfy requirements for a flexible data model, a powerful query language, scalability, performance, simple administration and high availability.

This course is designed to give an introuction into Couchbase's main use cases, teach the Couchbase Server's administration basics and it's architecture. The main focus of this 2 day workshop is to learn how to develop with Couchbase's standard development kits. You will learn how to manage connections, how to work with documents and how to model your data best for Couchbase.

This is a combined C/C++ & Java workshop. The Couchbase development basics will be thought together for Java and C/C++ developers. The audience will be split into 2 groups on the second day in order to perform programming language specific exercises.



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

## Downloads


* [DCDEVW/Downloads](https://www.dropbox.com/sh/8umsxntxn5ou5xa/AADR_1YmKzrdeKDBZDzDeFxGa?dl=0)


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
|                 | Security Features                       |
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
| 9               | Create/Update Documents                | Implement the Upsert method in the Data Source class |
| 10              | Get Documents                          | Implement the Get method in the Data Source class |
| 11              | Use the Sub-Documents API              | Implement a PartialGet method in the Data Source class |
| 12              | Delete Documents                       | Implement the Delete method in the Data Source class |
| 13              | Query a View                           | Create a View via the Admin UI, Implement the QueryView method in the Data Source class|
| 14              | Querying via N1QL                      | Inspect the Global Secondary Indexes, Simple queries, Join queries, Implement the QueryN1ql method in the DataSource class |
| 15              | Full Text Search                       | Inspect Full Text Indexes, Implement  the FullTextSearch method in the DataSource class |
| 16              | A Sample Application                   | Run and build the Travel-Sample application  |


## Change history

### Cpp content

#### Day 1

* Slide 37: Added the instruction how to disable the firewall for RHEL7
* Slide 38: Removed the VM snapshotting
* Slide 42: Added the instruction how to restart Couchbase on RHEL7
* Slide 69: Added periodic merge to the backup strategies
* Slide 70: Newly added slide regarding the backup archive structure
* Slide 71: Added a simple cbbackupmgr exercise
* Slide 75: Added filtered XDCR to the picture
