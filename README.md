# CFM56-7B-ENGINE-MONITORING
# CFM56-7B Engine Health Monitoring Dashboard

**Created by Y.A. Prasetya**

## Overview

This project is a simple **Aircraft Engine Health Monitoring (EHM) Dashboard** built using **Python and Streamlit**.
The application simulates a monitoring system similar to modern aviation analytics platforms used in aircraft maintenance environments.

The dashboard monitors key **CFM56-7B engine parameters** during **engine start and takeoff phases**, providing real-time status indications and maintenance recommendations.

This project is intended for:

* Aircraft Maintenance Engineers
* Reliability Engineers
* Aviation Data Analysts
* MRO Technical Development

---

## Features

### Aircraft Information Input

Users can enter operational information such as:

* Date
* Aircraft Registration
* Engine Number
* Route

### Engine Start Monitoring

The system monitors **EGT during engine start**.

Limit:

* **EGT > 725°C → HOT START**

If a hot start is detected, the system generates:

* Warning alert
* Possible cause
* Maintenance recommendation

---

### Takeoff Parameter Monitoring

The following engine parameters are monitored:

| Parameter       | Maximum Limit |
| --------------- | ------------- |
| N1              | 102 %         |
| N2              | 105 %         |
| Oil Pressure    | 60 psi        |
| Oil Temperature | 150 °C        |
| Fuel Flow       | 5200 pph      |
| EGT             | 950 °C        |

---

### Engine Status Logic

Each parameter is classified into three operational conditions:

| Status  | Condition           | Color  |
| ------- | ------------------- | ------ |
| Normal  | Below 80% of limit  | Green  |
| Caution | Within 20% of limit | Yellow |
| WARNING | Above limit         | Red    |

If **Caution or Warning** occurs, the system provides:

* Possible technical causes
* Maintenance recommendations

---

### Fleet Monitoring

The dashboard allows monitoring **multiple aircraft entries**.

Users can:

* Add aircraft data
* View fleet monitoring table
* Track engine parameter history

---

### Engine Parameter Trend

A small trend chart displays historical values for:

* N1
* N2
* EGT
* Oil Pressure
* Oil Temperature
* Fuel Flow

This helps visualize performance trends.

---

### Data Export

Users can:

* Save monitoring data
* Generate a printable report

---

## Technologies Used

Python libraries used in this project:

* **Streamlit** – interactive web dashboard
* **Pandas** – data processing
* **Matplotlib** – parameter trend visualization

---

## Installation

Install the required Python libraries:

```bash
pip install -r requirements.txt
```

---

## Requirements

The project requires the following libraries:

```
streamlit
pandas
matplotlib
```

---

## Running the Application

Navigate to the project directory and run:

```bash
streamlit run cfm56_7b_ehm.py
```

The dashboard will open automatically in your browser.

Default address:

```
http://localhost:8501
```

---

## Example Use Case

This dashboard can be used as a **conceptual prototype of an Engine Health Monitoring system** used in modern aircraft maintenance environments such as:

* Predictive Maintenance Systems
* Reliability Monitoring Platforms
* Fleet Health Dashboards

---

## Future Improvements

Possible enhancements include:

* Engine Health Score calculation
* EGT Margin tracking
* Vibration monitoring
* Predictive maintenance alerts
* Fleet reliability ranking
* Automatic PDF maintenance reports
* Integration with aircraft flight data

---

## Author

**Y.A. Prasetya**
Aircraft Maintenance Engineer
Batam Aero Technic
