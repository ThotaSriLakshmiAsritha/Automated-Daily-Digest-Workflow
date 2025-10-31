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

---


- ## 🧮 4. Data Aggregation & AI Integration

- Each branch is independently formatted by **Google Gemini LLM** for clear, natural outputs.  
- **Weather + AQI** nodes are merged to create a concise **Gmail summary**.  
- Optionally, you can **combine all outputs** (News + Quote + Weather + AQI) into a single WhatsApp message for simplicity.

**💻 Example n8n Function Node Code:**
```javascript
const news = $json.news || '';
const quote = $json.quote || '';
const weather = $json.weather || '';
const aqi = $json.aqi || '';
return [{ json: { combinedMessage: `${news}\n\n${quote}\n\n${weather}\n\n${aqi}` } }];

---

🧾 5. Example Combined Digest
🌤️ Weather — Hyderabad: 30°C, Clear skies ☀️  
🌫️ AQI: 118 (Moderate), Main Pollutant: PM2.5  
💨 Consider indoor exercises today.

---

## ⚙️ 6. Setup Instructions

### 🧱 6.1 Prerequisites

| Service | Credential Type | Purpose |
|----------|-----------------|----------|
| **NewsAPI** | API Key | Fetch news headlines |
| **ZenQuotes** | Open | Fetch quotes |
| **OpenWeatherMap** | API Key | Weather data |
| **IQAir** | API Key | AQI data |
| **Google Gemini** | API Key | AI text formatting |
| **Twilio** | SID + Auth | WhatsApp delivery |
| **Gmail** | OAuth2 | Email delivery |
| **Telegram** | Bot Token | Quote delivery |

---

### 📥 6.2 Workflow Import

1. **Download** the workflow JSON file  
2. **Import** it into [n8n](https://n8n.io)  
3. **Configure** all required credentials (API keys, tokens, OAuth details)  
4. **Update** node parameters such as:  
   - 🌆 City name  
   - 👥 Recipients (WhatsApp numbers, email addresses)  
   - 📧 Sender credentials  

> 💡 **Tip:** After import, run a manual test once to verify each branch before scheduling it for daily automation.

---

## ⚠️ 7. Error Handling

| Node | Failure Type | Handling |
|------|---------------|-----------|
| **API Nodes** | Request fail | Skip the branch and log the error |
| **Gemini LLM** | Output fail | Use a fallback template |
| **Twilio / Gmail** | Delivery fail | Retry sending or log the issue |

> 💡 **Tip:**  
> You can add a “Catch Error” node in n8n to handle failed executions gracefully — for example, to send a short alert message via email or Telegram when an API or delivery node fails.

---

## 🚀 8. Extensibility

You can easily expand this workflow with more smart features and integrations:

- 🗓️ **Add More APIs:** Integrate calendar events, tasks, or stock market data  
- 👋 **Personalized Greetings:** Pull user names or preferences from Google Sheets  
- 💬 **Interactive WhatsApp Replies:** Let users request updates (e.g., “Send me weather”)  
- 🖼️ **Include Media:** Add images, icons, or resource links to enhance readability  
- 📊 **Weekly Summary Reports:** Combine daily logs into end-of-week analytics  

> 💡 **Pro Tip:**  
> Use an **n8n Merge Node** to compile all your branch outputs (News, Quote, Weather, AQI) into one unified message for a single WhatsApp or Gmail summary.





