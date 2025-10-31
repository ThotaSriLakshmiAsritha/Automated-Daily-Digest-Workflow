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

