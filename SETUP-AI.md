# Builder real-stack setup

This package contains the polished frontend plus the server-side foundation for the checklist.

1. Supabase: create a project.
2. Supabase Auth: enable Email. Google can be added after basic auth works.
3. Supabase SQL Editor: run `supabase/schema.sql`.
4. Storage buckets `builder-attachments` and `builder-assets` are created by the schema and are private.
5. Copy `config.example.js` to `config.js`. Put only your Supabase project URL and publishable key there.
6. Supabase Function Secrets: set `GEMINI_API_KEY`, `GEMINI_MODEL=gemini-3.8-flash`, `GEMINI_EMBED_MODEL=gemini-embedding-001`, `SUPABASE_SERVICE_ROLE_KEY`. Keep all of these server-side.
7. Deploy functions: `supabase functions deploy ai`, `agent`, `research`, `github`, `deploy`.
8. AI function supports classify, plan, generate, stream, vision, embed, and grounded research.
9. Agent function performs inspect → snapshot → AI operations → safe-path/secret validation → retry once → persist files → record result.
10. Frontend still has localStorage as a safe fallback; next wiring step changes project CRUD/messages/files to Supabase calls. This avoids breaking the demo if the user opens the site before credentials exist.
11. Preview: generated web projects should target `index.html`, `styles.css`, `app.js`; render them in a sandboxed iframe. A full Node/React build runner is a later isolated worker.
12. Research uses Gemini Google Search grounding and stores returned sources against the project. Add a second search provider later behind the same interface for redundancy.
13. GitHub requires a GitHub OAuth App and server-side token storage before repo/branch/commit actions are enabled.
14. Cloudflare requires API token + account ID; deployment should be gated on tests/security. Cloudflare supports Git-connected deployments as well as project/deployment APIs.
15. Payments stay out until everything above is green.

Do not paste secret keys into chat.
