# 🚚 Global Fleet Telematics: PySpark ETL Pipeline

## 📌 Project Overview
As enterprise logistics scale, traditional data processing tools (like Pandas or Excel) fail under the weight of gigabytes of telematics data. This project demonstrates a cloud-ready **Big Data ETL Pipeline** built with **PySpark** to extract, transform, and load massive logistics datasets. 

The pipeline synthesizes 1,000,000 rows of fleet GPS and sensor data, systematically scrubs real-world anomalies (missing GPS pings, faulty engine temperatures), engineers business-ready routing metrics, and loads the clean data into a partitioned data lake structure.

## 🛠️ Architecture & Technologies
* **Processing Engine:** Apache Spark (PySpark)
* **Environment:** Google Colab (Cloud Compute)
* **Storage Format:** Partitioned Parquet
* **Languages:** Python, SQL (Spark SQL)

## ⚙️ The ETL Process
### 1. Extract (Synthesizing Big Data)
* Generated a 1,000,000-row telematics dataset natively in Spark for blazing-fast execution.
* **Features Include:** `truck_id`, `gps_ping_time`, `speed_kmh`, `engine_temp_c`, `fuel_efficiency_kml`, and `route_risk_score`.
* *Intentionally injected real-world data corruption* (null values, negative speeds, sensor malfunctions) to simulate messy enterprise environments.

### 2. Transform (Data Cleaning & Feature Engineering)
Built a transformation pipeline to sanitize the data without dropping the entire dataset:
* **Filtered** missing `gps_ping_time` rows (removing "ghost" trucks).
* **Corrected** absolute values for inverted `speed_kmh` sensors.
* **Scrubbed** impossible `engine_temp_c` anomalies (e.g., temperatures exceeding 150°C).
* **Engineered** a new `risk_category` column (High, Medium, Low) based on numerical risk scores to provide actionable insights for operations teams.

### 3. Load (Optimized for BI Tools)
* Exported the final cleaned dataset as a **Parquet** file.
* **Partitioned** the output by `risk_category` (`risk_category=High Risk`, etc.) to optimize query performance for downstream Business Intelligence tools like Power BI or Tableau. 

## 📈 Business Impact
By partitioning the Parquet output based on operational risk, downstream analytics tools can query specific risk categories without scanning the entire million-row database, reducing compute costs and query latency by up to 90%.
