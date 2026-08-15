# 🚗 AutoSage --- AI-Powered Vehicle Intelligence & Advisory System

AutoSage is an AI-powered vehicle intelligence application built with
**Python, Streamlit, and Google Gemini 2.5 Flash**. It provides
structured automotive analysis for the Indian automobile market using
**text, images, or text + images**.

The project is designed to reduce the effort of researching vehicles by
generating structured reports covering specifications, performance,
efficiency, pricing, ownership, depreciation/resale, safety,
competitors, and buyer-fit recommendations.

> **Project:** AUTOSAGE APP USING GEMINI FLASH\
> **Team ID:** LTVIP2026TMIDS88090\
> **AI Model:** Gemini 2.5 Flash\
> **Frontend:** Streamlit\
> **Backend:** Python\
> **Image Processing:** Pillow (PIL)

------------------------------------------------------------------------

## ✨ Features

### 1. Smart Query --- Text Analysis

Enter a vehicle name, model, comparison request, or buying/maintenance
question.

Examples:

-   `Honda City 2023`
-   `Suggest the best bike under ₹1 lakh`
-   `Compare Hyundai Creta and Kia Seltos`
-   `Is this car suitable for city driving?`

The application generates a structured automotive intelligence report.

### 2. Smart Vision --- Image Analysis

Upload a vehicle image in:

-   `.jpg`
-   `.jpeg`
-   `.png`

AutoSage uses Gemini's multimodal capability to infer the vehicle from
visible cues such as:

-   Brand/logo
-   Body type
-   Styling
-   Badging
-   Exhaust
-   Charging-port visibility
-   Other visible design characteristics

The application then generates a structured vehicle report.

### 3. Multimodal Analysis --- Image + Prompt

Provide both:

1.  A vehicle image
2.  A vehicle-related question

AutoSage combines both inputs. The project design specifies that when
both are available, the **text is used for primary identification and
the image is used for validation**.

### 4. Sidebar Context Controls

The sidebar allows the user to select:

-   Vehicle Type
    -   Car
    -   Bike
    -   Electric Vehicle
    -   Other
-   Purpose
    -   Buying Decision
    -   Maintenance Tips
    -   Eco-Friendly Search
    -   Other

Click **Apply Changes** to apply the selected context to subsequent
analysis.

### 5. ICE / EV Powertrain Logic

The application attempts to determine whether the vehicle is:

-   Petrol
-   Diesel
-   CNG
-   Hybrid
-   Electric

For multimodal analysis, the project uses text and visual cues such as
exhaust presence, EV badging, and charging-port visibility.

### 6. Structured Automotive Reports

Reports are designed to maintain a consistent format containing sections
such as:

-   Vehicle Identity
-   Engine & Performance
-   Efficiency & Running Cost
-   Key Features
-   Safety & Technology
-   Interior & Practicality
-   Price & Market Position
-   Ownership Experience
-   Depreciation & Resale
-   Buyer Fit
-   Final Expert Verdict

------------------------------------------------------------------------

# 🏗️ Architecture

AutoSage follows a modular layered architecture:

``` text
                    ┌──────────────────────┐
                    │        USER          │
                    │ Vehicle Query/Image   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    STREAMLIT UI      │
                    │                      │
                    │  Smart Query         │
                    │  Smart Vision        │
                    │  Multimodal Analysis │
                    │  Sidebar Controls    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   PYTHON APP LOGIC   │
                    │                      │
                    │ Input Validation     │
                    │ Prompt Engineering   │
                    │ Context Injection    │
                    │ Image Processing     │
                    │ Output Formatting    │
                    └──────────┬───────────┘
                               │
                     Text / Image / Both
                               │
                               ▼
                    ┌──────────────────────┐
                    │ GOOGLE GEMINI 2.5    │
                    │       FLASH          │
                    │                      │
                    │ Text Generation      │
                    │ Vision               │
                    │ Multimodal Reasoning │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ STRUCTURED VEHICLE   │
                    │ INTELLIGENCE REPORT  │
                    └──────────────────────┘
```

