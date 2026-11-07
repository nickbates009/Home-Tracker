# Home Project Tracker — First Working Version

A mobile-first installable web app for home renovation projects. Includes seven starter projects, tasks, notes, materials, photo/PDF attachments (small local previews), progress tracking, and JSON export/import.

## What works immediately
- Open the app in Safari after hosting it over HTTPS.
- Add/edit projects; add and complete tasks; record notes and materials; attach small photos or PDFs (3 MB each maximum, with browser storage limits).
- Data persists on that device in browser localStorage. Export a backup to Files > iCloud Drive.
- Install as a Home Screen web app: Safari > Share > Add to Home Screen.
- Offline use after first successful load via service worker.

## Deploy from iPhone
1. Create a free GitHub account and a repository called `home-project-tracker`.
2. Upload the contents of this folder to the repository using GitHub's web interface (or a compatible iPhone Git client).
3. In repository Settings > Pages, deploy from the main branch root. Wait for the HTTPS Pages URL.
4. Open the URL in Safari, then Share > Add to Home Screen. Repeat on the other iPhone.

## Enable hosted project syncing (Supabase)
1. Create a Supabase project in its web dashboard.
2. In the SQL editor, run `supabase-setup.sql` in a NEW empty project. Review SQL before executing.
3. In Supabase Authentication settings, enable email/password authentication; optionally turn on email confirmation.
4. In the app Settings > Configure cloud, enter the project URL and public publishable/anon key (never service_role or secret key).
5. Register your account and sign in. Your household is created automatically.
6. Your spouse registers on their phone. After their account exists, you sign in and tap Invite household member with their email.
7. Both users sign in. Project records sync on changes and when the app is opened; use Sync now to refresh manually.

**Important prototype limitations**
- The cloud implementation is a basic whole-household JSON record with last-write-wins synchronization. Simultaneous edits on two devices may overwrite one another; coordinate edits and tap Sync now before editing. It is not yet production-grade conflict resolution or real-time collaboration.
- Project records (projects/tasks/notes/materials) sync through Supabase. Image/PDF previews are **local only**, not shared automatically. Save full originals into the shared iCloud Drive folder using Files; browse them there. This first version does not have automatic iCloud Drive integration (web apps cannot silently access shared iCloud folders).
- localStorage is size-limited and may be cleared by the browser. Keep JSON backups in iCloud Drive. Files included in JSON backups can make the backup large.
- The app cannot be opened reliably by tapping index.html in Files; it must be hosted on HTTPS for installability and offline caching.
- The starter data on two separately initialized devices should not be merged automatically; sign in and sync before adding data on the second phone.
- If your Supabase account was created *before* running the SQL, the signup trigger will not create a household for that account. Create accounts after SQL setup.
- For a production release, add per-record sync, conflict resolution, durable attachment storage, permission roles, and automated backups.
