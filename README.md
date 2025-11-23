 Travel Planner Bot
LLM-powered Travel Planning Application using Streamlit, OpenAI GPT-4o-mini, Cloudflare Tunnel, and Google Colab.

Overview
This project is an intelligent travel-planning assistant that generates complete, personalized itineraries based on user input such as destination, duration, budget, traveler type, and interests.
The system uses a Large Language Model (LLM) to produce structured and detailed travel plans.

Objectives
Build a real-world LLM use case.
Develop an intuitive UI with Streamlit.
Integrate OpenAI’s GPT-4o-mini model through API calls.
Produce readable structured output (Markdown).
Apply responsible AI practices (privacy, citations, no hardcoded keys).

Features
Bilingual interface (Arabic + English)
Day-by-day travel plan
Hotel recommendations
Restaurants & cafés
Budget estimation
Attractions & activities
Travel checklist
Clean UI (Streamlit + custom CSS)

Model & API
Model: GPT-4o-mini
Provider: OpenAI
Input: destination, days, budget, traveler type, interests
Output: structured travel plan (Markdown)
Communication: REST API via Python (OpenAI client)

UI/UX Design
The interface is built in Streamlit and includes:
Language selector
Destination input
Slider for number of days
Dropdown for budget
Traveler type selector
Multi-interest selector
Button to generate the plan
Results container with formatted Markdown output
1)Application Interface
![Interface](Screenshot%202025-11-23%20090946.png)

2)Generated Travel Plan Example
![Output](Screenshot%202025-11-23%20091212.png)