The current version uses a real-time inference pipeline and does **not
require a traditional database**.

------------------------------------------------------------------------

# 🛠️ Technology Stack

  Component                   Technology
  --------------------------- ---------------------------------------------
  Frontend                    Streamlit
  Backend/Application Logic   Python
  AI Engine                   Google Gemini 2.5 Flash
  Gemini Integration          `google-generativeai`
  Image Processing            Pillow / PIL
  Environment Management      `python-dotenv`
  Configuration               `.env` locally / Streamlit Secrets in Cloud
  Deployment                  Local Server / Streamlit Community Cloud
  Database                    Not required in current version

------------------------------------------------------------------------

# 📋 Requirements

You need:

-   Python 3.10+ recommended
-   Internet connection
-   A Google Gemini API key
-   Git (optional, but required for the normal GitHub → Streamlit Cloud
    deployment flow)

The application depends on the external Gemini API, so it cannot operate
as a fully offline application.

------------------------------------------------------------------------

# 🚀 Local Installation

## Step 1 --- Clone the repository

``` bash
git clone https://github.com/M-Sudheer18/autosage-intelligence.git
cd autosage-intelligence
```

If you already have the project folder, simply open a terminal inside
that folder.

------------------------------------------------------------------------

## Step 2 --- Create a virtual environment

### Windows

``` bash
python -m venv venv
venv\Scripts\activate
```

### macOS / Linux

``` bash
python3 -m venv venv
source venv/bin/activate
```

------------------------------------------------------------------------

## Step 3 --- Install dependencies

Create a `requirements.txt` file if your repository does not already
contain one:

``` txt
streamlit
google-generativeai
Pillow
python-dotenv
pandas
```

Then install:

``` bash
pip install -r requirements.txt
```

Or install directly:

``` bash
pip install streamlit google-generativeai Pillow python-dotenv pandas
```

------------------------------------------------------------------------

# 🔑 Gemini API Key Configuration

AutoSage requires a Gemini API key.

The existing project source loads the key using:

``` python
from dotenv import load_dotenv
import os

load_dotenv()

api = os.getenv("GOOGLE_API_KEY")
```

The Gemini client is then configured with:

``` python
import google.generativeai as genai

genai.configure(api_key=api)
```

The project uses:

``` python
model = genai.GenerativeModel(
    model_name="models/gemini-2.5-flash",
    generation_config={
        "temperature": 0.3,
        "max_output_tokens": 4096
    }
)
```

------------------------------------------------------------------------

## Step 4 --- Create `.env`

Create a file named:

``` text
.env
```

in the project root.

Add:

``` env
GOOGLE_API_KEY=YOUR_GEMINI_API_KEY
```

Example:

``` env
GOOGLE_API_KEY=AIzaSyXXXXXXXXXXXXXXXXXXXXXXXX
```

Do **not** publish your real API key.

------------------------------------------------------------------------

# 🔒 Add `.gitignore`

Create a `.gitignore` file:

``` gitignore
.env
venv/
__pycache__/
*.pyc
.streamlit/secrets.toml
```

Never commit your `.env` file or API key to GitHub.

------------------------------------------------------------------------

# 📁 Recommended Project Structure

A clean repository can use:

``` text
autosage-intelligence/
│
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
├── .env
│
└── .streamlit/
    └── secrets.toml
```

The project documentation describes a modular architecture separating
the UI, application/prompt logic, AI processing, and configuration
layers. The exact physical source-file structure is not mandated by the
project documents, so the structure above is a recommended repository
organization.

------------------------------------------------------------------------

# ▶️ Run AutoSage Locally

If the Streamlit entry file is `app.py`:

``` bash
streamlit run app.py
```

You should see a local address similar to:

``` text
http://localhost:8501
```

Open that address in your browser.

If your entry file has a different name, replace `app.py`:

``` bash
streamlit run your_file_name.py
```

------------------------------------------------------------------------

# 🧪 How to Use the Application

## Step 1 --- Configure the Sidebar

