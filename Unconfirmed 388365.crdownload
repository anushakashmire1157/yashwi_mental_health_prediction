import streamlit as st
import pandas as pd
import joblib
import io

# Page config for mobile
st.set_page_config(page_title="Mental Health Predictor", layout="centered")

# Load model
model = joblib.load("mental_health_model.pkl")

# Font + Styling
st.markdown("""
    <style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
    html, body, [class*="css"] {
        font-family: 'Montserrat', sans-serif;
        scroll-behavior: smooth;
    }

    div.stButton > button {
        color: white !important;
        background-color: #4CAF50;
        border-radius: 8px;
        font-weight: bold;
    }

    .stDownloadButton > button {
        background-color: #6c63ff;
        color: white;
        font-weight: 600;
        border-radius: 8px;
        padding: 0.5em 1em;
        transition: 0.3s ease-in-out;
    }
    .stDownloadButton > button:hover {
        background-color: #5548c8;
        transform: scale(1.02);
    }
    </style>
""", unsafe_allow_html=True)

# Theme toggle
dark_mode = st.toggle("🌓 Dark Mode")

if dark_mode:
    st.markdown("""
        <style>
        .stApp { background-color: #0E1117; color: white; }
        .stSlider > div, .stSelectbox > div, .stButton > button {
            color: white !important;
        }
        label, div[data-testid="stMarkdownContainer"] p {
            color: white !important;
        }
        </style>
    """, unsafe_allow_html=True)

# Title and subtitle
st.markdown("<h1 style='color:#3949ab;'>Mental Health Treatment Predictor 💬</h1>", unsafe_allow_html=True)
st.markdown("<p>Fill in the details below to get a prediction:</p>", unsafe_allow_html=True)

# --- INPUT FORM ---
with st.container():
    age = st.slider("Age", 18, 100, 25)
    gender = st.selectbox("Gender", ["Male", "Female", "Other"])
    self_employed = st.selectbox("Are you self-employed?", ["No", "Yes"])
    family_history = st.selectbox("Family history of mental illness?", ["No", "Yes"])
    work_interfere = st.selectbox("Work Interference with mental health?", ["Never", "Rarely", "Sometimes", "Often"])
    remote_work = st.selectbox("Do you work remotely?", ["No", "Yes"])
    tech_company = st.selectbox("Do you work in a tech company?", ["No", "Yes"])
    benefits = st.selectbox("Employer provides mental health benefits?", ["No", "Yes"])
    care_options = st.selectbox("Access to care options?", ["No", "Yes"])
    wellness_program = st.selectbox("Has wellness program?", ["No", "Yes"])
    seek_help = st.selectbox("Is help encouraged at work?", ["No", "Yes"])
    anonymity = st.selectbox("Is anonymity protected?", ["No", "Yes"])
    leave = st.selectbox("Ease of taking mental health leave?", ["Difficult", "Don't know", "Somewhat easy", "Very easy"])
    mental_health_consequence = st.selectbox("Negative mental health consequence at work?", ["No", "Yes"])
    phys_health_consequence = st.selectbox("Negative physical health consequence at work?", ["No", "Yes"])
    coworkers = st.selectbox("Can you talk to coworkers?", ["No", "Some", "Yes"])
    supervisor = st.selectbox("Can you talk to supervisor?", ["No", "Some", "Yes"])
    mental_health_interview = st.selectbox("Willing to discuss mental health in interview?", ["No", "Maybe", "Yes"])
    phys_health_interview = st.selectbox("Willing to discuss physical health in interview?", ["No", "Maybe", "Yes"])
    mental_vs_physical = st.selectbox("Is mental health as important as physical?", ["No", "Don't know", "Yes"])
    obs_consequence = st.selectbox("Have you seen mental health-related consequences?", ["No", "Yes"])

# --- ENCODING MAPS ---
def encode(val, mapping): return mapping.get(val)
gender_map = {"Male": 1, "Female": 0, "Other": 2}
binary_map = {"Yes": 1, "No": 0}
work_map = {"Never": 0, "Rarely": 1, "Sometimes": 2, "Often": 3}
leave_map = {"Difficult": 0, "Don't know": 1, "Somewhat easy": 2, "Very easy": 3}
coworker_map = {"No": 0, "Some": 2, "Yes": 1}
interview_map = {"No": 0, "Maybe": 2, "Yes": 1}
mental_vs_physical_map = {"No": 0, "Don't know": 2, "Yes": 1}

# Input DataFrame
input_data = pd.DataFrame([[
    age,
    encode(gender, gender_map),
    encode(self_employed, binary_map),
    encode(family_history, binary_map),
    encode(work_interfere, work_map),
    encode(remote_work, binary_map),
    encode(tech_company, binary_map),
    encode(benefits, binary_map),
    encode(care_options, binary_map),
    encode(wellness_program, binary_map),
    encode(seek_help, binary_map),
    encode(anonymity, binary_map),
    encode(leave, leave_map),
    encode(mental_health_consequence, binary_map),
    encode(phys_health_consequence, binary_map),
    encode(coworkers, coworker_map),
    encode(supervisor, coworker_map),
    encode(mental_health_interview, interview_map),
    encode(phys_health_interview, interview_map),
    encode(mental_vs_physical, mental_vs_physical_map),
    encode(obs_consequence, binary_map)
]], columns=[
    'Age', 'Gender', 'self_employed', 'family_history', 'work_interfere',
    'remote_work', 'tech_company', 'benefits', 'care_options', 'wellness_program',
    'seek_help', 'anonymity', 'leave', 'mental_health_consequence',
    'phys_health_consequence', 'coworkers', 'supervisor',
    'mental_health_interview', 'phys_health_interview',
    'mental_vs_physical', 'obs_consequence'])

# --- PREDICT ---
if st.button("Predict"):
    result = model.predict(input_data)[0]
    input_data["Prediction"] = "Likely to seek treatment" if result == 1 else "Not likely to seek treatment"

    if result == 1:
        st.success("✅ Person is **likely** to seek mental health treatment.")
    else:
        st.warning("⚠️ Person is **not likely** to seek mental health treatment.")

    # CSV download
    output = io.StringIO()
    input_data.to_csv(output, index=False)
    st.download_button("📥 Download CSV", data=output.getvalue(), file_name="prediction_result.csv", mime="text/csv")
