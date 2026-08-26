# Retail Insights Agent - Databricks Data Agent Project

## Project Objective
This project builds a working Data Agent on Databricks that analyzes retail
sales transactions and answers business questions in plain language. The
agent is designed for executives and senior leadership who need fast,
decision-ready insights without digging into raw data themselves.

## Tools Used
- Databricks (Data Agent / Genie)
- SQL (validation queries)
- `retail_sales_data` dataset

## Dataset Overview
**Table:** `retail_sales_data`

| Column | Description |
|---|---|
| Transaction ID | Unique identifier for each sale |
| Date | The date the transaction occurred |
| Customer ID | Unique identifier for the customer who made the purchase |
| Gender | Customer's recorded gender |
| Age | Customer's age at time of purchase |
| Product Category | The category of product purchased |
| Quantity | Number of units bought in that transaction |
| Price per Unit | Price of a single unit of the product |
| Total Amount | Total value of the transaction (Quantity × Price per Unit) |

## Steps Followed
1. Uploaded and reviewed the dataset in Databricks
2. Registered the table with column-level descriptions
3. Created the Retail Insights Agent and connected it to `retail_sales_data`
4. Wrote original agent instructions (see below)
5. Tested the agent with 10 business questions
6. Independently validated 3 of the agent's answers using SQL
7. Compiled findings into a full write-up (see Word document)

## Agent Instructions

**1. Role of the Agent**
You are a Retail Sales Performance Analyst for a multi-store retail company.
Your role is to analyze transactional sales data and deliver clear,
actionable insights that help senior leadership understand business
performance and make informed decisions.

**2. Users**
Your primary users are executives (CEO, senior leadership) who have limited
time. They require: fast, high-level insights; clear business impact;
minimal technical detail; actionable recommendations when appropriate.

**3. Dataset**
You must only use the dataset named `retail_sales_data`. This dataset
includes sales fields (used to analyze performance), customer fields (used
to understand buying behavior), product fields (used to evaluate product
performance), and time fields (used to identify trends and seasonality).
Do not assume or create fields that are not present in the dataset.

**4. Question Types**
Sales (revenue, growth, comparisons) · Customers (purchasing patterns,
frequency, segmentation) · Products (best/worst performers, category
analysis) · Trends (time-based insights).

**5. How to Explain Insights (Tone & Structure)**
Responses follow: (1) a headline leading with the most important number,
(2) bullet-point explanation with exact numbers and brief context,
(3) an optional recommendation, only if there is strong evidence. Tone is
professional, clear, concise, and focused on business impact.

**6. Handling Ambiguity**
If a question is unclear or incomplete, do not guess - ask a clarifying
question. If partially answerable, provide what's available and state
what's missing. If data is missing, say so explicitly and suggest the
closest alternative insight if possible.

**7. No Fabrication Rule**
Never invent numbers, categories, or trends. Never assume missing data.
Only use what exists in `retail_sales_data`. If the data doesn't support
an answer, say so clearly and offer a related insight if possible.

**8. Recommendations**
Provide recommendations only when supported by clear, observable data
patterns. Suggest one clear, practical action to avoid overcomplicated
strategies. If confidence is low, present facts only, without a
recommendation.

## Sample Questions Tested
- Is there a noticeable difference in spending between male and female customers?
- Which product category generates the highest total revenue, and which one generates the lowest sales?
- How does average daily revenue change across the week?
- How are sales doing?
- What was the profit margin last quarter? *(tests the No Fabrication rule)*
- What is the most reviewed product, and were customers satisfied? *(tests the No Fabrication rule - no review data exists)*

*(Full set of 10 questions and answers, with screenshots, is in the Word document.)*

## Validation of 3 Agent Answers
Three of the agent's answers were independently checked against the dataset
using SQL queries -  all three were confirmed accurate:

1. **Gender spending difference** - SQL confirmed Male $223,160 / Female
   $232,840, matching the agent exactly.
2. **Highest/lowest revenue category** - SQL confirmed Electronics
   ($156,905), Clothing ($155,580), Beauty ($143,515), matching the agent
   exactly.
3. **Average daily revenue by day of week** - SQL confirmed Saturday
   highest ($1,608.47) and Thursday lowest ($1,098.67). The agent's 43%
   gap was slightly off from the SQL's 46.4%, most likely due to rounding this doesn't change the underlying conclusion.

*(Full validation evidence and verdicts are in the Word document.)*

## Key Insights
- **Zero customer retention** - all 1,000 transactions came from unique
  customers; the business has no repeat purchases.
- **Gender has no meaningful effect on spending** (0.2% difference between
  genders).
- **Beauty underperforms on transaction volume, not price** - it has the
  highest average transaction value ($467) but the fewest transactions.
- **Sales are highly volatile month-to-month** with no clear seasonal
  pattern (125% swing between weakest and strongest months).
- **Weekly demand peaks on Saturday and dips on Thursday**, driven mainly
  by Electronics - Beauty peaks on Fridays instead.

## Business Recommendations
1. Launch a customer retention program, zero repeat purchases is the
   single biggest growth opportunity.
2. Address Beauty's low transaction volume with targeted promotions or
   bundling, rather than discounting.
3. Smooth out month-to-month volatility with a consistent marketing
   cadence, and investigate what drove the September low.
4. Tailor weekly promotions by category rather than applying a single
   store-wide "weekend sale."

## Conclusion
The instructions proved robust under testing, the No Fabrication rule
correctly stopped the agent from inventing figures for profit margin and
product reviews, and the headline-first structure kept answers easy to
read. The main challenge was in SQL validation: an initial SUM/AVG mix-up
on the day-of-week query produced misleading numbers before being caught
and corrected. Given more time, the next step would be stress-testing the
instructions with edge cases to find where they start to break down,
rather than adding further rules pre-emptively.

## Full Documentation
See [`Retail_Insights_Agent_Report.docx`](./Retail_Insights_Agent_Report.docx)
in this repository for the complete write-up, including all screenshots,
the full 10 test questions with agent answers, and validation evidence.
