# FutureFeed 🛸

FutureFeed is a futuristic, automated AI news aggregator in Hebrew. It fetches articles from top AI news RSS feeds, analyzes them using OpenAI's GPT-4o model via GitHub Models, translates the titles and summaries to Hebrew, categorizes them, and presents them in a sleek, visually stunning Cyberpunk-style web interface.

## Features ✨

- **Automated Fetching:** Pulls the latest news from sources like TechCrunch, The Verge, and AI News.
- **AI-Powered Curation:** Uses GPT-4o to filter out non-AI-related news and focus strictly on AI advancements.
- **Auto-Translation & Summarization:** Translates titles and provides concise summaries in Hebrew.
- **Smart Categorization:** Automatically groups articles into specific topics:
  - מודלי AI (LLM, VLAM, רובוטיקה ועוד)
  - רגולציה, אבטחה ופרטיות
  - עסקים (מיזוגים, רכישות ועוד)
  - פרויקטים ואלגוריתמים מעניינים
- **Futuristic UI:** A responsive, RTL (Right-to-Left) web page with glowing orbs, glassmorphism, and a neon aesthetic.

## How It Works 🛠️

1. **Backend (`fetch_news.py`):**
   - Parses RSS feeds using `feedparser`.
   - Sends the article title, summary, and link to GPT-4o.
   - The AI responds with a JSON containing the translated title, Hebrew summary, and assigned category.
   - Saves the compiled data to `data/news.json`.

2. **Frontend (`index.html`, `script.js`, `styles.css`):**
   - Fetches the generated `news.json` on page load.
   - Renders the articles dynamically grouped by their respective categories.
   - Displays custom loaders and handles data updates effortlessly.

## Prompts Used in the Project 🤖

FutureFeed relies on AI to analyze and format the news data. Here are the exact prompts used in the backend script to instruct the model:

### System Prompt
```text
You are a professional Hebrew AI news summarizer and translator. You output exact JSON as requested.
```

### User Prompt
```text
Analyze the following news article. 
Determine if it is about Artificial Intelligence. If it's not strongly related to AI, return exactly the string "SKIP".
If it is related to AI, provide a short summary (up to an abstract length) in Hebrew.
Also, classify it into EXACTLY ONE of the following categories:
- מודלי AI (LLM, VLAM, רובוטיקה ועוד)
- רגולציה, אבטחה ופרטיות
- עסקים (מיזוגים, רכישות ועוד)
- פרויקטים ואלגוריתמים מעניינים

Title: {title}
Summary: {summary}
Link: {link}

Return the result STRICTLY as a JSON object with the following keys and no extra markdown formatting:
{
  "category": "One of the exact Hebrew categories listed above",
  "summary": "The Hebrew summary",
  "title_he": "The translated Hebrew title"
}
If not AI related, just return "SKIP" (not JSON).
```

## Running Locally 🚀

### Prerequisites
- Python 3.x
- A GitHub token with access to GitHub Models

### Setup
1. Clone the repository.
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Create a `.env` file in the root directory and add your GitHub API token:
   ```env
   GITHUB_TOKEN=your_personal_access_token
   ```
4. Run the data fetcher script to generate new data:
   ```bash
   python fetch_news.py
   ```
5. Open `index.html` in your web browser, or run a simple local web server:
   ```bash
   python -m http.server 8000
   ```
   Navigate to `http://localhost:8000` to view the news feed.
