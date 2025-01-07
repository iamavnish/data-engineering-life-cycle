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

