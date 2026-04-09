# Real-Time Stock Market Analysis

## Abstract:
The system focuses on designing a scalable and efficient real-time stock market data ingestion and processing system, along with visualization features. It is mainly an Azure-based architecture consisting of Azure Event Hub for ingestion; Stream Analytics for real-time processing; and Azure Synapse Analytics and Power BI for data storage and visualization. The core design will be for a data pipeline that can ingest both real-time stock market feeds from APIs, such as Alpha Vantage, and historical data fed in through CSV files. It will thus store the processed data safely at Azure Data Lake Storage Gen2 and expose it for further analysis via Synapse Analytics and Power BI dashboards. The pipeline provides seamless integration for speed insights and actionable intelligence on stock market decision-making. Through this pipeline process, to the financial analyst and companies, would come an understanding of the trend occurring in stocks, study market behavior, and make educated decisions backed up with time-now and historical data for insight surge into the financial world. At the time of the publication of its first edition, this report deals up to October 2023 with data training.

The project focuses on developing a scalable and efficient system for ingesting, processing, and visualizing real-time information related to stock markets. It implements a robust Azure-based architecture comprising Azure Event Hub for ingesting data into the system, Stream Analytics for real-time processing, and Azure Synapse Analytics and Power BI for storage and visualization of data. Design a data pipeline that, on one hand, ingests real-time stock market feeds provided by APIs such as Alpha Vantage, and on the other hand, historical data from CSV files. Then it would securely store and make the processed data available for analysis through Synapse Analytics and Power BI dashboards in Azure Data Lake Storage Gen2. This pipeline facilitates seamless integration, fast insights, and actionable intelligence on stock market decision-making. It helps the financial analyst and companies realize what is happening in stocks, study orientation in market behavior, and make informed decisions based on real-time and historical data for better insight surge in the financial world.

---

## Dataset:

This project uses two sets of data to do analysis for the stock market. These are:

### 1. Historical Data:
- **Source:** Historical data is fetched from a CSV file containing records on multiple indices like HSI, NYA, IXIC, and many others.  
- **Columns:** Date, Open, High, Low, Close, Adjusted Close, Volume, CloseUSD.  
- **Historical data:** from 2013 to the present, after truncation of larger data for best analysis.  
- **Dataset File:** [indexProcessed.csv]  

### 2. Real-Time Data:
- **Source:** The real-time stock market data will be fetched using the Alpha Vantage API.  
- **Columns provided by the API include:** Open, High, Low, Close, Adjusted Close, and Volume.  
- The API allows for real-time monitoring and the generation of insights in real time.  

