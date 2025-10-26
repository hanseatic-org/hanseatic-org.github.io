# ✈️ Flight Scoring Algorithm

The **flight scoring algorithm** determines the *best* itinerary among all available options by combining several key travel quality factors — including **price**, **duration**, **number of stops**, and **layover efficiency** — into a single composite score - a value normalised to 0.0 - 1.0 range.

---

## 🧠 Overview

The algorithm evaluates every itinerary using a **weighted scoring formula**, where each flight’s attributes are normalized and compared relative to the best (minimum) values in the current search set.  

The itinerary with the **highest overall score** is selected as the “best” option.

---

## ⚙️ Step-by-Step Process

### **1. Preprocessing and Normalization**

Before scoring, the algorithm:

- Calculates the **minimum flight price** among all itineraries.
- Calculates the **minimum total duration** (including flight and layover time).
- Stores total durations for each itinerary for later use.

These values are used to normalize other itineraries’ scores, ensuring a fair comparison between short and long trips or cheap and expensive flights.

---

### **2. Score Components**

Each itinerary is assigned multiple partial scores, each representing a different travel quality dimension.

| Component | Description | Formula | Weight |
|------------|-------------|----------|--------|
| **Price Score** | Rewards cheaper flights | `min_price / price` | **0.5** |
| **Duration Score** | Rewards shorter total travel time (flight + layovers) | `min_duration / duration` | **0.3** |
| **Stops Score** | Rewards fewer stops (nonstop > 1-stop > multi-stop) | `1 / (1 + total_layovers)` | **0.1** |
| **Layover Score** | Rewards efficient layovers (around 2 hours is ideal) | `exp(-((avg_layover_min - 120)^2) / 120)` | **0.1** |

> 💡 *Normalization ensures all values fall roughly between 0 and 1, allowing balanced weighting across different dimensions.*

---

### **3. Layover Efficiency (Special Handling)**

Layovers are treated with extra nuance:

- The algorithm finds all **layovers per itinerary**.
- It calculates their **average duration**.
- A “bell-curve” function centered at **2 hours (120 minutes)** assigns the best score for ideal layovers, penalizing both excessively short and long ones.

Example:

| Avg Layover Time | Layover Score |
|------------------:|--------------:|
| 60 min            | 0.61 |
| 120 min           | 1.00 ✅ |
| 240 min           | 0.37 |
| 480 min           | 0.04 |

---

### **4. Final Scoring Formula**

The overall score for each itinerary is calculated as:

```text
final_score = 
  0.5 * price_score +
  0.3 * duration_score +
  0.1 * stops_score +
  0.1 * layover_score
```