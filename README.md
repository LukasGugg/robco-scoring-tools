# Hosting the Scoring Tools on GitLab Pages

Three files here: `index.html` (Concept scorer), `admin.html` (admin panel),
`phase-scorer.html` (Design/Execution, phase dropdown built in). All three
point at the same unified Apps Script backend — nothing about hosting them
changes that.

## One-time setup

1. **Check with IT first** (Igor, per the meeting notes) whether GitLab Pages
   is enabled on RobCo's GitLab instance. On gitlab.com it's on by default;
   on self-hosted instances an admin has to turn it on. If it's not enabled,
   nothing below will work, and that's a config issue on the instance, not
   something wrong with these files.
2. Create a new GitLab project (e.g. `nudd-scorer`), visibility can be
   Internal or Private (unlike GitHub Pages, GitLab Pages can serve private
   projects to logged-in members only, depending on instance settings — a
   nicer fit than GitHub's "must be public" requirement).
3. Upload all four files in this folder (`index.html`, `admin.html`,
   `phase-scorer.html`, `.gitlab-ci.yml`) via the GitLab web UI —
   **Repository → Files → Upload file**, or drag-and-drop in the Web IDE.
   Commit directly to your default branch (usually `main`).
4. GitLab automatically runs the CI pipeline on that commit (**CI/CD →
   Pipelines** to watch it). Once it succeeds, **Deploy → Pages** in the
   project sidebar shows your live URL.
5. URL pattern is usually `https://<namespace>.pages.<gitlab-domain>/<project>/`
   for self-hosted instances, or `https://<namespace>.gitlab.io/<project>/`
   on gitlab.com — check the Pages settings page for the exact one, it varies
   by instance configuration.
   - Concept scorer: that URL directly (`index.html` is the default page)
   - Admin panel: same URL + `admin.html`
   - Design/Execution: same URL + `phase-scorer.html`

## Embedding in Notion / ClickUp

Same as before — Notion's `/embed` block or ClickUp's Dashboard "Embed"
widget, pointed at the live Pages URL. Nothing GitLab-specific here.

## Updating later

Whenever a tool changes:
1. Get the updated file.
2. Upload it again with the same filename (overwrite) via the GitLab web UI,
   or edit directly in GitLab's built-in editor.
3. The CI pipeline reruns automatically on commit — Pages republishes within
   a minute or two.
4. Notion/ClickUp show the new version immediately, since they're just
   iframing the live URL — nothing to touch there.

No command line needed anywhere in this flow; everything works through the
GitLab website. `.gitlab-ci.yml` only needs to exist once — you don't touch
it again unless you're adding more files to publish.
