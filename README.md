# E-Commerce Customer Segmentation & Recommender System

## 📌 Overview
This project implements an end-to-end customer analytics pipeline for an e-commerce platform. It combines **RFM (Recency, Frequency, Monetary)** analysis to segment customers based on their purchasing behavior with a **Content-Based Collaborative Filtering** approach to generate personalized product recommendations.

## 🚀 Features
* **RFM Customer Segmentation:** Automatically scores and groups customers into actionable segments:
  * Premium Customer
  * Repeat Customer
  * Top Spender
  * At Risk Customer
  * Inactive Customer
* **TF-IDF & Cosine Similarity Engine:** Builds a user-item profile based on aggregated product descriptions and calculates the cosine similarity between users to find "lookalike" customers.
* **Smart Recommendations:** Recommends products purchased by similar customers, strictly filtering out items the target customer has already bought.
* **Targeted Cohort Analysis:** Designed to generate recommendations within specific business segments (e.g., generating high-value cross-sells for "Premium Customers").

## 🛠️ Tech Stack & Dependencies
This project relies on standard data science libraries in Python.
* `pandas` (Data manipulation and aggregation)
* `scikit-learn` (TF-IDF Vectorization and Cosine Similarity calculations)

To install the required dependencies, run:
```bash
pip install pandas scikit-learn
```

## 📊 Dataset Requirements
The script expects a dataset named `ecommerce_data_electronics.csv` in the root directory. Based on the pipeline, the dataset must contain the following columns:
* `time_stamp`: Date and time of the transaction.
* `card_name`: Unique identifier for the customer (e.g., customer name or ID).
* `product_id`: Unique identifier for the purchased item.
* `price`: The cost of the transaction/product.
* `product`: The name or short title of the product.
* `product_description`: Text description of the product used for TF-IDF vectorization.

## 🧠 How It Works

### Phase 1: RFM Analysis
1. Calculates **Recency** (days since last purchase), **Frequency** (total number of purchases), and **Monetary Value** (total amount spent).
2. Assigns quartiles (1-4) to each metric.
3. Concatenates the scores into a 3-digit RFM score (e.g., `444` for the best customers) and maps them to business logic segments.

### Phase 2: Recommendation Generation
1. Filters the dataset down to a specific target cohort (e.g., Top 10 Premium Customers).
2. Aggregates all purchased product descriptions for each user into a single text document.
3. Converts these documents into a TF-IDF matrix.
4. Computes a Cosine Similarity matrix to find the most similar users to the target user.
5. Identifies products bought by similar users but *not* by the target user and returns the top `N` recommendations.

## 💻 Usage
Run the script directly using Python. 

```bash
python recommender.py
```

### Example Output
The script will output the head of the RFM tables, the distribution of customer segments, and specific recommendations for target customers:

```text
Recommendations for Ashley Perry:
['Wireless Noise-Cancelling Headphones', 'Ergonomic Office Chair', 'Mechanical Keyboard']

Recommendations for Clifford Stanley:
['4K Web Camera', 'USB-C Hub', 'Smart LED Desk Lamp']
```

***
