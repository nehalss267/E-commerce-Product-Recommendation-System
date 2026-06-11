# 🛒 E-Commerce Recommender System V2

An end-to-end Machine Learning Recommender System built with Python, Scikit-Learn, and Gradio. This project uses NLP-based Collaborative Filtering to analyze an e-commerce transaction dataset and generate personalized product recommendations based on lookalike audiences.

## 🚀 Features

* **Collaborative Filtering:** Uses TF-IDF vectorization and Cosine Similarity to find users with overlapping purchase histories.
* **Feature Engineering:** Goes beyond simple product counts by injecting behavioral context into the NLP model:
* **Chronological Sorting:** Respects the timeline of purchases to understand buying sequences.
* **Price Personas:** Calculates average user spend to group customers into spending brackets (Cheap, Budget, Mid, Premium), preventing the system from recommending high-ticket items to low-spend users.
* **Recency Weighting:** Artificially boosts the mathematical importance of the most recently purchased item.


* **Offline Evaluation Pipeline:** Includes a custom "Leave-One-Out" testing harness to mathematically prove the model's accuracy before deployment.
* **Interactive UI:** A fully functional, web-accessible dashboard built with Gradio for real-time inference and demonstration.

## 🛠️ Tech Stack

* **Language:** Python 3.x
* **Data Processing:** Pandas, NumPy
* **Machine Learning:** Scikit-Learn (`TfidfVectorizer`, `cosine_similarity`)
* **Frontend/UI:** Gradio
* **Environment:** Jupyter Notebook / Google Colab

## 📊 Dataset

The model is trained on `Updated_sales.csv` (~2.55 MB / 30,394 rows). Each row represents a single transaction line item.

* **Key Columns Used:** `Order Date`, `Product`, `Price Each`, `Purchase Address` (used as the unique User ID).

## 📈 Evaluation Metrics

This system was evaluated using a **Leave-One-Out** approach (hiding exactly 1 item from users with 3+ purchases and asking the system to predict it in the Top 5).

* **Mean Recall@5:** `0.2800` (The model successfully predicted the exact hidden future purchase for 28% of the test users).
* **Mean Precision@5:** `0.0560` (Out of 5 recommendations given, how many were hits. Note: Mathematical max for this specific test design was 0.20).

## 💻 How to Run

This project is designed to run seamlessly in Google Colab or a local Jupyter Notebook environment.

1. Clone the repository and ensure you have the required libraries installed:
```bash
pip install pandas numpy scikit-learn gradio

```


2. Ensure the dataset (`Updated_sales.csv`) is in the same directory as the script/notebook.
3. Run the notebook cells sequentially.
* **Part 1 & 2:** Loads the data and runs the offline evaluation (printing metrics to the console).
* **Part 3:** Trains the final production model on 100% of the data.
* **Part 4:** Launches the Gradio web interface.


4. Click the public `share=True` link generated at the bottom of the notebook to interact with the UI in your browser.

