# SessionHound
A script to import session information that has been collected from alternate data sources  into BloodHound's Neo4j database.

## Problem
SharpHound's privileged session collection requires an account with elevated permissions to operate. When using BloodHound as a Blue tool to locate and resolve misconfigurations and identify dangerous behaviors, detailed and accurate session information is highly beneficial. An account that has local administrative rights on all endpoints is a security risk.

## Solution
Session information can be obtained from alternate sources. This information can be obtained by collecting the information from centrally logged local Windows Security Events or from other tools that can poll information about logged on users from live endpoints. It can be collected into a spreadsheet and added to the BloodHound database via Cypher queries.

## Requirments
```
neo4j
```

## Usage
```
usage: SessionHound.py [-h] [-d DOMAIN] [-c CSV]

Import computer session data from a CSV file into BloodHound's Neo4j database.
The CSV should have two colums matching the following header structure:
['username', 'hostname']

optional arguments:
  -h, --help            show this help message and exit
  -d DOMAIN, --domain DOMAIN
                        The base AD Domain for your environment. i.e.
                        EXAMPLE.COM
  -c CSV, --csv CSV     The path to the CSV file containing the session data
                        to import.
```

## CSV File Format
The CSV file needs to have two columns:
- username: The User Principal Name (UPN). i.e. USER01@EXAMPLE.COM
- hostname: The Host's FQDN. i.e. HOSTNAME.EXAMPLE.COM

### Example
```
username,hostname
user01@example.com,host01.example.com
user02@example.com,host01.example.com
user02@example.com,host02.example.com
```
**NOTE:** If using Excel to prepare your CSV, saving the CSV in Unicode/UTF-8 format will cause some errors. To avoid these issues use the **CSV (Comma delimited)** option and not **CSV UTF-8 (Comma delimited)**.
