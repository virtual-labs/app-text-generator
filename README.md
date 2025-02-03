# Virtual Labs Prompt Repository

## Table of Contents

- [Virtual Labs Prompt Repository](#virtual-labs-prompt-repository)
  - [Table of Contents](#table-of-contents)
  - [Project Overview](#project-overview)
  - [Key Features](#key-features)
  - [Components](#components)
  - [Usage](#usage)
  - [Installation](#installation)
    - [Prerequisites](#prerequisites)
    - [Frontend Setup](#frontend-setup)
    - [Backend Setup](#backend-setup)
    - [Set up OAuth with GitHub:](#set-up-oauth-with-github)
    - [Generating an API Key](#generating-an-api-key)
    - [Environment Variables](#environment-variables)
    - [Google Sheet Structure](#google-sheet-structure)
    - [Hierarchical Structure](#hierarchical-structure)
    - [Basic Usage](#basic-usage)
  - [Deployment](#deployment)

## Project Overview

**Virtual Labs Prompt Repository** is a tool designed for Virtual Labs staff to generate various types of content, such as blogs and documentation, using large language models (LLMs). The repository contains predefined prompt templates, allowing users to input specific information to generate content efficiently.

## Key Features

- **Content Generation**: Generate content like blogs and documentation using predefined prompt templates.
- **User Inputs**: Customize content generation by providing specific inputs.
- **Hierarchical Structure**: Organized structure with prompt directories, categories, and templates for easy navigation and usage.

## Components

The project is divided into two main components:

1. **Frontend**:

   - Developed using ReactJS and CSS.
   - Provides an interactive user interface for inputting data and generating content.

2. **Backend**:
   - Developed using Flask (Python).
   - Handles server-side logic and integrates with the Gemeni API for text generation.

## Usage

Only registered users can access the tool. To gain access, please send a request email to support@vlabs.ac.in with your GitHub ID.

1. Log in to the prompt repository using your GitHub account.
2. Select the type of documentation you need (Social Media Prompts, Dev Manual, User Manual).
3. Add or replace placeholders and their content to view the prompt preview on the right.
4. Click on "Run" to generate and view the output on the screen.
   
## Installation

### Prerequisites

- **Node.js and npm** for the frontend.
- **Python 3.9+** for the backend.

### Frontend Setup

- Navigate to the frontend directory:

```
cd frontend
```

- Install dependencies:

  ```
  npm install
  ```

- Start the frontend server:

  ```
  npm start
  ```

### Backend Setup

1. Create a .env file and a secrets folder in the backend directory.
2. Place the service-account-secret.json file inside the secrets folder.
3. Set up a Python virtual environment and activate it:

```bash
python -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`

```

4. Install dependencies:

```bash
pip install -r requirements.txt
```

5. Start the backend server:

```bash
python server.py
```

### Set up OAuth with GitHub:

- Register a new OAuth application within GitHub account by navigating to GitHub Settings > Developer Settings > OAuth Apps > New OAuth App.
- Set the Homepage URL to the deployment domain (https://docgen.vlabs.ac.in)
- Set the Authorization callback URL to the callback url (https://docgen.vlabs.ac.in/callback)
- This will generate a Client ID and Client Secret.

### Generating an API Key

Users can generate their Gemeni API key from [this link](https://ai.google.dev/gemini-api/docs/api-key).


### Environment Variables

**.env file:**

- `GOOGLE_SHEET_ID`: ID of the Google Sheet used for storing data.
- `GEMENI_API`: API key for Gemeni, used for text generation.

### Google Sheet Structure

The Google Sheet contains three tabs:

**Users:**

- **Github Account**: The GitHub account of the user.
- **Role**: The role of the user.

**Prompt Directories:**

- **Prompt Directory**: Name of the prompt directory.
- **Category List**: List of categories under the directory.

**Prompt Templates:**

- **Prompt Directory**: The directory to which the template belongs.
- **Category**: The category under the directory.
- **Template Name**: Name of the template.
- **Prompt Template**: The template text.
- **Placeholders**: Placeholders to be filled by user inputs.

### Hierarchical Structure

The application is organized in a hierarchical manner:

Prompt Directory → Prompt Category → Prompt Template

Users add inputs in the Prompt Template to generate the desired content.

### Basic Usage

1. Start the frontend and backend servers as described in the installation section.
2. Open the frontend in your browser.
3. Navigate through the prompt directories and categories to find the desired prompt template.
4. Fill in the required placeholders and generate content.

## Deployment
This app is deployed on GCP (Google Cloud Platform) using App Engine for backend and bucket for frontend.

Ensure that the production frontend and backend urls are updated in `frontend/config.js` and `backend/.env`


The documentation generator tool can be deployed using the following steps:

1. **Google Cloud Platform CLI Setup** :- Install the Google Cloud SDK by following the instructions [here](https://cloud.google.com/sdk/docs/install).

2. **Login to GCP from CLI**

```bash
gcloud auth login
```

3. **Set the project ID**

```bash
gcloud config set project documentation-generator
```

4. **Deploy the backend**

```bash
cd backend
gcloud app deploy
```

5. **Deploy the frontend**

```bash
cd frontend
npm run build:prod
gsutil cp -r build/* gs://app-text-generator
```
