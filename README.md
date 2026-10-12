# Sayed Salih Mahmoud — Academic Website

A 15-page static HTML academic website, with all 14 CV sections in the same order and Decap CMS content management.

## Preview locally

Run `python -m http.server 8000` from this directory, then open `http://localhost:8000/`.
Do not open the HTML files using `file://`, because the content is loaded using `fetch()`.

## Publish on GitHub Pages

1. Create a GitHub repository and upload the contents of this folder to its `main` branch.
2. In Settings → Pages, select Deploy from a branch, branch `main`, folder `/ (root)`.
3. Open the published Pages address. The site works from either the root or a repository subpath.
4. Configure Decap CMS authentication **before** trying to sign in.

## Secure Decap CMS sign-in — required deployment step

GitHub Pages cannot run a GitHub OAuth backend. **The included admin dashboard is not ready for sign-in until you configure an external OAuth provider.**

1. Choose an OAuth provider compatible with the Decap GitHub backend, such as a trusted hosted provider or a Cloudflare Worker OAuth proxy. Official reference: https://decapcms.org/docs/github-backend/ and https://decapcms.org/docs/backends-overview/.
2. Create the GitHub OAuth App as required by that provider, register its exact callback URL and store the client secret **only on the server/provider**, never in this repository or browser JavaScript.
3. Edit `admin/config.yml` and replace `salihsayd-lab/sayed-academic-website` with the actual `owner/repository` identifier, including capitalization.
4. Add `base_url` and `auth_endpoint` under `backend` as specified by your selected OAuth provider. Do not copy an unverified sample domain.
5. Keep the GitHub repo and account protected with 2FA. Grant push access only to yourself. Do not enable open authoring. Keep OAuth credentials out of Git.
6. Commit the configuration change and access `/admin/` on your Pages website. Log in with the GitHub account that has write access. After saving entries, GitHub Pages republishes the site.

**Security model:** `/admin/` is a public URL with an OAuth sign-in screen, not a private web page. Editing is restricted by authentication and GitHub repository write permissions. Page text, CV, and uploaded assets published on GitHub Pages are public.

## Editing content

Use the CMS `CV Sections` collection to update the entries in each CV section. Use `Home page and contact` to change headline details or profile links. Entries are stored in `content/*.json`. The Home overview is automatically drawn from those files, so edits appear in both overview and dedicated pages.

The navigation structure is deliberately fixed to match the original CV. To add or remove CV pages, update `content/sections.json`, create/remove an HTML page and CMS collection entry as appropriate.

## CV accuracy and unresolved information

- Google Scholar h-index is 12 in Summary of Qualifications, but 11 in List of Publications. Both are preserved unchanged in their sections.
- In the source DOCX, some publication citations contain links, but most provide no DOI; no missing links were fabricated.
- The publication list has year-based reverse chronology, but within-year order cannot be confirmed without dates.
- 'Gen AI and in MIS' under Research Areas appears incomplete; retained as written.
- Workshop 'UTM Engineering-Industry Innovation Day' includes a year 2019 and a separate line with 11 September 2011; retained unchanged.
- Certification table includes missing provider/duration values; retained without guessing.
- Personal information under Additional Information (date of birth and nationality) is included because the CV contains it; remove it before publishing if you do not want it public.
- Some entries use line breaks inside a paragraph, and training data is presented as row text to preserve the source content.
- The original CV names the Research/Working section exactly as 'Working and research Experience'.
- The profile photo is a placeholder; no photograph has been assumed.

## File organization

- `index.html` — Home overview
- `*.html` — 14 dedicated section pages
- `assets/style.css` — shared responsive styling
- `assets/site.js` — plain JavaScript rendering and navigation
- `assets/Sayed-Salih-Academic-CV.docx` — CV download
- `content/site.json`, `content/sections.json`, `content/*.json` — editable source content
- `admin/index.html`, `admin/config.yml` — Decap CMS interface and GitHub backend configuration

## This configured repository
- Repository: https://github.com/salihsayd-lab/sayed-academic-website
- Website (once GitHub Pages is enabled): https://salihsayd-lab.github.io/sayed-academic-website/
- CMS login page (after OAuth configuration): https://salihsayd-lab.github.io/sayed-academic-website/admin/

## Profile photograph

The homepage uses `assets/profile-photo.jpg`, supplied as the second uploaded portrait. The first uploaded image is not included. You can replace the photo through **Admin → Home page and contact → Academic profile → Profile photograph** once GitHub OAuth is configured.
