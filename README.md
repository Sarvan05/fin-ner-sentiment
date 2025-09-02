# fin-ner-sentiment
# 🏦 Financial Named Entity Recognition (NER) + Sentiment Analysis with BERT

This project fine-tunes a **BERT-based model** for **Named Entity Recognition (NER)** and **Sentiment Detection** on financial text using the [FinEntity dataset](https://huggingface.co/datasets/yixuantt/FinEntity).  

The model not only extracts financial entities (e.g., organizations, money, locations) but also identifies the **sentiment polarity** (**Positive, Negative, Neutral**) expressed about them.

---

## 📌 Features
- Uses **BERT (`bert-base-uncased`)** for token classification
- Detects **financial entities** (ORG, MONEY, LOC, etc.)
- Identifies **sentiment** behind entities (Positive / Negative / Neutral)
- Handles **IOB2 tagging scheme** (`B-Positive`, `I-Negative`, etc.)
- Trained & evaluated with Hugging Face **Trainer API**
- Supports **precision, recall, F1, accuracy** evaluation via `seqeval`
- Inference pipeline for real-world financial news & documents

---

## 🚀 Project Workflow

1. **Load Dataset**  
   - Uses the [FinEntity dataset](https://huggingface.co/datasets/yixuantt/FinEntity)  
   - Contains annotated financial text with entity spans and sentiment labels  

2. **Preprocessing**  
   - Tokenize input text with BERT tokenizer  
   - Convert entity labels into **IOB2 format**  
   - Align character-based annotations with tokens  

3. **Model Setup**  
   - Fine-tunes `bert-base-uncased` with `AutoModelForTokenClassification`  
   - Uses sentiment-aware label schema:  
     ```
     ['O', 'B-Negative', 'I-Negative', 'B-Neutral', 'I-Neutral', 'B-Positive', 'I-Positive']
     ```

4. **Training**  
   - 5 epochs, AdamW optimizer, weight decay = 0.01  
   - Dynamic padding with `DataCollatorForTokenClassification`  

5. **Evaluation**  
   - Metrics: Precision, Recall, F1, Accuracy (via `seqeval`)  

6. **Inference**  
   - Run trained model in an **NER + Sentiment pipeline**  
   - Example input:  
     ```
     "Tesla shares rose 15% after 1 year"
     ```  
   - Example output:  
     ```
     Entity: Tesla | Sentiment: Positive | Score: 0.9876
     Entity: 15%   | Sentiment: Positive | Score: 0.9812
     ```

---

## ⚙️ Installation & Setup

Clone the repository:
```bash
git clone https://github.com/your-username/fin-ner-sentiment.git
cd fin-ner-sentiment

