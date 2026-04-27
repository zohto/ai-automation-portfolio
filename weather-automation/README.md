# Automation of Weather-Based Sales and Staffing Decisions

A scheduled automation (TripleTen AI Automation, Project 5) that retrieves daily weather data and generates business-ready operational guidance — product focus, staffing recommendation, and two promotional messages — delivered by email each morning before opening.

The workflow runs on a daily 7:00 AM schedule, pulls forecast data from the OpenWeather API (Postman-validated), passes it through a Gemini AI prompt with kiosk context, and emails the structured output to the manager. A severe-weather conditional path (>91°F or rain/storms) routes to a dedicated alert email for rapid operational adjustments.

**Stack:** Zapier (daily 7 AM schedule) · OpenWeather API · Gemini AI · Gmail
**Document:** [Weather Automation - Brandon Robinson.pdf](./Weather%20Automation%20-%20Brandon%20Robinson.pdf)
