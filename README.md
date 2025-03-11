# Frequent Itemset Analysis on Amazon Metadata using Apache Kafka

## Introduction: 

The objective of this assignment was to implement frequent itemset mining on streaming data using Apache Kafka to extract valuable insights from the vast and complex dataset. In the realm of data analytics, real-time processing of streaming data is crucial for extracting valuable insights. Apache Kafka offers a powerful platform for handling streaming data, known for its scalability and fault-tolerance. By combining Kafka's capabilities with frequent itemset mining algorithms like Apriori and PCY, we were able to find recurring patterns within the streaming data.

## Implementation: 

### Preprocessing:

The preprocessing step is crucial for extracting meaningful patterns from streaming data, particularly for frequent itemset mining. Special attention was given to the 'also_buy' and 'also_view' columns, which represent related products that customers tend to buy or view together. The main preprocessing function parses each JSON line, converting it into a Pandas DataFrame and setting default values for expected keys. It ensures data completeness by filling missing values with defaults and standardizes text fields by cleaning HTML tags and converting to lowercase. The processed data is stored in a dictionary containing only the expected keys. After preprocessing, the resulting data is saved in a new JSON format to an output file. 

### Streaming pipeline:

In our streaming pipeline setup, we've established one producer application and three consumer applications. The producer application efficiently streams the data we obtained after preprocessing the amazon metadata in real-time. This ensures a continuous flow of information through the pipeline. On the consumption end, three consumer applications have been deployed, each subscribing to the data stream generated by the producer.

### Frequent Itemset Mining:

For frequent itemset mining, we made use of three consumers within kafka, each containg a different algorithm to analyze the recurring patterns in our streaming data.

### •	Sliding Window Approach:

In the context of streaming data analysis, applying algorithms like Apriori or PCY poses a significant challenge due to their reliance on access to the entire dataset for accurate itemset calculations. Unlike traditional batch processing where the entire dataset is available, streaming data scenarios only provide access to a portion of the data at any given time. To address this challenge, a sliding window approach is employed. This approach involves dividing the data stream into fixed-size windows, where each window represents a subset of the overall data. By continuously updating and processing these windows as new data arrives, the sliding window approach enables real-time analysis of streaming data while maintaining memory efficiency. This allows for the application of frequent itemset mining algorithms to streaming data, providing insights into evolving patterns and trends over time.

### •	Apriori Algorithm:

The Apriori algorithm is implemented for frequent itemset mining within a Kafka consumer application. The algorithm is applied to two types of transactions: 'also_view' and 'also_buy'. As messages are consumed from the Kafka topic, the script collects these transactions into sliding windows to handle real-time data streams efficiently. When the window size is reached, the Apriori algorithm is executed on the collected transactions to identify frequent itemsets that meet or exceed the specified minimum support threshold. The frequent itemsets are then printed, indicating the categories or related items that appear frequently in the data stream. This process allows for continuous analysis of streaming data, enabling insights into user preferences and purchasing behavior in real-time.

### •	PCY Algorithm:

In another consumer, we implemented the PCY algorithm within the kafka application. The PCY algorithm addresses the challenge of accurately identifying frequent itemsets in streaming data scenarios where only a portion of the data is available at any given time. As messages are consumed from the Kafka topic, transactions containing 'also_buy' data are collected into a sliding window of fixed size. When the window size is reached, the PCY algorithm is executed to identify frequent items and candidate pairs based on a minimum support threshold and the number of hash buckets. By efficiently counting item frequencies and hash counts within the sliding window, the PCY algorithm identifies frequent itemsets while minimizing memory overhead. The frequent items and candidate pairs are then printed, providing insights into item associations and purchase patterns within the streaming data.

### •	FP-Growth Algorithm:

In the third consumer, we implemented the FP-Growth “Frequent Pattern Growth” algorithm within the kafka application. The FP-Growth algorithm addresses the challenge of identifying frequent itemsets in streaming data scenarios where access to the entire dataset is limited. As messages are consumed from the Kafka topic, transactions containing 'category' data are collected into a sliding window of fixed size. When the window size is reached, the FP-Growth algorithm is executed to discover frequent patterns and generate association rules based on a minimum support threshold. By efficiently constructing a compact data structure called the FP-tree and recursively mining frequent itemsets, FP-Growth identifies frequent patterns while minimizing memory and computation overhead. The frequent patterns and association rules are then printed, providing insights into item associations and co-occurrences within the streaming data.

### Database Integration

In our data processing pipeline, we integrated MongoDB into each consumer application to enhance data storage and management capabilities. This integration involved modifying each consumer to establish a connection with a MongoDB database and store the results of the data analysis. By leveraging MongoDB's flexible document-based data model and powerful query capabilities, we were able to efficiently store and retrieve the frequent itemsets, candidate pairs, or other relevant insights generated by the respective algorithms running in each consumer. This integration not only ensures persistent storage of valuable data but also facilitates further analysis, reporting, and decision-making processes downstream. 

## Conclusion

In conclusion, our assignment on frequent itemset analysis using Apache Kafka for streaming Amazon metadata has yielded significant insights into customer behavior and preferences. The implementation of the Apriori, PCY, and FP-Growth algorithms within Kafka consumers has allowed for efficient mining of frequent itemsets and association rules, providing actionable insights for business decision-making. Additionally, the integration of MongoDB into each consumer application enhances data storage and management capabilities, ensuring the persistence and accessibility of valuable analysis results. This assignment demonstrates how combining advanced data analytics techniques with scalable streaming platforms like Kafka enables us to extract valuable insights from large-scale, real-time data streams.
