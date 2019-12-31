# Checkmarx Github Action

## Scan project with Checkmarx via Github Actions

## Inputs available

| Input Name  | Variable Value (Example) | Variable Type | Is Required* |
| ------------- | ------------- | ------------- | ------------- |
| cxServer | https://checkmarx.company.com  | String | Yes* |
| cxUsername | admin@cx | String | Yes* |
| cxPassword | ${{ secrets.CX_PASSWORD }} | Secure String | Yes* |
| cxTeam | \CxServer\SP\Company\TeamA | String | Yes* |
| cxPreset | Checkmarx Default | String | No |
| cxHigh | 0 | Integer | No |
| cxMedium | 0 | Integer | No |
| cxMedium | 0 | Integer | No |

## Secrets

Configure the Password in Secrets section (Repo → Settings → Secrets → Add New Secret): 

| Secret Name  | Variable Value (Example) | Variable Type | Is Required* |
| ------------- | ------------- |  ------------- | ------------- |
| CX_PASSWORD | ******** | Secure String | Yes* |

## Sample Github Action Workflow Config
```
name: Checkmarx Scan

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v1
    - name: Checkmarx Scan
      uses: miguelfreitas93/checkmarx-github-action@8.9.0
      with:
        # Checkmarx Server URL
        cxServer: https://cxprivatecloud.checkmarx.net
        # Checkmarx Username
        cxUsername: Miguel.Freitas@checkmarx.com
        # Checkmarx Password
        cxPassword: ${{ secrets.CX_PASSWORD }}
        # Checkmarx Team
        cxTeam: \CxServer\SP\EMEA\__psteam
        # Checkmarx Project Preset
        cxPreset: Checkmarx Default
        # Threshold for High Severity Vulnerabilities
        cxHigh: 0
        # Threshold for Medium Severity Vulnerabilities
        cxMedium: 0
        # Threshold for Low Severity Vulnerabilities
        cxLow: 0
    - name: Upload PDF Artifact
      uses: actions/upload-artifact@master
      with:
        name: results.pdf
        path: results.pdf
    - name: Upload XML Artifact
      uses: actions/upload-artifact@master
      with:
        name: results.xml
        path: results.xml

```

### Notes:

- Make sure you do **Checkout** of the code, before Checkmarx Scan Step;
- PDF and XML produced will have always the name **"results.pdf"** or **"results.xml"**, respectively;