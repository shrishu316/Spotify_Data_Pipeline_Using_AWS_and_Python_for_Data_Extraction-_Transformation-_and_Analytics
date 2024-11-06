# Spotify Data Pipeline Using AWS and Python

This project leverages Spotify's API and AWS services to build a robust ETL (Extract, Transform, Load) data pipeline. The pipeline extracts music data daily from Spotify, transforms it, and stores it in an S3 bucket. It then uses AWS Glue and Athena for data cataloging and analytics, respectively, making it easy to query and analyze Spotify's data.

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Tech Stack](#tech-stack)
- [Pipeline Components](#pipeline-components)
- [Setup & Configuration](#setup--configuration)
- [Running the Project](#running-the-project)
- [Project Structure](#project-structure)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

---

## Architecture Overview

![aws_project drawio](https://github.com/user-attachments/assets/ebc5e10e-76f2-4581-aeab-66f5a735ed5f)

The architecture of this project is as follows:

1. **Spotify API**: Extracts music data from Spotify.
2. **AWS Lambda (Data Extraction)**: A Lambda function scheduled daily using AWS CloudWatch triggers to extract data from the Spotify API.
3. **AWS S3 (Raw Data Storage)**: Raw data is stored in an S3 bucket.
4. **S3 Trigger & Lambda (Data Transformation)**: An S3 trigger activates another Lambda function that transforms the raw data.
5. **AWS S3 (Transformed Data Storage)**: The transformed data is stored in a different S3 bucket.
6. **AWS Glue (Data Catalog)**: Crawls the transformed data and infers schema to create a data catalog.
7. **AWS Athena**: Enables analytics and querying of the cataloged data using SQL.

---

## Tech Stack

- **Languages**: Python
- **APIs**: Spotify API
- **AWS Services**:
  - AWS Lambda (Data Extraction and Transformation)
  - AWS S3 (Data Storage)
  - AWS CloudWatch (Triggering Lambda for Data Extraction)
  - AWS Glue (Data Catalog)
  - AWS Athena (Data Analytics)

---

## Pipeline Components

1. **Data Extraction**:
   - **Lambda Function**: Uses the Spotify API to pull data on artists, albums, or tracks daily.
   - **CloudWatch Trigger**: Configured to trigger the Lambda function daily.

2. **Raw Data Storage**:
   - **S3 Bucket**: Stores raw JSON data from Spotify in a designated S3 bucket for further processing.

3. **Data Transformation**:
   - **Lambda Function**: Triggered when raw data is uploaded. This function processes, cleans, and transforms the data.
   - **S3 Trigger**: Initiates the transformation Lambda upon new data in the raw data S3 bucket.

4. **Transformed Data Storage**:
   - **S3 Bucket**: Holds the cleaned and processed data in a format suitable for querying, such as Parquet or CSV.

5. **Data Cataloging**:
   - **AWS Glue Crawler**: Crawls the transformed data and automatically creates a schema in the AWS Glue Data Catalog.

6. **Analytics**:
   - **AWS Athena**: Enables querying of the data using SQL. Easily access transformed data for analytical purposes.

---

## Setup & Configuration

1. **Spotify API Setup**:
   - Sign up on [Spotify for Developers](https://developer.spotify.com/) and create a new application to get `Client ID` and `Client Secret`.
   - Enable required permissions to access Spotify data.

2. **AWS Configuration**:
   - Set up AWS Lambda, S3, Glue, and Athena according to your AWS environment.
   - Ensure roles and policies are in place for Lambda functions to access Spotify, S3, Glue, and Athena.

3. **Environment Variables**:
   - Add environment variables for the Spotify API credentials (`SPOTIFY_CLIENT_ID`, `SPOTIFY_CLIENT_SECRET`) and any other configurations needed in the Lambda functions.

---

## Running the Project

1. **Daily Data Extraction**:
   - CloudWatch triggers the extraction Lambda daily, pulling data from Spotify and storing it as raw data in S3.

2. **Data Transformation**:
   - An S3 trigger initiates the transformation Lambda upon new data in the raw S3 bucket, which processes the data and saves it in a different bucket.

3. **Data Cataloging and Analytics**:
   - AWS Glue Crawler runs periodically (or can be triggered manually) to catalog the transformed data.
   - Use AWS Athena to run SQL queries on the cataloged data for analysis.

---
