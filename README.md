# The Payment Advantage: Capturing Untapped Fare Revenue in NYC's Yellow Taxi Fleet

## Project Story (Animated Deck)
<p align="center">

<img src="https://github.com/anikaa20/Statistical-Analysis-of-Revenue-Across-Payment-Methods--/blob/main/NY_TAXI_DECK_900px_3s.gif" width="900"/>

</p>
<p align="center">
  <a href="https://docs.google.com/presentation/d/1Bpw3ZNhzPbRM4KQABSnSnpISHPkOALkH/edit?usp=sharing&ouid=108825657904597871730&rtpof=true&sd=true">
    📊 <b>View the Complete Project Deck</b>
  </a>
</p>

## Project Background

New York City's yellow taxi fleet operates on a per-trip revenue model where base fares, distance metering, and surcharges determine driver earnings. As a data analyst within the operations team, this project investigates a single, high-leverage question: **does payment type systematically affect fare revenue and can management act on it?**

Analysis is based on January 2015 trip data sourced from Kaggle, covering four key variables: `payment_type`, `fare_amount`, `trip_distance`, and `passenger_count`.

Insights and recommendations are provided across four areas:
- **Payment Type Distribution** : the 58/42 card-cash split and what it signals
- **Fare Amount Analysis** : quantifying and statistically validating the revenue gap
- **Trip Distance Patterns** : why the gap is structural, not incidental
- **Passenger Count Behavior** : identifying the highest-volume nudge opportunity

Full Python EDA code → [`Notebook.ipynb`](https://github.com/anikaa20/Statistical-Analysis-of-Revenue-Across-Payment-Methods--/blob/main/Notebook.ipynb)

---

## Data Structure & Initial Checks

**Source:** Single flat table — NYC Yellow Taxi Trip Records, January 2015 (Kaggle)

**Raw dataset :** 908,819 rows × 19 columns → **Cleaned dataset :** 104,816 rows × 4 columns

| Cleaning Step | Action |
|---|---|
| Null removal | Dropped 1 null per column |
| Deduplication | Removed duplicate rows → 114,829 rows |
| Payment type filter | Retained Card & Cash only; excluded No Charge & Dispute |
| Passenger count filter | Retained 1-5 passengers only |
| Zero/negative values | Removed zero fares and zero distances |
| Outlier removal (IQR) | Applied IQR bounds on `fare_amount` and `trip_distance` → **104,816 rows** |

---

## Executive Summary

Card payments generate **$1.89 more per trip** than cash ($20.24 vs. $18.35), a difference confirmed as statistically significant via Welch's T-test (p-value ≈ 0.0). This gap is structural, card customers self-select onto longer, higher-value trips (5.38 vs. 4.79 miles). With **41.7% of trips still paid in cash** and solo riders making up 39.1% of all volume, the fleet has a large, reachable base that , **with the right nudge** can be shifted toward the higher-revenue channel at near-zero cost.

> ![Insights Overview](https://github.com/anikaa20/Statistical-Analysis-of-Revenue-Across-Payment-Methods--/blob/main/Overview.png)

---

## Insights Deep Dive

### Category 1: Payment Type Distribution
* Card dominates at **58.3%** of trips vs. cash at **41.7%**, but the cash base is large enough (≈44K monthly trips) to represent a material conversion opportunity.
* Card preference holds consistently across all passenger count segments, confirming it reflects genuine customer behavior rather than situational convenience.

### Category 2: Fare Amount Analysis
* Card customers average **$20.24/trip** vs. **$18.35** for cash, a **$1.89 gap** that compounds significantly at fleet scale.
* Welch's T-test result: **T-stat = -223.36, p-value = 0.0** → null hypothesis rejected. The fare gap is real, systematic, and actionable.


### Category 3: Trip Distance Patterns
* Card trips average **5.38 miles** vs. **4.79 miles** for cash, confirming card customers are disproportionately on longer, higher-value routes.
* Cash is structurally concentrated in short, low-fare trips. This isn't random, it reinforces the revenue gap at the behavioral level.


### Category 4: Passenger Count Behavior
* **Solo riders (1 passenger) = 39.1% of all trips**, the single largest cohort and the highest-volume target for any nudge intervention.
* Card adoption is strong even in the 5-6 passenger segments, indicating willingness to pay by card exists broadly across the customer base.


---

## Recommendations

* **Deploy in-cab payment prompts at trip start.** Default to card selection on the in-cab screen. Default bias is proven :- no new infrastructure needed, card machines already exist.

* **Target the solo-rider segment first.** At 39.1% of volume, a nudge campaign here delivers the highest reach-to-effort ratio across the fleet.

* **Introduce card-exclusive micro-benefits.** Loyalty points or ride credits create a pull factor for cash customers to switch without penalizing cash explicitly.

* **Build a driver incentive tied to card-payment ratio.** Align driver behavior with fleet revenue goals through a monthly performance bonus, turning drivers into active advocates at the point of service.

---

## Assumptions & Caveats

* **IQR outlier removal** reduced the dataset significantly but was necessary to prevent extreme fares and distances from distorting payment-type comparisons.
* **January 2015 only** : Findings reflect a single month; seasonal variation is not captured. Replication across multiple months is recommended before fleet-wide rollout.
* **Tip amounts excluded** : Analysis uses `fare_amount`, not `total_amount`. Since card customers likely tip more (cash tips go unrecorded), the true revenue gap per trip is probably **larger** than $1.89.
* **P-value of ~0.0** reflects Python's floating-point precision limit, interpreted as "vanishingly small," not literally zero.
