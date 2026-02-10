# Splunk DNS Log Analysis Project

## Objective
This project focuses on ingesting and analyzing DNS logs in Splunk to understand DNS traffic patterns and practice basic SPL queries commonly used in SOC investigations.

## Environment
- Splunk Enterprise (local lab setup)
- Data format: JSON
- Index used: dns_lab
- Sourcetype: json

## Data Description
The dataset contains sample DNS log entries in JSON format.  
Each event includes fields such as:
- ts – timestamp
- id.orig_h – source IP (client)
- id.resp_h – destination IP (DNS server)
- query – domain name requested
- qtype – DNS record type (A, AAAA, CNAME, PTR)
- rcode – response code
- rtt – response time

This dataset was used only for learning and practice purposes.

## Data Ingestion
The DNS log file was uploaded through Splunk Web:

Settings → Add Data → Upload  
Sourcetype: json  
Index: dns_lab  

Data ingestion was verified using:
index=dns_lab | head 5

## Analysis Tasks

### Task 1: Identify the most frequently queried domains
Query:
index=dns_lab sourcetype="json"
| stats count by query
| sort -count

This helps identify domains that are accessed most often and can highlight unusual or suspicious domain activity.

---

### Task 2: Find the most active client IPs generating DNS traffic
Query:
index=dns_lab sourcetype="json"
| stats count by id.orig_h
| sort -count

This shows which hosts are generating the highest number of DNS requests, useful for spotting infected or misconfigured systems.

---

### Task 3: Breakdown of DNS query types
Query:
index=dns_lab sourcetype="json"
| stats count by qtype

This provides visibility into DNS record usage such as A, AAAA, CNAME, and PTR records.

## Conclusion
Through this project, I gained hands-on experience with DNS log ingestion and analysis in Splunk.  
I practiced writing SPL queries to analyze DNS activity, identify top queried domains, observe client behavior, and understand different DNS record types.  
This type of analysis is commonly used in SOC environments to detect anomalies, suspicious domains, and abnormal host behavior.
