# Frequent Itemset Analysis on Amazon Metadata using Apache Kafka

## Introduction:
This project implements frequent itemset mining on streaming Amazon metadata using Apache Kafka to uncover valuable insights into customer behavior and preferences. Real-time streaming data analysis is crucial in modern data analytics, and Kafka's scalability and fault-tolerance make it an ideal platform for processing high-velocity data streams. By leveraging frequent itemset mining algorithms such as Apriori, PCY, and FP-Growth, this project identifies recurring patterns and associations in the streaming data.

## Features:
- Real-time frequent itemset mining using sliding windows for streaming data

- Implementation of three frequent itemset mining algorithms:

- Apriori: Finds frequent itemsets based on minimum support

- PCY (Park-Chen-Yu): Optimizes memory usage for counting frequent pairs

- FP-Growth: Uses an FP-tree structure for compact and efficient mining

- MongoDB Integration for persistent data storage

- Streaming pipeline with Kafka producer and three Kafka consumer applications
  

## Project Architecture:
The project follows a producer-consumer model:

- Producer: Streams preprocessed Amazon metadata in real-time.

- Consumers: Three separate consumers, each running a different algorithm (Apriori, PCY, FP-Growth) to process and mine frequent itemsets in the streaming data.


## Implementation Details: 
1. Data Preprocessing
The preprocessing stage standardizes the streaming data to prepare it for analysis. Key steps include:

Parsing JSON data and handling missing keys

Cleaning text fields by removing HTML tags and converting text to lowercase

Storing the cleaned data in a new JSON format for streaming

2. Streaming Pipeline Setup
Producer Application: Streams preprocessed Amazon metadata to a Kafka topic in real-time.

Three Kafka Consumers:

Apriori Consumer: Processes 'also_view' and 'also_buy' transactions to find frequent itemsets.

PCY Consumer: Counts item frequencies and candidate pairs within a sliding window.

FP-Growth Consumer: Mines frequent patterns and generates association rules from the 'category' data.

3. Sliding Window Approach
Since streaming data is continuously flowing, we apply a sliding window to divide the data into fixed-size windows. This allows real-time frequent itemset mining without needing access to the full dataset, maintaining memory efficiency while capturing evolving patterns over time.

## Frequent Itemset Mining Algorithms:
### Apriori Algorithm
Processes 'also_view' and 'also_buy' transactions in real-time.

Collects data within sliding windows and runs the Apriori algorithm when the window size is reached.

Identifies frequent itemsets based on a minimum support threshold.

### PCY Algorithm
Optimizes memory usage by hashing item pairs into buckets and counting their frequencies.

Finds frequent items and candidate pairs from 'also_buy' data within the sliding window.

### FP-Growth Algorithm
Builds an FP-tree from 'category' transactions in the sliding window.

Mines frequent patterns and generates association rules efficiently.

## Database Integration:
Each consumer is integrated with MongoDB to store the results of the frequent itemset analysis. This allows:

Persistent storage of frequent itemsets, candidate pairs, and association rules.

Enhanced data retrieval and further analysis, reporting, and decision-making.

## How to Run the Project:
### Prerequisites
Apache Kafka installed and configured

Python with the following libraries:

pandas, nltk, pymongo, kafka-python

MongoDB installed and running

### Steps to Run
1)Set up Kafka and Create a Topic

Start the Kafka server and create a topic (e.g., amazon_metadata_stream).

2)Preprocess the Data

Run the preprocessing script to clean and format the Amazon metadata.

3)Start the Producer

Stream the preprocessed data to the Kafka topic using the producer application.

4)Start the Consumers

Run the three Kafka consumers (Apriori, PCY, and FP-Growth).

Monitor the terminal outputs for frequent itemsets and association rules.

5)View Results in MongoDB

Connect to your MongoDB database to view the stored frequent itemsets and patterns.



## Conclusion:
This project demonstrates how to combine Apache Kafka's streaming capabilities with frequent itemset mining techniques to extract valuable insights from large-scale, real-time data streams. By leveraging Apriori, PCY, and FP-Growth algorithms, we efficiently uncover patterns, associations, and trends in customer behavior, with MongoDB integration ensuring persistent data storage for downstream analysis.


