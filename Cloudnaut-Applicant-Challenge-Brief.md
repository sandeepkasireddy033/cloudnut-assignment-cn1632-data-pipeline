# Cloudnaut Applicant Challenge

## Contact Operations Data Rescue

Cloudnaut is selecting freshers for an intensive AWS Data, AI/ML, GenAI, AgentCore and Amazon Connect enablement program. Prior professional experience with these technologies is not required.

This challenge evaluates whether you can understand an unfamiliar problem, use available resources and AI tools responsibly, produce a working result, verify it, and explain your decisions.

## Scenario

A client operates a contact centre across voice, chat and email. Its weekly operations report is unreliable because the exported contact records contain duplicates, inconsistent labels, invalid values and missing information.

You have been asked to create a reproducible Jupyter notebook that cleans the data, calculates operational metrics, prioritises contacts and produces a queue-level report.

## What you receive

- A personalised Jupyter notebook containing your candidate code
- A personalised CSV dataset
- This assignment brief
- Submission instructions

Do not exchange your candidate code or dataset with another applicant.

## Environment

Google Colab is recommended. You may instead use Kaggle Notebooks or a local Jupyter environment.

You need only:

- Python 3.11 or later
- pandas
- matplotlib

No AWS account, paid API, GPU, VPS, Git repository or external service is required.

## Time expectations

- Expected focused effort: approximately 3 hours
- Recommended maximum effort: 4 hours
- Submission window: specified in your invitation email

Record your approximate time spent in the final notebook section. Time is not used as a speed competition. It helps us interpret the work fairly.

## AI usage policy

You may use ChatGPT, Claude, Gemini, Copilot, Cursor or any other AI tool.

You remain responsible for every submitted line and statement. You must be able to:

1. Explain the solution in your own words.
2. Identify what you accepted, changed or rejected from AI output.
3. Show how you verified important claims.
4. Modify the solution if a requirement changes.

Do not include complete private chat histories. Complete the AI Assistance Log in the notebook for your most consequential uses of AI.

## Required functions

Do not rename these functions or change their parameters:

```python
def clean_contacts(df):
    ...

def calculate_metrics(clean_df):
    ...

def assign_priority(contact):
    ...

def build_queue_summary(clean_df):
    ...
```

Your functions will be tested using your dataset and unseen test data.

## Data-cleaning contract

`clean_contacts(df)` must return a new pandas DataFrame and must not modify the input DataFrame in place.

Apply the following rules in the stated order:

1. Preserve the original row order while cleaning.
2. Convert `contact_id` to trimmed text. Remove rows with a missing or blank contact ID.
3. Parse `started_at` as a timezone-aware UTC timestamp. The source may contain ISO timestamps or `DD/MM/YYYY HH:MM` timestamps. Remove rows with an invalid timestamp.
4. Remove duplicate contact IDs, keeping the first remaining occurrence in the original row order.
5. Trim text labels and compare them case-insensitively.
6. Canonical `channel` values are `voice`, `chat` and `email`. Use `unknown` for missing or unrecognised values.
7. Your dataset contains all the queue values used by the contact centre. Examine the `queue` column to determine the valid canonical values. Use `unassigned` for any missing or unrecognised queue values.
8. Canonical `outcome` values are `resolved`, `abandoned`, `transferred` and `unresolved`. Use `unresolved` for missing or unrecognised values.
9. Convert `wait_seconds` and `handle_seconds` to numeric values. Convert invalid or negative values to missing values. Zero is valid.
10. Convert `customer_rating` to a numeric value. Only whole-number ratings from 1 to 5 are valid. Convert every other value to missing.
11. Trim `agent_id` and `customer_message`. Use `unassigned` for a missing agent and an empty string for a missing message.
12. Preserve the original column order and return a clean zero-based index.

## Metrics contract

`calculate_metrics(clean_df)` must return a dictionary containing exactly these keys:

```text
total_contacts
voice_contacts
chat_contacts
email_contacts
unknown_channel_contacts
average_wait_seconds
p90_wait_seconds
abandonment_rate_pct
resolution_rate_pct
```

Rules:

- Channel counts use the cleaned `channel` column.
- Average and 90th-percentile wait calculations ignore missing values.
- Use pandas' default linear quantile calculation for the 90th percentile.
- Rate denominator is `total_contacts`.
- Rates and wait metrics must be rounded to two decimal places.
- Return `None` for a wait metric if there are no valid wait values.
- Return `0.0` for a rate if there are no contacts.

## Priority contract

`assign_priority(contact)` receives a pandas Series or dictionary representing one cleaned contact.

Apply these rules from top to bottom:

1. Return `High` if the outcome is `abandoned`.
2. Return `High` if `wait_seconds` is at least 180.
3. Return `High` if the lower-cased customer message contains `fraud`, `charged twice` or `refund`.
4. Return `Medium` if the outcome is `transferred`.
5. Return `Medium` if `wait_seconds` is at least 60.
6. Otherwise return `Low`.

Missing wait time must not cause an error.

## Queue summary contract

`build_queue_summary(clean_df)` must return a DataFrame with these columns in this order:

```text
queue
contacts
average_wait_seconds
abandonment_rate_pct
```

Rules:

- Include every queue present in the cleaned data.
- `contacts` is the number of contacts in the queue.
- Average wait ignores missing values and is rounded to two decimal places.
- Abandonment rate uses all contacts in that queue and is rounded to two decimal places.
- Sort by `contacts` descending, then `queue` ascending.
- Return a clean zero-based index.

## Required outputs

Your notebook must create:

- `cleaned_contacts.csv`, including the new `priority` column
- `queue_summary.csv`
- `submission_summary.json`, containing your candidate code and calculated metrics
- At least one meaningful chart
- At least four additional assertions written by you
- A completed AI Assistance Log
- A concise management summary and reflection

## What we assess

- Whether the notebook runs from beginning to end
- Functional correctness on visible and unseen inputs
- Data reasoning and handling of edge cases
- Reproducibility and code organisation
- Quality of verification
- Judgement when using AI
- Clarity and honesty of communication

A polished notebook with incorrect or unexplained results will not score well. A simple working solution that is verified and clearly understood can score strongly.

## Important rules

- Work independently.
- Do not hard-code outputs from your assigned CSV.
- Do not rename required functions.
- Do not delete the candidate code from the notebook.
- Do not call external APIs from the submitted notebook.
- Do not include credentials or secrets.
- Your notebook must work after selecting **Runtime > Restart session and run all** in Google Colab.
- Finalists may be asked to explain and modify the submitted solution in a short live session.
