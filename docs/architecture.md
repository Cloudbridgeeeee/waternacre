# WaterNacre — proposed AWS architecture

WaterNacre uses AWS to read field reports at scale, classify issues and keep a reliable maintenance history — encrypted and separated per operator.

## Request flow

1. Field reports
2. Amazon S3
3. Textract
4. Bedrock
5. Engineer review
6. DynamoDB
7. Maintenance tasks

## Services

### Amazon Textract

**Role:** Read inspection reports

Extracts text, tables and checkbox answers from scanned field forms and PDFs, including handwritten notes, so every report becomes structured data.

### Amazon Bedrock

**Role:** Classify issues and summarise

Classifies findings into your maintenance categories, suggests severity with the supporting sentence, and drafts monthly recurring-defect summaries for review.

### Amazon S3

**Role:** Archive original reports

Keeps every original report and photo encrypted and versioned — the permanent record behind each asset history.

### Amazon DynamoDB

**Role:** Store assets, issues and tasks

Holds assets, extracted findings, classifications, review decisions and maintenance tasks with fast reads for dashboards.

### AWS Lambda

**Role:** Orchestrate the pipeline

Runs extraction and classification for each upload, links findings to assets and creates tasks once issues are confirmed.

## Principles

- **Originals preserved** — Every source report is kept exactly as received.
- **Engineers confirm** — Classifications guide planning only once reviewed.
- **Operator separation** — Each utility’s data is isolated and encrypted.

## Safeguards

- **Engineers decide** — Classifications and severities are suggestions until an engineer confirms them.
- **Not a control system** — WaterNacre works with records. It doesn’t operate pumps, valves or treatment processes.
- **Evidence shown** — Every classification shows the sentence in the report it was based on.
- **Critical-infrastructure care** — Encryption, access control and audit logs protect sensitive asset data.

## MVP scope

We digitise and classify a year of inspection reports for one zone or asset class, build asset histories and deliver a maintenance dashboard your engineers review weekly.

- Report upload and extraction
- Issue classification with review
- Asset maintenance histories
- Recurring defect dashboard
- Basic task tracking
