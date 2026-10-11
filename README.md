# cloudnut-assignment-cn1632-data-pipeline

# Contact Center Data Analysis & Cleaning (Candidate ID: CN-1632)

## 📌 Project Overview
This repository contains the data processing, deduplication, and performance analysis workflow for customer contact records under assessment **CN-1632**. The pipeline processes raw omnichannel contact records, handles missing and duplicate entries, and aggregates key service performance metrics.

---

## 📁 Repository Structure

```text
├── data/
│   ├── raw_contacts.csv               # Original raw contact data (189 records)
│   ├── CN-1632_cleaned_contacts.csv   # Cleaned and deduplicated dataset (115 records)
│   └── CN-1632_queue_summary.csv      # Queue-level performance metrics
├── output/
│   └── CN-1632_submission_summary.json# Overall performance metrics summary
├── process_data.py                    # Data cleaning and transformation script
└── README.md                          # Project documentation

⚙️ Data Cleaning & Processing Workflow
Deduplication:

Identified and removed duplicate entries using contact_id, narrowing the dataset from 189 records down to 115 unique contacts.

Standardization & Missing Values:

Standardized contact channels (email, chat, voice, unknown).

Mapped and normalized contact outcomes (resolved, unresolved, transferred, abandoned).

Handled null values across agent assignments and rating fields.

Feature Engineering:

Derived the contact priority attribute based on urgency and wait times.

📊 Summary of Results
Key Performance Indicators (KPIs)
Total Valid Contacts: 115

Channel Distribution:

Email: 35

Chat: 33

Voice: 24

Unknown: 23

Average Wait Time: 110.40 seconds (~1.84 minutes)

P90 Wait Time: 202.00 seconds (~3.37 minutes)

Abandonment Rate: 16.52%

Resolution Rate: 22.61%

🚀 How to Run
Prerequisites
Python 3.8+

Required libraries:

Bash
pip install pandas numpy
Execution
Run the data pipeline script to regenerate cleaned datasets and JSON summaries:

Bash
python process_data.py

---

### Key Tips for Your README:
* **Replace `process_data.py`** with whatever filename you used for your code (e.g., `main.py`, `analysis.ipynb`, etc.).
* If your evaluator requires specific instructions on how to grade or run your code, pla
