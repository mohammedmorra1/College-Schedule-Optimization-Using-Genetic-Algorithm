# Genetic Algorithm Based Faculty Timetable Generator

## Overview

This project demonstrates the use of a **Genetic Algorithm (GA)** to solve a **complex university timetabling problem**, a classic NP-hard optimization challenge.

The system generates weekly schedules for a **single academic year/level** in a faculty where:

* All students belong to one of three majors:

  * Computer Science (CS)
  * Information Technology (IT)
  * Information Systems (IS)
* Students from different majors may have **overlapping lectures or labs**
* Courses differ in duration, professors, and room requirements
* The goal is to produce **conflict-free, compact, and realistic schedules**

Rather than being a production-ready scheduler, this project is designed as an **academic and experimental exploration** of how genetic algorithms can model and optimize real-world constraints.

---

## Problem Being Solved

University scheduling involves balancing many competing constraints:

* A professor cannot teach two classes at the same time
* The same course should not appear twice at the same time slot
* Rooms have limited capacity types (Hall vs Lab)
* Students should not have excessive gaps
* Daily workload should be reasonable

This project encodes these constraints into a **fitness function** and lets evolution gradually improve schedules over generations.

---

## Key Concepts Used

* Genetic Algorithms
* Fitness-based selection
* Crossover and mutation
* Constraint optimization
* Schedule encoding and decoding
* Visualization using Pandas and Tkinter

---

## Genetic Representation

### Genes

* **Course**: course ID, name, duration, type, program
* **Professor**
* **Room**
* **Gap**: represents free hours between lectures

### Individual (Chromosome)

An individual represents **one full day** of scheduling and consists of three pools:

* Pool 0: CS schedule
* Pool 1: IT schedule
* Pool 2: IS schedule

Each pool fills up to **8 hours per day**, mixing courses and gaps.

### Population

A population consists of many such daily schedules, each competing to be the best according to the fitness function.

---

## Fitness Function

The fitness function rewards schedules that:

### ✅ Avoid Conflicts

* Same course at the same time
* Same professor at the same time
* Same course using the same room type simultaneously

### ✅ Have Good Gap Distribution

* Avoid empty days
* Avoid excessive or pointless gaps
* Prefer compact lecture blocks

### ✅ Maintain Reasonable Workload

* Penalizes days with:

  * Less than 4 hours
  * More than 6 hours per program

The goal is to **maximize fitness**, with a perfect schedule approaching fitness `0`.

---

## Evolution Process

1. **Initialize population** with random schedules
2. **Evaluate fitness** for each individual
3. **Select best parents**
4. Apply:

   * **Single-point crossover**
   * **Random mutation**
5. Replace weakest individuals
6. Repeat until:

   * Optimal solution is found, or
   * Maximum generations reached

Courses used in a finalized day are removed, and the algorithm continues generating new days until **all courses are scheduled**.

---

## Output

### CSV Files

The program generates:

* `days/day X.csv` for each generated day
* `week.csv` containing the full combined schedule

Each CSV represents:

* Rows: CS, IT, IS
* Columns: hourly time slots (8:00 → 16:00)

---

### GUI Visualization

A simple **Tkinter-based table** displays the full weekly schedule:

* Alternating row colors for readability
* Day separators
* Each cell shows:

  * Course
  * Professor
  * Room

This visualization is meant for **inspection and demonstration**, not user interaction.

---

## How to Run

### Requirements

* Python 3.8+
* pandas

Install dependencies:

```bash
pip install pandas
```

### Run the project

```bash
python main.py
```

The program will:

1. Run the genetic algorithm
2. Generate CSV files in a `days/` directory
3. Display the final weekly schedule in a GUI window

---
## Limitations

* No hard constraints on professor availability
* No multi-section or parallel course handling
* No student group modeling beyond major
* GA parameters are fixed and not auto-tuned

These limitations are intentional to keep the focus on **genetic algorithm mechanics**.

---

## Future Improvements

* Separate lecture/lab modeling
* Professor availability windows
* Adaptive mutation rates
* Multi-year or multi-level scheduling
* Constraint weighting configuration
* Web-based visualization
