# Lightweight Voice Memo Uploader – Implementation Plan

## Product Goals
- Allow podcast guests to upload large voice memo files from mobile devices with clear status feedback.
- Deliver uploaded assets to Cloudflare R2 storage and notify internal staff through email (with direct download links) as well as the guest when the file is available.
- Embed the experience seamlessly inside a Ghost-powered site without requiring guests to leave the host domain.

## Target Users & Flows
1. **Guest upload journey**
   - Follow a Ghost page link, review simple instructions, select a file (iOS/Android voice memos).
   - See file validation (size, type) and an upload progress indicator.
   - Receive confirmation on-screen and via email when upload completes.
2. **Admin follow-up**
   - Receive an email containing the guest’s metadata plus a direct, signed link to the R2 object.
   - Optionally review upload logs/metrics within Cloudflare.

## Architecture Overview
- **Ghost front-end embed** renders a minimal uploader widget inside a Ghost template/partial so editors can drop it into any post or landing page (`knowledge/ghost/theme-structure.md:96`, `knowledge/ghost/theme-structure.md:117`, `knowledge/ghost/theme-structure.md:144`).
- **Cloudflare Worker** serves the upload API, parses `multipart/form-data`, coordinates multipart uploads to R2, and triggers notifications (`knowledge/cloudflare-workers/handle-form-submissions.md:874`, `knowledge/cloudflare-r2/multipart-from-workers.md:132`).
- **Cloudflare R2** stores objects in a dedicated bucket with scoped tokens and CORS configured for the Ghost origin (`knowledge/cloudflare-r2/overview.md:141`, `knowledge/cloudflare-r2/overview.md:152`, `knowledge/cloudflare-r2/upload-objects.md:133`).
- **Email Routing + Workers binding** dispatches admin/guest notifications via `send_email` bindings after successful uploads (`knowledge/cloudflare-email/email-workers.md:72`, `knowledge/cloudflare-email/email-workers.md:103`, `knowledge/cloudflare-email/email-workers.md:135`).

## Implementation Phases for the Implementer Agent
1. **Foundation**
   - Provision R2 bucket, configure CORS to accept the Ghost site origin, and generate scoped API tokens.
   - Bootstrap Worker project (`wrangler.toml`, `package.json`) with R2 + `send_email` bindings as outlined in the bindings docs (`knowledge/cloudflare-workers/bindings.md:456`).
   - Define environment variables (admin email, reply-to, allowed MIME types, max size).
2. **Upload API**
   - Build Worker endpoints for:
     - `POST /upload/init` to return upload session metadata (presigned part URLs or Worker-managed uploadId).
     - `POST /upload/part` to stream parts via Worker to R2 using the multipart API (`knowledge/cloudflare-r2/multipart-from-workers.md:136`).
     - `POST /upload/complete` to finalize multipart uploads and persist object metadata.
   - Validate file size/type server-side; tag objects with metadata (guest name, email, timestamp).
3. **Ghost Embed UI**
   - Create a responsive HTML/JS widget (e.g., vanilla JS or lightweight framework) that:
     - Provides drag/drop and file picker support.
     - Shows progress per part and overall completion status.
     - Captures guest name/email (for notifications) before starting the upload.
   - Package as a partial or custom template that Ghost editors can include (e.g., `partials/upload-widget.hbs`).
4. **Notifications & Confirmation**
   - Implement Worker logic to trigger admin + guest emails after upload completion, including R2 object link (use short-lived signed URL).
   - Render confirmation screen with download ETA and email sent message.
5. **Operational Hardening**
   - Add server-side logging (Cloudflare Logs or Analytics) for traceability.
   - Record uploads in R2 object metadata or KV for deduplication/resume support.
   - Write smoke tests using `python3 -m compileall` and Worker unit tests (Miniflare/Vitest).
   - Document manual verification (CLI upload test, Ghost embed test, email receipt).

## Integration & Deployment Notes
- Ghost pages can include the uploader via a custom template (`post.hbs` variant) or by injecting a partial into `default.hbs` for reusable blocks (`knowledge/ghost/theme-structure.md:117`, `knowledge/ghost/theme-structure.md:144`).
- Configure Ghost to load the uploader bundle from a static asset path (e.g., Worker served static JS) and ensure CSP allows POST requests to the Worker domain.
- Use Wrangler deployments with environments (`wrangler publish --env production`) to separate staging from production.
- Automate signed download links by leveraging R2’s S3-compatible `GetObject` presign flow and limiting expiry durations (`knowledge/cloudflare-r2/s3-api.md:143`, `knowledge/cloudflare-r2/s3-api.md:169`).

## Security & Compliance Considerations
- Enforce file size caps client- and server-side; reject unexpected MIME types.
- Generate per-upload object keys that avoid PII; metadata should store contact info if necessary.
- Ensure emails contain only necessary data; avoid exposing raw R2 bucket names in guest-facing links.
- Maintain audit logs for uploads to satisfy data retention policies and enable delete-on-request workflows.

## Future Enhancements
- Add optional guest consent checkbox and integrate with CRM or project management tools.
- Provide admin dashboard (Workers + KV/D1) for managing incoming submissions.
- Support direct mobile recording via MediaRecorder API for guests without saved memos.

## Handoff Checklist for Implementer Agent
- [ ] `wrangler.toml` with R2 + `send_email` bindings checked into repo (sans secrets).
- [ ] Worker endpoints implemented with validation and multipart support.
- [ ] Upload widget embedded in Ghost theme/partial with responsive styles.
- [ ] Email templates tested and documented with sample payloads.
- [ ] README updates describing deployment steps, environment variables, and manual QA scenarios.
