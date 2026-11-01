<div align="center">

# Lab 02 · NumPy for Numerical Computing

### CS-3105 · Machine Learning Lab

*Implementation documentation: approach, function signatures and observations for every task.*

<br>

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?style=flat-square&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Vectorised-013243?style=flat-square&logo=numpy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)
![CLO](https://img.shields.io/badge/CLO-5-0F766E?style=flat-square)
![Level](https://img.shields.io/badge/Bloom-C--3%20Apply-334155?style=flat-square)
![Loops](https://img.shields.io/badge/Loops%20in%20graded%20tasks-0-DC2626?style=flat-square)

<br>

| 11 | 52 | 4 | 0 | 20+ |
|:---:|:---:|:---:|:---:|:---:|
| **Tasks** | **Parts** | **Datasets** | **Loops** | **Functions documented** |

</div>

<br>

## 👤 Submission details

| Field | Detail |
|:--|:--|
| **Student** | [Shahzad Ahmed Awan](https://github.com/ShahzadAhmedAwan) |
| **Roll No** | 2024-SE-15 |
| **Instructor** | Engr. Muhammad Awais |
| **Course** | CS-3105 Machine Learning Lab, Lab 02 |
| **Outcome** | CLO 5 · Cognitive C-3 (Apply) · PLO 5 Modern Tool Usage |
| **Environment** | Python 3.9+ in Jupyter or Google Colab |
| **Libraries** | `numpy` (all tasks), `matplotlib` (bonus plot only) |
| **Recorded with** | NumPy 2.5.4 |

---

## 📑 Contents

| # | Section | # | Section |
|:-:|:--|:-:|:--|
| 1 | [Overview and workflow](#-overview-and-workflow) | 9 | [Task 7 · Climate](#-task-7--climate-of-five-cities) |
| 2 | [Datasets](#-datasets) | 10 | [Task 8 · Inflation](#-task-8--inflation) |
| 3 | [Lab at a glance](#-lab-at-a-glance) | 11 | [Tasks 9 to 11](#-task-9--grace-marks) |
| 4 | [Tasks 1 to 2](#-task-1--setup) | 12 | [Bonus](#-bonus-not-graded) |
| 5 | [Task 3 · Randomness](#-task-3--randomness-and-reproducibility) | 13 | [Function reference](#-function-reference) |
| 6 | [Task 4 · Reshaping](#-task-4--spacing-and-reshaping) | 14 | [Syntax cheat sheet](#-syntax-cheat-sheet) |
| 7 | [Task 5 · Slicing](#-task-5--exam-hall-seating-plan) | 15 | [Key learnings](#-key-learnings) |
| 8 | [Task 6 · Census](#-task-6--census-2023) | 16 | [Pitfalls](#-common-pitfalls) · [Running](#-running-the-notebook) |

---

## 🗺️ Overview and workflow

```mermaid
flowchart LR
    A["Toolkit<br/><sub>Tasks 1 to 5</sub>"] --> B["Real data<br/><sub>Tasks 6 to 8</sub>"]
    B --> C["Applications<br/><sub>Tasks 9 to 10</sub>"]
    C --> D["Reflection<br/><sub>Task 11</sub>"]
    D --> E["Bonus<br/><sub>Not graded</sub>"]
```

| Phase | Tasks | Parts | Focus |
|:--|:-:|:-:|:--|
| Toolkit | 1 to 5 | 23 | Creating, randomising, reshaping and slicing arrays |
| Real data | 6 to 8 | 19 | Census, climate and inflation analysis |
| Applications | 9 to 10 | 10 | Grace marks and an image stored as an array |
| Reflection | 11 | n/a | Written findings |

**Working rules followed throughout**

| Rule | How it is applied |
|:--|:--|
| No Python loops | Every graded task uses a NumPy function instead |
| Labelled output | Each print starts with its task ID, for example `T6b:` |
| Units shown | %, °C, °F, mm, percentage points and people appear in every result |
| Reproducible | Seeds 2026 and 42 are set before any random call |
| Starter data | The data cell is unchanged |

---

## 📊 Datasets

| Dataset | Variables | Shape | Content | Source |
|:--|:--|:-:|:--|:--|
| 🏛️ Census | `units`, `pop_2023`, `pop_2017` | (7,) | 4 provinces, Islamabad, AJK, Gilgit-Baltistan | PBS 7th Census |
| 🌡️ Climate | `cities`, `months`, `tmax`, `rain` | (5, 12) | Max temperature (°C) and rainfall (mm) | PMD / WMO 1991–2020 |
| 💹 Inflation | `cpi_months`, `cpi` | (2, 10) | Year-on-year CPI (%), FY2024 and FY2025, Jul to Apr | Economic Survey 2024-25 |
| 📝 Marks | `marks` | (10,) | Marks of one lab section | Sample class data |

**Row and column meaning**

| Array | Rows | Columns |
|:--|:--|:--|
| `tmax`, `rain` | Lahore, Karachi, Islamabad, Peshawar, Quetta | Jan to Dec |
| `cpi` | FY2024, FY2025 | Jul to Apr |

**Helper function**

| Item | Detail |
|:--|:--|
| Name | `table(names, values, fmt="%.2f", unit="", width=20)` |
| Purpose | Prints names and values as an aligned table |
| Built from | `np.char.mod`, `np.char.add`, `np.char.ljust`, `np.char.rjust`, no loops |
| Graded | No, formatting only |

---

## 🧭 Lab at a glance

| Task | Topic | Core technique | Main signature | Headline result |
|:-:|:--|:--|:--|:--|
| 1 | Setup | Version check | `np.__version__` | NumPy 2.5.4 |
| 2 | Class register | Array creation | `np.arange(start, stop, step)` | 7 arrays built |
| 3 | Randomness | Seeded sampling | `np.random.randint(low, high, size)` | P(six) = 0.1657 |
| 4 | Spacing, reshape | Reshape and sum by axis | `a.reshape(rows, cols)` | Wettest quarter Q3, 454.3 mm |
| 5 | Exam hall | 2-D slicing | `a[rows, cols]` | Sum 325, std 7.2111 |
| 6 | Census | Vectorised arithmetic | `a / a.sum()` | Balochistan fastest, 3.19 % |
| 7 | Climate | Reductions by axis | `np.mean(a, axis)` | Karachi highest mean, 32.5 °C |
| 8 | Inflation | Row maths and labels | `np.where(cond, x, y)` | 26.22 % down to 4.87 % |
| 9 | Grace marks | Clipping and z-scores | `np.clip(a, a_min, a_max)` | 90 % pass, indices 0 and 6 rescued |
| 10 | Image array | Slice assignment | `a[r0:r1, c0:c1] = value` | 10 white pixels |
| 11 | Reflection | Written findings | n/a | One finding per dataset |

---

## ✅ Task 1 · Setup

| Input | Technique | Output |
|:--|:--|:--|
| None | Import and attribute lookup | Version string |

| Item | Detail |
|:--|:--|
| Goal | Import NumPy and show its version |
| Syntax | `import numpy as np` · `np.__version__` |
| Result | NumPy **2.5.4** |

---

## ✅ Task 2 · Class register

| Input | Technique | Output |
|:--|:--|:--|
| Class size of 10 students | Array creation functions | Seven arrays |

| Part | Array | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | Attendance | Ten zeros | `np.zeros(shape, dtype=float)` | Ten `0.` floats |
| b | Fee paid | Ten ones | `np.ones(shape, dtype=None)` | Ten `1.` floats |
| c | Grace marks | Fill ten slots with 5 | `np.full(shape, fill_value, dtype=None)` | Ten integer 5s |
| d | Roll numbers 10 to 50 | Stop is excluded, so stop at 51 | `np.arange(start, stop)` | 41 integers |
| e | Even roll numbers | Same range with step 2 | `np.arange(start, stop, step)` | 21 integers, 10 to 50 |
| f | 3 × 3 seat map | Nine values reshaped | `np.arange(stop)` then `a.reshape(rows, cols)` | Values 0 to 8 |
| g | 3 × 3 identity | Built directly | `np.eye(N, M=None, k=0, dtype=float)` | Float identity matrix |

**Observation:** `zeros`, `ones` and `eye` return floats by default, while `full` with an integer fill and `arange` return integers.

---

## ✅ Task 3 · Randomness and reproducibility

| Input | Technique | Output |
|:--|:--|:--|
| Seeds 2026 and 42 | Random sampling and boolean masks | Random values, dice counts, probabilities |

| Part | Goal | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | One number in [0, 1) | Seed 2026, then one uniform draw | `np.random.seed(seed)` · `np.random.rand(d0, d1, ...)` | 0.2193 |
| b | 25 normal values | Continue the same seeded stream | `np.random.randn(d0, d1, ...)` | 25 values, from -1.78 to 2.01 |
| c | 10,000 Ludo dice | Seed 42, draw 1 to 6, count each face | `np.random.randint(low, high, size)` · `np.unique(ar, return_counts=True)` | See table below |
| d | P(six) vs 1/6 | Mean of a True/False mask | `np.mean(a)` on a boolean array | 0.1657 vs 0.1667 |
| e | Two sixes in a row | Compare six-mask with a copy shifted by one, logical AND, count | `mask[:-1] & mask[1:]` · `np.sum(a)` | 265 times |

**Dice counts (seed 42)**

| Face | 1 | 2 | 3 | 4 | 5 | 6 |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Count | 1665 | 1692 | 1625 | 1672 | 1689 | 1657 |

**Observations**

| Point | Finding |
|:--|:--|
| Upper bound | `randint` excludes `high`, so `high=7` gives faces 1 to 6 |
| `unique` return | With `return_counts=True` it returns two arrays: values and counts |
| Fairness | Every face lies close to 10,000 ÷ 6 ≈ 1,667 |
| P(six) gap | The estimate is 0.0010 below 1/6 |
| Double sixes | 265 is close to the expected 10,000 × 1/36 ≈ 278 |
| Reproducibility | Re-running with the same seeds gives identical output |

---

## ✅ Task 4 · Spacing and reshaping

| Input | Technique | Output |
|:--|:--|:--|
| `rain[0]` (Lahore, 12 values) | Reshape, then aggregate along an axis | 10 × 10 grid, 4 × 3 table, quarterly totals |

| Part | Goal | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | 0.01 to 1.00 as 10 × 10 | Integers 1 to 100, divided by 100, reshaped | `np.arange(start, stop)` · `a.reshape(rows, cols)` | 10 × 10 grid, last value 1.0 |
| b | 20 points in [0, 1] | Evenly spaced, both ends included | `np.linspace(start, stop, num=50, endpoint=True)` | Step ≈ 0.0526 |
| c | Lahore rain as 4 × 3 | First row of `rain`, reshaped into quarters | `a.reshape(4, 3)` | 4 quarters × 3 months |
| d | Quarterly totals, wettest quarter | Sum across months, then index of the maximum | `np.sum(a, axis=1)` · `np.argmax(a)` | Q3, index 2 |

**Lahore quarterly rain**

| Quarter | Months | Rain (mm) |
|:--|:--|:-:|
| Q1 | Jan to Mar | 84.9 |
| Q2 | Apr to Jun | 111.0 |
| **Q3** | **Jul to Sep** | **454.3** |
| Q4 | Oct to Dec | 24.0 |

**Observations**

| Point | Finding |
|:--|:--|
| Reshape rule | Rows × columns must equal the element count (12 = 4 × 3) |
| Wettest quarter | Q3 holds the monsoon, over four times wetter than any other quarter |

---

## ✅ Task 5 · Exam hall seating plan

| Input | Technique | Output |
|:--|:--|:--|
| 5 × 5 hall numbered 1 to 25 | 2-D slicing | Five slices plus two statistics |

**Setup:** `np.arange(1, 26).reshape(5, 5)`. Each slice has a comment naming the seats the invigilator points at.

| Part | Slice | Rows | Columns | Seats selected | Output shape |
|:-:|:--|:--|:--|:--|:-:|
| a | `hall[2:, 1:]` | 3 to 5 | 2 to 5 | 12–15, 17–20, 22–25 | (3, 4) |
| b | `hall[3, 4]` | 4 | 5 | Seat 20 | single value |
| c | `hall[0:3, 1:2]` | 1 to 3 | 2 only | Seats 2, 7, 12 | (3, 1) |
| d | `hall[4]` | 5 | all | Seats 21 to 25 | (5,) |
| e | `hall[3:]` | 4 to 5 | all | Seats 16 to 25 | (2, 5) |
| f | whole array | all | all | All 25 seats | sum and std |

| Statistic | Function signature | Result |
|:--|:--|:-:|
| Sum | `np.sum(a, axis=None)` | 325 |
| Standard deviation | `np.std(a, axis=None, ddof=0)` | 7.2111 |

**Observations**

| Point | Finding |
|:--|:--|
| Slice syntax | `a[start:stop:step]` per axis, start included and stop excluded |
| Single numbers | A single index drops a dimension, so (b) and (d) lose a dimension |
| Range of width one | `1:2` keeps the dimension, so (c) stays a column of shape (3, 1) |
| Std type | `std` is the population standard deviation (ddof = 0) |

---

## ✅ Task 6 · Census 2023

| Input | Technique | Output |
|:--|:--|:--|
| `units`, `pop_2023`, `pop_2017` (each shape (7,)) | Vectorised arithmetic, `argmax`, masking | Total, shares, growth rates, rankings |

| Part | Goal | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | Total population | Sum of 2023 values | `np.sum(a)` | 247,541,947 |
| b | Share of total (%) | Divide all seven values by one total, times 100 | `array / scalar` (broadcasting) | Table below |
| c | Most populous unit | Index of the maximum, used to pick a name | `np.argmax(a)` · `names[index]` | Punjab |
| d | Units above 20 million | Boolean mask applied to names | `names[array > value]` | Punjab, Sindh, Khyber Pakhtunkhwa |
| e | Annual growth 2017 to 2023 | Compound rate over 6 years, element by element | `a / b` · `a ** (1/n)` | Table below |
| f | Fastest-growing unit | Index of the maximum growth | `np.argmax(a)` | Balochistan, 3.19 % |
| extra | National growth and doubling time | Same formula on the totals, then a log ratio | `np.log(x)` | 2.52 %, about 28 years |

**Share and growth by unit**

| Unit | Population 2023 | Share (%) | Growth (% per year) |
|:--|--:|--:|--:|
| Punjab | 127,688,922 | 51.58 | 2.52 |
| Sindh | 55,696,147 | 22.50 | 2.56 |
| Khyber Pakhtunkhwa | 40,856,097 | 16.50 | 2.37 |
| Balochistan | 14,894,402 | 6.02 | **3.19** |
| Islamabad | 2,363,863 | 0.95 | 2.80 |
| AJK | 4,333,467 | 1.75 | **1.15** |
| Gilgit-Baltistan | 1,709,049 | 0.69 | 2.28 |

**Interpretation**

| Observation | Evidence | Reading |
|:--|:--|:--|
| All units grew | Every rate is above 1 % | Population rose everywhere |
| Balochistan is fastest | 3.19 % a year | Well above the national 2.52 % |
| Large units sit near the national rate | Punjab, Sindh, KP at 2.37 to 2.56 % | They set the national average |
| AJK is slowest | 1.15 %, under half the national rate | The census counts people, not births, so migration may play a part but the data cannot confirm it |

---

## ✅ Task 7 · Climate of five cities

| Input | Technique | Output |
|:--|:--|:--|
| `tmax`, `rain` (each shape (5, 12)) | Reductions along an axis, slicing, masking | Per-city and per-month statistics |

| Part | Goal | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | Shape of `tmax` | Read the shape attribute | `a.shape` | (5, 12) |
| b | Annual mean per city | Average across months | `np.mean(a, axis=1)` | Table below |
| c | Hottest month per city | Index of row maximum, mapped to month names | `np.argmax(a, axis=1)` · `months[index]` | Table below |
| d | 5-city monthly average | Average down the cities | `np.mean(a, axis=0)` | 12 values, 18.5 to 37.6 °C |
| e | Months above 35 °C | Mask the array, count True per row | `(a > 35)` · `np.sum(mask, axis=1)` | Table below |
| f | Lahore in °F | Multiply and add a scalar across 12 months | `array * 9/5 + 32` (broadcasting) | 65.1 to 102.0 °F |
| g | Monsoon rain per city | Slice columns for Jul to Sep, sum across them | `a[:, 6:9]` · `np.sum(a, axis=1)` | Table below |
| h | Wettest monsoon city and share | Index of maximum, then monsoon ÷ yearly rain × 100 | `np.argmax(a)` · `np.sum(a, axis=1)` | Islamabad, table below |

**Results by city**

| City | Annual mean (°C) | Hottest month | Months > 35 °C | Monsoon rain (mm) | Monsoon share (%) |
|:--|:-:|:-:|:-:|--:|--:|
| Lahore | 30.5 | May | 3 | 454.3 | 67.4 |
| Karachi | **32.5** | May | 3 | 234.8 | 73.8 |
| Islamabad | 28.9 | Jun | 3 | **763.0** | 60.5 |
| Peshawar | 29.5 | Jun | **4** | 172.3 | 31.8 |
| Quetta | 25.2 | Jul | 3 | 17.9 | **6.0** |

**5-city monthly averages (°C)**

| Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 18.5 | 21.0 | 25.8 | 31.3 | 35.7 | **37.6** | 35.8 | 34.5 | 33.6 | 31.2 | 26.0 | 21.1 |

**Interpretation**

| Observation | Evidence | Reading |
|:--|:--|:--|
| Karachi has the highest yearly mean | 32.5 °C, though its hottest month is 35.7 °C | Lahore (38.9 °C) and Peshawar (39.6 °C) peak higher |
| Why | Karachi January is 26.3 °C against 18.4 °C in Lahore | Warm winters lift the average, most likely from the sea |
| Monsoon contrast | Islamabad 763.0 mm, about 1.7 × Lahore | The capital is the wettest by a wide margin |
| Quetta | 17.9 mm, 6.0 % of its yearly rain | It has almost no monsoon |

**Tie note:** Lahore reaches 38.9 °C in both May and June. `np.argmax` returns the first, so May is reported, and a code comment says so.

---

## ✅ Task 8 · Inflation

| Input | Technique | Output |
|:--|:--|:--|
| `cpi` (shape (2, 10)) | Row arithmetic, masking, nested conditions | Averages, drops, labels |

| Part | Goal | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | Average per year | Mean across months | `np.mean(a, axis=1)` | 26.22 % and 4.87 % |
| b | FY2024 months above 25 % | Mask the FY2024 row, apply it to month names | `names[row > value]` | Jul to Jan (7 months) |
| c | Monthly drop | FY2024 row minus FY2025 row | `row_a - row_b` | Table below |
| d | Biggest drop | Index of the maximum drop | `np.argmax(a)` | Jan, 25.9 points |
| e | Low / Moderate / High labels | Two nested conditions on FY2025 | `np.where(condition, x, y)` | Table below |

**Monthly detail**

| Month | FY2024 (%) | FY2025 (%) | Drop (pts) | FY2025 label |
|:--|--:|--:|--:|:--|
| Jul | 28.3 | 11.1 | 17.2 | High |
| Aug | 27.4 | 9.6 | 17.8 | Moderate |
| Sep | 31.4 | 6.9 | 24.5 | Moderate |
| Oct | 26.8 | 7.2 | 19.6 | Moderate |
| Nov | 29.2 | 4.9 | 24.3 | Low |
| Dec | 29.7 | 4.1 | 25.6 | Low |
| **Jan** | 28.3 | 2.4 | **25.9** | Low |
| Feb | 23.1 | 1.5 | 21.6 | Low |
| Mar | 20.7 | 0.7 | 20.0 | Low |
| Apr | 17.3 | 0.3 | 17.0 | Low |

| Label | Rule |
|:--|:--|
| Low | below 5 % |
| Moderate | 5 % up to below 10 % |
| High | 10 % or more |

**Interpretation**

| Observation | Evidence | Reading |
|:--|:--|:--|
| Sharp fall | Average dropped from 26.22 % to 4.87 % | Price growth slowed greatly |
| Biggest drop in January | 28.3 % down to 2.4 % | A fall of 25.9 percentage points |
| Near zero by April | 0.3 % | Almost no yearly price rise |
| Prices did not fall | Rates stayed positive every month | Prices kept rising, only much more slowly |
| Base effect | Each month is compared with an already high year | Part of the fall is probably statistical |

---

## ✅ Task 9 · Grace marks

| Input | Technique | Output |
|:--|:--|:--|
| `marks` (shape (10,)) | Clipping, masking, standardisation | Adjusted marks, pass rate, indices, z-scores |

| Part | Goal | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | Add 5, cap at 100 | Add 5 to all marks, limit between 0 and 100 | `np.clip(a, a_min, a_max)` | Table below |
| b | Pass % (≥ 50) | Mean of a True/False pass mask, times 100 | `np.mean(mask)` | 90.0 % |
| c | Passed only because of grace | Failed before AND pass after, then take the indices | `np.where(condition)` · `mask1 & mask2` | Indices 0 and 6 |
| d | Z-scores after grace | Subtract the mean, divide by the standard deviation | `(a - np.mean(a)) / np.std(a)` | -1.54 to 1.47 |

**Per-student detail**

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Before | 45 | 78 | 92 | 38 | 66 | 97 | 49 | 55 | 71 | 83 |
| After | 50 | 83 | 97 | 43 | 71 | **100** | 54 | 60 | 76 | 88 |
| Z-score | -1.17 | 0.57 | 1.31 | -1.54 | -0.06 | 1.47 | -0.96 | -0.64 | 0.20 | 0.83 |

**Observations**

| Point | Finding |
|:--|:--|
| Cap | Student 5 would reach 102 but is held at 100 |
| Rescued by grace | Students 0 (45 to 50) and 6 (49 to 54) |
| Still failing | Student 3 (38 to 43) |
| Z-score | Uses the population standard deviation (ddof = 0) |

---

## ✅ Task 10 · An image is an array

| Input | Technique | Output |
|:--|:--|:--|
| 8 × 8 integer canvas of zeros | Slice assignment, reversed slices, clipping | A drawn "7" and four transformations |

**Canvas:** `np.zeros((8, 8), dtype=int)`, drawn into with three slice assignments.

| Part | Goal | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| a | Draw the "7" | Top bar, vertical stem, grey middle bar | `a[r0:r1, c0:c1] = value` | 255 white, 128 grey |
| b | Flip left-right | Reverse the column order | `a[:, ::-1]` | Mirror image |
| c | Invert | Subtract the image from 255 | `255 - a` | Negative image |
| d | Crop | Take rows 1 to 4 and columns 3 to 6 | `a[1:5, 3:7]` | 4 × 4 block |
| e | Brighten by 80, cap at 255 | Add 80 then limit to 255 | `np.clip(a + 80, 0, 255)` | Background 80, grey 208, white 255 |
| f | Shape, dtype, white pixels | Read attributes, count pixels equal to 255 | `a.shape` · `a.dtype` · `np.sum(a == 255)` | (8, 8), int64, 10 |

**Drawing steps**

| Step | Region | Value |
|:-:|:--|:-:|
| 1 | Row 1, columns 1 to 6 (top bar) | 255 |
| 2 | Rows 2 to 6, column 5 (stem) | 255 |
| 3 | Row 4, columns 3 to 6 (middle bar) | 128 |

**Observations**

| Point | Finding |
|:--|:--|
| Overlap | Step 3 overwrites the stem pixel at row 4, column 5, so it is grey |
| White count | 6 (bar) + 4 (stem) = 10 |
| Brighten | Capping keeps white at 255 instead of overflowing to 335 |
| Invert | Grey 128 becomes 127 |

---

## ✅ Task 11 · Reflection

| Source | New finding |
|:--|:--|
| Census | Punjab holds 51.58 % of 247,541,947 people, so over half the country lives in one province |
| Climate | Islamabad's monsoon rain (763.0 mm) is about 1.7 × Lahore's (454.3 mm), while Quetta gets 17.9 mm |
| Inflation | Average rate fell from 26.22 % to 4.87 % and was only 0.3 % in April |
| NumPy function | `np.sum(a, axis=1)` on the monsoon columns replaced an outer loop over five cities and an inner loop adding Jul, Aug and Sep |

---

## 🎁 Bonus (not graded)

| # | Challenge | Approach | Function signature | Result |
|:-:|:--|:--|:--|:--|
| 1 | List vs NumPy on 1,000,000 numbers | Time a list comprehension against one array operation | `%timeit -o statement` | 52.80 ms vs 0.63 ms, about **84×** faster |
| 2 | Months all five cities exceed 30 °C | Mask, then require True down every city | `np.all(a, axis=0)` | May to September (5 months) |
| 3 | Show the "7" and climate table | Two image panels, hot colour map and colour bar for climate | `plt.imshow(X, cmap=None)` | Two-panel figure |

| Point | Detail |
|:--|:--|
| Only loop in the notebook | The list comprehension in Bonus 1, where the loop is the subject of the test |
| Timing | Speed-up varies between machines |
| Magic command | `%timeit` needs Jupyter or Colab |

---

## 📚 Function reference

**Array creation**

| Function | Signature | Returns | Used in this lab for | Tasks |
|:--|:--|:--|:--|:-:|
| `np.zeros` | `np.zeros(shape, dtype=float)` | Array of zeros | Attendance, blank 8 × 8 canvas | 2, 10 |
| `np.ones` | `np.ones(shape, dtype=None)` | Array of ones | Fee-paid flags | 2 |
| `np.full` | `np.full(shape, fill_value, dtype=None)` | Array of one value | Ten grace marks of 5 | 2 |
| `np.arange` | `np.arange(start, stop, step=1)` | Evenly stepped values, stop excluded | Roll numbers, grid, hall | 2, 4, 5 |
| `np.linspace` | `np.linspace(start, stop, num=50, endpoint=True)` | Evenly spaced points, both ends included | 20 points in [0, 1] | 4 |
| `np.eye` | `np.eye(N, M=None, k=0, dtype=float)` | Identity matrix | 3 × 3 identity | 2 |

**Shape and random numbers**

| Function | Signature | Returns | Used in this lab for | Tasks |
|:--|:--|:--|:--|:-:|
| `ndarray.reshape` | `a.reshape(rows, cols)` (use -1 to infer one size) | Same data, new shape | Seat map, grid, quarters, hall | 2, 4, 5 |
| `np.random.seed` | `np.random.seed(seed)` | None (fixes the stream) | Reproducible results | 3 |
| `np.random.rand` | `np.random.rand(d0, d1, ...)` | Uniform values in [0, 1) | One random number | 3 |
| `np.random.randn` | `np.random.randn(d0, d1, ...)` | Standard normal values | 25 normal values | 3 |
| `np.random.randint` | `np.random.randint(low, high=None, size=None)` | Integers in [low, high) | 10,000 dice rolls | 3 |
| `np.unique` | `np.unique(ar, return_counts=False)` | Distinct values (and counts) | Count of each die face | 3 |

**Aggregation and search**

| Function | Signature | Returns | Used in this lab for | Tasks |
|:--|:--|:--|:--|:-:|
| `np.sum` | `np.sum(a, axis=None)` | Total, optionally per axis | Population, quarters, monsoon, counts | 3 to 9 |
| `np.mean` | `np.mean(a, axis=None)` | Average, optionally per axis | City means, P(six), pass % | 3, 7, 8, 9 |
| `np.std` | `np.std(a, axis=None, ddof=0)` | Standard deviation | Hall statistic, z-scores | 5, 9 |
| `np.argmax` | `np.argmax(a, axis=None)` | Index of the largest value | Fastest unit, hottest month | 4, 6, 7, 8 |
| `np.all` | `np.all(a, axis=None)` | True where every value is True | Months all above 30 °C | Bonus 2 |
| `np.log` | `np.log(x)` | Natural logarithm | Doubling time | 6 |

**Conditions and limits**

| Function | Signature | Returns | Used in this lab for | Tasks |
|:--|:--|:--|:--|:-:|
| `np.where` (3 arguments) | `np.where(condition, x, y)` | x where True, y where False | Low / Moderate / High labels | 8 |
| `np.where` (1 argument) | `np.where(condition)` | Indices where True | Students rescued by grace | 9 |
| `np.clip` | `np.clip(a, a_min, a_max)` | Values limited to a range | Marks capped at 100, pixels at 255 | 9, 10 |
| `np.round` | `np.round(a, decimals=0)` | Rounded values | Tidy printing of points and z-scores | 4, 9 |

**Formatting and plotting**

| Function | Signature | Returns | Used in this lab for | Tasks |
|:--|:--|:--|:--|:-:|
| `np.char.mod` | `np.char.mod(format, values)` | Formatted strings | Helper output | Helper |
| `np.char.add` | `np.char.add(a, b)` | Joined strings | Helper rows | Helper |
| `np.char.ljust` / `rjust` | `np.char.ljust(a, width)` | Padded strings | Helper alignment | Helper |
| `plt.imshow` | `plt.imshow(X, cmap=None)` | Image display | Show the "7" and climate table | Bonus 3 |
| `%timeit` | `%timeit -o statement` | Timing result | List vs NumPy race | Bonus 1 |

**Key parameters explained**

| Parameter | Meaning | Example from this lab |
|:--|:--|:--|
| `axis` | The axis that is collapsed | `axis=1` per city, `axis=0` per month |
| `dtype` | Element type | `dtype=int` for the image canvas |
| `size` | Output shape of random draws | 10,000 dice rolls |
| `return_counts` | Also return how often each value appears | Dice face counts |
| `num` | Number of points | 20 points between 0 and 1 |
| `endpoint` | Whether stop is included | `linspace` includes 1, `arange` does not |
| `ddof` | Divisor offset for std | 0 gives population std |
| `a_min`, `a_max` | Lower and upper limits | 0 and 100 for marks |
| `cmap` | Colour map | `gray` for the "7", `hot` for climate |

---

## 🧩 Syntax cheat sheet

**Indexing and slicing**

| Pattern | Meaning | Example from this lab |
|:--|:--|:--|
| `a[i]` | Row i (drops a dimension) | `hall[4]` is the last row |
| `a[i, j]` | Single element | `hall[3, 4]` is seat 20 |
| `a[start:stop]` | Range, stop excluded | `hall[3:]` last two rows |
| `a[r0:r1, c0:c1]` | Block of rows and columns | `hall[2:, 1:]` bottom-right block |
| `a[:, c0:c1]` | All rows, chosen columns | Monsoon columns Jul to Sep |
| `a[::-1]` / `a[:, ::-1]` | Reverse rows / columns | Left-right image flip |
| `a[mask]` | Keep only True positions | Units above 20 million |
| `a[i:j] = value` | Assign into a slice | Drawing the "7" |

**Operators and attributes**

| Item | Meaning | Used in |
|:--|:--|:--|
| `+  -  *  /  **` | Element-wise arithmetic | Tasks 6 to 10 |
| `>  <  >=  ==` | Element-wise comparison, gives True/False array | Tasks 3, 6 to 9 |
| `&` | Element-wise AND of two masks | Tasks 3, 9 |
| `a.shape` | Dimensions as a tuple | Tasks 7, 10 |
| `a.dtype` | Element type | Task 10 |
| `a.nbytes` | Memory used | Reference |

---

## 💡 Key learnings

| # | Learning | Evidence from this lab |
|:-:|:--|:--|
| 1 | The axis you name is the axis that disappears | `axis=1` on (5, 12) gave five city values, `axis=0` gave twelve month values |
| 2 | Slices exclude the stop index | `arange(10, 51)` was needed to include roll number 50 |
| 3 | A boolean mask replaces a loop | Counted months above 35 °C and units above 20 million with no loop |
| 4 | Comparing an array with a shifted copy finds patterns | Counted 265 double sixes loop-free |
| 5 | Seeds make random results repeatable | Seeds 2026 and 42 reproduce the same output every run |
| 6 | Broadcasting stretches scalars and small arrays | Shares, °C to °F, inversion and brightening in one step each |
| 7 | `clip` prevents overflow | Marks held at 100 and pixels at 255 |
| 8 | Ties return the first index | Lahore's May and June tie reported May |
| 9 | Inflation is a rate, not a price level | Low inflation still means prices rose |
| 10 | A grid of numbers is a picture | The "7" is an (8, 8) array, flipped and cropped by slicing |

---

## ⚠️ Common pitfalls

| Pitfall | Where it appears | Remedy |
|:--|:--|:--|
| Forgetting that stop is excluded | Roll numbers, `randint` for dice | Use stop + 1 (51 and 7) |
| Mixing up axis 0 and axis 1 | Per-city vs per-month results | Say which axis disappears, then check the output shape |
| Reshape size mismatch | Quarters from 12 months | Rows × columns must equal the element count |
| Slice returns a view | Image and hall slices | Copy the array before changing a slice, if the original must survive |
| Single index drops a dimension | `hall[4]`, `hall[3, 4]` | Use a width-one range such as `1:2` to keep the dimension |
| Ties in `argmax` | Lahore May and June | Document that the first index is returned |
| Sample vs population std | Hall and z-scores | NumPy defaults to ddof = 0 |
| Integer overflow in images | Brightening | Cap with `np.clip` |
| Reading low inflation as falling prices | Task 8 | Remember rates are year-on-year |

---

## 🚀 Running the notebook

| Step | Google Colab (recommended) | Local Jupyter |
|:-:|:--|:--|
| 1 | Open colab.research.google.com and sign in | Install `notebook`, `numpy` and `matplotlib` with pip |
| 2 | File → Upload notebook, choose `Lab02.ipynb` | Start Jupyter and open `Lab02.ipynb` |
| 3 | Runtime → Restart and run all | Kernel → Restart and Run All |

**Reproducibility**

| Seed | Used in | Output that repeats |
|:-:|:--|:--|
| 2026 | Task 3a and 3b | One uniform value and 25 normal values |
| 42 | Task 3c to 3e | Dice counts, P(six) and double-six count |

**Repository layout**

| Path | Content |
|:--|:--|
| `ML-Lab-2024-SE-15/Lab01/` | Previous lab |
| `ML-Lab-2024-SE-15/Lab02/Lab02.ipynb` | Solutions: 11 tasks, 52 parts, interpretations, bonus |
| `ML-Lab-2024-SE-15/Lab02/README.md` | This document |

---

<div align="center">

**Shahzad Ahmed Awan** ·
[GitHub: @ShahzadAhmedAwan](https://github.com/ShahzadAhmedAwan)

</div>