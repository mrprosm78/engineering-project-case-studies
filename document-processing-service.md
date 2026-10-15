# Document Processing Service

## The problem

Care organisations receive documents in different formats and from different sources. Staff need the original file, useful extracted details and a clear review path when the document or its owner cannot be identified reliably.

## The solution

A separate Python processing service accepts documents, extracts text and proposes metadata for review. A connector in the care application receives results and keeps the original document in its own storage. Processing, delivery acknowledgement and final filing are distinct steps.

## How the workflow is designed

1. An authorised source submits a PDF, image or supported document file.
2. The service extracts text using direct PDF extraction or OCR, with configurable engines including RapidOCR and Tesseract.
3. Rules, approved layouts and configured model profiles can propose document type and field values. Unknown values remain unknown; uncertain results go to review.
4. A queued delivery sends the result and original through an authenticated connection. The receiver records durable receipt before acknowledging delivery.
5. The care application confirms the destination and handles its own document and staff records.

## Engineering detail

- FastAPI processing endpoints, job queue and review states
- OCR engine selection, document-type layouts and operator correction workflow
- Per-connection access, bounded uploads, short-lived mobile upload sessions and signed delivery
- Retry and acknowledgement handling that preserves an original when delivery fails
- Separate local/VPS container packaging and operational health checks

## Technologies

Python, FastAPI, RapidOCR, Tesseract, PDF extraction, Docker Compose, PHP connector and web interfaces.

## Status and outcome

Project handoff notes record a dedicated hosted scanner container and later local UI and integration work. They also record synthetic tests and browser checks. Complete automatic filing, validated accuracy across real documents and deployment of all local changes are not claimed.