**API Documentation:** [Alpha Vantage API Documentation](https://www.alphavantage.co/documentation/)  

Merging these two datasets allows the project to deliver effective analytics by taking advantage of past trends and real-time updates. Past records serve the basis for trend analysis. Therefore, it then augments the pipeline with contemporary market data for more vigorous analysis in stock market decision-making through API.

---

## Objectives:

### 1. Data Ingestion:
- Ingest historic stock market data from the CSV dataset `indexProcessed.csv` and real-time data from Alpha Vantage API.  
- Combine data in a centralized system for analysis and visualization.  

### 2. Data Transformation:
- Use Python libraries such as Pandas to preprocess the data.  
- Clean, normalize, and enrich in order to have consistency between the historical and real-time datasets.  

### 3. Data Analytics:
- Write analytics for calculating key metrics of stocks based on trading volume, closing price, currency effect, and market trends.  
- Provide market performance and volatility insights about different indices like HSI, NYA, and IXIC.  

### 4. Data Storage:
- Store historical and real-time data securely in Azure Data Lake Storage Gen2.  
- Organize data by index and timestamp for efficient retrieval and future analysis.  

### 5. Batch and Real-Time Processing:
- Implement Azure Stream Analytics for real-time data processing and integration with historical data.  
- Batch job configurations that allow for the processing of historical data to gain insight into things like long-term trends and anomalies.  

### 6. Data Visualization:
- Create interactive dashboards in Power BI to visualize stock market data in real time, emphasizing the main patterns.  
- Provide reports on the volume of trade, performance of stocks, and market trends in a graphical form.  

### 7. Monitoring and Logging:
- Azure Monitor or another logging tool monitors the system performance and data pipeline for efficiency.  
- Make sure the system continuously runs reliably through tracking performances that may cause anomalies to arise.  

---

## Project Pipeline:
![Image 1](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/1.png?raw=true)


### Setup and Process:
Initially, it creates an Event Hub Namespace entitled "StockMarketNamespace." Then, it creates
an Event Hub "stockmarketeventhub" under the above namespace specifically for real-time
ingestion of stock market data. The below image shows the Event Hub overview that includes
metrics such as the number of Incoming requests, successful requests, and throughput for the
past hour. So, it ensures that the Event Hub is working in readiness for efficient data processing.
![Image 2](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/2.png?raw=true)


The Event Hub has two Consumer Groups-'SDefault' and 'dataexplorerconsumergroup' and
these consumer groups let several systems or applications independently consume the same
stream of stock market data. The second image displays the consumer groups together with
their locations in the East US region. The graph shows the number of incoming requests and a
smooth handling of data streams without any errors.
![Image 3](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/3.png?raw=true)



Thus, the Azure Stream Analytics job "StockMarket_StreamAnalyticsJob" created for processing
the ingested data would use the input source "stockmarketeventhub," and would eventually set
its output to Power BI for visualization. The third screenshot captures a detailed job
configuration, including resource group, location, input source, and output details. Meanwhile,
the status of the Stream Analytics job is "Ready to Start," meaning that it has been correctly set
up and is ready to take in and process data. The Stream Analytics job will ingest its input
through the Event Hub (stockmarketeventhub) and will be configured to ingest online data
streams in real time from Event Hubs. The settings related to this ensure proper data formatting
and its downstream processing.

![Image 4](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/4.png?raw=true)

This is the homepage of Azure Portal.This image depicts the Azure Services Dashboard, which
provides access to major services such as Event Hubs, Stream Analytics Jobs, and Data Explorer.
The page serves as the portal to create and manage resources for stock market analysis.

![Image 5](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/5.png?raw=true)

This screenshot shows the creation of the "Stock_Market_Resource_Group" so that all
resources of the project such as Event Hubs, Stream Analytics Jobs, and Data Explorer will be
organized under this group. Resource groups facilitate efficient management and monitoring of
all related Azure resources.

![Image 6](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/6.png?raw=true)
The screenshot displays the establishment of the "StockMarketNamespace," which serves as a
bucket for the Event Hub instance. The namespace supplies a single endpoint to manage all the
Event Hubs pertaining to the project. The screenshot thus shows the configuration of the
"stockmarketeventhub," created in the namespace. This Event Hub pulls live stock market data,
and the metrics such as throughput, messages, and requests are visible for the seamless
functioning of the hub.
![Image 7](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/7.png?raw=true)

This screenshot illustrates the shared access policies for the Event Hub, such as
StockMarketPolicy, which enables such authorized access to send and listen to data streams.
![Image 8](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/8.png?raw=true)
This screenshot demonstrates the settings of the "StockMarket_StreamAnalyticsJob". The job
utilizes data from the Event Hub for the purpose of analytics in Power BI. The Stream Analytics
Job implements real-time data processing through querying logic or a no-code editor.
![Image 9](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/9.png?raw=true)

This screenshot represents the configuration of the input of the Stream Analytics Job. The input
is connected to the "stockmarketeventhub," providing data feed from the Event Hub smoothly
to the processing pipeline.
![Image 10](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/10.png?raw=true)

The output in to the Stream Analytics Job as depicted in this screenshot is wired to Power BI for
Realtime data visualization under the name "StockDataOutput".
![Image 11](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/11.png?raw=true)

This is an example of a query in Azure Data Explorer through which data from the
"StockMarketDB" is accessed. This table consists of real-time stock market data including
"open, close, volume and adjusted close" figures.
![Image 12](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/12.png?raw=true)

The query will retrieve maximum closing prices for each stock index from a table named
stock_datatable grouped by indexes and order them in descending order with respect to
maximum closing prices.
![Image 13](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/13.png?raw=true)

It calculates the change in price from one day to another, using the High - Low data of various index
stocks from the Stock_Datatable table, orders them according to highest to lowest price change, and
selects the top records, with their corresponding dates.
![Image 14](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/14.png?raw=true)

This query averages the trading volume for each stock index and identifies it from the table called Stock
Data. It groups all this information according to the Index and sorts the resulting average trading volume
from highest to lowest.

![Image 15](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/15.png?raw=true)

Computes the volatility (standard deviation of the Close prices) of each of the stock indexes from the
Stock_Datatable table. The outcome is grouped by Index and ordered in descending order for volatility.

![Image 16](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/16.png?raw=true)



---

## Visualizations:

- Visualization in Azure Data Explorer
  ![Image 17](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/17.png?raw=true)


  ![Image 18](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/18.png?raw=true)
![Image 19](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/19.png?raw=true)

- Visualization in Power BI
  ![Image 20](https://github.com/Khushi-13/Real-Time-Stock-Market-Analysis-with-Azure-Data-Pipeline-/blob/main/20.png?raw=true)



---

## Conclusion:

The "Real-Time Stock Market Analysis with Azure Pipeline" project demonstrated how you can use cloud solutions to keep track of the stocks in real-time. This solution entered the advanced data pipeline, also bringing the complete set of activities concerning data ingestion, processing, and visualization under a single workflow.

### Key Achievements:
- The full pipeline automated the data handling and analysis to improve efficiency entirely.  
- Real-time and historical datasets provide an opportunity to improve understanding of market dynamics and trends.  
- Use of Azure services like Stream Analytics and Power BI to represent complex stock market data visually and powerfully.  

### Impact on Stock Market Analytics:
The project provides significant insights into financial decision-making by correlating live data with historical trend data. This equips analysts to detect trends and make decisions that are more informed and time-consistent in a rapidly changing market.  

### Lessons Learned:
- To achieve accurate and meaningful results, it was necessary to maintain high quality and consistent data.  
- The use of a multitude of Azure tools emphasizes flexibility and extensibility of solutions for large data management and analysis.  
- Processing and visualizing in real time is critical to enabling interesting insights.  

### Future Enhancements:
- Enriching the analysis further by expanding data sources to include sentiment analysis from social media platforms.  
- Predictive models and machine learning for improved trend forecasting and advanced predictive capabilities.  
- Real-time alerts and a more robust dashboarding tool could greatly enhance end-user usability of the system.  

### Final Remarks:
This project shows what modern cloud technologies can do to stock market analysis: combine historical data with real-time data for actionable insights. It has thus exhibited the strength that analytical tools can be developed to aid informed decisions in the fast-paced financial industry.  

**Reference links:**  
[API Documentation | Alpha Vantage](https://www.alphavantage.co/documentation/)
