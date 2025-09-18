# Sentinel: Multi-Platform Social Sentiment Analyzer

A powerful command-line tool (CLI) built in Python to analyze the correlation between social media hype on **Reddit and Twitter (X)** and market movements for stocks and cryptocurrencies.

## 🚧 Project Status: Active Development

**Current Phase:** Building core data acquisition functionality.
**Next Goal:** Implement the CLI interface using Typer.

## 🛠️ Tech Stack

*   **Language:** Python 3.11+
*   **Data Acquisition:** praw (Reddit API), tweepy (Twitter API v2), yfinance
*   **Data Processing & Analysis:** pandas, numpy, vaderSentiment (NLP)
*   **CLI & UI:** typer, rich
*   **Data Storage:** SQLite (initial), PostgreSQL (planned)
*   **Deployment:** Docker, GitHub Actions (CI/CD)

## 📋 Project Goals

1.  **Core Functionality:** Accept any ticker symbol and output a correlation analysis between Reddit *and* Twitter mention volume/sentiment and price/volume.
2.  **Robustness:** Implement full error handling and logging for reliable operation.
3.  **Depth:** Integrate NLP-based sentiment analysis for both platforms and historical data tracking.
4.  **Professionalism:** Deliver a well-documented, tested, and containerized application.

## 🚀 Installation & Usage

*This section will be filled in as the project develops.*
<!-- Eventually, it will have commands like:
git clone https://github.com/yourusername/sentinel-analysis.git
cd sentinel-analysis
pip install -e .
sentinel analyze GME
-->

## 🔧 Development Setup

1.  **Clone the repo:**
    ```bash
    git clone https://github.com/yourusername/sentinel-analysis.git
    cd sentinel-analysis
    ```
2.  **Create a virtual environment and activate it:**
    ```bash
    python -m venv venv
    # On Windows:
    .\venv\Scripts\activate
    # On macOS/Linux:
    source venv/bin/activate
    ```
3.  **Install development dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Set up Environment Variables:**
    Create a `.env` file in the root directory to securely store your API keys. It should look like this:
    ```
    # Reddit API Credentials (from https://www.reddit.com/prefs/apps)
    REDDIT_CLIENT_ID=your_client_id_here
    REDDIT_CLIENT_SECRET=your_client_secret_here
    REDDIT_USER_AGENT="your_user_agent_here"

    # Twitter API Credentials (from https://developer.twitter.com/)
    TWITTER_BEARER_TOKEN=your_bearer_token_here
    ```
    **Important:** Add `.env` to your `.gitignore` file immediately to avoid committing secrets.

## 🤝 Contributing

This is a personal learning project. Contributions are not expected, but the code is open for exploration under the MIT License.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙋‍♂️ FAQ

**Q: Why are you building this?**
A: To deeply learn Python, data engineering, and data science by building a full end-to-end project that mimics a real-world application.

---
*This README is a living document and will be updated throughout the project's development.*