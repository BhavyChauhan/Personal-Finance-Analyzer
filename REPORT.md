# Project Report

## Personal Finance Analyzer

**Course:** Python Essentials
**Submitted by:** [Your Name]
**Roll No. / Enrollment No.:** [Your Roll No.]
**Branch / Year:** B.Tech, 1st Year
**Date:** [Date of Submission]

---

## 1. Abstract

Personal Finance Analyzer is a command-line application written in Python. It lets a user record income and expenses, view all transactions, search them, and analyse spending by month and by category. It also calculates savings and the savings rate, and it can export a report as a text file. All data is stored in a JSON file, so nothing is lost when the program is closed. The project uses only the Python standard library and shows the basic concepts learnt in the Python Essentials course through a real-world problem.

---

## 2. Introduction

Students and beginners often do not know how much money they spend and on what. Most of them do not keep any record, so at the end of the month the money is finished and they do not know where it went. Writing everything in a notebook is slow, and adding up the numbers by hand can lead to mistakes.

This project solves that problem with a small Python program. The user only enters the amount, date and category of each transaction. The program does all the calculations, saves the data and shows useful summaries.

---

## 3. Objectives

1. To build a useful real-world application using only basic Python.
2. To record income and expenses and store them permanently.
3. To calculate total income, total expenses, savings and savings rate.
4. To show spending by category and by month.
5. To validate user input so that the program does not crash.
6. To practise functions, loops, lists, dictionaries, file handling, JSON, exception handling and the `datetime` module.

---

## 4. Problem Statement

To develop a menu-driven Python program that stores the income and expenses of a user, analyses the spending habits, calculates savings and generates a financial report, without using any external library or database.

---

## 5. Tools and Technologies

| Item | Details |
|---|---|
| Language | Python 3.8 or above |
| Modules used | `json`, `os`, `datetime` (all from the standard library) |
| Data storage | JSON file (`finance_data.json`) |
| Report format | Text file (`financial_report.txt`) |
| Editor | Visual Studio Code |
| Interface | Command line (terminal) |

No external packages are required, so `requirements.txt` is empty.

---

## 6. Features

1. **Dashboard** - total income, expenses, savings, savings rate, number of transactions, current month and top spending category.
2. **Add Income** - amount, date, source (Salary, Pocket Money, Freelancing, Scholarship, Other) and an optional description.
3. **Add Expense** - amount, date, category (Food, Transport, Education, Shopping, Hostel/Rent, Entertainment, Health, Bills, Other) and description.
4. **View Transactions** - all transactions in a table, sorted by date.
5. **Search Transactions** - by date, category, type or amount range.
6. **Monthly Analysis** - income, expenses, savings, savings rate, number of transactions, highest expense and top category for a selected month.
7. **Spending Categories** - amount spent in each category and its percentage of total expenses.
8. **Savings Analysis** - savings, savings rate and a simple status message.
9. **Financial Summary** - complete summary with highest and lowest expense, and a comparison of months.
10. **Export Report** - saves everything to `financial_report.txt`.

---

## 7. Project Structure

```
personal_finance_analyzer/
├── main.py                 # the complete program
├── requirements.txt        # no extra packages needed
├── README.md               # how to run and use the project
├── REPORT.md               # this report
├── finance_data.json       # created automatically when data is saved
└── financial_report.txt    # created automatically when a report is exported
```

---

## 8. System Design

### 8.1 How the program works

```
Start
  |
  v
Load data from finance_data.json  (empty list if missing or corrupted)
  |
  v
+--> Show dashboard and menu
|         |
|         v
|    User enters choice (1-10)
|         |
|         v
|    Run the selected feature  --> data changed? --> save to JSON file
|         |
+---------+   (until the user chooses 10)
  |
  v
Exit
```

### 8.2 Data structure

Each transaction is a dictionary, and all transactions are kept in a list:

```python
{
    "date": "01-09-2026",
    "type": "Income",          # or "Expense"
    "category": "Salary",
    "amount": 30000.0,
    "description": "September salary"
}
```

In the file the list is stored like this:

```json
{
    "transactions": [
        { "date": "01-09-2026", "type": "Income", "category": "Salary",
          "amount": 30000.0, "description": "September salary" }
    ]
}
```

### 8.3 Organisation of `main.py`

The program is divided into six parts:

| Part | Purpose | Main functions |
|---|---|---|
| 1. Helper functions | Printing and taking valid input | `print_heading()`, `format_money()`, `get_amount()`, `get_date()`, `get_text()`, `get_number()`, `pick_from_list()`, `ask_yes_no()` |
| 2. Saving and loading | File handling | `load_data()`, `save_data()`, `export_report()`, `is_valid()` |
| 3. Calculations | All the maths | `get_total()`, `get_savings_rate()`, `get_category_totals()`, `get_top_category()`, `get_highest_expense()`, `get_lowest_expense()`, `get_months()`, `get_message()` |
| 4. Transactions | Add, view, search | `add_income()`, `add_expense()`, `print_table()`, `view_transactions()`, `search_transactions()` |
| 5. Analysis and report | Analysis screens | `show_monthly_analysis()`, `show_categories()`, `show_savings_analysis()`, `show_summary()`, `make_report()` |
| 6. Main program | Dashboard and menu | `show_dashboard()`, `show_menu()`, `main()` |

---

## 9. Important Formulas

```
Savings       = Total Income - Total Expenses
Savings Rate  = (Savings / Total Income) x 100
Category %    = (Category Total / Total Expenses) x 100
```

If the total income is 0, the savings rate is shown as 0.00% so that the program does not divide by zero.

**Savings messages:**

