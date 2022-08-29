# Splunk Enterprise on-prem

## Setup
### Dependencies
- wget
- net-tools

### Download Splunk Enterprise

`wget -O splunk-8.1.3-63079c59e632-linux-2.6-amd64.deb 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.1.3&product=splunk&filename=splunk-8.1.3-63079c59e632-linux-2.6-amd64.deb&wget=true'`

### Install on Ubuntu Server 20.04

`sudo dpkg -i splunk-[rest of filename]`

### Start Splunk

`sudo /opt/splunk/bin/splunk start --accept-license`

Splunk uses port 8000 as the default for the Splunk web site.

## Operations
