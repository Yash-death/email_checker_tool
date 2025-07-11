# Email Checker Tool

A simple Go command-line tool to check domains for email-related DNS records: MX, SPF, and DMARC.

## Features
- Checks if a domain has MX records (can receive email)
- Checks for SPF records and outputs the record if present
- Checks for DMARC records and outputs the record if present
- Outputs results in CSV format

## Usage

1. **Build the tool:**
   ```sh
   go build -o email-checker-tool main.go
   ```

2. **Run the tool:**
   Provide a list of domains via standard input (one per line):
   ```sh
   cat domains.txt | ./email-checker-tool
   ```
   or interactively:
   ```sh
   ./email-checker-tool
   example.com
   gmail.com
   (Ctrl+D to end input)
   ```

## Output
The tool prints a CSV with the following columns:
- `domain`: The domain checked
- `hasMX`: Whether MX records exist
- `hasSPF`: Whether an SPF record exists
- `spfRecord`: The SPF record (if any)
- `hasDMARC`: Whether a DMARC record exists
- `dmarcRecord`: The DMARC record (if any)

Example output:
```
domain,hasMX,hasSPF,spfRecord,hasDMARC,dmarcRecord
mailchimp.com
% mailchimp.com true true v=spf1 ip4:205.201.128.0/20 ip4:198.2.128.0/18 ip4:148.105.0.0/16 ip4:129.145.74.12 include:_spf.google.com include:mailsenders.netsuite.com include:_spf2.intuit.com include:_spf.qualtrics.com ip4:199.33.145.1 ip4:199.33.145.32 ip4:35.176.132.251 ip4:52.60.115.116 ~all true v=DMARC1; p=reject; rua=mailto:19ezfriw@ag.dmarcian.com,mailto:dmarc_rua@emaildefense.proofpoint.com; ruf=mailto:19ezfriw@fr.dmarcian.com,mailto:dmarc_ruf@emaildefense.proofpoint.com;

youtube.com
% youtube.com true true v=spf1 include:google.com mx -all true v=DMARC1; p=reject; rua=mailto:mailauth-reports@google.com

gmail.com
% gmail.com true true v=spf1 redirect=_spf.google.com true v=DMARC1; p=none; sp=quarantine; rua=mailto:mailauth-reports@google.com
```


## Requirements
- Go 1.13 or later

## License
MIT
