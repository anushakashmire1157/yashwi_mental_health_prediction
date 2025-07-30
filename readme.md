🧠 Mental Health Treatment Predictor
A user-friendly Streamlit web application that predicts whether an individual is likely to seek mental health treatment based on workplace and personal factors.


🚀 Key Features

🎨 Clean and responsive UI with light/dark theme toggle
📋 Intuitive form-based input interface
📥 Option to download predictions as CSV
📊 Powered by a trained Random Forest model
🔐 No data is stored – runs entirely client-side


📁 Project Structure
FIRST_APP/
├── app.py                    # Streamlit application code
├── mental_health_model.pkl   # Trained ML model
├── requirements.txt          # Python dependencies


⚙️ Installation
Install required packages:

pip install -r requirements.txt

▶️ Running the App Locally
Run the app using Streamlit:
streamlit run app.py


🌐 Deployment (No GitHub Needed)
You can deploy the app using Streamlit Cloud in minutes:

Compress the FIRST_APP folder as a .zip
Visit streamlit.io/cloud
Sign in (Google/GitHub/email)
Click "New App" and choose to upload your .zip
Set the entry point as app.py
Click Deploy


✅ Done! Your app is live.


🧠 About the Model
Model: RandomForestClassifier

Purpose: Predict if a person is likely to seek mental health treatment (Yes/No)

Training Data: Real-world mental health survey data


💡 Use Cases
Corporate wellness programs
HR tools for proactive support
Anonymous screening platforms
Student mental health initiatives


👤 Author
Made with ❤️ by Yashswi 
Empowering mental health awareness through technology