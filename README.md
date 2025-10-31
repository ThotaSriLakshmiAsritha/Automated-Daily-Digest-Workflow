# 🧠 Productivity Companion — Automated Daily Digest Workflow (WhatsApp & Email)

![n8n](https://img.shields.io/badge/Built%20with-n8n-orange?style=for-the-badge)
![Twilio](https://img.shields.io/badge/Powered%20by-Twilio-green?style=for-the-badge)
![Google Gemini](https://img.shields.io/badge/AI-Google%20Gemini-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Version-1.0-lightgrey?style=for-the-badge)

---

## 📋 Table of Contents
- [Overview](#overview)
- [High-Level Workflow](#high-level-workflow)
- [Nodes & Responsibilities](#nodes--responsibilities)
  - [Trigger Node](#trigger-node)
  - [News Branch](#news-branch)
  - [Quote Branch](#quote-branch)
  - [Weather Branch](#weather-branch)
  - [AQI Branch](#aqi-branch)
- [Data Aggregation & AI Integration](#data-aggregation--ai-integration)
- [Example Combined Digest](#example-combined-digest)
- [Setup Instructions](#setup-instructions)
  - [Prerequisites](#prerequisites)
  - [Workflow Import](#workflow-import)
- [Error Handling](#error-handling)
- [Extensibility](#extensibility)
- [Visuals & Demo](#visuals--demo)
- [Author](#author)

---

## 🧩 Overview
The **Productivity Companion** is an automated workflow that delivers **daily digest updates** via **WhatsApp**, **Gmail**, and optionally **Telegram**.

It gathers data from multiple APIs, processes it using **Google Gemini AI**, and formats the information into short, friendly, and visually appealing messages.

### 🗂️ Data Sources
- 📰 **News:** [NewsAPI.org](https://newsapi.org)
- 💬 **Quotes:** [ZenQuotes.io](https://zenquotes.io)
- ☁️ **Weather:** [OpenWeatherMap](https://openweathermap.org)
- 🌫️ **Air Quality:** [IQAir API](https://www.iqair.com/air-pollution-data-api)

### 🤖 AI Processing
All data is refined through **Google Gemini AI**, ensuring conversational tone, clear formatting, and the right touch of emojis ✨

### 📤 Outputs
- **WhatsApp:** via Twilio Cloud API  
- **Gmail:** structured daily digest  
- **Telegram:** for quotes and short messages  

---

## 🧭 High-Level Workflow
<img width="592" height="322" alt="image" src="https://github.com/user-attachments/assets/03bd8881-b022-48a1-ae19-95b48f50f39e" />


---

## ⚙️ 3. Nodes & Responsibilities

This section outlines each major node and its purpose in the workflow.

---

### 🔘 3.1 Trigger Node
- **Type:** Manual or Scheduled  
- **Function:** Starts all parallel branches  
- **Note:** Easily swapped for daily automation using Cron in n8n  

---

### 🗞️ 3.2 News Branch
- **API:** [NewsAPI.org](https://newsapi.org)  
- **Purpose:** Fetch top 3 daily headlines  

**🧠 Gemini Prompt Example:**  
> Transform the top 3 news stories into a friendly, engaging newsletter snippet with emojis.  
> Include title, description, and 'Read more' link.

**📰 Output Example:**
🗞️ Top News Today!
1️⃣ India’s tech startups hit new milestones 💡
2️⃣ Global climate summit begins 🌍
3️⃣ New study reveals health benefits of tea 🍵


- **Output Nodes:** WhatsApp + Gmail  

---

### 💬 3.3 Quote Branch
- **API:** [ZenQuotes.io](https://zenquotes.io)  
- **Purpose:** Fetch motivational quotes  

**🧠 Gemini Prompt Example:**  
> Enhance this quote with a short reflection and actionable suggestion.

**💡 Output Example:**
💬 “The future depends on what you do today.”
🌟 Take one small step toward your goal!


- **Output Nodes:** WhatsApp + Telegram  

---

### 🌤️ 3.4 Weather Branch
- **API:** [OpenWeatherMap](https://openweathermap.org)  
- **Purpose:** Fetch current weather for user’s location  

**🧠 Gemini Prompt Example:**  
> Convert weather data into a short, friendly daily advisory.

**🌞 Output Example:**
🌤️ Weather in Hyderabad:
30°C, Clear skies ☀️
Perfect morning for a walk or breakfast!


- **Output Nodes:** WhatsApp + Gmail  

---

### 🌫️ 3.5 AQI Branch
- **API:** [IQAir](https://www.iqair.com/air-pollution-data-api) / [OpenWeather AQI](https://openweathermap.org/api/air-pollution)  
- **Purpose:** Fetch AQI levels and main pollutants  

**🧠 Gemini Prompt Example:**  
> Format AQI data into a short health advisory with AQI number, main pollutant, and suggestion.

**🌫️ Output Example:**
🌫️ Air Quality in Hyderabad:
AQI: 118 (Moderate)
Main Pollutant: PM2.5
💨 Consider indoor workout today.

- **Output Nodes:** WhatsApp + Gmail  