Select:

``` text
Vehicle Type → Car / Bike / Electric Vehicle / Other
```

Then select:

``` text
Purpose → Buying Decision / Maintenance Tips / Eco-Friendly Search / Other
```

Click:

``` text
Apply Changes
```

------------------------------------------------------------------------

## Step 2 --- Smart Query

Open:

``` text
Smart Query
```

Enter a vehicle query.

Example:

``` text
Suggest the best bike under ₹1 lakh
```

Click:

``` text
Smart Suggest
```

The application sends the structured prompt to Gemini and displays the
generated report.

### Buying Decision

The prompt emphasizes:

-   Pricing
-   Competitors
-   Resale
-   Value score

### Maintenance Tips

The prompt emphasizes:

-   Reliability
-   Service cost
-   Ownership risk

### Eco-Friendly Search

The prompt emphasizes:

-   Efficiency
-   Emissions
-   Cost per km
-   EV alternatives

------------------------------------------------------------------------

# 🖼️ Step 3 --- Smart Vision

Open:

``` text
Smart Vision
```

Upload:

``` text
.jpg
.jpeg
.png
```

Then click:

``` text
Unlock Insights
```

The image is converted into bytes and sent to Gemini together with the
visual-analysis prompt.

The application generates a structured visual vehicle analysis.

If no image is uploaded, the application displays a warning instead of
making the API request.

------------------------------------------------------------------------

# 🔀 Step 4 --- Multimodal Analysis

Open:

``` text
Multimodal Analysis
```

Upload a vehicle image.

Then enter a question such as:

``` text
Is this vehicle suitable for long-distance family travel?
```

Click:

``` text
Execute Analysis
```

The application sends:

``` text
Structured Prompt + Image
```

to Gemini.

The multimodal logic prioritizes:

``` text
Text → Primary identification
Image → Visual validation
```

and also applies powertrain determination logic.

------------------------------------------------------------------------

# 🔌 How Gemini Integration Works

The integration has three main parts.

## 1. Text Request

``` python
response = model.generate_content(prompt)
```

The returned text is displayed using:

``` python
st.markdown(response.text)
```

------------------------------------------------------------------------

## 2. Image Preparation

Uploaded files are converted into Gemini-compatible byte data:

``` python
def input_image_setup(uploaded_file):
    if uploaded_file is not None:
        bytes_data = uploaded_file.getvalue()

        return [{
            "mime_type": uploaded_file.type,
            "data": bytes_data
        }]

    return None
```

------------------------------------------------------------------------

## 3. Multimodal Request

The application combines the prompt and image:

``` python
input_image_data = input_image_setup(uploaded_image)

response = model.generate_content(
    [final_prompt, *input_image_data]
)
```

This enables Gemini to perform image + text reasoning.

------------------------------------------------------------------------

# ☁️ Deploy on Streamlit Community Cloud

The project is designed to support Streamlit Cloud deployment.

## Step 1 --- Push the project to GitHub

If Git is not initialized:

``` bash
git init
git add .
git commit -m "Initial AutoSage project"
```

Connect your GitHub repository:

``` bash
git remote add origin https://github.com/M-Sudheer18/autosage-intelligence.git
git branch -M main
git push -u origin main
```

If the repository is already connected:

``` bash
git add .
git commit -m "Update AutoSage"
git push
```

------------------------------------------------------------------------

## Step 2 --- Open Streamlit Community Cloud

Go to:

``` text
https://share.streamlit.io/
```

Sign in/connect your GitHub account.

Choose:

``` text
Create app
```

Then select:

``` text
Repository: M-Sudheer18/autosage-intelligence
Branch: main
Main file: app.py
```

If your actual entry file has another name, select that file instead.

------------------------------------------------------------------------

## Step 3 --- Configure the API Secret

Do **not** upload `.env` to GitHub.

In Streamlit Community Cloud, open the app's advanced settings/secrets
configuration and add:

``` toml
GOOGLE_API_KEY = "YOUR_GEMINI_API_KEY"
```

