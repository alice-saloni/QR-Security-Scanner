QR Code Security Analysis System

A cybersecurity project that scans QR codes, analyses their hidden content, detects malicious behavior, and generates a security rating to determine how safe the QR code is to use.


Project Overview

QR codes can hide unsafe URLs, phishing pages, or malicious downloads. Since users cannot verify the content visually, attackers often misuse QR codes (“Quishing”).
This project solves that problem by creating a system that:

* Decodes QR content
* Analyses URLs, files, text, and WiFi credentials
* Detects security issues using heuristics, rules, and reputation checks
* Identifies potential malware indicators
* Generates a clear, human-readable security report
* Provides a Security Rating showing how safe the QR code is

---

## 🧩 **Key Features**

* ✔ QR code scanning (upload or camera input)
* ✔ URL reputation checks (domain age, redirects, blacklist)
* ✔ Malware indication detection
* ✔ Content-type classification
* ✔ Heuristic-based threat analysis
* ✔ Optional ML-based malicious content classification
* ✔ Security Score (0–100)
* ✔ Detailed risk report
* ✔ User-friendly frontend

---

## 📁 **Project Structure / Layout**

```
qr-security/
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── utils/
│   │   └── services/
│   ├── public/
│   └── package.json
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   ├── scan.py          # Main QR analysis endpoint
│   │   │   ├── report.py
│   │   │   └── ml_model.py
│   │   ├── core/
│   │   │   ├── decoder.py       # QR decoding
│   │   │   ├── url_analyzer.py
│   │   │   ├── heuristics.py
│   │   │   ├── reputation.py
│   │   │   ├── content_parser.py
│   │   │   └── scoring_engine.py
│   │   ├── models/
│   │   ├── utils/
│   │   └── main.py
│   │
│   ├── requirements.txt
│
├── dataset/
│   ├── benign_urls.csv
│   ├── malicious_urls.csv
│   └── features.csv
│
├── docs/
│   ├── architecture.png
│   ├── flowchart.png
│   └── report_samples/
│
└── README.md
```

---

## ⚙️ **System Architecture**

### **1. QR Decoder Module**

* Extracts content using ZBar / ZXing.
* Normalizes and classifies it (URL, text, Wi-Fi, file link).

### **2. Content Analysis Module**

* URL analysis (domain, redirects, certificate).
* Text analysis for scripts/encoded payloads.
* File metadata inspection (extension, MIME type).

### **3. Threat Detection**

* Heuristic rules
* Suspicious pattern detection
* Threat-intel lookup (VirusTotal, PhishTank)*
  (*optional based on API availability*)

### **4. ML Classifier (Optional)**

* Predicts malicious/benign probability.
* Features include URL entropy, TLD, age, redirects, path length.

### **5. Scoring Engine**

Produces the **Security Score (0–100)** based on:

```
- URL safety
- Domain reputation
- File risk
- Heuristic indicators
- ML prediction
```

### **6. Reporting Module**

* Clear verdict: Safe / Caution / Suspicious / Dangerous
* Key reasons
* Detailed breakdown

---

## 🛠 **Tech Stack**

### **Frontend**

* React / Next.js
* jsQR / ZXing for scanning

### **Backend**

* Python (FastAPI or Flask)
* QR decoding: pyzbar / qrcode
* Analysis: requests, regex, whois, urllib
* ML: scikit-learn / XGBoost (optional)

### **Database**

* PostgreSQL or SQLite (for logs & scans)

---

## 🔄 **Workflow**

1. User uploads/scans QR
2. Backend decodes QR payload
3. Payload is classified (URL, text, file, Wi-Fi, etc.)
4. Appropriate analyzers run
5. Reputation/blacklist checks
6. Heuristics + ML model detect suspicious behavior
7. Scoring engine calculates safety rating
8. Final report returned to frontend

---

## 📊 **Security Rating System**

```
0–30   → SAFE  
31–60  → CAUTION  
61–85  → SUSPICIOUS  
86–100 → DANGEROUS  
```

Calculated based on:

* Domain issues
* Redirects
* Encoded scripts
* File type risks
* Blacklist lookups
* ML-based threat detection

---

## 🧪 **How to Run**

### **Backend**

```
cd backend
pip install -r requirements.txt
uvicorn app.main:app --reload
```

### **Frontend**

```
cd frontend
npm install
npm start
```

---

## 🚧 **Future Enhancements**

* Real-time scanning mobile app
* Advanced sandbox execution for suspicious URLs
* Browser extension
* Offline QR safety model
* Blockchain-based QR authenticity verification

