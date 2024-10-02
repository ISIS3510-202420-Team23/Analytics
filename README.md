# Analytics Pipeline for Firestore and Google Sheets Integration

## Overview

This repository contains a pipeline for extracting data from Firestore, processing it, and uploading it to Google Sheets. The project is set up to analyze data from the `user_actions`, `properties`, and `offers` collections in Firestore, and then store the processed data in a Google Sheet named `analyticsBQ`.

The processed data is then available for visualization and analysis in Google Looker. The dashboard includes various insights and metrics derived from the data extracted from Firestore.

## Requirements

To run this pipeline, you will need:

1. **Python 3.8 or higher**: Make sure you have Python installed. If not, download it from [Python's official site](https://www.python.org/downloads/).
2. **Required Libraries**: Install the required libraries with `pip`.
3. **Service Account Credentials**: You must have two service account files for:
   - Firestore access (`serviceAccountKey.json`)
   - Google Sheets access (`client_secret.json`)

### How to Obtain the Service Account Credentials

If you don't have access to the service account credentials, please request them from **Thais Tamaio**. 

If you have access to the Firestore and Google API Console, you can generate the credentials as follows:

#### Firestore Access
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Select your project or create a new one.
3. Navigate to **IAM & Admin** and select **Service Accounts**.
4. Click on **Create Service Account**, provide a name and description, and click **Create**.
5. Under **Service account permissions**, add the role **Firestore Admin**.
6. Click **Done** and then find your newly created service account in the list.
7. Click on the three dots next to it, select **Manage Keys**, and click **Add Key** -> **Create New Key**.
8. Select **JSON** and click **Create** to download the `serviceAccountKey.json` file.

#### Google Sheets Access
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Select your project or create a new one.
3. Navigate to **API & Services** and select **Credentials**.
4. Click **Create Credentials** -> **Service Account**.
5. Provide a name and description, and click **Create**.
6. Assign a role, such as **Editor** or **Google Sheets API Admin**, depending on your requirements.
7. Click **Done** and navigate back to the **Credentials** page.
8. Find your service account and click on it, then select **Keys** -> **Add Key** -> **Create New Key**.
9. Choose **JSON** and click **Create** to download the `client_secret.json` file.

Make sure to place both `serviceAccountKey.json` and `client_secret.json` in the `credentials/` folder of your project directory.

## How to Set Up the Pipeline

### Step 1: Install Required Packages

Create a virtual environment (optional but recommended):

```bash

python3 -m venv env  
source env/bin/activate  # For Linux/Mac  
.\env\Scripts\activate   # For Windows

```

Install the required Python packages:

```bash

pip install -r requirements.txt

```

### Step 2: Place Service Account Credentials

Ensure you have the following credential files in the `credentials/` folder:

- `client_secret.json` (for Google Sheets)
- `serviceAccountKey.json` (for Firestore)

The credentials should be generated from your Google Cloud Console and must have permissions for accessing the corresponding APIs.

### Step 3: Configure Firestore and Google Sheets

1. **Firestore**: Set up Firestore with collections named `user_actions`, `properties`, and `offers`.
2. **Google Sheets**: Create a Google Sheet named `analyticsBQ` to upload the data.

### Step 4: Run the Pipeline

Execute the main script:

```bash

python GoogleSheets.py

```

This script will:

- Extract data from the Firestore collections (`user_actions`, `properties`, and `offers`).
- Process the data and calculate relevant metrics.
- Save the processed data into CSV files located in the `data_sources/` folder.
- Upload the CSV files to corresponding sheets named "User Actions" and "Ofertas" in the Google Sheet `analyticsBQ`.

### Step 5: View the Results

You can view the results directly in the [Google Looker Dashboard](https://lookerstudio.google.com/reporting/2a1b4818-3834-425e-b33c-1d4339e47f91).

## Important Considerations

- **Credentials**: Make sure the service account credentials (`client_secret.json` and `serviceAccountKey.json`) are not exposed in the repository. Use `.gitignore` to exclude them from version control.
- **Permissions**: The Google Cloud Service account must have sufficient permissions to access Firestore and manage Google Sheets.
- **Data Privacy**: Ensure that the data extracted and processed adheres to privacy standards and regulations.

# Commands to Install Required Libraries on Windows and Mac

### Windows

```bash

pip install pandas  
pip install firebase-admin  
pip install gspread  
pip install oauth2client  

```

### Mac

```bash

pip install pandas  
pip install firebase-admin  
pip install gspread  
pip install oauth2client  

```

If using a virtual environment, make sure to activate it before running these commands:

- For Windows:

```bash

.\env\Scripts\activate  

```

- For Mac:

```bash

source env/bin/activate  

```
