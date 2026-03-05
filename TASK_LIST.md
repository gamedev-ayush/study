# Multimodal Study Hub — Task List

## Phase 1 — Planning
- [x] Define technical architecture for frontend/backend/AI integration.
- [x] Draft API surface for upload, context, and chat operations.
- [x] Establish milestone sequence and acceptance criteria.

## Phase 2 — Scaffolding
- [ ] Initialize React app with Tailwind CSS.
- [ ] Initialize FastAPI backend service.
- [ ] Add environment config for Gemini API key and model names.
- [ ] Create `uploads/` directory and file-management utilities.
- [ ] Install PDF/rendering and parsing dependencies.

## Phase 3 — Development
- [ ] Build split-pane Study Mode layout.
- [ ] Implement PDF upload + viewer with selectable text layer.
- [ ] Implement floating Ask AI button for highlighted text.
- [ ] Wire selected text to chat auto-submit flow.
- [ ] Build persistent chat thread UI with markdown-safe rendering.
- [ ] Implement image upload and preview in chat composer.
- [ ] Add backend PDF parsing and per-document context cache.
- [ ] Add chat endpoint integrating Gemini text + vision requests.
- [ ] Connect frontend chat client to backend endpoints.

## Phase 4 — Verification
- [ ] Run backend + frontend locally.
- [ ] Upload test PDF and confirm render + text select behavior.
- [ ] Verify Ask AI sends selected text and returns contextual answer.
- [ ] Verify image upload yields multimodal analysis response.
- [ ] Capture browser recording artifact for the full verification flow.

## Risks / Notes
- PDF text selection behavior may vary by library and PDF encoding quality.
- Gemini model naming/version may require environment-specific fallback.
- Large PDFs should use chunking/summarization to avoid context overrun.
