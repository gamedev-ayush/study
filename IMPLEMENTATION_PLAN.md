# Multimodal Study Hub — Implementation Plan

## Phase 1: Planning (Current Deliverable)
Define architecture, delivery milestones, and acceptance criteria before writing feature code.

## Proposed Architecture

### Frontend (React + Tailwind)
- **Split-pane Study Dashboard**
  - Left pane: PDF viewer with text-selection support.
  - Right pane: persistent AI chat panel.
- **PDF Rendering Layer**
  - Use `react-pdf` + `pdfjs-dist` (or `@react-pdf-viewer/core` if selection behavior is better during implementation).
- **Highlight-to-Ask UX**
  - Detect selected text in PDF text layer.
  - Show floating **Ask AI** action button near selection.
  - On click: inject prompt in chat input and submit automatically.
- **Multimodal Chat UX**
  - Text input + image upload button.
  - Message bubbles supporting text and image thumbnails.

### Backend (FastAPI)
- **Upload endpoints**
  - Store chapter PDFs + user images in local `uploads/` workspace directory.
- **PDF ingestion + context extraction**
  - Parse PDF text and cache per-document context.
- **Chat endpoint**
  - Accept conversation, selected quote, active PDF ID, and optional image.
  - Build prompt with PDF context and user message.
  - Call Gemini 3 Pro (and Gemini Vision-capable model path for image content).

### Data Flow
1. User uploads/selects PDF.
2. Backend parses + stores text context.
3. User highlights text in viewer → clicks Ask AI.
4. Frontend sends selected text + PDF reference to chat endpoint.
5. Backend composes contextual prompt and returns answer.
6. If image attached, backend includes image bytes/media part for multimodal reasoning.

## API Contract (Draft)
- `POST /api/upload/pdf` → `{ pdf_id, filename, page_count }`
- `POST /api/upload/image` → `{ image_id, filename, url }`
- `GET /api/pdf/{pdf_id}/context` → `{ text_excerpt | metadata }` (internal/debug)
- `POST /api/chat` → `{ answer, citations?, usage? }`

## Delivery Milestones
1. Scaffold frontend/backend workspaces + dependencies.
2. Implement split-pane UI and persistent chat shell.
3. Integrate PDF rendering + text selection detection.
4. Implement Ask AI trigger from selection.
5. Implement uploads pipeline (`uploads/`).
6. Implement backend PDF parsing + context cache.
7. Implement Gemini integration (text + image).
8. E2E verification in browser with sample PDF + selection flow.

## Acceptance Criteria
- PDF + chat visible simultaneously in responsive split-pane.
- Highlighting text shows Ask AI button and auto-sends quote to chat.
- AI replies are context-aware to active PDF content.
- Image upload in chat works and model analyzes diagram/handwriting content.
- Uploaded files persist under local `uploads/`.
- Manual browser verification confirms end-to-end flow.
