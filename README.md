# E-commerce Product Association Mining Using Apache Spark and FP-Growth

## About the Project

This project analyses online retail transactions to identify products that customers frequently purchase together. It uses **Apache Spark (PySpark)** and the **FP-Growth algorithm** to find frequent product combinations and generate association rules.

These patterns can help retailers understand customer purchasing behaviour and make better decisions about product bundling, cross-selling, and product recommendations.

## Objectives

- Clean and prepare real-world retail transaction data.
- Group products into transaction baskets using invoice numbers.
- Identify frequently purchased product combinations.
- Generate association rules using support and confidence thresholds.
- Analyse product relationships using support, confidence, and lift.
- Export the results to CSV files for further analysis.

## Dataset

**Dataset:** Online Retail  
**Source:** UCI Machine Learning Repository  
**Link:** https://archive.ics.uci.edu/dataset/352/online+retail

The dataset contains transactions from a UK-based online retail business between 1 December 2010 and 9 December 2011.

The original dataset contains 541,909 records and includes invoice numbers, product codes, descriptions, quantities, prices, customer IDs, and countries.

Download `Online Retail.xlsx` from the dataset source before running the notebook.

## Technologies Used

- Python
- Apache Spark (PySpark 3.5.9)
- Pandas
- Java 8
- Jupyter Notebook
- FP-Growth algorithm

The project runs Spark in **local mode** using two processing threads. It does not require a multi-node cluster.

## Project Workflow

1. **Environment setup:** Check the Python and PySpark versions and create a Spark session.
2. **Data loading:** Convert the Excel dataset to CSV using Pandas and load it into Spark.
3. **Data cleaning:** Remove missing values, blank fields, cancelled invoices, invalid quantities and prices, non-numeric product codes, and duplicate records.
4. **Transaction basket creation:** Group distinct product codes by invoice and retain transactions containing at least two products.
5. **Frequent itemset mining:** Apply FP-Growth with a minimum support of `0.02`.
6. **Association rule generation:** Generate rules using a minimum confidence of `0.30`.
7. **Result interpretation:** Examine support, confidence, and lift to understand product associations.
8. **Export:** Save the association rules and frequent itemsets as CSV files.

## Results

| Metric | Result |
|---|---:|
| Original records | 541,909 |
| Records after cleaning | 472,253 |
| Records removed | 69,656 |
| Valid transaction baskets | 18,052 |
| Distinct products | 2,868 |
| Frequent itemsets | 430 |
| Association rules | 181 |

### Example Finding

One discovered rule was:

**WOODEN STAR CHRISTMAS SCANDINAVIAN → WOODEN HEART CHRISTMAS SCANDINAVIAN**

- **Confidence:** Approximately 75.93%
- **Lift:** Approximately 25.48

This means that about 75.93% of the transactions containing the wooden star also contained the wooden heart. The high lift indicates a strong association between the two products compared with their independent occurrence.

Association rules reveal patterns in historical transactions; they do not prove that purchasing one product causes a customer to purchase another.

## Output Files

After successfully running the notebook, the `output` folder contains:

- `association_rules.csv` — association rules with readable product names, confidence, lift, and support.
- `frequent_itemsets.csv` — frequent product combinations and their occurrence counts.

## How to Run the Project

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd <your-project-folder>
```

Replace the placeholders with your actual GitHub repository URL and folder name.

### 2. Install the required Python packages

```bash
pip install pyspark==3.5.9 pandas openpyxl notebook
```

Make sure Java 8 and Python are installed and configured correctly. The notebook should run with a compatible Java and PySpark environment.

### 3. Download the dataset

Download `Online Retail.xlsx` from the UCI Machine Learning Repository and place it in the notebook's working directory.

### 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open the project notebook and run the cells in order, starting with environment setup and ending with result export.

The notebook creates the `output` folder automatically.

## Project Limitations

- Spark is used in local mode rather than on a distributed multi-node cluster.
- Only transactions containing at least two distinct products are analysed.
- The support and confidence thresholds affect which itemsets and rules are generated.
- The results describe historical purchasing patterns and are not a live recommendation system.

## Conclusion

This project demonstrates how Apache Spark and FP-Growth can be used to discover frequently purchased product combinations from retail transaction data. It provides practical experience in data cleaning, transaction analysis, association rule mining, and exporting results for further analysis.

## Acknowledgement

The Online Retail dataset is provided by the UCI Machine Learning Repository and is used here for academic and learning purposes.
