
# Multi-Cloud Data Transfer with AWS and GCP

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-multicloud-storage)

**Author:** Albert  
**Email:** tapcyberx@gmail.com

---

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-multicloud-storage_s5k4l5m6)

---

## Introducing Today's Project!

In this project, I will demonstrate how to set up storage transfer between multiple cloud providers. The goal is to build hands-on skills in multicloud environments and cloud storage management.

I'm doing this project to learn how engineering teams can enhance data redundancy, improve availability, and avoid vendor lock-in by leveraging cross-cloud strategies for storing and transferring data securely and efficiently.



### Tools and concepts

Services I used were GCP Cloud Storage, Amazon S3, AWS IAM  and Google Storage Transfer Service. Key concepts I learnt include storage transfers, identity federation, manifest file and how to create GCP bucket.

### Project reflection

This project took me approximately 3 hours to complete.

The most challenging part was the "secret mission" step, which required deeper attention to authentication and cross-cloud permissions.

The most rewarding part was seeing how Storage Transfer Service works in action and realizing how a secure, multi-cloud data transfer system can be built with strong hardening practices across different cloud providers.

---

## Setting up Data in S3

I started this project by setting up an S3 bucket I uploaded around 10 files, all documentation of Nextwork project that they provide.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-multicloud-storage_s1g7h8j9)

---

## Setting up GCP

---

## Storage Transfer

Data transfers play a critical role in setting up backup storage locations across multiple cloud providers. In a multi-cloud architecture, transferring data between providers helps ensure redundancy, resilience, and better disaster recovery.

Additionally, when an application runs in a different cloud service provider (CSP) environment, having the data locally available in that CSP can reduce latency and improve performance making cross-cloud data transfers a smart strategy for both availability and efficiency.

The transfer is set up using Storage Transfer Service, which is Google Cloud Platform’s (GCP) native service for moving data in and out of its storage solution GCP Cloud Storage.

This service is essential in a multicloud environment because it helps manage key aspects of a file transfer, such as authentication, scheduling, and automation. It simplifies the process of securely and efficiently transferring large volumes of data between different cloud providers.



There are two main types of transfers you can configure with Storage Transfer Service: batch transfers and event-driven transfers.

The key difference lies in when the transfer occurs:

Batch transfers are scheduled either as a one-time operation or set to run on a recurring schedule.

Event-driven transfers happen in real time, triggered automatically whenever updates occur in the source bucket (e.g., an upload to an AWS S3 bucket).

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-multicloud-storage_s3k2l3m4)

---

## Granting GCP Access to AWS

To connect AWS and GCP, I'm using identity federation, which allows GCP's Storage Transfer Service (STS) to gain temporary, secure access to AWS resources.

This method is more secure than traditional approaches because it’s passwordless GCP doesn't need to store any long-term AWS credentials, reducing the risk of password leaks. Instead, AWS recognizes STS as a trusted identity and grants access automatically through federated permissions, allowing it to complete the transfer without exposing sensitive credentials.

I created a custom IAM role for Storage Tranfer Service because it needs read only access in order to read and retrive files to later store it in GCS. 

To enable secure access, I created a custom trust policy within the AWS IAM role. This trust policy is essential because AWS uses it to recognize GCP's Storage Transfer Service (STS) as a trusted identity.

The policy specifically identifies STS using a subject ID, which is the unique identifier of the GCP service account associated with the transfer. This ensures that only authorized requests from that service account are granted the temporary permissions needed to access AWS resources during the transfer.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-multicloud-storage_s4k3l4m5)

---

## Transferring from S3 to GCS!

To set up my destination Google Cloud Storage (GCS) bucket, I needed to define two key settings: the region and the storage class.

I selected a single region, which determines the physical location where the data will be stored, and chose the Standard storage class since I plan to access the backup data frequently and soon after transfer. This setup balances performance and cost for my specific use case.



I verified the success of my data transfer by visiting the Google Cloud Storage (GCS) bucket after the transfer was complete.

There, I confirmed that all the objects originally uploaded to the AWS S3 bucket were now present in the GCS bucket, indicating that the transfer was completed accurately and without data loss.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-multicloud-storage_s5k4l5m6)

---

## Transfer with a Manifest

In a project extension, I'm doing a selective transfer, which means I'm going to transfer only a select bunch of files from the source. A manifest file is the shooping/instruction list that STS will use to identify which files to transfer today. 

I verified the success of my data transfer by visiting the Google Cloud Storage (GCS) bucket after the transfer was complete.

There, I confirmed that all the objects originally uploaded to the AWS S3 bucket were now present in the GCS bucket, indicating that the transfer was completed accurately and without data loss.



---

## Trial, Error, Success

---

---
