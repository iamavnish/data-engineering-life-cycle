# Streaming ETL with Amazon Kinesis Data Stream

## Overview

This is Proof of Concept for creating a streaming ETL pipeline using Amazon Kinesis Data Stream as Event Streaming Platform.

## PoC Complexity Level

Medium

## Tech Stack

- Amazon Kinesis Data Stream
- Amazon Kinesis Firehose
- S3
- Python 3 incuding boto3 library

## Use Case / Problem Statement

An e-commerce application is streaming user activity records as events into Kinesis Data Stream. The customer wants to filter user activity records based on the country of user because the users which are in USA have a different purchasing behavior from the ones who are outside of USA. Later these records would be processed by different recommendation engines (based on whether country of user is USA or outside of USA) to recommend products to users in real-time. The segregated user activity records would also be used to serve real-time BI dashboards.

## Dataset

User activity data from e-commerce application. Below are two sample records:

![image](https://github.com/user-attachments/assets/e19e105b-cfc6-43db-ad1a-bf00f6193809)

![image](https://github.com/user-attachments/assets/f99abbcf-757b-457a-aa8c-cc0e6bd7300e)




## Solution Architecture

![image](https://github.com/user-attachments/assets/d1b79003-153b-470f-8afe-cceced63c57a)

A consumer application pulls messages from Kinesis Data Stream which is part of source system. Then it applies some transformations on the ingested data and send the transformed data to one of the new Kinesis Data Streams. Each of those data streams will then be delivered through Kinesis Firehose to their respective S3 buckets (one for USA users and another for non USA users) to be processed differently by downstream applications like recommendation engine or BI application.

The transformations consist of adding additional attributes as shown below:

![image](https://github.com/user-attachments/assets/22b90f6d-8d0f-477e-accd-cdba37db2892)

![image](https://github.com/user-attachments/assets/9155917a-7f59-4fc1-8397-25d655c6f4e5)


Plus a filter is created to send records with "country" as "USA" to one data stream and records with "country" not as "USA" to another data stream.

