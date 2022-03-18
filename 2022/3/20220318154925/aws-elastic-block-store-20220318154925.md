---
path: '/2022/3/aws-elastic-block-store-20220318154925'
title: 'aws elastic block store'
date: '20220318154925'
category: 'aws'
tags: ['aws certification', 'ebs']
---

# aws elastic block store
EBS volumes are storage volumes that can be attached to EC2
instances. These are disks can be assigned to an EC2, there
are at least 1 volume per EC2 instance (for operating systems).

More volumes can be added depending on the need of the application.
These are used in the same way as any system disk for storage.

Examples:
* Store data
* Run a database
* Create a filesystem

## Mission critical design
1. Production workloads
1. Highly available - replicated within a single availability zone to prevent hardware
failures
1. Scalable - capacity and type of volume can be changed without downtime or performance
impact to live systems

## Types of volumes
Several types are available, this is pertinent to the exam.

### General Purpose SSD (gp2)
The most cost effective disk, these are standard SSDs.

* 3 IOPS per GiB up to 16,000 IPS per volume
* gp2 volumes <1TB can burst up to 3,000 IOPS
* Great for low latency applications, boot volumes,
boot volumes

### General Purpose SSD (gp3)
Latest generation of the general purpose solution.

* Baseline 3,000 IOPS for any volume size (1-16 GB)
* Delivers up to 16,000 IOPS
* 20% cheaper than gp2
* Good for similar applications to gp2

### Provisioned IOPS SSD (io1)
High performance option, the most expensive.

* Up to 64,000 IOPS per volume. 50 IOPS per GiB.
* Use if you need >16k IOPS
* Designed for IO intensive apps (databases, latency-sensitive workloads)

### Provisioned IOPS SSD (io2)
Latest generation of provisioned IOPS volumes.

* Higher durability and more IOPS than io1
* Same maximum 64k/IOPS volume
* Same price as io1
* 500 IOPS per GiB
* 99.999% durability, all others have 99.8%-99.9%

### Provisioned IOPS SSD io2 Block Express
SAN (Storage Area Network) in the cloud. This has the highest performance, with the
lowest latency (sub-millisecond).

* Uses EBS Block Express architecture
* 4x the throughput capacity of regular io2 volumes
* Up to 64 TB, 256,000 IOPS per volume
* 99.999% durability
* Great for the largest, critical, high-performance apps like SAP HANA, Oracle, SQL Server

### Throughput Optimized HDD (st1)
These are actual hard drives, non-SSD.

* Low-cost HDD volume
* Good for mountains of data that we access frequently
* Baseline throughput of 40 MB/s per TB
* Ability to burst up to 250 MB/s per TB
* Maximum throughput of 500 MB/s per volume
* Good for throughput intensive workloads like ETL, data warehouses, or log processing
* **Note:** These can't be a boot volume

### Cold HDD (sc1)
The cheapest volume option.

* Baseline throughput of 12 MB/s per TB
* Ability to burst up to 80 MB/s per TB
* Max throughput of 250 MB/s per volume
* Good for colder data with fewer scans per day
* Good for apps with lowest cost and performance doesn't matter
* **Note:** These can't be a boot volume

## IOPS vs. Throughput

### IOPS
* Measures the number of read/writes per second
* Important metric for quick transactions, low latency apps, etc.
* Ability to read and write very quickly
* Choose based on IOPS required by the app

### Throughput
* Measures the number of bits read/written per second (MB/s)
* Important metric for large datasets, large I/O sizes, complex queries
* The ability to deal with large datasets
* Choose Throughput Optimized HHDs for high throughput