Save the secret and deploy/reboot the application if required.

------------------------------------------------------------------------

# ⚠️ Important Cloud Configuration

The original project source reads:

``` python
os.getenv("GOOGLE_API_KEY")
```

For a more robust Streamlit Cloud configuration, use this pattern:

``` python
import os
import streamlit as st
from dotenv import load_dotenv

load_dotenv()

api = os.getenv("GOOGLE_API_KEY")

if not api and "GOOGLE_API_KEY" in st.secrets:
    api = st.secrets["GOOGLE_API_KEY"]

if not api:
    st.error("GOOGLE_API_KEY is not configured.")
    st.stop()
```

Then:

``` python
import google.generativeai as genai

genai.configure(api_key=api)
```

This allows the same application to work with:

``` text
Local → .env
Streamlit Cloud → st.secrets
```

------------------------------------------------------------------------

# 📦 Streamlit Cloud Dependencies

Make sure `requirements.txt` is committed to the repository:

``` txt
streamlit
google-generativeai
Pillow
python-dotenv
pandas
```

The dependency file should be in the repository root or alongside the
Streamlit entrypoint.

------------------------------------------------------------------------

# 🔐 Security

Never do this:

``` python
api = "AIzaSyXXXXXXXXXXXX"
```

Never commit:

``` text
.env
.streamlit/secrets.toml
```

Use:

``` text
Local:
.env

Streamlit Cloud:
Secrets
```

If an API key is accidentally committed to GitHub, revoke/rotate the key
and replace it with a new one.

------------------------------------------------------------------------

# 🧪 Functional Testing

The project testing documentation covers the following major scenarios:

  -----------------------------------------------------------------------
  Test                                Expected Behavior
  ----------------------------------- -----------------------------------
  Text input validation               Valid queries accepted;
                                      invalid/empty input produces a
                                      warning

  Sidebar validation                  Selected vehicle type and purpose
                                      affect generated output

  Text report generation              Structured report is generated

  Image validation                    JPG/PNG accepted; unsupported
                                      formats rejected

  Image analysis                      Vehicle report generated from
                                      visual input

  Multimodal analysis                 Image + text produce a combined
                                      report

  Powertrain detection                ICE/EV/fuel type is identified
                                      logically

  Gemini API connection               Analysis request completes without
                                      connection failure
  -----------------------------------------------------------------------

The performance plan targets approximately:

-   Text report: **≤ 5 seconds average**
-   Multimodal report: **≤ 8 seconds average**
-   Load testing target: **10--20 concurrent requests**
-   Large image testing: approximately **2--5 MB**

Actual latency depends on network conditions and Gemini API response
time.

------------------------------------------------------------------------

# 🛠️ Troubleshooting

## 1. `GOOGLE_API_KEY` is missing

Error cause:

``` text
GOOGLE_API_KEY is not configured
```

Fix:

### Local

Check `.env`:

``` env
GOOGLE_API_KEY=YOUR_GEMINI_API_KEY
```

Restart Streamlit:

``` bash
streamlit run app.py
```

### Streamlit Cloud

Add:

``` toml
GOOGLE_API_KEY = "YOUR_GEMINI_API_KEY"
```

to the app's Secrets settings.

------------------------------------------------------------------------

## 2. `ModuleNotFoundError`

Example:

``` text
ModuleNotFoundError: No module named 'streamlit'
```

Install dependencies:

``` bash
pip install -r requirements.txt
```

Or install the missing package directly.

------------------------------------------------------------------------

## 3. Image upload fails

Check that the uploaded file is:

``` text
.jpg
.jpeg
.png
```

The application intentionally limits the supported image formats.

------------------------------------------------------------------------

## 4. Gemini API error

Check:

1.  API key is valid.
2.  Internet connection is available.
3.  Gemini API access is enabled for the key/project.
4.  The configured model is available.
5.  You have not exceeded your API quota/rate limit.

The project documentation identifies external API dependency and rate
limits as important limitations.

------------------------------------------------------------------------

## 5. Streamlit Cloud build fails

