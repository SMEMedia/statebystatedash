# State by State Manufacturing Dashboard

This is SME Media's internal reporting dashboard for the **State by State of the Manufacturing Industry** program on [AdvancedManufacturing.org](https://www.advancedmanufacturing.org/states-of-the-industry/).

The dashboard brings website, social media, advertising, sponsor, and state-level performance into one place. It is built with Streamlit and is intended to be usable by editorial, audience, marketing, and sales teams without needing to understand the code.

## Quick start for dashboard users

1. Open the Streamlit dashboard link supplied by the dashboard owner.
2. Choose a **Start date** and **End date** in the left sidebar.
3. Move between the tabs at the top of the dashboard.
4. Use **Refresh connected data** when you need to clear the one-hour cache and request fresh data from the connected services.

Nothing needs to be installed to use the published dashboard in a web browser.

> GA4 data can take 24–48 hours to finalize. Very recent numbers may increase after Google finishes processing them.

## What each tab does

### National overview

Provides the overall picture of State by State readership:

- Active users, pageviews, sessions, and engagement rate
- Number of states receiving traffic
- Monthly audience trend
- A locked U.S. map showing traffic by state
- A state leaderboard for quick comparison

### State explorer

Lets you select one state and review its performance:

- Users, pageviews, sessions, and engagement rate
- Individual articles responsible for that state's traffic
- Direct links to open the articles on AdvancedManufacturing.org

### Social performance

Combines matching State by State posts from Facebook and Instagram:

- Facebook and Instagram follower counts
- Number of campaign posts found
- Likes, reactions, comments, shares, saves, views, and reach when available
- Post-level charts and tables
- Direct links to the original social posts

Only content identified as part of State by State is included. Social APIs do not provide every metric for every post type, so blank or zero values can be legitimate.

### Zeiss performance

Shows sponsor delivery from two different sources:

**Google Ad Manager (GAM)**

- Delivered ad impressions
- Ad clicks
- Ad click-through rate
- Line-item delivery and targeted inventory

**Google Analytics 4 (GA4)**

- Outbound clicks from State by State pages to `zeiss.com`
- Clicks to ZEISS Industrial Quality Solutions
- Clicking users and originating pages
- Destination and source-page detail

GAM ad clicks and GA4 outbound clicks measure different actions and should not be expected to match exactly. GA4 also combines the map-sign and sponsored-logo links when they use the same destination because the collected link URL is truncated and no link text is available.

### Sponsor opportunity

Provides a simple sales-planning model. Adjust:

- **Display ad opportunities per pageview:** estimated number of sponsor ad placements available each time a page is viewed
- **Expected sell-through:** percentage of the available inventory expected to be sold and delivered
- **Proposed CPM:** price charged per 1,000 billable impressions

The resulting media value is a planning estimate, not an invoice or guaranteed delivery amount.

## Plain-language metric guide

| Metric | Meaning |
|---|---|
| Active users | Estimated number of distinct people who actively used the site during the selected period |
| Pageviews | Total times State by State pages were viewed; one person can create several pageviews |
| Sessions | Visits to the site; one person can have multiple sessions |
| Engagement rate | Percentage of sessions that met GA4's engaged-session criteria |
| Impressions | Number of times an advertisement was delivered |
| Ad clicks | Clicks recorded by Google Ad Manager on an advertisement |
| Outbound clicks | Click events recorded by GA4 when someone left a State by State page for a ZEISS website |
| CTR | Click-through rate: clicks divided by impressions |
| Reach | Number of accounts estimated to have seen social content |
| Engagements | Likes/reactions, comments, shares, and saves available from the platform |
| CPM | Cost per 1,000 ad impressions |

## Data sources and update timing

| Source | Used for | Typical behavior |
|---|---|---|
| Google Analytics 4 | Website audience, state/article traffic, ZEISS outbound clicks | Recent data may take 24–48 hours to finalize |
| Facebook Graph API | Page followers and State by State post engagement | Requires a valid Page access token |
| Instagram Graph API | Followers, post reach/views, and engagement | Availability varies by media type and token permissions |
| Google Ad Manager API | ZEISS order and line-item delivery | Shows GAM delivery totals returned for the matching Zeiss line items |

Connected results are cached for one hour to keep the dashboard responsive and reduce API usage. The sidebar refresh button clears that cache.

