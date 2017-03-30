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
|                 |                                        | Install Curl |
|                 |                                        | Get details via the REST API |
| 3               | Working with Buckets                   | Create a Bucket via the UI |
|                 |                                        | Add a document to the Bucket |
|                 |                                        | Create a Bucket via the CLI|
| 4               | Working with the Cluster               | Add/remove nodes via the UI|
|                 |                                        | Rebalance|
|                 |                                        | Add/remove nodes via the CLI |
| 5               | Backup/Restore                         | Use cbbackup to backup a Bucket|
|                 |                                        | Use cbrestore to restore to another Bucket|
| 6               | XDCR                                   | Create an XDCR link via the UI |

### Day 2: Using the Couchbase Java 2.x Client Library

The starting point for the day 2 execises is the '1' folder. This is basically an empty application skeleton. Folder '2' is a bit more progressed. The final solution can be found in folder '3'.

| #               | Title                                  | Content                                      | 
| --------------- | -------------------------------------- | -------------------------------------------- |
| 7               | Project Setup                          | Maven Dependencies | 
| 8               | Connection Management                  | ConnectionFactory, Singleton approach |
| 9               | CRUD Operations                        | Create Documents, Reference Documents, Get Documents |
| 10              | Querying via Views                     | Create a Design Document, Create View, Query via the Browser and Client |
| 11              | Querying via N1QL                      | Create a Secondary Index via the CLI, A simple Query, Query by performing a Join |
