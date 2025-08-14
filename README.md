# Logistics Automation n8n

This project is an automated workflow built with n8n to streamline logistics operations. It automatically processes incoming data from various sources like emails and spreadsheets, enriches it with geographical information, and organizes it to find potential shipping carriers. This automation saves significant manual effort and speeds up the carrier selection process.

## Key Features
*   **Scheduled Data Processing:** The workflow runs automatically on a daily schedule.
*   **Email Data Extraction:** It triggers on new emails, parsing the body and attachments to extract relevant data.
*   **Spreadsheet Integration:** It can be triggered when new Excel files are added to a specific Google Drive folder.
*   **Data Validation and Enrichment:** Uses OpenAI to validate and extract information, and external APIs to get geographical data (latitude and longitude).
*   **Automated Filtering and Grouping:** Automatically groups pickup locations into geographical clusters and filters potential carriers based on proximity.
*   **Automated Reporting:** Populates Google Sheets with the processed and formatted data.

## Workflow Visualization
Here is a visual representation of the entire workflow:

![Workflow Visualization] https://github.com/Muneeb20019/logistics-automation-n8n/blob/main/logistics%20workflow.jpeg
## How It Works
The workflow is divided into three main automated processes:

### 1. Daily Scheduled Carrier Search 
*   **Triggers Daily:** The workflow starts every day at a set time.
*   **Reads Master Data:** It accesses a master Google Sheet containing raw data of pickup locations from emails.
*   **Geographical Clustering:** The data is grouped into geographical clusters.
*   **API Enrichment:** It uses an external API to fetch the latitude and longitude for one city from each cluster.
*   **Carrier Filtering:** An external service is used to find a list of potential carriers in that area.
*   **Data Segregation:** The results are filtered into two groups: "within 150 miles" and "outside 150 miles".
*   **Final Output:** Two separate sheets in a Google Sheet are populated with the filtered carrier data for the current date.

### 2. New Email Processing 
*   **Email Trigger:** The workflow starts whenever a new email is received in a specific inbox.
*   **Data Routing:** A switch node directs the email body, attachments (like .xls files), and other data down three separate processing paths.
*   **AI-Powered Data Extraction:** Each path uses an OpenAI node to extract the relevant information from the data.
*   **Validation and Storage:** An IF node validates the extracted data, which is then added to the appropriate Google Sheet.

### 3. New Carrier Portal File Processing 
*   **Drive Trigger:** This workflow begins when a new Excel file from a carrier portal is added to a specific folder in Google Drive.
*   **Data Extraction:** The workflow downloads the file and extracts contact data.
*   **Data Appending:** The new contact information is added to a designated Google Sheet.
*   **Automated Communication:** The email address is isolated from the new data, and a pre-written template is sent to each new contact using the Gmail node.

## Technologies Used
*   **Automation Platform:** n8n.io
*   **Data Storage & Management:** Google Sheets, Google Drive
*   **AI & Data Processing:** OpenAI
*   **APIs:** Nomination API (for geolocation), other external services
*   **Communication:** Gmail
