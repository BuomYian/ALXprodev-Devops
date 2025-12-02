# **Advanced Shell Scripting – Pokémon API Automation**

### *ALX ProDev – DevOps Track*

This project is a hands-on journey into advanced shell scripting, centered around automating interactions with a RESTful API—the Pokémon API. Each task grows a little bigger, a little bolder, until you're building a miniature ETL pipeline directly from the terminal.

The work mirrors real-world DevOps/Data Engineering responsibilities: reliable automation, robust error handling, safe parallel processing, and clean data reporting.

---

## **📌 Project Overview**

You will build a suite of shell scripts that:

* Fetch Pokémon data from the Pokémon REST API
* Parse JSON results using `jq`, `awk`, and `sed`
* Handle errors and implement retry logic
* Process data in parallel using background jobs
* Aggregate results into CSV reports
* Produce maintainable, modular scripts used for automation workflows

By the end, you’ll have a fully functional command-line data pipeline.

---

## **🎯 Learning Objectives**

You will demonstrate proficiency in:

### **API Interaction**

* Making HTTP requests with `curl`
* Checking HTTP status codes and curl exit codes

### **JSON Manipulation**

* Extracting and transforming data using `jq`

### **UNIX Text Processing**

* Using `awk`, `sed`, and `grep` to clean and transform output

### **Robust Scripting**

* Error handling
* Retry logic
* Logging failures

### **Process Management**

* Running parallel jobs
* Using `&`, `wait`, and `$!` safely

### **Data Reporting**

* Generating CSV files
* Calculating averages with `awk`

---

## **🧩 Project Structure**

All tasks live under:

```
GitHub: ALXprodev-Devops  
Directory: Advanced_shell
```

Each file corresponds to a task.

---

# **📜 Tasks**

---

## **0. API Request Automation**

File: `apiAutomation-0x00`
**Objective:** Fetch Pikachu’s data using the Pokémon API and save it locally.

### Requirements

* Use `curl` to GET `https://pokeapi.co/api/v2/pokemon/pikachu`
* Save output to `data.json`
* Log failures to `errors.txt`

---

## **1. Extract Pokémon Data**

File: `data_extraction_automation-0x01`
**Objective:** Parse the JSON from Task 0 using text-processing tools.

### Requirements

* Extract **name**, **height**, **weight**, **type**
* Use only: `jq`, `awk`, `sed`
* Print a formatted line:

  ```
  Pikachu is of type Electric, weighs 6kg, and is 0.4m tall.
  ```

---

## **2. Batch Pokémon Data Retrieval**

File: `batchProcessing-0x02`
**Objective:** Automate retrieval for a list of Pokémon.

### Requirements

* Pokémon list:

  ```
  Bulbasaur, Ivysaur, Venusaur, Charmander, Charmeleon
  ```
* For each:

  * Fetch API data
  * Save to `pokemon_data/<name>.json`
* Add a delay to handle rate limits

---

## **3. Summarize Pokémon Data**

File: `summaryData-0x03`
**Objective:** Generate a CSV report from all JSON files.

### Requirements

* Extract name, height, weight using `jq`
* Create a CSV:

  ```
  Name,Height (m),Weight (kg)
  ...
  ```
* Use `awk` to compute:

  * Average height
  * Average weight

---

## **4. Error Handling & Retry Logic**

File: `batchProcessing-0x02` (updated)
**Objective:** Add reliable error handling to Task 2.

### Requirements

* Retry failed requests up to 3 times
* Log failures
* Skip Pokémon if all retries fail

---

## **5. Parallel Data Fetching**

File: `batchProcessing-0x04`
**Objective:** Speed up batch fetching using background jobs.

### Requirements

* Fetch the same list of Pokémon in parallel
* Use:

  * Background processes (`&`)
  * Job control
  * `wait` to synchronize
* Ensure all processes finish before exiting

---

## **6. Manual Review**

Standard ALX manual review for correctness, structure, and output.

---

# **📦 Tools Used**

* **curl** — API requests
* **jq** — JSON parsing
* **awk** — pattern scanning & calculations
* **sed** — text manipulation
* **grep**, **cut**, loops, conditions
* Shell job control (`&`, `wait`, `$!`)

---

# **🧭 Real-World Use Case**

This project models a typical **data pipeline**:

1. **Extract**
   Fetch raw data from external APIs (Tasks 0, 2, 5).

2. **Transform**
   Parse, clean, and format JSON output (Tasks 1, 3).

3. **Load**
   Store cleaned results into JSON/CSV files for analysts (Task 3).

This mirrors workflows used in:

* Data Engineering
* DevOps automation
* ETL/ELT pipelines
* Cloud scripting tasks

---

# **🚀 How to Run**

From the `Advanced_shell` directory:

```
chmod +x scriptname.sh
./scriptname.sh
```

Ensure `jq` is installed:

```
sudo apt install jq
```

---

# **📁 Repository Layout**

```
ALXprodev-Devops/
└── Advanced_shell/
    ├── apiAutomation-0x00
    ├── data_extraction_automation-0x01
    ├── batchProcessing-0x02
    ├── batchProcessing-0x04
    ├── summaryData-0x03
    └── pokemon_data/
```

---