| Condition | Message |
|---|---|
| Expenses greater than income | Your expenses are higher than your income. |
| Savings rate 30% or more | Excellent saving! |
| Savings rate 10% to below 30% | Your savings are moderate. |
| Savings rate below 10% | Your savings are low. |

These are only simple messages. The program does not give financial or investment advice.

---

## 10. Python Concepts Used

| Concept | Where it is used |
|---|---|
| Variables, strings, integers, floats | Throughout the program, e.g. `format_money()` |
| Lists | `transactions`, `EXPENSE_CATEGORIES`, `INCOME_SOURCES` |
| Dictionaries | Each transaction, `get_category_totals()` |
| if / elif / else | Menu in `main()`, `get_message()` |
| for loops | `get_total()`, `print_table()`, searching |
| while loops | Main menu loop, input functions such as `get_amount()` |
| Functions, parameters, return values | Every part of the program |
| Exception handling | `try / except` in `get_amount()`, `get_date()`, `load_data()`, `save_data()` |
| File handling | Reading and writing the JSON file and the report file |
| JSON | `json.load()` and `json.dump()` |
| datetime | Date validation in `get_date()`, month grouping in `get_month_key()` |
| Modular programming | Program divided into small functions and six parts |

---

## 11. Input Validation and Error Handling

The program should not crash because of wrong input, so every input is checked in a loop until the user enters a valid value.

| Problem | How it is handled |
|---|---|
| Letters entered instead of a number | `try / except ValueError`, message shown, asked again |
| Negative or zero amount | Rejected with a message |
| Very large amount, `nan` or `inf` | Rejected as not valid |
| Empty input | Rejected with a message |
| Invalid date (for example 31-02-2026) | `datetime.strptime()` raises `ValueError`, asked again |
| Invalid menu choice | Range check, asked again |
| Missing data file | Program starts with empty data, file is created on first save |
| Corrupted JSON file | Warning shown, old file is renamed to `finance_data.json.bak`, program starts with empty data |
| Some invalid transactions in the file | Those are skipped and the rest are loaded |
| Ctrl + C pressed | Program closes politely without an error |

---

## 12. Testing

The program was tested by running it with different inputs. Some of the tests:

| No. | Test | Expected result | Result |
|---|---|---|---|
| 1 | Enter `abc` as amount | Error message, asked again | Pass |
| 2 | Enter `-5` and `0` as amount | Error message, asked again | Pass |
| 3 | Enter an empty amount | Error message, asked again | Pass |
| 4 | Enter date `31-02-2026` | Invalid date message | Pass |
| 5 | Press Enter on the date | Today's date is used | Pass |
| 6 | Enter `abc`, `0` or `11` in the main menu | Error message, asked again | Pass |
| 7 | Add income and expense, close and reopen | Data is still there | Pass |
| 8 | Search by category `food` | Only food transactions shown | Pass |
| 9 | Search by amount range with maximum less than minimum | Error message, asked again | Pass |
| 10 | Monthly analysis for September 2026 with income ₹30,000 and expenses ₹21,500 | Savings ₹8,500 and rate 28.33% | Pass |
| 11 | Expenses more than income | Message says expenses are higher | Pass |
| 12 | Delete `finance_data.json` and run | Program starts with empty data | Pass |
| 13 | Put wrong text in `finance_data.json` | Warning shown, backup made, program continues | Pass |
| 14 | Open every menu option with no data | "No transactions" style messages, no crash | Pass |
| 15 | Export report | `financial_report.txt` is created | Pass |

### Sample calculation (September 2026)

| Category | Amount |
|---|---|
| Hostel/Rent | ₹8,000 |
| Food | ₹5,000 |
| Transport | ₹2,500 |
| Education | ₹3,000 |
| Shopping | ₹3,000 |
| **Total expenses** | **₹21,500** |

Income = ₹30,000, so Savings = ₹30,000 - ₹21,500 = ₹8,500 and Savings Rate = (8,500 / 30,000) x 100 = **28.33%**.

---

## 13. Limitations

- A transaction cannot be edited or deleted from the program. It can only be changed by editing the JSON file by hand.
- The program has a text interface only, with no graphs.
- It is made for a single user and a single data file.
- Future dates are accepted, so a wrong year will not be detected.
- If the total income is 0, the savings rate is shown as 0.00%.
- The `₹` symbol may not display properly in very old Windows command prompts.
- Long lists of transactions are not shown page by page.

---

## 14. Future Scope

- Edit and delete transactions
- Monthly budget with a warning when it is crossed
- Recurring transactions such as rent and subscriptions
- Export data to CSV and open it in Excel
- Graphs and charts using `matplotlib`
- A graphical interface using `tkinter`
- Use of classes (OOP) and splitting the code into multiple files
- Multiple users with a login

---

## 15. Conclusion

The Personal Finance Analyzer meets the objectives of the project. It records income and expenses, saves them permanently, calculates savings and shows useful summaries, and it handles wrong input without crashing. While building it I practised functions, loops, lists, dictionaries, exception handling, file handling, JSON and the `datetime` module. The project shows how the basic concepts of Python can be used to solve a real problem.

---

## 16. How to Run

1. Install Python 3.8 or above.
2. Keep `main.py` in a folder and open the folder in VS Code (or a terminal).
3. Run:

```
python main.py
```

No packages need to be installed.

---

## 17. References

1. Python Documentation - https://docs.python.org/3/
2. Python `json` module - https://docs.python.org/3/library/json.html
3. Python `datetime` module - https://docs.python.org/3/library/datetime.html
4. Python Essentials course material

---

**Author:** Bhavy Chauhan
