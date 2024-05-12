# DesigniteJava action for GitHub

## What it does?
This action analyzes your Java code using [DesigniteJava](https://www.designite-tools.com/designitejava/), detects a comprehensive set of architecture, design, and implementation smells, computes a large set of object-oriented code quality metrics, and uploads the results as an artifact.

## How to configure it?
It is a one-time process.

### Step 1. Obtain Personal access token and add it to GitHub secrets
- Create a new personal access token for your GitHub repository. You may do it by going to “Settings” -> “Developer settings” page of your GitHub account. Select “Personal access token” tab and create a new token.
- Add this token to your repository’s secrets. Go to “Settings” within your repository page and select “Secrets”. Add a new secret by pasting the access token in the Value field and giving a meaning name (e.g. PAT).

### Step 2: Optional: Add your Designite key to secrets

If you have Designite’s professional (or academic) license key, add the key to your GitHub’s repository secrets. Let us call it D_KEY

### Step 4: Add a GitHub Actions workflow file

This is the last and very crucial step. Create a folder `.github` on your root directory of the project and create `workflows` folder inside the `.github` folder. Create a workflow file (say `actions.yml`) in the newly created `workflows` folder. The contents of the `action.yml` file depend upon your project language and tasks.

A sample action file is provided below.

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: DesigniteJava_action
      uses: DesigniteTools/DJAction@v1.0.0
      with:
          PAT: ${{ secrets.PAT }}
```

Change the version number of action.

## What you will get?
Once configured, your Java project will be analyzed on each push in the main branch (can be configured differently), and the analysis report will be placed as an Actions artifact in your GitHub account. You can later download the artifact for further analysis.
