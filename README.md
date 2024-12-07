# CS532-final-project 
## System 2 Overview

This project performs sentiment analysis on news articles to estimate stock market trends. Two systems were implemented: one using PySpark and Flan-T5 (System 1) and the other using Llama-3.2-1B (System 2). Performance metrics such as memory usage, throughput, and accuracy are used to evaluate these systems.

---

## How to Run the Program

### Prerequisites
- Required Python libraries: `transformers`, `torch`, `psutil`, `pandas`, `scikit-learn`, `requests`, `GPUtil`
- GPU-enabled environment for optimal performance
- News API Key: Obtain from [NewsAPI](https://newsapi.org/)
- OpenAI API Key: Obtain from [OpenAI](https://openai.com/)

---

## Running the Program

You can run each cell of the python notebook sequentially:

### Step 1: Fetch News Articles
Modify the `fetch_news_api` function:
- Update the `search_keyword`, `start_date`, and `end_date` parameters to fetch relevant news.
- Replace the placeholder API key with your NewsAPI key.

This will fetch articles and save them in `news_data.json`.

### Step 2: Preprocess Articles
The program preprocesses articles using `extract_news_api`. It removes irrelevant data, saving clean content for sentiment analysis.

### Step 3: Sentiment Analysis
Sentiment analysis uses:
1. **Llama-3.2-1B Model (System 2)**.
2. **GPT-4o-mini** for ground truth comparison.

Results are saved in `analyze_news.json` and `analyze_news_openai.json`.

### Step 4: Evaluation
Evaluate accuracy, memory usage, and throughput

---

## Experiments and Test Cases

### Test Scenarios
Test results for different keywords and time ranges:
| Search Keyword | Date Range  | Accuracy |
|----------------|-------------|----------|
| Apple          | 1 Day       | 66.30%   |
| Apple          | 1 Month     | 56%      |
| Nvidia         | 1 Day       | 52.58%   |

### Quantization
Three techniques were tested:
1. **Base Model (No Quantization)**: High memory usage and low throughput.
2. **TorchAO INT8 Weight-Only Quantization**: Moderate memory savings, but reduced throughput.
3. **LLM BNB 8-bit Quantization**: Significant memory savings with minimal throughput impact.

---

## Performance Metrics
Metrics used:
1. **Peak Memory Usage**
2. **Throughput (seconds/article)**
3. **Accuracy**

Results:
| System | GPU Memory Usage | Throughput | Accuracy |
|--------|------------------|------------|----------|
| 1      | 2.23 GB          | 0.29       | 72.97%   |
| 2      | 1.29 GB          | 0.23       | 63.03%   |

---

## Conclusion
- **System 1** excels in accuracy.
- **System 2** is superior in GPU memory usage and throughput.
- LLM BNB 8-bit quantization offers the best trade-off between memory and throughput.

---

## Possible Improvements
1. Fine-tune Llama-3.2-1B to reduce neutral sentiment classifications.
2. Implement real-time news analysis.
3. Explore advanced quantization techniques for better performance.
