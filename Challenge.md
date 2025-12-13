# 🧹 Data Preprocessing Challenge: From Classical ML to LLMs

## 🚀 Overview & Objective

Welcome to the real world of Data Engineering! In this assignment, you will step into the role of a **Data Scientist/Engineer** at a tech company. Your mission is to prepare raw data for two distinct internal stakeholders:

1.  **The Analytics Team (Classic ML):** They need clean, structured tabular data for statistical analysis, regression, and classification models.
2.  **The AI Team (Generative AI):** They need high-quality, normalized unstructured text to Fine-tune a Large Language Model (LLM).

You will work with **two datasets**: one English and one Persian. This will test your ability to handle general data cleaning as well as language-specific challenges.

---

## 🛠️ Prerequisites & Tools

- **Language:** Python 3.x
- **Libraries:** `pandas`, `numpy`, `matplotlib/seaborn`, `scikit-learn`, `re` (Regex).
- **Optional (for Persian NLP):** `hazm` or `parsivar`.

---

## 📂 Part 1: The English Dataset

**Dataset:** Women's E-Commerce Clothing Reviews
This dataset contains customer reviews, ratings, and categorical data. It is a "Hybrid" dataset suitable for both numerical analysis and NLP.

🔗 **Download Link:** [Women's E-Commerce Clothing Reviews (Kaggle)](https://www.kaggle.com/datasets/nicapotato/womens-ecommerce-clothing-reviews)

### 🔹 Task A: Classic Preprocessing (Structured Data)

_Goal: Prepare the data for a Sentiment Classification Model (Logistic Regression/Random Forest)._

1.  **Handling Missing Values:**
    - Analyze the `Title` and `Age` columns.
    - Decide on a strategy: Imputation (filling with mean/median/constant) or Dropping rows? Justify your choice.
2.  **Outlier Detection:**
    - Inspect the `Positive Feedback Count` column.
    - Use **IQR (Interquartile Range)** or **Z-Score** to identify and handle statistical outliers.
3.  **Categorical Encoding:**
    - Convert the `Department Name` or `Class Name` column into numerical format using **One-Hot Encoding** or **Label Encoding**.

### 🔹 Task B: LLM Preprocessing (Unstructured Text)

_Goal: Clean the text to Fine-tune a Llama-3 or GPT model._

1.  **Text Noise Removal:**
    - Remove artifacts like HTML tags (e.g., `<br />`) if present.
    - Collapse multiple whitespaces into a single space.
2.  **Contraction Expansion:**
    - Convert contractions to full forms for better model embedding (e.g., _"won't"_ $\rightarrow$ _"will not"_, _"I'm"_ $\rightarrow$ _"I am"_).
3.  **Instruction Formatting (JSONL):**
    - Transform the data into the standard **Instruction Tuning** format.
    - **Output Example:**
      ```json
      {
        "instruction": "Classify the sentiment of the following review.",
        "input": "This dress is stunning but runs slightly small.",
        "output": "Positive"
      }
      ```

---

## 📂 Part 2: The Persian Dataset

**Dataset:** Digikala Product Reviews
This dataset contains comments from Iranian users. It presents unique challenges regarding character encoding and mixed languages (Persian/English).

🔗 **Download Link:** [Digikala Comments Persian Dataset (Kaggle)](https://www.kaggle.com/datasets/mfaaris/digikala-comments-persian-dataset)
_(Note: If the link is unavailable, use any "Digikala User Comments" dataset found on Kaggle)._

### 🔹 Task A: Classic Preprocessing (Structured Data)

_Goal: Analyze user behavior and engagement._

1.  **Date Conversion:**
    - The dates are likely in **Jalali (Shamsi)** format or string format. Convert them to a standard Gregorian `Datetime` object to visualize "Reviews per Month".
2.  **Handling Imbalanced Data:**
    - Analyze the `Recommendation` column (e.g., "Recommended" vs. "Not Recommended").
    - Visualize the class imbalance and propose a method to fix it (e.g., Undersampling or SMOTE).
3.  **Feature Engineering:**
    - Create a new column: `word_count`.
    - Investigate: Is there a correlation between the length of the comment and the number of `Likes` it received?

### 🔹 Task B: LLM Preprocessing (Persian Challenges)

_Goal: Clean the text for a Persian LLM (e.g., Dorna or PersianGPT)._

1.  **Character Normalization (Crucial):**
    - Standardize Arabic characters to Persian:
      - Replace Arabic 'Kaf' (ك) with Persian 'Ke' (ک).
      - Replace Arabic 'Yeh' (ي) with Persian 'Ye' (ی).
    - Normalize numbers: Convert Persian/Arabic numerals (۱۲۳) to English numerals (123).
2.  **Zero-Width Non-Joiner (Half-Space):**
    - Fix spacing issues. Convert words like "می شود" (two words) to "می‌شود" (one word with ZWNJ).
    - _Hint: You can use the `Hazm` library or Regex for this._
3.  **PII Redaction (Privacy):**
    - Write a Regex pattern to detect Iranian phone numbers (starting with 09...) inside the comments.
    - Replace them with a token: `[PHONE_NUMBER_REMOVED]`.

---

## 📦 Deliverables

Please submit a single **Jupyter Notebook (.ipynb)** containing:

1.  **Code:** Clean, commented code for all tasks above.
2.  **Visualizations:** "Before" and "After" plots (e.g., distribution of Age before and after filling missing values).
3.  **LLM Sample:** A small export (text file) showing 5 rows of the Persian data converted to JSONL format.

---

## 💡 Helpful Tips

- **Do not** simply drop all missing data. Try to save as much information as possible.
- For LLM cleaning, remember that "Stopword Removal" is often **bad** for modern LLMs because it destroys the sentence structure. Focus on noise removal instead.
- Regular Expressions (`re` library) are your best friend for text cleaning!

**Good Luck! Happy Cleaning! 🧹✨**
