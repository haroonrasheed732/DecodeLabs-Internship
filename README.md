# 🐍 DecodeLabs Python Training Kit
### Industrial Internship Portfolio | Batch 2026

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![Projects](https://img.shields.io/badge/Projects-4%2F4-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

---

## 📌 Overview

This repository contains **4 production-quality Python projects** developed during the **DecodeLabs Industrial Training Program (Batch 2026)**. Each project represents a progressive milestone — from fundamental data structures to enterprise-grade security tools — following real-world backend engineering principles.

> *"You aren't just writing a script. You are building the memory for your application."*
> — DecodeLabs

---

## 🗂️ Project Structure

```
decodelabs-python-portfolio/
│
├── 📄 README.md
│
├── 📁 Project_1_ToDo_List/
│   └── todo_list.py
│
├── 📁 Project_2_Expense_Tracker/
│   └── expense_tracker.py
│
├── 📁 Project_3_Password_Generator/
│   └── password_generator.py
│
└── 📁 Project_4_Contact_Book/
    └── contact_book.py
```

---

## 🚀 The 4-Week Journey

| Week | Project | Core Concept | Key Skills |
|------|---------|-------------|------------|
| 1 | ✅ To-Do List | Data Storage | Lists, `append()`, `enumerate()` |
| 2 | ✅ Expense Tracker | Data Processing | Accumulators, `try/except`, Sentinel Values |
| 3 | ✅ Password Generator | Data Security | `secrets`, `string`, Shannon Entropy |
| 4 | ✅ Contact Book | Data Management | Nested Dicts, CRUD, Regex, Hash Tables |

---

## 📦 Project 1 — To-Do List

### 🎯 Goal
Build a program where users can **add**, **view**, **complete**, and **delete** tasks through a CLI interface.

### 💡 Key Concepts
- **Python Lists as Dynamic Arrays** — `my_tasks = []` is the primitive structure of every database ever built
- **Accumulator Pattern** — `list.append()` runs in amortized O(1) via heap pre-allocation
- **Stack vs Heap Memory** — variable lives on Stack; actual list object lives on the Heap
- **`enumerate()`** — professional Pythonic iteration giving simultaneous index + value access
- **Decoupled Architecture** — data logic (Model) separated from user interface (View)

### 🔑 Core Operations
```python
# INSERT — Add a task
my_tasks.append({"id": 1, "task": "Finish Python", "done": False})

# SELECT — View all tasks
for index, task in enumerate(my_tasks, start=1):
    print(f"{index}. {task['task']}")

# UPDATE — Mark complete
task["done"] = True

# DELETE — Remove task (list comprehension)
my_tasks = [t for t in my_tasks if t["id"] != task_id]
```

### 📊 Architecture
```
INPUT          PROCESS           OUTPUT
(User Entry) → (append/filter) → (enumerate + print)
```

---

## 📦 Project 2 — Expense Tracker

### 🎯 Goal
Build a real-time expense accumulation engine where users enter amounts and the program **continuously tracks and displays the total spent**.

### 💡 Key Concepts
- **The Accumulator Pattern** — `total += new_expense` → `State(new) = State(old) + Input`
- **State Initialization** — `total = 0` declared **outside** the loop (Initialization = Memory; Inside loop = Amnesia)
- **Defensive Coding / Digital Poka-Yoke** — `try/except ValueError` as type-safety barrier
- **Type Conversion Gatekeeper** — `'100' + '50' = '10050'` (Disaster) vs `float('100') + float('50') = 150.0` (Truth)
- **Sentinel Values** — `'quit'` as the kill switch for graceful shutdown

### 🔑 Core Logic
```python
total = 0.0  # ✅ OUTSIDE the loop — State preserved

while True:
    user_input = input("Amount (or 'quit'): ").strip().lower()

    if user_input == "quit":   # Sentinel Value — kill switch
        break

    try:
        amount = float(user_input)   # Gatekeeper — type conversion
        total += amount              # Accumulator Pattern ❤️
    except ValueError:
        print("Invalid! Numbers only.")
```

### 📊 IPO Model
```
INPUT              PROCESS                    OUTPUT
(float input)  →  (validation + total +=)  →  (running total display)
```

---

## 📦 Project 3 — Random Password Generator

### 🎯 Goal
Build an **enterprise-grade, cryptographically secure** password generator with real-time entropy validation and NIST 2024 compliance.

### 💡 Key Concepts
- **`secrets` vs `random`** — `random` uses Mersenne Twister (deterministic, predictable). `secrets` uses OS-level hardware entropy (cryptographically unpredictable). For passwords: `secrets` is mandatory.
- **String Immutability & Memory** — `password += char` creates a new object every iteration → O(N²). `''.join(list)` allocates memory once → O(N).
- **Shannon Entropy Formula** — `E = L × log₂(R)` where L = length, R = character pool size
- **NIST SP 800-63-4 (2024)** — Minimum 15 characters; mandatory complexity rules are obsolete; length drives security
- **Standard Library Integration** — `string.ascii_letters`, `string.digits`, `string.punctuation`

### 🔑 Core Logic
```python
import string, secrets, math

# Character Pool — string module (professional, locale-independent)
pool = string.ascii_letters + string.digits + string.punctuation  # R = 94

# Generation — secrets module (cryptographically secure)
chars    = [secrets.choice(pool) for _ in range(length)]  # O(N)
password = ''.join(chars)  # ✅ Enterprise approach — O(N), not O(N²)

# Entropy Validation — Shannon Formula
entropy = length * math.log2(len(pool))  # E = L × log₂(R)
```

### 📊 Security Benchmarks
```
 8 characters  →  ~52  bits  →  Cracked in days      🔴
16 characters  →  ~104 bits  →  Secure for centuries  🟢
32 characters  →  ~209 bits  →  Universe lifetime+    💎
```

### 📊 Architecture
```
INPUT              PROCESS                        OUTPUT
(length + opts) → (secrets.choice + .join())  →  (password + entropy score)
```

---

## 📦 Project 4 — Contact Book

### 🎯 Goal
Build a **full CRUD contact management system** backed by a nested dictionary acting as an in-memory relational database.

### 💡 Key Concepts
- **Hash Table Architecture** — Dictionary lookup = O(1). List search = O(N). At scale, this is the difference between instant and slow.
- **Nested Dictionaries as Database** — `contacts[name] = {"phone": ..., "email": ...}` → key = Primary Key, value dict = table row
- **Dictionary Methods** — `.keys()` (names only), `.values()` (details only), `.items()` (both — like SQL `SELECT *`)
- **Regex Validation** — `re.match()` for phone and email format enforcement before data enters the system
- **Case-insensitive Partial Search** — `query.lower() in name.lower()` — substring matching without external libraries
- **CRUD Operations** — The universal backbone of every application on earth

### 🔑 Core Logic
```python
import re

# Data Structure — Nested Dictionary (In-Memory Database)
contacts = {}   # Outer dict = Table | Inner dict = Row

# CREATE — Insert a contact (O(1))
contacts["Ali Hassan"] = {"phone": "03001234567", "email": "ali@gmail.com", "id": 1}

# READ — View all (.items() = key + value simultaneously)
for name, details in contacts.items():
    print(f"{name} → {details['phone']}")

# SEARCH — Case-insensitive partial match
results = [(n, d) for n, d in contacts.items() if query.lower() in n.lower()]

# UPDATE — Mutable dictionary (direct modification)
contacts["Ali Hassan"]["phone"] = "03009999999"

# DELETE — Remove by key
del contacts["Ali Hassan"]

# VALIDATE — Regex gatekeeper
re.match(r'^\d{10,13}$', phone)         # Phone
re.match(r'^[\w.-]+@[\w.-]+\.\w+$', email)  # Email
```

### 📊 Architecture
```
INPUT              PROCESS                           OUTPUT
(name/phone) → (dict CRUD + regex validation)  →  (formatted contact display)
```

---

## 🧠 Core Engineering Principles Applied

Throughout all 4 projects, the following professional engineering principles were consistently applied:

| Principle | Application |
|-----------|-------------|
| **IPO Model** | Every project follows Input → Process → Output architecture |
| **Defensive Coding** | `try/except` blocks on all user inputs |
| **Decoupled Architecture** | Data logic (Model) always separated from display (View) |
| **Sentinel Values** | Graceful program termination via special input values |
| **Standard Library First** | `string`, `secrets`, `re` — no reinventing the wheel |
| **O(1) over O(N)** | Dictionary over List for data retrieval; `.join()` over `+=` for strings |
| **RAM Volatility Awareness** | All projects acknowledge in-memory data is non-persistent |

---

## ⚙️ How to Run

### Prerequisites
```bash
Python 3.8 or higher
```

### Installation
```bash
# Clone the repository
git clone https://github.com/yourusername/decodelabs-python-portfolio.git

# Navigate to project directory
cd decodelabs-python-portfolio
```

### Run Any Project
```bash
# Project 1 — To-Do List
python Project_1_ToDo_List/todo_list.py

# Project 2 — Expense Tracker
python Project_2_Expense_Tracker/expense_tracker.py

# Project 3 — Password Generator
python Project_3_Password_Generator/password_generator.py

# Project 4 — Contact Book
python Project_4_Contact_Book/contact_book.py
```

> **Note:** No external libraries required. All projects use Python's built-in standard library only.

---

## 📈 Complexity Analysis

| Operation | Data Structure Used | Time Complexity |
|-----------|--------------------|----|
| Add task / contact | List `append()` / Dict insert | O(1) amortized |
| View all items | List / Dict iteration | O(N) |
| Search contact | Dict key lookup | O(1) |
| Delete task | List comprehension | O(N) |
| Delete contact | Dict `del` | O(1) |
| Password generation | List + `.join()` | O(N) |
| String concatenation ❌ | `+=` in loop | O(N²) — avoided |

---

## 🏗️ What's Next

These 4 projects form the **foundation layer** of backend engineering. The natural progression:

```
Current Stack          →    Next Steps
─────────────────────────────────────────────────────
In-Memory Storage      →    File I/O (JSON / CSV)
CLI Interface          →    REST API (Flask / FastAPI)
Manual Validation      →    Schema Validation (Pydantic)
Single-user            →    Multi-user (Authentication)
Volatile RAM           →    Persistent Database (SQLite / PostgreSQL)
```

---

## 👨‍💻 Author

**[Your Name]**
Junior Python Developer Intern @ DecodeLabs
Batch 2026

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/yourprofile)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat&logo=github)](https://github.com/yourusername)

---

## 🏢 About DecodeLabs

DecodeLabs is an industrial training organization based in Greater Lucknow, India, focused on bridging the gap between academic learning and professional software development.

🌐 [www.decodelabs.tech](https://www.decodelabs.tech)
📧 decodelabs.tech@gmail.com

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with 💪 during DecodeLabs Industrial Training | Batch 2026**

*"From a single [] to the architecture of a bank — the logic is the same."*

</div>
