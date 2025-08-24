# Cyber-Security-Automation-Project-2: Real Time Email Analysis & SIEM Integration

## 📌 Overview
This project implements a **cybersecurity automation workflow** that continuously monitors, analyzes, and responds to email-based threats by integrating with threat intelligence platforms and security monitoring systems. Since **email remains the primary attack vector** for cyber threats, this solution provides critical defense capabilities through automated detection and SIEM integration.

The Python-based automation system:
- Monitors email accounts (Inbox & Spam) via IMAP
- Analyzes suspicious emails for potential threats
- Extracts and scans URLs & attachments using **VirusTotal** API
- Forwards structured security events to **Splunk** for centralized monitoring and correlation

---

## 🏗️ Architecture Components

### 1. Email Access Layer (Gmail/IMAP)
- Secure IMAP connection to retrieve emails from both primary inbox and spam folder
- Requires IMAP enabled in Gmail settings
- Authentication via **Google App Passwords** for enhanced security

### 2. Threat Intelligence Integration (VirusTotal)
- Automated scanning of email attachments (hashed) and extracted URLs
- API integration with **VirusTotal** for multi-engine threat detection
- Configurable threshold-based alerting

### 3. SIEM Integration (Splunk HTTP Event Collector)
- Secure data transmission to Splunk via **HTTP Event Collector (HEC)**
- Configurable endpoint, authentication token, and port (default: `8088`)
- Structured data formatting for optimal Splunk ingestion

---
## Project Structure
```
├── send_email.py              # Phishing simulation tool for testing
├── main.py                    # Primary monitoring and analysis engine
├── .env.example               # Environment configuration template
├── requirements.txt           # Python dependencies
└── README.md                  # Comprehensive documentation
```

---
## ⚙️ Configuration
Sensitive credentials are managed through environment variables in a `.env` file:
```bash
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_generated_app_password
VT_API_KEY=your_virustotal_api_key
SPLUNK_TOKEN=your_splunk_hec_token
SPLUNK_URL=https://yoursplunkserver:8088
```

---
## 🛠️ Implementation Scripts

### 1. **Phishing Simulation Tool (`send_email.py`)**
- Generates **10 simulated phishing emails** (1 per minute interval)
- Creates safe testing environment for detection validation
- Features:
  - Realistic phishing subject lines and content
  - Secure Gmail SMTP authentication using App Passwords
  - Configurable sender and recipient addresses

### 2. **Email Monitoring & Analysis Engine (`main.py`)**
- Establishes persistent IMAP connection to Gmail
- Monitors both **Inbox** and **Spam** folders for unread messages
- Extracts and analyzes links, attachments, and email content
- Integrates with **VirusTotal** for threat scanning
- Forwards structured security events to **Splunk HEC**

**Processing Workflow:**
1. Load configuration and authenticate with all services
2. Retrieve and process unread emails
3. Parse headers, body content, attachments, and embedded URLs
4. Submit suspicious indicators to VirusTotal for analysis
5. Format and transmit results to Splunk for centralized monitoring
6. Maintain processing state to prevent duplicate analysis
7. Execute continuous monitoring cycle (4-minute intervals)

---
## 🔒 Security & Operational Considerations
- Gmail requires IMAP access and App Password authentication
- VirusTotal API implements rate limiting - appropriate throttling implemented
- Splunk HEC must be properly configured and network accessible
- Processed email tracking prevents re-analysis and duplicate alerts
- All sensitive credentials stored externally in environment variables

---
## 🎯 Practical Applications
When combined, both scripts create a comprehensive testing and detection environment:
- **Phishing Simulation**: generates realistic test data for validation
- **Threat Detection**: identifies and analyzes potential email threats
- **SIEM Integration**: provides centralized security monitoring capabilities

**Ideal for:**
- **Security awareness training** and simulation exercises
- **SIEM integration testing** and validation
- **Threat detection development** and refinement
- **Incident response workflow** automation

---
## 📥 Installation & Deployment

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/email-threat-automation.git
   cd email-threat-automation
   ```

2. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your actual credentials
   ```

4. Execute phishing simulation (optional, for testing):
   ```bash
   python send_email.py
   ```

5. Launch the monitoring and analysis system:
   ```bash
   python main.py
   ```

---
## 📊 Splunk Dashboard Implementation
The solution enables comprehensive Splunk dashboards for:
- **Email Traffic Monitoring**: Date, sender, subject, and content analysis
- **Threat Indicator Tracking**: URLs flagged by VirusTotal scanning
- **Attachment Analysis**: Malicious file detection statistics and trends
- **Real-Time Alerting**: Automated correlation with existing security data

---
## ✅ Conclusion
This project provides a **production-ready framework** for building automated email security pipelines using **Python, VirusTotal, and Splunk**. It demonstrates practical implementation of security automation that proactively defends against **email-borne threats** through continuous monitoring, threat intelligence integration, and centralized SIEM correlation.

The solution offers organizations a scalable blueprint for enhancing their email security posture through automation, structured analysis, and integrated security monitoring.