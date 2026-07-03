# Compliance Report Collector (Google Form → Drive + MySQL)

This n8n workflow automates the collection and archival of compliance reports submitted via Google Forms. Uploaded documents (PDF, DOCX, etc.) are archived into Google Drive and submission metadata is logged into a MySQL database. It ensures compliance documentation is properly stored, searchable, and auditable without manual effort.

## Quick Start – Implementation Steps

1. Import the workflow JSON into n8n.
2. Set up a Google Form to POST the uploaded file and metadata (reporter, category, etc.) to the `/submit-report` webhook.
3. Update the **Set Config** node with:
   - MySQL connection details
   - Google Drive folder ID
4. Deploy the workflow and test a form submission with a file upload.
5. Each submitted report is automatically stored in Google Drive and logged in your MySQL database.

## Who’s It For

- Compliance officers handling environmental or safety reports.
- Administrators managing inspection documentation.
- Renewable energy companies maintaining audit-ready records.
- Any organization requiring structured report archival and metadata logging.

## Requirements to Use This Workflow

To run this workflow, you need:

- **[n8n account (Self-hosted or Cloud)](https://n8n.partnerlinks.io/om1efg2qgvwi)**
- **Google account** with access to Google Drive
- **MySQL database** with appropriate access credentials
- **Google Form** or HTML form for report submissions
- OAuth credentials configured for Google Drive
- MySQL credentials configured in n8n

## What It Does

This workflow automatically:

- Listens for incoming POST requests containing a file and metadata.
- Uploads the submitted file to a designated Google Drive folder.
- Extracts metadata including:
  - Reporter name
  - Category or report type
  - Submission timestamp
  - File name
  - MIME type
- Stores the metadata in a MySQL table for auditing and reporting purposes.

## Sample MySQL Table Schema

```sql
CREATE TABLE report_logs (
  id INT AUTO_INCREMENT PRIMARY KEY,
  reporter VARCHAR(100),
  category VARCHAR(100),
  timestamp DATETIME,
  file_name VARCHAR(255),
  mime_type VARCHAR(50),
  folder_id VARCHAR(100)
);
```

## Setup Steps

1. Import the workflow JSON into n8n.
2. Configure the **Set Config** node:
   - MySQL:
     - `dbHost`
     - `dbUser`
     - `dbPassword`
     - `dbName`
     - `dbTable`
   - Google Drive:
     - `driveFolderId`
3. Update your Google Form (or middleware) to submit data to the n8n webhook URL.
4. Submit a test report with a file upload.
5. Verify:
   - The file is uploaded to Google Drive.
   - A metadata record is created in MySQL.

## How To Customize

| Customization | How |
|--------------|-----|
| Add more form fields | Extend the metadata mapping in the Function node |
| Rename uploaded files | Modify the filename before the Google Drive upload |
| Send email confirmations | Add an Email node after the MySQL insert |
| Restrict file types | Add an IF node to validate MIME types before uploading |

## Add-Ons (Optional Enhancements)

| Feature | Description |
|---------|-------------|
| Email Acknowledgment | Send confirmation emails with the uploaded file link |
| PDF Parsing | Automatically extract PDF content using PDF.co or OpenAI |
| Admin Dashboard | Display report logs in Supabase or Metabase |
| File Backup | Copy uploaded files to Dropbox or Amazon S3 |

## Use Case Examples

1. Collect monthly safety audits from plant staff into a centralized Drive archive.
2. Accept vendor compliance declarations through Google Forms and automatically log them in MySQL.
3. Capture field inspection reports and organize them by category.
4. Store weekly environmental compliance reports for long-term auditing.

## Troubleshooting Guide

| Issue | Possible Cause | Solution |
|--------|----------------|----------|
| File not uploaded | Invalid Google Drive folder ID | Verify the folder ID and sharing permissions |
| Database not logging | Database connection or schema issue | Verify MySQL credentials and table structure |
| Webhook not triggered | Form not configured correctly | Ensure the form submits data to the correct n8n webhook |
| Unsupported file type | MIME type validation failed | Update the Function or IF node to allow the required file types |

## Need Help?

If you need help customizing this workflow, integrating it with your compliance management ecosystem, or extending it with dashboards, document processing, database integrations, and audit automation, our **WeblineIndia** team is ready to assist. **[Contact us](https://www.weblineindia.com/contact-us.html)** to discuss your requirements or explore our **[Process Automation Solutions](https://www.weblineindia.com/process-automation-solutions.html)** to build, customize, and scale your business automation with confidence.
