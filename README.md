import requests
from bs4 import BeautifulSoup

# Function to fetch the top headlines from a news website
def fetch_top_headlines(url):
    try:
        # Send a GET request to the website
        response = requests.get(url)
        response.raise_for_status()  # Raise an exception for HTTP errors

        # Parse the HTML content using BeautifulSoup
        soup = BeautifulSoup(response.text, 'html.parser')

        # Find all headline elements (modify this selector as per the website's structure)
        headlines = soup.find_all('h2', class_='headline')

        # Extract and print the headlines
        top_headlines = [headline.get_text() for headline in headlines]
        return top_headlines

    except requests.exceptions.RequestException as e:
        return f"An error occurred: {e}"

# Example usage
if __name__ == "__main__":
    url = 'https://example-news-site.com'  # Replace with an actual news website
    headlines = fetch_top_headlines(url)
    for idx, headline in enumerate(headlines, 1):
        print(f"{idx}. {headline}")
