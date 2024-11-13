# Email Extractor Tool

A Python tool that extracts emails from websites, designed to be run on Google Colab. This tool fetches page content and uses Regular Expressions to find and display email addresses on each URL entered.

---

## 🌟 Features
- **Easy to Use**: Run it directly in Google Colab without local installation.
- **Fast and Efficient**: Extracts all unique emails from multiple websites.
- **Portable**: Just copy and paste URLs, and the tool does the rest.

---

## 🚀 Getting Started

### Requirements
- [Google Colab](https://colab.research.google.com/)

### Installation
No installation needed. Just open in Google Colab and run the cells.

### Usage
1. **Open Google Colab**.
2. **Copy the code** below into a new Colab cell:
   
```python
# Import necessary libraries
!pip install requests beautifulsoup4

# Importing libraries
import requests
import re
from bs4 import BeautifulSoup

# Function to extract emails from a single URL
def extract_emails_from_url(url):
    try:
        response = requests.get(url)
        response.raise_for_status()
        soup = BeautifulSoup(response.text, 'html.parser')
        text = soup.get_text()
        email_pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'
        emails = re.findall(email_pattern, text)
        return list(set(emails))
    except requests.exceptions.RequestException as e:
        print(f"Error accessing {url}: {e}")
        return []

# Function to extract emails from multiple URLs
def extract_emails_from_urls(urls):
    all_emails = {}
    for url in urls:
        emails = extract_emails_from_url(url)
        all_emails[url] = emails
        print(f"Emails found in {url}: {emails}")
    return all_emails

# Example usage
urls = ["https://treeservicesmodesto.org", "https://example.com"]
all_emails = extract_emails_from_urls(urls)