## If something looks wrong

### A social section says data is unavailable

The Facebook or Instagram token may have expired or lost permission. Ask the dashboard administrator to replace the relevant token in Streamlit Secrets, then use **Refresh connected data**.

### GA4 does not load

Confirm that:

- The GA4 service account still has Viewer access to the Advanced Manufacturing GA4 property
- The Google Analytics Admin API and Google Analytics Data API are enabled for its Google Cloud project
- The `[gcp_service_account]` entry in Streamlit Secrets is complete

### GAM or the Zeiss section does not load

Confirm that:

- The GAM service account is an authorized user in the correct Google Ad Manager network
- The Google Ad Manager API is enabled in its Google Cloud project
- The `[gam_service_account]` entry in Streamlit Secrets is complete
- Zeiss still appears in the relevant GAM order or line-item name

### Numbers changed after an earlier report

This is normal when GA4 finalizes recent data, a platform updates attribution, or the selected date range changes. Record the date range and dashboard refresh time when sharing results.

## Administrator guide

The remainder of this document is for the person who maintains or republishes the dashboard.

### Repository contents

| File | Purpose |
|---|---|
| `app.py` | Complete Streamlit dashboard and API connections |
| `requirements.txt` | Python packages required to run the app |
| `.streamlit/config.toml` | Dashboard colors and Streamlit theme |
| `.streamlit/secrets.toml.example` | Safe template showing the required secret sections |
| `.gitignore` | Prevents credentials, caches, and local files from entering GitHub |
| `README.md` | This operating and setup guide |

The real `.streamlit/secrets.toml` file is local-only and must never be committed to GitHub.

### Required secret sections

The app expects four sections in Streamlit Secrets:

| Section | Purpose |
|---|---|
| `[gcp_service_account]` | GA4 website reporting |
| `[gam_service_account]` | Google Ad Manager reporting |
| `[meta]` | Facebook Page access |
| `[instagram]` | Instagram Business access |

Use `.streamlit/secrets.toml.example` as the structure. Replace every placeholder only in the private secrets editor or local `.streamlit/secrets.toml` file.

### Run the dashboard locally

These steps are only needed for development or troubleshooting.

1. Install Python 3.11 or newer.
2. Download or clone this repository.
3. Open PowerShell in the repository folder.
4. Install the required packages:

   ```powershell
   python -m pip install -r requirements.txt
   ```

5. Copy `.streamlit/secrets.toml.example` to `.streamlit/secrets.toml`.
6. Fill the new local file with the real credentials. Do not edit the example with real values.
7. Start the dashboard:

   ```powershell
   python -m streamlit run app.py
   ```

8. Open the local address Streamlit displays, normally `http://localhost:8501`.

### Publish or update on Streamlit Community Cloud

1. Sign in to Streamlit Community Cloud.
2. Select the app connected to the `myschne/statebystatedash` GitHub repository.
3. Confirm the branch is `main` and the entry file is `app.py`.
4. Open the app's **Settings → Secrets** area.
5. Copy the full contents of the private local `.streamlit/secrets.toml` into the cloud secrets editor.
6. Save the secrets and reboot or redeploy the app if prompted.

Pushing code to `main` normally triggers a new deployment automatically. Secrets are not transferred through GitHub and must be maintained separately in Streamlit Cloud.

## Security rules

- Never commit `.streamlit/secrets.toml`, service-account JSON files, access-token text files, or `googleads.yaml`.
- Never paste private keys or access tokens into an issue, pull request, README, screenshot, or chat message.
- Use read-only API roles where possible.
- Replace a token or key immediately if it may have been exposed.
- Keep the example secrets file limited to placeholders.

## Safe maintenance checklist

Before publishing a dashboard change:

1. Confirm no credentials appear in `git status` or the staged changes.
2. Compile the app with `python -m py_compile app.py`.
3. Open the dashboard and check all five tabs.
4. Confirm the selected date range is appropriate.
5. Verify that GA4, Facebook, Instagram, and GAM warnings are not displayed.
6. Commit and push only the intended files.

## Ownership and support

This dashboard is an internal SME Media audience-intelligence tool. Repository: [myschne/statebystatedash](https://github.com/myschne/statebystatedash).

For access, expired credentials, or reporting questions, contact the dashboard owner or the SME Media team member responsible for analytics integrations.
