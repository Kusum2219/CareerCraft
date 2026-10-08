The Problem

Important college information (exam form dates, fee deadlines, placement drives, scholarship notices) is scattered across WhatsApp groups, PDF circulars, scanned images and notice boards. Students miss deadlines because:

Notices are long, unstructured and often posted as images or PDFs
Most notices are irrelevant to a given student's branch, year or CGPA
There is no single place that tracks "what do I need to do, and by when?"
The Solution

NoticeFlow ingests notices from multiple sources, extracts the actionable details with an LLM, validates them against a strict schema, filters them by each student's profile, and pushes only the relevant items to the student's calendar and reminders. Low-confidence extractions go to a human reviewer instead of being silently trusted.

Features
Multi-source ingestion: PDF upload, image upload (OCR), pasted text / exported chat, and optional website scraping
Structured extraction: event title, category, deadline, eligibility (branch / year / CGPA), required documents and links
Schema validation and confidence scoring: invalid or low-confidence output is never auto-published
Human-in-the-loop review queue: an admin or CR approves, edits or rejects uncertain extractions
Personalized filtering: deterministic rules match notices to a student's profile (no LLM guessing for eligibility)
Calendar and reminders: Google Calendar events plus email / Telegram reminders at configurable intervals
Duplicate detection: the same notice reposted in five groups creates one event
Dashboard: upcoming deadlines, missed items, and extraction accuracy stats
Architecture
High confidence
Low confidence
Sources: PDF / Image / Text/ Web
Ingestion + OCR
LLM Extraction
Schema Validation +Confidence Score
PostgreSQL
Review Queue
Eligibility Rules Engine
Calendar + ReminderService
Web Dashboard

Key design principle: the LLM is used only for understanding unstructured text. Eligibility matching, deduplication and scheduling are plain, testable code.

Tech Stack
Layer	Technology
Frontend	React + Vite, Tailwind CSS
Backend	FastAPI (Python)
Database	PostgreSQL (Neon / Supabase)
OCR / Parsing	Tesseract or a vision LLM, PyMuPDF
LLM	Gemini / Claude / OpenAI API (configurable)
Validation	Pydantic
Integrations	Google Calendar API, Telegram Bot API, SMTP
Testing / CI	pytest, GitHub Actions
Deployment	Vercel (frontend), Render / Railway (backend)
