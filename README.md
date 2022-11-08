# automation-gsheets-ghactions

## Overview

- triggering event: A value in a Google Spreadsheet is modified. *Does not detect changes in formatting or changes to the spreadsheet's structure, e.g., insertion of a row or a sheet. See more details [here](https://developers.google.com/apps-script/guides/triggers/installable).*
- resulting action: GitHub Actions workflow. *Currently just outputs a message about which sheet was edited.*
 
## Components

- this GitHub repository
- [the Google Spreadsheet](https://docs.google.com/spreadsheets/d/1bfE9KkzvVl85DhwNV01pfD9y8dGuuH8nI1E-0BsVZu0)

## Replicating the system

1. Create a new Google Spreadsheet.
    1. Log into the Google account that you want to be the owner of the new spreadsheet.
    1. Make a copy of the original spreadsheet. The spreadsheet has an attached Apps Script file called "webhook", which should be identical to the code/webhook.js file in this repo.
    1. In the spreadsheet, click on Extensions, then Apps Script.
    1. Click on Triggers, then Add Trigger.
        - Choose which function to run: at_edit
        - Select event type: On edit
    1. Click Save, choose the appropriate Google account, click Allow.
    1. Close the Apps Script.

1. Create a new GitHub repository.
    1. Log into the GitHub account that you want to be the owner of the new repository.
    1. On this repository's main page, click "Use this template" to create a new repository.

1. Create a repo-specific personal access token.
    1. Go to https://github.com/settings/tokens.
    1. Click on Fine-grained tokens, then Generate new token.
        - Token name: create a name based on the new repo's name
        - Custom expiration: current maximum is one year
        - Resource owner: select the organization of the new repo
        - Repository access: select "Only select repositories" and select the new repo
        - Repository permissions: for Contents, select "Access: Read and write"
    1. Click Generate token.
    1. Click Copy to clipboard.
    1. Paste the token into a new text file and save the file with the same name as the token.
    1. Upload the text file to Google Drive.

1. Update the Google Spreadsheet.
    1. Right-click on the new Drive file, select Get link, click Copy link, click Done.
    1. In the new spreadsheet, click on the github sheet.
    1. Paste the link in the cell below pat_url.
    1. Copy the URL of the new GitHub repo and paste it in the cell below repo_url.

## Modifying a replicated system

- To enable or disable the triggering of the GH Actions workflow, change the value below "enabled" in the github sheet to 1 or 0.
- To change which sheets (when values in them are modified) trigger the GH Actions workflow, change the values below "sheet_name" in the triggers sheet.
- To change what the GH Actions workflow actually does, update the .github/workflows/ci.yaml file.
