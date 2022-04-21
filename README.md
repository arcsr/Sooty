[![Generic badge](https://img.shields.io/badge/Made%20with-Python-blue.svg?style=flat-square)](https://GitHub.com/theresafewconors/sooty)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-green.svg?style=flat-square)](https://GitHub.com/theresafewconors/sooty)
[![GitHub contributors](https://img.shields.io/github/contributors/theresafewconors/sooty.svg?style=flat-square)](https://GitHub.com/theresafewconors/sooty/graphs/contributors/)
[![Generic badge](https://img.shields.io/badge/Built%20For-SOC%20Analyst's-olive.svg?style=flat-square)](https://GitHub.com/theresafewconors/sooty)
[![HitCount](http://hits.dwyl.io/theresafewconors/sooty.svg)](https://GitHub.com/theresafewconors/sooty)
![Docker](https://img.shields.io/badge/Docker-Supported-blue)


![](readmeimages/sooty_logo.png)
[![](readmeimages/tines_banner.png)](https://tines.io?utm_source=github&utm_medium=sponsorship&utm_campaign=sooty)
# Overview

Sooty is a tool developed with the task of aiding SOC analysts with automating part of their workflow. One of the goals of Sooty is to perform as many of the routine checks as possible, allowing the analyst more time to spend on deeper analysis within the same time-frame. Details for many of Sooty's features can be found below.

Sooty is now proudly supported by [Tines.io](https://tines.io?utm_source=github&utm_medium=sponsorship&utm_campaign=sooty)! The SOAR Platform for Enterprise Security Teams.

## Contents
 - [Current Features](#sooty-can-currently)
 - [Requirements & Installation](#requirements-and-installation)
 - [Development](#development)
 - [Changelog](#changelog)
 - [Roadmap](#roadmap)
 - [Contributors](#contributors)
 
 
![](readmeimages/repcheck.gif)


## Sooty can Currently:
  - Sanitise URL's to be safe to send in emails
  - Perform reverse DNS and DNS lookups
  - Perform reputation checks from:
    - [VirusTotal](https://www.virustotal.com)
    - [BadIP's](https://www.badips.com/)
    - [Abuse IPDB](https://www.abuseipdb.com/)
  - Identify if an address is potentially malicious, used for spam, web bots:
    - [Botvrij.eu](https://botvrij.eu)
    - [myip.ms](https://myip.ms)
    - [Firehol](https://raw.githubusercontent.com/firehol/blocklist-ipsets/master/nixspam.ipset)
  - Check if an IP address is a TOR exit node
  - Decode Proofpoint URL's, UTF-8 encoded URLS, Office SafeLink URL's, Base64 Strings and Cisco7 Passwords.
  - Get file hashes and compare them against [VirusTotal](https://www.virustotal.com) (see requirements)
  - Perform WhoIs Lookups
  - Check Usernames and Emails against [HaveIBeenPwned](https://haveibeenpwned.com) to see if a breach has occurred. (see requirements)
  - Simple analysis of emails to retrieve URL's, emails and header information.
  - Extract IP addresses from emails.
  - Unshorten URL's that have been shortened by external services. (Limited to 10 requests per hour)
  - Query [URLScan.io](https://urlscan.io) for reputation reports.
  - Analyze email addresses for known malicious activity and report on domain reputation utilising [EmailRep.io](https://emailrep.io)
  - Create dynamic email templates that can be used as a base for phishing triage response.(.msg only, .eml coming in future update)
  - Perform analysis enrichment on phishing mails using the HaveIBeenPwned database, and can identify if an email address has been compromised in the past, when it happened and where the breach occurred. (Requires API Key).
  - Submit URL's to [PhishTank](https://www.phishtank.com/). (see requirements)
  - [Unfurl](https://github.com/obsidianforensics/unfurl) URL's via the CLI version of Unfurl. 
  - See below for a full list and layout of currently available tools:
  
  
```
└── Main Menu
   ├── Sanitize URL's for use in emails
   |  └── URL Sanitizing Tool
   ├── Decoders
   |   ├── ProofPoint Decoder
   |   ├── URL Decoder
   |   ├── Office Safelinks Decoder
   |   ├── URL Unshortener
   |   ├── Base 64 Decoder
   |   ├── Cisco Password 7 Decoder
   |   └── Unfurl URL
   ├── Reputation Checker
   |   └── Reputation Checker for IP's, URL's or email addresses
   ├── DNS Tools
   |   ├── Reverse DNS Lookup
   |   ├── DNS Lookup
   |   └── WhoIs Lookup
   ├── Hashing Functions
   |   ├── Hash a File
   |   ├── Hash a Text Input
   |   ├── Check a hash for known malicious activity
   |   └── Hash a file and check for known malicious activity
   ├── Phishing Analysis
   |   ├── Analyze an Email
   |   ├── Analyze an email address for known malicious activity
   |   ├── Generate an email template based on analysis
   |   ├── Analyze a URL with Phishtank
   |   └── HaveIBeenPwned Lookup
   ├── URL Scan
   |   └── URLScan.io lookup
   ├── Extra's
   |   ├── About
   |   ├── Contributors
   |   ├── Version
   |   ├── Wiki
   |   └── Github Repo
   └── Exit
```
![](https://github.com/TheresAFewConors/Sooty/blob/master/readmeimages/unfurl.PNG)

![](readmeimages/email_analysis.gif)

## Requirements and Installation
 - [Python 3.x](https://www.python.org/)
 - Install all dependencies from the requirements.txt file. `pip install -r requirements.txt`
 - Launch the tool by navigating to the main directory, and executing with `python Sooty.py`, or simply `Sooty.py` 
 - Several API Keys are required to have full functionality with Sooty. However, it will still function without these keys, just without the added functionality they provide. Links are found below:
   - [VirusTotal API Key](https://developers.virustotal.com/reference)
   - [URLScan.io API Key](https://urlscan.io/about-api/)
   - [AbuseIPDB API Key](https://www.abuseipdb.com/api)
   - [HaveIBeenPwned API Key](https://haveibeenpwned.com/API/Key)
   - [PhishTank API Key](https://www.phishtank.com/api_info.php)
   - [EMAILREP API KEY](https://emailrep.io/key)
   - [VPNIO_API_KEY](https://vpnapi.io)
 - Replace the corresponding key in the `example_config.yaml` file, and rename the file to `config.yaml`, example layout below:
 - For PhishTank support, an unique app name is also required as an additional field. Simply update the `config.yaml` file with your unique name.
 
![](readmeimages/example_config.png)

## Launch with Docker
- docker build -t sooty . && docker run --rm -it sooty 
 
 <!-- - To use the Hash comparison with VirusTotal requires an [API key](https://developers.virustotal.com/reference), replace the key `VT_API_KEY` in the code with your own key. The tool will still function without this key, however this feature will not work.
 - To use the Reputation Checker with AbuseIPDB requires an [API Key](https://www.abuseipdb.com/api), replace the key `AB_API_KEY` in the code with your own key. The tool will still function without this key, however this feature will not work.
 - To use the URLScan.io checker function with URLScan requires an [API Key](https://urlscan.io/about-api/), replace the key `URLSCAN_IO_KEY` in the code with your own key. The tool will still function without this key, however this feature will not work. 
 - Use of the HaveIBeenPwned functionality requires an [API Key](https://haveibeenpwned.com/API/Key), replace the key `HIBP_API_KEY` in the code with your own key. The tool will still function without this key, however this feature will not work. -->
 
## Development

### Want to contribute? Great!

  #### Code Contributions
  - If you wish to work on a feature, leave a comment on the issue page and I will assign you to it.
  - Under the projects tab is a list of features that are waiting to be started / completed. 
  - All code modifications, enhancements or additions must be done through a pull request. 
  - Once reviewed and merged, contributors will be added to the ReadMe.