Check:

``` text
requirements.txt
```

Make sure it contains all imported third-party packages.

For this project:

``` txt
streamlit
google-generativeai
Pillow
python-dotenv
pandas
```

Then commit and push:

``` bash
git add requirements.txt
git commit -m "Fix dependencies"
git push
```

Streamlit Community Cloud will rebuild the application after dependency
changes.

------------------------------------------------------------------------

# 📊 Current Project Scope

## Included

-   Smart Query
-   Smart Vision
-   Multimodal Analysis
-   Structured intelligence reports
-   Indian automobile market context
-   Vehicle type and purpose controls
-   ICE/EV powertrain reasoning
-   Gemini Flash integration
-   Input validation
-   Error handling
-   Streamlit deployment support

## Not Included in the Current Version

-   User authentication
-   Persistent database
-   Payment integration
-   External live pricing APIs
-   Real-time dealership inventory
-   Mobile application deployment
-   Direct OEM database integration

------------------------------------------------------------------------

# ⚠️ Limitations

AutoSage depends on an external Gemini API and therefore requires
internet connectivity.

AI-generated vehicle information can contain estimates, especially when
exact variant-level information is unavailable.

Image identification depends on image quality and visible vehicle cues.

Pricing is market-estimated rather than connected to live dealership
inventory.

EV charging cost can vary by location and electricity tariff.

Large prompts and high-resolution images can increase processing time.

The application should therefore be treated as an **AI-assisted
automotive advisory/research tool**, not as a substitute for official
manufacturer specifications, dealership quotations, inspection reports,
or professional automotive advice.

------------------------------------------------------------------------

# 🔮 Future Enhancements

The project documentation identifies several possible future extensions:

-   Fine-tuned automotive domain models
-   Live camera vehicle recognition
-   Predictive resale forecasting
-   Multi-vehicle comparison engine
-   Official automotive API integration
-   Dealership inventory integration
-   Insurance/loan estimation
-   Fuel and electricity price integration
-   User profiles
-   Budget-based filtering
-   Maintenance reminders
-   Dealership/enterprise APIs
-   Android/iOS applications
-   Regional Indian language support

------------------------------------------------------------------------

# 📚 Project Documentation

The project documentation covers:

-   Problem Statement
-   Problem--Solution Fit
-   Proposed Solution
-   Functional & Non-Functional Requirements
-   Technology Stack
-   Solution Architecture
-   Data Flow Diagram
-   Project Planning
-   Product Backlog
-   Sprint Planning
-   Model Performance Testing
-   UAT Execution
-   Final Project Report

------------------------------------------------------------------------

# 👨‍💻 Developer

**Sudheer Muthyala**

GitHub:

``` text
https://github.com/M-Sudheer18
```

Project Repository:

``` text
https://github.com/M-Sudheer18/autosage-intelligence
```

------------------------------------------------------------------------

# 📄 License

Add the project's chosen license here if the repository is intended for
public redistribution.

------------------------------------------------------------------------

## Quick Start

For experienced users:

``` bash
git clone https://github.com/M-Sudheer18/autosage-intelligence.git
cd autosage-intelligence

python -m venv venv
venv\Scripts\activate

pip install -r requirements.txt
```

Create `.env`:

``` env
GOOGLE_API_KEY=YOUR_GEMINI_API_KEY
```

Run:

``` bash
streamlit run app.py
```

Then open:

``` text
http://localhost:8501
```

For Streamlit Community Cloud:

``` text
GitHub Repository
      ↓
requirements.txt
      ↓
Create App
      ↓
Select app.py
      ↓
Add GOOGLE_API_KEY in Secrets
      ↓
Deploy
      ↓
Share the streamlit.app URL
```

------------------------------------------------------------------------

## 🔗 Official Deployment Reference

For the current Streamlit Community Cloud workflow, see the official
Streamlit documentation:

-   Deploy an app:
    https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/deploy
-   App dependencies:
    https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/app-dependencies
-   Secrets management:
    https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/secrets-management
