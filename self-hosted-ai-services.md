# Self-hosted AI and Container Services

## The problem

Document extraction and automation experiments need repeatable environments where OCR, language-model and speech services can be tested separately, with access controls and a clear route from local development to hosted use.

## The solution

A VPS was configured with Docker Compose services and an HTTPS reverse proxy. A document-processing prototype separates OCR, a local-model API, speech-to-text and an internal dashboard into distinct containers. Other applications are deployed in their own projects rather than sharing a single runtime.

## Engineering detail

- Python/FastAPI wrappers for OCR, LLM formatting and speech-to-text test APIs
- Docker Compose services with loopback-bound application ports and health checks
- Local testing with multiple open-weight language models
- A separate faster-whisper speech service and an OCR service using RapidOCR/Tesseract and document parsers
- Caddy HTTPS routing, firewall setup and application isolation documented for the VPS
- Local comparison of alternative OCR/model approaches before choosing a default for a given workload

## Technologies

Ubuntu, Docker, Docker Compose, Caddy, Python, FastAPI, Ollama, open-weight LLMs, OCR and faster-whisper.

## Status and outcome

The project records describe working **test services and prototypes**, including hosted OCR, LLM, speech and dashboard components. A finished commercial document platform, production capacity and benchmarked accuracy are not claimed.

