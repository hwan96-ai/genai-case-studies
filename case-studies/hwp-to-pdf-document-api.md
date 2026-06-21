# HWP/HWPX to PDF Document Workflow API

## One-line Summary

A concise supporting proof for packaging a Korean HWP/HWPX document-conversion workflow as a FastAPI PoC.

## Why It Exists

Korean business workflows often depend on document formats and office automation constraints that do not fit generic web-service assumptions. A consultant still needs to package those workflows into a reviewable API or PoC surface.

This mini case exists to show document workflow automation and API packaging literacy, not GenAI or RAG capability by itself.

## What I Built / Did

- Packaged a FastAPI-based prototype for converting HWP-family documents to PDF.
- Framed the work around Korean document workflow automation and business-process PoC needs.
- Documented setup, run steps, conversion flow, supported file-family scope, and platform requirements.
- Replaced unsafe local-machine and private-network examples in public-facing documentation with safer generic wording.
- Added public limitations around Windows, local office automation, environment review, and deployment constraints.

## How It Works (from the public repository)

These details are grounded in the public repository (`hwan96-ai/hwp-to-pdf-api`) and contain no secrets, internal endpoints, or customer data.

- **Stack**: Python 3.12 + FastAPI (served by uvicorn). Conversion is driven through `pywin32` COM automation against a locally installed Hancom Office (한컴 오피스 2024) — there is no pure-Python HWP renderer, so the work is fundamentally Windows + office-automation bound.
- **Platform**: designed to run on an AWS EC2 Windows Server instance (the service's own description targets "EC2 Windows"). This is a PoC host pattern, not a hardened hosted service.
- **The core hurdle — bypassing the Hancom security dialog**: headless HWP automation normally triggers a blocking "file path security" modal that breaks server-side conversion. The converter registers a `FilePathCheckerModule` (a committed DLL) via an `HKCU` registry key plus `RegisterModule('FilePathCheckDLL', ...)` so the COM call can open files without the prompt. This registry/DLL step is the main engineering obstacle for unattended HWP→PDF on a server.
- **Conversion flow**: instantiate the `HWPFrame.HwpObject` COM object → register the file-path-check module → `Open(input)` → set the save format to PDF (`HFileOpenSave.Format = 'PDF'`) → execute `FileSaveAs_S` → `Quit()`.
- **Process isolation & reliability**: each request runs the converter as a separate subprocess (one COM instance per request, 120s timeout); uploaded inputs are deleted after conversion; a background thread restarts the server every 24h to contain COM/memory drift; uploads are capped at 50MB.

### API shape

| Method · Path | Purpose |
| --- | --- |
| `POST /convert` | Single multipart file → JSON `{status, job_id, pdf_filename, pdf_size_mb, conversion_time_seconds, download_url}` |
| `POST /convert-batch` | Multiple files in one call |
| `GET /download/{filename}` | Retrieve the generated PDF |
| `GET /health` | Liveness check |

Input formats: `.hwp`, `.hwpx`, `.hwt`, `.hwtx`. Interactive API docs are exposed at `/docs`.

## What It Proves

- Ability to turn a Korean document workflow into an API-shaped PoC.
- Practical understanding of document conversion constraints and environment dependencies.
- Backend/API packaging skill useful for consulting prototypes.
- Public documentation cleanup judgment for sensitive local path and network examples.
- Supporting credibility for business workflow automation work.

## What It Does Not Prove

- GenAI, RAG, or model-evaluation capability by itself.
- Production-grade hosted conversion service readiness.
- Security, compliance, scalability, or reliability completeness.
- Customer impact, adoption, or cost savings.
- Cross-platform portability.

## Limitations

- Platform-specific automation with Windows and local office dependencies.
- Prototype-level public evidence.
- Security and deployment posture must be reviewed per environment.
- No benchmark, throughput, reliability, or production usage claims.
- CORS is wide-open (`allow_origins=['*']`) and the converter assumes a single host with Hancom installed — both are PoC-level choices that need hardening before any shared or public deployment.
