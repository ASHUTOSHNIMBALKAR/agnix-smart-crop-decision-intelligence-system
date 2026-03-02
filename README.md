# 🌾 AgniX — Smart Crop Decision Intelligence System

<div align="center">

![AgniX Banner](https://img.shields.io/badge/AgniX-Smart%20Crop%20AI-green?style=for-the-badge&logo=leaf&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen?style=for-the-badge)
![ML](https://img.shields.io/badge/ML-GaussianNB%20%7C%20RandomForest-orange?style=for-the-badge&logo=python)

**An AI-powered, full-stack web application that helps Indian farmers select the best crops based on their soil composition, weather conditions, water availability, and regional geography — with confidence scores, expected profit per acre, fertilizer roadmaps, and PDF report export.**

[Features](#-features) • [Tech Stack](#-tech-stack) • [Architecture](#-system-architecture) • [Setup](#-installation--setup) • [API Reference](#-api-reference) • [Screenshots](#-screenshots) • [Contributing](#-contributing)

</div>

---

## 📌 Table of Contents

- [About the Project](#-about-the-project)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Project Structure](#-project-structure)
- [Installation & Setup](#-installation--setup)
  - [1. ML Service (Python / Flask)](#1-ml-service-python--flask)
  - [2. Backend (Node.js / Express)](#2-backend-nodejs--express)
  - [3. Frontend (React / Vite)](#3-frontend-react--vite)
- [Environment Variables](#-environment-variables)
- [API Reference](#-api-reference)
- [ML Model Details](#-ml-model-details)
- [Database Schema](#-database-schema)
- [Regional Intelligence](#-regional-intelligence)
- [PDF Export Feature](#-pdf-export-feature)
- [Future Roadmap](#-future-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌱 About the Project

**AgniX** is a production-ready, scalable crop decision intelligence platform designed specifically for Indian agriculture. India has over **146 million farming households**, and most crop selection decisions are made based on tradition or guesswork — leading to poor yields, financial losses, and soil degradation.

AgniX solves this by combining **Machine Learning**, **real agronomic data**, and **region-specific crop intelligence** into a simple, farmer-friendly interface that works even on mobile devices.

> **"Right crop. Right soil. Right season. Maximized yield."**

### 🎯 Problem It Solves
| Problem | AgniX Solution |
|---------|----------------|
| Wrong crop selection → poor yield | ML model predicts top 3 best-fit crops with confidence % |
| No knowledge of soil NPK needs | Soil analysis input + fertilizer roadmap |
| Ignoring regional crop suitability | 16 Indian states with regional boosting logic |
| No profit estimation | Expected profit per acre for each crop |
| No offline access to reports | PDF report download for offline use |
| Language barriers | Clean UI with dropdowns — minimal typing required |

---

## ✨ Features

### 🤖 AI-Powered Crop Recommendations
- Uses a trained **GaussianNB (Gaussian Naive Bayes)** model on real agronomic data
- Returns **Top 3 crop recommendations** with confidence percentages
- Inputs: Nitrogen (N), Phosphorus (P), Potassium (K), pH, Moisture, Temperature, Humidity, Rainfall, Season, Water Availability

### 📍 Regional Intelligence
- Supports **16 Indian states** with custom crop boosting/penalty logic
- Crops native to the user's state get a **+15% confidence boost**
- Non-native crops get a **-15% confidence adjustment**
- States covered: Maharashtra, Punjab, Haryana, Karnataka, Kerala, Gujarat, UP, West Bengal, Assam, MP, Andhra Pradesh, Telangana, Tamil Nadu, Rajasthan, Bihar, Odisha, Chhattisgarh

### 💰 Expected Profit Estimation
- Static market-average profit per acre (INR) for each crop
- Crops mapped: Rice, Maize, Cotton, Soybean, Tur, Chickpea, Sugarcane, Wheat

### 🧪 Fertilizer Roadmap
- 3-stage fertilizer plan for every recommended crop:
  - **Pre-Sowing**: Organic compost + basal NPK dose
  - **Growth Stage**: Urea top dressing + soil moisture management
  - **Harvest Stage**: Water cutoff + dry condition guidelines

### 📄 PDF Export
- Farmers can download a full **PDF report** containing:
  - All input parameters
  - Top 3 crop recommendations with confidence scores
  - Expected profit per acre
  - Fertilizer roadmap
- Works offline after download

### 📱 Farmer-Friendly UI
- Mobile-responsive React frontend
- Large inputs and dropdowns — minimal typing required
- Clean, intuitive UX with loading states and error handling

### 🤖 WhatsApp Bot Ready
- Backend generates a concise **text summary** of each recommendation
- Example: `"Best crops: Cotton, Soybean, Tur. Expected profit: ₹45000 per acre."`
- Ready for integration with WhatsApp Business API or Twilio

### 🗄️ Persistent Database
- Every recommendation is **saved to MongoDB** for analytics and audit
- Full request payload stored: soil, weather, water, season, location, recommended crops

---

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|------------|---------|
| **React.js (v18)** | UI framework |
| **Vite** | Build tool & dev server |
| **CSS3** | Custom responsive styling |
| **jsPDF / html2pdf** | PDF report generation |
| **Fetch API** | HTTP calls to backend |

### Backend
| Technology | Purpose |
|------------|---------|
| **Node.js (v18+)** | Runtime environment |
| **Express.js** | REST API framework |
| **Mongoose** | MongoDB ODM |
| **Axios** | HTTP calls to ML microservice |
| **CORS** | Cross-origin support |
| **dotenv** | Environment variable management |

### ML Service
| Technology | Purpose |
|------------|---------|
| **Python 3.9+** | ML language |
| **Flask** | Microservice API framework |
| **Flask-CORS** | Cross-origin support |
| **scikit-learn** | GaussianNB model training |
| **NumPy** | Numerical operations |
| **Pandas** | Dataset handling |
| **Pickle** | Model serialization |

### Database
| Technology | Purpose |
|------------|---------|
| **MongoDB** | NoSQL document database |
| **MongoDB Atlas** (optional) | Cloud-hosted MongoDB |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         USER (Browser)                          │
│                     React.js + Vite Frontend                    │
│                      localhost:5173                             │
└──────────────────────────┬──────────────────────────────────────┘
                           │ POST /api/recommend
                           │ GET  /api/weather
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Node.js + Express Backend                     │
│                        localhost:5000                            │
│                                                                  │
│   ┌──────────────┐   ┌─────────────────┐   ┌────────────────┐  │
│   │  API Routes  │   │  Regional Logic  │   │  Profit Map    │  │
│   │  /recommend  │   │  16 States Boost │   │  Fertilizer    │  │
│   │  /weather    │   │  + Penalty       │   │  Roadmap       │  │
│   └──────┬───────┘   └─────────────────┘   └────────────────┘  │
│          │                                                       │
│          │ POST /predict                                         │
│          ▼                                                       │
│   ┌─────────────────┐           ┌──────────────────────────┐   │
│   │  ML Microservice │           │     MongoDB Database      │   │
│   │  Python + Flask  │           │    Recommendations       │   │
│   │  localhost:8000  │           │    Collection            │   │
│   │                  │           └──────────────────────────┘   │
│   │  GaussianNB Model│                                          │
│   │  7 Features Input│                                          │
│   │  22 Crop Classes │                                          │
│   └─────────────────┘                                           │
└─────────────────────────────────────────────────────────────────┘
```

**Data Flow:**
1. Farmer fills the form → React sends POST to `/api/recommend`
2. Backend extracts soil/weather params → calls ML service `/predict`
3. ML service returns Top 3 crops with probabilities
4. Backend enriches data: applies regional boosts, profit map, fertilizer roadmap
5. Result saved to MongoDB, returned to frontend
6. Frontend displays results; farmer can download PDF

---

## 📁 Project Structure

```
agnix-smart-crop-decision-intelligence-system/
│
├── 📂 backend/                          # Node.js + Express API Server
│   ├── 📂 models/
│   │   └── Recommendation.js            # Mongoose schema for DB records
│   ├── 📂 routes/
│   │   └── api.js                       # /recommend and /weather endpoints
│   ├── server.js                        # Express app entry point
│   ├── test.js                          # API test script
│   ├── package.json                     # Node dependencies
│   └── .env                             # Environment variables (not committed)
│
├── 📂 frontend/                         # React.js + Vite UI
│   ├── 📂 public/
│   │   ├── favicon.svg
│   │   └── icons.svg
│   ├── 📂 src/
│   │   ├── 📂 assets/                   # Static assets (hero image, SVGs)
│   │   ├── 📂 components/
│   │   │   ├── RecommendationForm.jsx   # Input form component
│   │   │   └── ResultsDisplay.jsx       # Results + PDF export component
│   │   ├── 📂 utils/
│   │   │   └── pdfGenerator.js          # PDF generation utility
│   │   ├── App.jsx                      # Root component
│   │   ├── App.css                      # Global styles
│   │   ├── main.jsx                     # React entry point
│   │   └── index.css                    # Base CSS reset
│   ├── index.html                       # HTML template
│   ├── vite.config.js                   # Vite configuration
│   └── package.json                     # Frontend dependencies
│
├── 📂 ml-service/                       # Python Flask ML Microservice
│   ├── app.py                           # Flask API with /predict endpoint
│   ├── train_model.py                   # Model training script
│   ├── model.pkl                        # Trained GaussianNB model (binary)
│   ├── test_probs.py                    # Model probability testing script
│   └── requirements.txt                 # Python dependencies
│
├── check_ports.js                       # Port availability checker utility
├── .gitignore                           # Git ignore rules
└── README.md                            # This file
```

---

## ⚙️ Installation & Setup

### Prerequisites

| Requirement | Version |
|------------|---------|
| Node.js | v16+ |
| Python | 3.9+ |
| MongoDB | Local (port 27017) or Atlas URI |
| npm | v8+ |
| pip | latest |

---

### 1. ML Service (Python / Flask)

This service trains the model and exposes the `/predict` API.

```bash
cd ml-service

# (Optional but recommended) Create a virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Mac / Linux:
source venv/bin/activate

# Install Python dependencies
pip install -r requirements.txt

# Train the model (downloads dataset, trains GaussianNB, saves model.pkl)
python train_model.py

# Start the Flask microservice
python app.py
```

> ✅ Runs on **http://localhost:8000**

**What `train_model.py` does:**
- Downloads the real **Crop Recommendation Dataset** from GitHub (2200 records, 22 crop types)
- Features: `N, P, K, temperature, humidity, ph, rainfall`
- Trains a **GaussianNB classifier**
- Achieves ~99% accuracy on the test split
- Saves the model as `model.pkl`

---

### 2. Backend (Node.js / Express)

This acts as the main API gateway orchestrating the database, UI, and ML service.

```bash
cd backend

# Install Node.js dependencies
npm install

# Create .env file (see Environment Variables section below)

# Start in development mode (with nodemon)
npm run dev

# OR start in production mode
npm start
```

> ✅ Runs on **http://localhost:5000**

---

### 3. Frontend (React / Vite)

The farmer-facing portal built with React.

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

> ✅ Runs on **http://localhost:5173**

---

## 🔐 Environment Variables

Create a `.env` file inside the `/backend` directory:

```env
# MongoDB connection string
MONGO_URI=mongodb://localhost:27017/agnix

# Backend port
PORT=5000

# ML microservice URL
ML_API_URL=http://127.0.0.1:8000

# (Optional) Weather API Key for future integration
WEATHER_API_KEY=your_openweathermap_api_key
```

---

## 📡 API Reference

### `POST /api/recommend`

Get AI-powered crop recommendations based on soil, weather, and location.

**Request Body:**
```json
{
  "soil": {
    "N": 90,
    "P": 42,
    "K": 43,
    "type": "Black",
    "pH": 6.5,
    "moisture": "Medium"
  },
  "weather": {
    "temperature": 28,
    "humidity": 70,
    "rainfall": 150
  },
  "water": {
    "availability": "Medium",
    "pH": 7.0
  },
  "season": "Kharif",
  "location": {
    "state": "Maharashtra",
    "address": "Pune, Maharashtra"
  }
}
```

**Success Response (200):**
```json
{
  "success": true,
  "recommendations": [
    {
      "crop": "cotton",
      "confidence": 92.5,
      "expectedProfit": 45000,
      "reason": "Based on soil NPK levels (90, 42, 43), pH of 6.5, and local weather suitability. This crop is highly suitable for the Maharashtra region.",
      "fertilizerRoadmap": {
        "pre_sowing": "Apply organic compost and basal dose of NPK.",
        "growth_stage": "Apply urea as top dressing. Maintain soil moisture.",
        "harvest_stage": "Stop watering 10 days before harvest. Ensure dry conditions."
      }
    },
    {
      "crop": "soybean",
      "confidence": 78.0,
      "expectedProfit": 30000,
      "reason": "Based on soil NPK levels (90, 42, 43), pH of 6.5, and local weather suitability. This crop is highly suitable for the Maharashtra region.",
      "fertilizerRoadmap": { "..." : "..." }
    }
  ],
  "textResponse": "Best crops: Cotton, Soybean, Tur. Expected profit: ₹45000 per acre."
}
```

---

### `GET /api/weather`

Fetch simulated (or live, when integrated) weather data.

**Success Response (200):**
```json
{
  "success": true,
  "weather": {
    "temperature": 31,
    "humidity": 74,
    "rainfall": 127
  }
}
```

---

### `POST /predict` *(ML Service — Internal)*

Direct ML microservice endpoint. Normally called by the backend only.

**Request Body:**
```json
{
  "N": 90,
  "P": 42,
  "K": 43,
  "temperature": 28,
  "humidity": 70,
  "ph": 6.5,
  "rainfall": 150
}
```

**Response:**
```json
{
  "recommendations": [
    { "crop": "cotton", "confidence": 77.5 },
    { "crop": "soybean", "confidence": 63.0 },
    { "crop": "tur", "confidence": 51.2 }
  ]
}
```

---

## 🤖 ML Model Details

| Property | Value |
|----------|-------|
| **Algorithm** | Gaussian Naive Bayes (GaussianNB) |
| **Dataset** | Crop Recommendation Dataset (2200 records) |
| **Input Features** | N, P, K, temperature, humidity, pH, rainfall |
| **Output Classes** | 22 crop types |
| **Test Accuracy** | ~99.09% |
| **Training Split** | 80% train / 20% test |
| **Random State** | 42 |
| **Model File** | `ml-service/model.pkl` (Pickle serialized) |

### Supported Crop Classes
`rice`, `maize`, `chickpea`, `kidneybeans`, `pigeonpeas`, `mothbeans`, `mungbean`, `blackgram`, `lentil`, `pomegranate`, `banana`, `mango`, `grapes`, `watermelon`, `muskmelon`, `apple`, `orange`, `papaya`, `coconut`, `cotton`, `jute`, `coffee`

### Feature Input Ranges (Training Data)
| Feature | Min | Max | Unit |
|---------|-----|-----|------|
| N (Nitrogen) | 0 | 140 | kg/ha |
| P (Phosphorus) | 5 | 145 | kg/ha |
| K (Potassium) | 5 | 205 | kg/ha |
| Temperature | 8.8 | 43.7 | °C |
| Humidity | 14.3 | 99.9 | % |
| pH | 3.5 | 9.9 | — |
| Rainfall | 20.2 | 298.6 | mm |

---

## 🗄️ Database Schema

**Collection:** `recommendations`

```javascript
{
  soil: {
    N: Number,           // Nitrogen (kg/ha)
    P: Number,           // Phosphorus (kg/ha)
    K: Number,           // Potassium (kg/ha)
    type: String,        // "Black", "Red", "Loamy", "Sandy", "Clay"
    pH: Number,          // 0 - 14
    moisture: String     // "Low", "Medium", "High"
  },
  weather: {
    temperature: Number, // Celsius
    humidity: Number,    // Percentage
    rainfall: Number     // mm
  },
  water: {
    availability: String, // "Low", "Medium", "High"
    pH: Number
  },
  location: {
    address: String,
    state: String,
    lat: Number,
    lon: Number
  },
  season: String,        // "Kharif", "Rabi", "Zaid"
  recommendedCrops: [
    {
      crop: String,
      confidence: Number
    }
  ],
  createdAt: Date        // Auto-generated timestamp
}
```

---

## 🗺️ Regional Intelligence

AgniX applies state-specific crop intelligence for **17 Indian states**:

| State | Top Recommended Crops |
|-------|-----------------------|
| Maharashtra | Cotton, Soybean, Tur, Sugarcane, Pomegranate, Grapes |
| Punjab | Wheat, Rice, Cotton, Maize |
| Haryana | Wheat, Rice, Mustard |
| Karnataka | Coffee, Ragi, Tur, Sunflower |
| Kerala | Coconut, Rubber, Coffee, Tea, Spices |
| Gujarat | Cotton, Groundnut, Castor |
| Uttar Pradesh | Sugarcane, Wheat, Rice, Potato, Mango |
| West Bengal | Jute, Rice, Tea |
| Assam | Tea, Jute, Rice |
| Madhya Pradesh | Soybean, Wheat, Chickpea |
| Andhra Pradesh | Rice, Cotton, Chilli, Tobacco |
| Telangana | Cotton, Rice, Maize, Tur |
| Tamil Nadu | Rice, Groundnut, Sugarcane, Cotton |
| Rajasthan | Mustard, Bajra, Chickpea, Guar |
| Bihar | Rice, Maize, Makhana, Litchi |
| Odisha | Rice, Jute |
| Chhattisgarh | Rice, Soybean |

**Confidence Adjustment Logic:**
- Native crop in state → **+15% confidence** (capped at 99%)
- Non-native crop → **-15% confidence** (floored at 10%)

---

## 📄 PDF Export Feature

The PDF report includes:
- **Header**: AgniX branding + report timestamp
- **Input Summary**: All soil, weather, water, season, and location values entered
- **Recommendations Table**: Crop name, confidence %, expected profit/acre
- **Fertilizer Roadmap**: 3-stage plan for the top recommended crop
- **AI Reasoning**: Explanation of why each crop was suggested

The PDF is generated client-side using `jsPDF` / `html2pdf.js` and downloaded directly to the farmer's device — **no server upload needed**.

---

## 🔭 Future Roadmap

| Feature | Status | Priority |
|---------|--------|----------|
| WhatsApp Bot Integration (Twilio) | 🔜 Planned | High |
| Live Weather API (OpenWeatherMap) | 🔜 Planned | High |
| Multilingual Support (Hindi, Marathi, Tamil) | 🔜 Planned | High |
| Market Price Integration (MSP) | 🔜 Planned | Medium |
| Disease Detection from Leaf Images (CNN) | 🔜 Planned | Medium |
| Offline PWA Mode | 🔜 Planned | Medium |
| Government Scheme Recommendations | 🔜 Planned | Low |
| Farmer Login & History Dashboard | 🔜 Planned | Low |
| Android / iOS App (React Native) | 🔜 Planned | Low |
| Irrigation Scheduling Module | 🔜 Planned | Low |

---

## 🤝 Contributing

Contributions are welcome! Here's how:

1. **Fork** this repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push to your branch: `git push origin feature/your-feature-name`
5. Open a **Pull Request**

### Commit Convention
This project follows [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` — New feature
- `fix:` — Bug fix
- `docs:` — Documentation update
- `style:` — Code formatting
- `refactor:` — Code restructuring
- `test:` — Tests
- `chore:` — Maintenance

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Ashutosh Nimbalkar**
- GitHub: [@ASHUTOSHNIMBALKAR](https://github.com/ASHUTOSHNIMBALKAR)
- Project: [agnix-smart-crop-decision-intelligence-system](https://github.com/ASHUTOSHNIMBALKAR/agnix-smart-crop-decision-intelligence-system)

---

<div align="center">

**Made with ❤️ for Indian Farmers 🇮🇳**

*"Technology should serve those who feed the nation."*

⭐ Star this repo if you found it useful!

</div>
