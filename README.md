# 🌿 PlantCare: AI-Powered Banana Disease Diagnosis & Management

**PlantCare** is a comprehensive web application designed to assist farmers and agricultural experts in diagnosing banana plant diseases. By leveraging Deep Learning (CNN) for image analysis and Generative AI (Google Gemini) for treatment advice, it provides actionable insights, task scheduling, and weather-based recommendations.

---

### Dashboard


---

## 🚀 Key Features

### 🔍 **AI Diagnosis**
* **Visual Detection:** Upload images of banana leaves or fruit. The system uses a fine-tuned **MobileNetV2** model to classify pests and diseases (12 classes including Panama Disease, Sigatoka, etc.).
* **Smart Advice:** Integrates **Google Gemini AI** to generate detailed descriptions, step-by-step treatment plans, and prevention strategies based on the diagnosis.

### 📅 **Task Management**
* **Automated Scheduling:** AI generates a 4-6 week care schedule based on the specific disease.
* **Interactive Calendar:** Visual interface (powered by FullCalendar) to track watering, fungicide application, and inspections.
* **Progress Tracking:** Upload follow-up images to compare against original diagnoses and track recovery.

### 🌦️ **Environmental Insights**
* **Weather Integration:** Fetches real-time weather and forecasts (via OpenWeatherMap) for the user's specific crop location.
* **Dynamic Recommendations:** AI analyzes current weather conditions to suggest adjustments to farm tasks (e.g., "Delay spraying due to rain").

### 🛠️ **Admin Dashboard**
* **User Management:** Admins can view, edit, or delete users.
* **Analytics:** Interactive charts showing diagnosis accuracy feedback (Confirmed vs. Inaccurate).
* **Feedback Loop:** Admin review system for reported inaccuracies to improve model performance over time.

---

## 🛠️ Tech Stack

* **Backend:** Python, Flask
* **Database:** MongoDB (via Flask-PyMongo)
* **AI & Machine Learning:**
    * **Vision:** TensorFlow/Keras (MobileNetV2 Transfer Learning)
    * **LLM:** Google Gemini API (`gemini-2.5-flash`)
* **Frontend:** HTML5, CSS3, JavaScript
* **Libraries:**
    * **Charts:** Chart.js
    * **Calendar:** FullCalendar
    * **PDF:** xhtml2pdf (Report generation)
    * **Sheets:** gspread (Google Sheets for contact form)
    * **Other Basic **

---

## ⚙️ Installation & Setup

Follow these steps to run the project locally.

### 1. Create a Virtual Environment
```Bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
```

### 2. Install Dependencies
```Bash
pip install -r requirements.txt
```

### 3. Environment Configuration
Create a .env file in the root directory and add the following variables:

```Code snippet
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/plantcare_db
GEMINI_API_KEY=your_google_gemini_api_key
WEATHER_API_KEY=your_openweathermap_api_key
```

### 4. Google Sheets Setup (Contact Form)
1. Enable the Google Sheets API and Google Drive API in Google Cloud Console.
2. Download your service account credentials and rename the file to credentials.json.
3. Place credentials.json in the project root.
4. Create a Google Sheet named "PlantCare Messages" and share it with your service account email.

### 5. Model Setup
Ensure the trained model file banana_disease_model.keras is placed in the root directory.

### 6. Run the Application
```Bash
python app.py
```

Access the app at http://127.0.0.1:5000.

---

## 📂 Project Structure
```
PlantCare/
├── app.py                   # Main Flask application logic
├── banana_disease_model.keras # Trained CNN model
├── requirements.txt         # Python dependencies
├── credentials.json         # Google Service Account keys (DO NOT COMMIT)
├── .env                     # Environment variables (DO NOT COMMIT)
├── static/
│   ├── style.css            # Global styling
│   ├── main.js              # Frontend logic (Modals, Charts, Calendar)
│   ├── uploads/             # User uploaded plant images
│   └── profile_pics/        # User avatars
├── templates/
│   ├── layout.html          # Base template
│   ├── dashboard.html       # User dashboard
│   ├── diagnose.html        # Image upload page
│   ├── results.html         # Analysis results
│   ├── calendar.html        # Task calendar
│   ├── logbook.html         # History & Filtering
│   ├── admin_dashboard.html # Admin user management
│   └── ...                  # Other .html pages
```

---

## 🧠 AI Workflow
1. Input: User uploads an image of a banana leaf/fruit.
2. Preprocessing: Image is resized to 256x256 and normalized.
3. Classification: The MobileNetV2 model predicts the disease class (e.g., Leaf Banana Panama Disease) and confidence score.
4. Generative Advice: app.py constructs a prompt with the disease name and sends it to Gemini.
5. Output: Gemini returns structured Markdown containing the Description, Treatment, Prevention, and a Tabular Schedule, which is rendered in the UI.

---

## 📄 License
This project is licensed under the MIT License - see the [![License: MIT](LICENSE) file for details.
