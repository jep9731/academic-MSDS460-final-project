# Clinical Trial Scan Scheduling Optimization

## 📌 Overview
This project develops a **Mixed-Integer Linear Programming (MILP)** model to optimize scheduling for a **neuroimaging clinical trial** requiring:
- **MRI** scans
- **Amyloid PET** scans
- **Tau PET** scans

The model minimizes the **total number of distinct visit days per patient**, subject to scanner availability, clinical constraints, and biological safety constraints.

---

## 📓 Python Notebook

The `Pasaye_Final Project.ipynb` contains the first simulated a patient list, scanner availability, scan time slots, and capacity for each facility.
Additionally, the Jupyter Notebook details the decision variables, constraints, objective function, and finds an optimal solution using `PuLP`.
Lastly, after the solution has been determined, a Gantt visualization, highlighting the patient schedule of the model, a scan utilization plot, determining how much each facility was used during in the model, and a daily usage plot, illustrates the number of days each facility was used in the model.

---

## 🎯 Problem Statement
We aim to schedule **24 participants** for three different imaging modalities within a **6-month window**, while satisfying operational and biological constraints.

---

## 🏥 Facility Constraints
- **MRI Facility**:  
  - 90-minute sessions  
  - Available **Monday–Friday**, 8:30 AM – 4:30 PM
- **PET Facility**:  
  - 2 sessions/day  
  - Available **Tuesday–Thursdays** at:
    - 4:30 PM – 5:00 PM
    - 5:00 PM – 5:30 PM

---

## ⚠️ Biological Constraints
- PET scans **cannot occur on the same day** and must be **≥ 24 hours apart**
- **Amyloid PET**: Available **Tuesday–Thursday**
- **Tau PET**: Available **Thursday only**
- All scans must occur **within 6 months** for each participant

---

## 🔢 Model Formulation

**Decision Variables**  
- $x_{p,d,t,s} \in \{0,1\}$: 1 if patient $p$ has scan $s$ on day $d$ at time $t$  
- $y_{p,d} \in \{0,1\}$: 1 if patient $p$ has any scan on day $d$

**Objective**  
$$
\min \sum_p \sum_d y_{p,d}
$$
Minimize the total number of distinct scan days.

**Key Constraints**
1. **Linking Constraint**: If any scan is assigned on day $d$, then $y_{p,d} = 1$
2. **One Scan per Type per Patient**
3. **Facility Capacity Constraints**
4. **Biological Constraints** (PET spacing)

---

## 🛠️ Summary of Techniques Used
- **Mixed-Integer Linear Programming** (MILP) with binary decision variables
- **Big-M linking constraints** to track patient visit days
- **Operational constraint modeling** for:
  - Time-specific scan slots
  - Day-of-week restrictions
  - Sequential scan rules
- **Visualization outputs**:
  - Gantt chart of scan schedules
  - Resource utilization line chart
  - Daily scan usage bar chart

---
