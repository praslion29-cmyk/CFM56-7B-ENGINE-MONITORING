import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
from datetime import datetime

st.set_page_config(page_title="CFM56-7B Engine Monitoring", layout="wide")

st.title("CFM56-7B ENGINE HEALTH MONITORING")
st.subheader("Create by Y.A. Prasetya")

# -----------------------------
# LIMIT CONFIG
# -----------------------------

limits = {
    "N1":102,
    "N2":105,
    "Oil Pressure":60,
    "Oil Temp":150,
    "Fuel Flow":5200,
    "EGT Takeoff":950,
}

# -----------------------------
# STATUS FUNCTION
# -----------------------------

def check_status(value, limit):

    caution = limit * 0.8

    if value > limit:
        return "WARNING", "red"

    elif value >= caution:
        return "CAUTION", "orange"

    else:
        return "Normal", "green"


# -----------------------------
# POSSIBLE CAUSE
# -----------------------------

def maintenance_advice(param):

    advice = {

        "EGT":"Possible Cause: Fuel nozzle dirty / compressor efficiency drop\nRecommendation: Borescope inspection & engine performance check",

        "N1":"Possible Cause: Engine overspeed / FADEC issue\nRecommendation: Engine inspection & FADEC system check",

        "N2":"Possible Cause: High core speed\nRecommendation: Check turbine condition",

        "Oil Pressure":"Possible Cause: Oil pump malfunction / blockage\nRecommendation: Check lubrication system",

        "Oil Temp":"Possible Cause: Cooling inefficiency / high engine load\nRecommendation: Check oil cooler",

        "Fuel Flow":"Possible Cause: Combustion inefficiency\nRecommendation: Inspect fuel control unit"

    }

    return advice.get(param,"Check engine system")


# -----------------------------
# AIRCRAFT DATA STORAGE
# -----------------------------

if "data" not in st.session_state:
    st.session_state.data = pd.DataFrame()

# -----------------------------
# AIRCRAFT INFO
# -----------------------------

st.header("Aircraft Information")

col1,col2,col3,col4 = st.columns(4)

date = col1.date_input("Date",datetime.today())
reg = col2.text_input("Aircraft Registration")
engine = col3.text_input("Engine No")
route = col4.text_input("Route")


# -----------------------------
# ENGINE START MONITOR
# -----------------------------

st.header("Engine Start Monitoring")

egt_start = st.number_input("EGT Start (°C)")

if egt_start > 725:
    st.error("WARNING : HOT START DETECTED")
    st.write("Possible Cause: Excessive fuel during start")
    st.write("Recommendation: Combustion chamber inspection")


# -----------------------------
# TAKEOFF PARAMETERS
# -----------------------------

st.header("Takeoff Parameter Monitoring")

col1,col2,col3 = st.columns(3)

N1 = col1.number_input("N1 (%)")
N2 = col2.number_input("N2 (%)")
EGT = col3.number_input("EGT Takeoff (°C)")

col4,col5,col6 = st.columns(3)

oil_press = col4.number_input("Oil Pressure (psi)")
oil_temp = col5.number_input("Oil Temp (°C)")
fuel_flow = col6.number_input("Fuel Flow (pph)")


# -----------------------------
# STATUS DISPLAY
# -----------------------------

st.header("Engine Status")

params = {
    "N1":N1,
    "N2":N2,
    "Oil Pressure":oil_press,
    "Oil Temp":oil_temp,
    "Fuel Flow":fuel_flow,
    "EGT":EGT
}

for p,v in params.items():

    limit = limits["EGT Takeoff"] if p=="EGT" else limits[p]

    status,color = check_status(v,limit)

    st.markdown(f"**{p} : {v} → :{color}[{status}]**")

    if status != "Normal":
        st.warning(maintenance_advice(p))


# -----------------------------
# SAVE DATA
# -----------------------------

if st.button("Add Aircraft Data"):

    new_data = {

        "Date":date,
        "Aircraft":reg,
        "Engine":engine,
        "Route":route,
        "N1":N1,
        "N2":N2,
        "EGT":EGT,
        "Oil Pressure":oil_press,
        "Oil Temp":oil_temp,
        "Fuel Flow":fuel_flow
    }

    st.session_state.data = pd.concat(
        [st.session_state.data,pd.DataFrame([new_data])],
        ignore_index=True
    )

    st.success("Aircraft Data Added")


# -----------------------------
# SHOW DATA
# -----------------------------

st.header("Fleet Monitoring Data")

st.dataframe(st.session_state.data)


# -----------------------------
# TREND GRAPH
# -----------------------------

st.header("Engine Parameter Trend")

if not st.session_state.data.empty:

    fig = plt.figure(figsize=(6,3))

    for col in ["N1","N2","EGT","Oil Pressure","Oil Temp","Fuel Flow"]:
        plt.plot(st.session_state.data[col],label=col)

    plt.legend(fontsize=6)
    plt.xticks(fontsize=6)
    plt.yticks(fontsize=6)

    st.pyplot(fig)


# -----------------------------
# EXPORT
# -----------------------------

st.header("Report")

if st.button("Save Data"):

    st.session_state.data.to_csv("engine_monitoring.csv",index=False)

    st.success("Data Saved")


st.button("PRINT REPORT")
