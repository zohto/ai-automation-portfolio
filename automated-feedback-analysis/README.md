# Automated Feedback Analysis Workflow

A built-and-tested feedback analysis pipeline (TripleTen AI Automation, Project 3) for a small e-commerce scenario. Customer feedback flows from Google Forms into a Make automation that calls Gemini AI for sentiment classification and structured summarization, stores the result in Google Sheets, and triggers an email alert to the Customer Success team when sentiment is negative.

Live test data in the deck: 6 submissions processed end-to-end (2 positive, 2 neutral, 2 negative). Negative entries triggered alerts as designed; structured JSON output from Gemini made downstream parsing consistent.

**Stack:** Google Forms · Make · Gemini AI · Google Sheets · Gmail
**Document:** [Automated Feedback Analysis Workflow.pdf](./Automated%20Feedback%20Analysis%20Workflow.pdf)
