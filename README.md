# Automated-Daily-Digest-Workflow
Title:  Productivity Companion — Automated Daily Digest Workflow (WhatsApp & Email) 
________________________________________
Table of Contents
1.	Overview
2.	High-Level Workflow
3.	Nodes & Responsibilities
o	Trigger Node
o	News Branch
o	Quote Branch
o	Weather Branch
o	AQI Branch
4.	Data Aggregation & AI Integration
5.	Example Combined Digest
6.	Setup Instructions
o	Prerequisites
o	Workflow Import
7.	Error Handling
8.	Extensibility
9.	Visuals & Demo
10.	Author
________________________________________
1. Overview
The Productivity Companion is an automated workflow delivering daily digest updates to users via WhatsApp, Gmail, and optionally Telegram. The system gathers data from multiple APIs, processes it through Google Gemini AI for friendly formatting, and sends structured, engaging updates.
Data Sources
•	News headlines: NewsAPI.org
•	Motivational quotes: ZenQuotes.io
•	Weather & AQI: OpenWeatherMap + IQAir API
AI Processing
Google Gemini ensures messages are concise, friendly, and readable, using emojis and clear formatting.
Outputs
•	WhatsApp (Twilio Cloud API)
•	Gmail
•	Telegram ( for quotes)
________________________________________
2. High-Level Workflow
           ┌───────────────────────┐
           │ Trigger (Manual/Auto) │
           └───────────┬───────────┘
                       │
    ┌──────────────┬───────────────┬───────────────┐
    │              │               │               │
    ▼              ▼               ▼               ▼
News API       Quote API       Weather API       AQI API
    │              │               │               │
    ▼              ▼               ▼               ▼
Gemini AI      Gemini AI       Gemini AI       Gemini AI
    │              │               │               │
    ▼              ▼               ▼               ▼
Twilio +        Telegram+       Twilio +         Twilio +
Gmail           Twilio               Combined Gmail
________________________________________
3. Nodes & Responsibilities
3.1 Trigger Node
•	Type: Manual or Scheduled
•	Starts all parallel branches.
•	Easily swapped for daily automation.
3.2 News Branch
•	API: NewsAPI.org
•	Purpose: Fetch top 3 headlines
•	Gemini Prompt Example:
Transform the top 3 news stories into a friendly, engaging newsletter snippet with emojis.
Include title, description, and 'Read more' link.
•	Output Example:
🗞️ *Top News Today!*
1️⃣ India’s tech startups hit new milestones 💡
2️⃣ Global climate summit begins 🌍
3️⃣ New study reveals health benefits of tea 🍵
•	Output Nodes: WhatsApp + Gmail
3.3 Quote Branch
•	API: ZenQuotes.io
•	Purpose: Fetch motivational quotes
•	Gemini Prompt Example:
Enhance this quote with a short reflection and actionable suggestion.
•	Output Example:
💬 “The future depends on what you do today.”
🌟 Take one small step toward your goal!
•	Output Nodes: WhatsApp + Telegram
3.4 Weather Branch
•	API: OpenWeatherMap
•	Purpose: Fetch current weather
•	Gemini Prompt Example:
Convert weather data into a short friendly daily advisory.
•	Output Example:
🌤️ *Weather in Hyderabad:*
30°C, Clear skies ☀️
Perfect morning for a walk or breakfast!
•	Output Nodes: WhatsApp + Gmail
3.5 AQI Branch
•	API: IQAir / OpenWeather AQI
•	Purpose: Fetch AQI and main pollutants
•	Gemini Prompt Example:
Format AQI data into a short health advisory with AQI number, main pollutant, and suggestion.
•	Output Example:
🌫️ *Air Quality in Hyderabad:*
AQI: 118 (Moderate)
Main Pollutant: PM2.5
💨 Consider indoor workout today.
•	Output Nodes: WhatsApp + Gmail
________________________________________
4. Data Aggregation & AI Integration
•	Branches independently formatted by Gemini LLM.
•	Weather + AQI nodes merged for Gmail summary.
•	Optional: Combine all outputs into a single WhatsApp message.
Example n8n Function Node Code:
const news = $json.news || '';
const quote = $json.quote || '';
const weather = $json.weather || '';
const aqi = $json.aqi || '';
return [{ json: { combinedMessage: `${news}\n\n${quote}\n\n${weather}\n\n${aqi}` } }];
________________________________________
5. Example Combined Digest

🌤️ Weather — Hyderabad: 30°C, Clear skies ☀️
🌫️ AQI: 118 (Moderate), Main Pollutant: PM2.5
💨 Consider indoor exercises today.
________________________________________
6. Setup Instructions
6.1 Prerequisites
Service	Credential Type	Purpose
NewsAPI	API Key	Fetch news headlines
ZenQuotes	Open	Fetch quotes
OpenWeatherMap	API Key	Weather data
IQAir	API Key	AQI data
Google Gemini	API Key	AI text formatting
Twilio	SID + Auth	WhatsApp delivery
Gmail	OAuth2	Email delivery
Telegram	Bot Token	Quote delivery
6.2 Workflow Import
1.	Download workflow JSON
2.	Import into n8n
3.	Configure credentials
4.	Update node parameters (city, recipients, email addresses)
________________________________________
7. Error Handling
Node	Failure Type	Handling
API Nodes	Request fail	Skip branch, log error
Gemini LLM	Output fail	Fallback template
Twilio / Gmail	Delivery fail	Retry or log
________________________________________
8. Extensibility
•	Add more APIs (calendar, tasks, stocks)
•	Personalized greetings via Google Sheets
•	Interactive WhatsApp replies
•	Include images or links
•	Weekly summary reports
________________________________________
<img width="1368" height="619" alt="Screenshot 2025-10-31 202155" src="https://github.com/user-attachments/assets/bf7df9f6-1460-4937-b974-4ce8f244fb2a" />

________________________________________
10. Author
T.S.L. Asritha Built with n8n, Twilio, Google Gemini, OpenWeather, IQAir, NewsAPI 📅 Project Year: 2025
