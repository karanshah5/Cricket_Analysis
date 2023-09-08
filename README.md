<h1 align="center">ICC T20 World Cup 2022 Analysis</h1>

## Problem Statement
The ICC T20 World Cup 2022 Analysis project is dedicated to assembling the ultimate team of 11 players from all participating teams based on specific criteria and statistics. This team selection process aims to optimize overall team performance, creating a combined 11 that represents the best talent from the tournament.

Additionally, this project seeks to analyze data from the ICC T20 World Cup 2022, providing valuable insights for cricket enthusiasts and data analysts. This project is a personal endeavor and is currently in progress, with the goal of comprehensive analysis of the matches, players, and teams in the ICC T20 World Cup 2022.

## Data Source
[ICC T20 World Cup 2022 data](https://stats.espncricinfo.com/ci/engine/records/team/match_results.html?id=14450;type=tournament)

## Libraries Used
I have provided a `requirements.txt` file to simplify the setup process on your machine.

## Description
This project involves web scraping ICC T20 World Cup 2022 data from various sources, preprocessing the data, and performing exploratory data analysis (EDA) to uncover patterns and trends in the tournament. The analysis will cover aspects such as match results, player statistics, team performance, and more, all specifically related to the ICC T20 World Cup 2022.

## Data Description
The data collected for this project includes:

### 1. Match Results
<p align="center">
  <img src="https://github.com/karanshah5/Cricket_Analysis/blob/main/csv_data_snippets/match_results.png", title="Hello"/>
</p>

- ICC T20 World Cup 2022 match results, including  participating teams, match outcomes, margins of victory, match venues, match dates, and unique match IDs, are scraped and stored in a structured format.

The scraping process for match results involves using the following libraries and modules:

- `requests`: The `requests` library is used to make HTTP requests to a specific URL containing match results data. It allows the code to fetch the web page's content.

- `pandas`: The `pandas` library is used for data manipulation and analysis. In this case, it is used to create and manage a DataFrame to store the extracted match results data in a tabular format.

- `BeautifulSoup` from `bs4`: BeautifulSoup is a Python library used for web scraping. It is specifically used here to parse the HTML content of the web page containing match results data. It allows the code to navigate and extract relevant information from the HTML structure.

The extracted match results data is then organized and stored in CSV files for further analysis and reference.

### 2. Scorecard Links
- The next step in the project involves grabbing all the links to the scorecards of all the matches from a specific URL. These scorecard links will be used to fetch detailed statistics for each match.

The code for extracting scorecard links uses the following libraries and imports:

- `import requests`: This import allows the code to make HTTP requests to fetch the web page containing scorecard links. It is used to retrieve the web page's content.

- `re`: The `re` module is used for regular expressions. Specifically, it is employed to define a regular expression pattern to match links containing '/series.'

- `from bs4 import BeautifulSoup`: This import brings in the `BeautifulSoup` module from the `bs4` library. BeautifulSoup is used for parsing the HTML content of the web page containing scorecard links. It enables the code to navigate and extract relevant information from the HTML structure.

- `from urllib.parse import urljoin`: This import is used to join relative URLs with the base URL to create absolute URLs for the scorecard links. It ensures that the links are complete and can be used to access the scorecard pages.

### 3. `batting_data` Function

<p align="center">
  <img src="https://github.com/karanshah5/Cricket_Analysis/blob/main/csv_data_snippets/batting.png", title="Hello"/>
</p>

The `batting_data` function is responsible for extracting batting data from a given URL, which typically points to a specific match's scorecard. Here's an overview of how it works:

1. It makes an HTTP request to the provided URL and fetches the HTML content of the page.

2. BeautifulSoup is used to parse the HTML content, making it easier to navigate and extract information.

3. A regular expression pattern is employed to find team innings information within the HTML content.

4. If the necessary pattern is found, it extracts information about the teams playing in the match.

5. It then searches for batting tables within the HTML using BeautifulSoup.

6. A nested function, `extract_innings_data`, is defined to extract batting data from a single innings of a team. This includes details like the batsman's name, dismissal, runs scored, balls faced, boundaries, and strike rate.

7. The function iterates through both teams, extracting batting data for each team separately.

8. The extracted data is structured into a pandas DataFrame for further analysis.

9. The resulting DataFrames for both teams are concatenated, and the final result contains comprehensive batting data for the match.

10. The `batting_data` function is then called for each scorecard URL in the `all_links` list, and the results are appended to the `final_result` DataFrame

11. After extracting the data, additional transformations are performed on the DataFrame:
    - A new column 'out/not_out' is added to categorize whether a batsman was 'out' or 'not out' based on the 'dismissal' column.
    - The 'dismissal' column is dropped from the DataFrame.
    - Special characters (e.g., '†') are removed from batsmen's names.
    - Match IDs are assigned to each row based on a dictionary that maps match descriptions to Match IDs.
    - This mapping is crucial for further analysis, as it enables the alignment of batting statistics with specific matches. With this 'Match ID' column, you can easily filter and analyze bowling data for individual matches or calculate overall tournament statistics.

This process ensures that the batting data is structured and enriched with relevant information, making it suitable for further analysis and team selection.

### 4. `extract_bowling_data` Function

<p align="center">
  <img src="https://github.com/karanshah5/Cricket_Analysis/blob/main/csv_data_snippets/bowling.png", title="Hello"/>
</p>

The `extract_bowling_data` function is responsible for extracting bowling data from a given URL, which typically points to a specific match's scorecard. Here's an overview of how it works:

1. It makes an HTTP request to the provided URL and fetches the HTML content of the page.

2. BeautifulSoup is used to parse the HTML content, making it easier to navigate and extract information.

3. A regular expression pattern is employed to find team innings information within the HTML content.

4. If the necessary pattern is found, it extracts information about the teams playing in the match.

5. It then searches for bowling tables within the HTML. These tables are identified by checking if any table header ('th') contains the text 'BOWLING.'

6. A nested function, `extract_innings_data`, is defined to extract bowling data from a single innings of a team. This includes details such as the bowler's name, overs bowled, maidens, runs conceded, wickets taken, economy rate, wides, no-balls, and more.

7. The function iterates through both teams, extracting bowling data for each team separately.

8. The extracted data is structured into a pandas DataFrame for further analysis.

9. The resulting DataFrames for both teams are concatenated, and the final result contains comprehensive bowling data for the match.

10. The `extract_bowling_data` function is then called for each scorecard URL in the `all_links` list, and the results are appended to the `final_result1` DataFrame.

11. After extracting the data, additional transformations are performed on the DataFrame:
    - Match IDs are assigned to each row based on a dictionary that maps match descriptions to Match IDs.
    - This mapping is crucial for further analysis, as it enables the alignment of bowling statistics with specific matches. With this 'Match ID' column, you can easily filter and analyze bowling data for individual matches or calculate overall tournament statistics.

This process ensures that the bowling data is structured and enriched with relevant information, making it suitable for further analysis and team selection.

### 5. Player Details Extraction

<p align="center">
  <img src="https://github.com/karanshah5/Cricket_Analysis/blob/main/csv_data_snippets/players.png", title="Hello"/>
</p>

The extraction of player details is a crucial step in the ICC T20 World Cup 2022 Analysis project, as it provides comprehensive information about each player participating in the tournament. This information includes player names, team affiliations, batting styles, bowling styles, playing roles, descriptions, and even images. Here's an overview of how player details are extracted:

### Retrieving HTML Pages
To begin, the code retrieves the HTML content of multiple web pages containing player information. These web pages are accessed through unique links obtained from match scorecards. The key steps include:

- Making HTTP requests to each link to fetch the HTML content.
- Storing the HTML content of each page in a list for further processing.
- Combining the HTML content of all pages into a single string for easier parsing.

### Extracting Player Profiles
The player profiles are identified within the combined HTML content, and the code uses BeautifulSoup to extract relevant information. Specifically, it searches for 'div' elements with the class 'ds-p-0,' which typically contain player profiles. The following player details are extracted:

- **Team names**: The team name of each player is extracted.
- **Player names**: The names of the players are extracted.

The extraction of player details involves parsing the HTML content of player profiles to obtain valuable information about each player's **playing style and role**. This step is crucial for understanding the characteristics of players participating in the ICC T20 World Cup 2022. Here's how player details are extracted and structured:

- **HTML Parsing**: The code first identifies the player details section within the HTML content of each player's profile. It searches for 'div' elements with the class 'ds-grid-cols-2' to locate this section.

- **Detail Categories**: The code defines three categories of player details to extract: 'Batting Style,' 'Bowling Style,' and 'Playing Role.' These categories represent essential attributes that define a player's role in cricket.

- **Iterating Through Details**: For each player, the code creates a temporary BeautifulSoup object to parse the HTML structure within the 'div' element. It then finds all 'p' elements within this temporary object.

- **Extracting Details**: The code iterates through the 'p' elements to find and extract the following details:
    - **Batting Style**: The player's preferred batting style, such as right-handed or left-handed.
    - **Bowling Style**: The player's primary bowling style, such as right-arm medium or left-arm spin.
    - **Playing Role**: The role the player typically performs in cricket matches, such as opening batsman or fast bowler.

- **Structured Data**: The extracted details are stored in separate lists for each category ('Batting Style,' 'Bowling Style,' 'Playing Role'). These lists are used to create a structured DataFrame containing player attributes.

- **DataFrame Creation**: The extracted details are organized into a DataFrame, where each row represents a player, and the columns include 'Batting Style,' 'Bowling Style,' and 'Playing Role.' This structured data format facilitates further analysis and visualization of player attributes.

### Extracting Player Descriptions
The extraction of player descriptions involves gathering textual information from player profiles to provide additional context and insights about each player. This textual data can include personal details, career highlights, and other relevant information. Here's how player descriptions are extracted and processed:

- **List Initialization**: An empty list named 'all_descriptions' is initialized to store the descriptions of each player. This list will be populated with textual data from player profiles.

- **Iterating Through HTML Pages**: The code iterates through each HTML page containing player profiles. For each page, it performs the following steps:

    - **HTML Parsing**: It creates a BeautifulSoup object to parse the HTML structure of the current player's profile page.

    - **Finding Description Elements**: The code searches for 'div' elements with the class 'ci-player-bio-content.' These elements typically contain textual information about the player.

    - **List Initialization**: An empty list named 'descriptions' is initialized to store descriptions specific to the current player profile.

    - **Populating Descriptions**: For each 'ci-player-bio-content' element found, the code extracts the text content (description_text) and adds it to the 'descriptions' list. Empty or missing descriptions are represented as 'None' in the list.

    - **Appending to Overall List**: After processing all 'ci-player-bio-content' elements on the page, the 'descriptions' list for that page is appended to the 'all_descriptions' list, which accumulates descriptions for all players.

- **Adding 'Description' Column**: The collected descriptions are added to the existing DataFrame as a new column named 'Description.'

- **Data Cleaning**: To ensure consistency and readability, the 'Description' column is converted to a string data type. Additionally, a custom function is applied to each description to remove any square brackets, double quotes, and single quotes, enhancing the cleanliness and uniformity of the text data.

This process enables the inclusion of textual player descriptions in the dataset, providing valuable insights and context about each player's background and career in the ICC T20 World Cup 2022 Analysis project.

### Structuring Player Details
The extracted player details are organized into a DataFrame for further analysis. The following details are included in the DataFrame:

- Name: Player names.
- Team: Team affiliations.
- Batting Style: The player's batting style (e.g., right-handed, left-handed).
- Bowling Style: The player's bowling style (e.g., right-arm medium, left-arm spin).
- Playing Role: The role the player typically plays in matches (e.g., opening batsman, fast bowler).
- Description: Additional textual information about the player.

### Cleaning and Enhancing Data
To ensure data quality and consistency, the following data cleaning and enhancements are applied:

- Removing square brackets and quotes from descriptions.
- Handling missing values in the 'Bowling Style' column.

### Retrieving Player Images with Selenium and Requests
The retrieval of player images involves collecting image URLs associated with each player in the dataset. These images can provide visual context and recognition for each player in the ICC T20 World Cup 2022. Here's how player images are retrieved and processed using the Selenium and Requests libraries:

- **Initialization of Lists**: Before proceeding, two empty lists are initialized:
    - `image_urls`: This list will store the URLs of player images.
    - `player_names`: This list is created by extracting player names from the DataFrame and converting them to a Python list.

- **Configuring Headless Chrome**: To interact with web pages and collect image URLs, a headless Chrome browser is configured. The following libraries and settings are used for this purpose:
    - **Requests (`import requests`)**: This library is used to make HTTP requests to retrieve web pages containing player profile information. It allows us to fetch the web page's content.

    - **Selenium (`from selenium import webdriver`)**: Selenium is employed for web automation tasks. It enables interaction with web pages, including navigation and data retrieval.

    - **Selenium Chrome WebDriver (`webdriver.Chrome`)**: The Chrome WebDriver, provided by Selenium, is configured to automate the Chrome browser. It allows us to programmatically interact with web pages and extract data.

    - **Selenium Chrome Options (`chrome_options`)**: Chrome options are set to configure the behavior of the Chrome browser. In this case, we enable headless mode (no graphical user interface), specify the Chrome binary location, disable GPU (required for Windows), enable verbosity, and specify a log path for detailed logging.

- **Iterating Through Player Names and URLs**: The code iterates through player names and their corresponding profile URLs. For each player, it performs the following steps:
    - Navigates to the player's profile page using the WebDriver.
    - Sets up an explicit wait of up to 200 seconds (adjustable) for an image element to be present on the page.
    - Searches for all image elements (`<img>`) within the page.
    - Iterates through the image elements to find one with an `alt` attribute containing the player's name (case-insensitive match).
    - Scrolls to trigger lazy loading (if required) and waits for images to load.
    - Retrieves the `src` attribute, which contains the image URL, and adds it to the `image_urls` list.
    - Exits the loop after finding the first matching image URL. If no match is found, an empty string is added to the list.

- **Error Handling**: The code includes error handling to account for exceptions that may occur during image retrieval. In case of an error, an empty string is added to the `image_urls` list, and details of the error are printed.

- **Completing the Process**: After processing all players, the WebDriver is terminated to release system resources.

- **Data Integration**: The collected image URLs are added to the existing DataFrame as a new column named 'Image.'

- **Data Cleaning**: To enhance data consistency, URLs containing patterns related to 'wassets' are replaced with spaces, ensuring uniform representation of image URLs.

This process enables the integration of player images into the dataset, enriching the analysis with visual references to the ICC T20 World Cup 2022 players.

### Image URL Cleaning
Image URLs are cleaned to remove unwanted parts, such as those containing 'wassets.' This ensures that the URLs are valid and can be used to display player images.

### Final Player Details DataFrame
The resulting DataFrame contains comprehensive player details, including names, teams, images, batting styles, bowling styles, playing roles, and descriptions. This data is invaluable for various analyses and visualizations within the ICC T20 World Cup 2022 Analysis project.

This process ensures that player details are systematically extracted, structured, and enhanced for further analysis and visualization within the project.

## Project Progress
As a solo developer, I have completed the web scraping part of the project, which involves fetching ICC T20 World Cup 2022 data from relevant sources. The code for this part is marked with annotations to explain each step in detail.

## Disclaimer
The ICC T20 World Cup 2022 data used in this project is sourced from publicly available cricket websites. Credit goes to the respective website owners and data providers. This project is intended to demonstrate how web scraping and data analysis can be applied to ICC T20 World Cup 2022 data. I do not claim ownership of the data, and it is hosted on the respective websites.

Feel free to explore the project, provide feedback, and stay tuned for updates as I continue to develop and expand the ICC T20 World Cup 2022 Analysis project.
