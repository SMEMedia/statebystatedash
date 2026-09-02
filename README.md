# State by State Manufacturing Dashboard

This dashboard brings website, social, advertising, sponsor, and state-level performance for the **State by State of the Manufacturing Industry** program into one place.

## Important links

- [Open the State by State Dashboard](https://statebystate.streamlit.app/)
- [State by State program](https://www.advancedmanufacturing.org/states-of-the-industry/)
- [SMEMedia repository](https://github.com/SMEMedia/statebystatedash)

## Use the dashboard

1. Choose the start and end dates.
2. Move among **National overview**, **State explorer**, **Social performance**, **Zeiss performance**, and **Sponsor opportunity**.
3. Select **Refresh connected data** when a fresh pull is needed.

Connected results are temporarily saved to keep the dashboard responsive. GA4 can take 24–48 hours to finalize, so recent numbers may increase.

## What each section shows

- **National overview:** audience totals, trends, map, and state leaderboard.
- **State explorer:** performance and articles for an individual state.
- **Social performance:** matching Facebook and Instagram posts and available engagement.
- **Zeiss performance:** Google Ad Manager delivery and GA4 outbound clicks.
- **Sponsor opportunity:** adjustable planning estimates for inventory and media value.

Google Ad Manager clicks and GA4 outbound clicks measure different actions and should not be expected to match exactly. Sponsor-opportunity values are estimates, not invoices or guaranteed delivery.

## Troubleshooting

### GA4 information does not load

- Refresh once.
- Confirm whether all website sections or only one state are affected.
- Ask the analytics and Streamlit owners to verify the dashboard’s GA4 access.
- Provide the selected dates, affected section, time, and screenshot.

### Facebook or Instagram information is unavailable

- Confirm the date range includes campaign posts.
- Refresh once.
- If the message remains, ask the Meta and Streamlit owners to check the saved connection and account permissions.

### Zeiss advertising information is missing

- Confirm the selected dates include delivery.
- Check whether Zeiss still appears in the relevant Google Ad Manager order or line-item name.
- Compare the same period in Google Ad Manager.
- Send the order or line-item name, date range, and screenshot to support.

### GAM clicks and GA4 outbound clicks do not match

This is expected because the systems count different actions. Confirm the same dates are selected, then report both figures with their source labels rather than treating one as a correction to the other.

### A state or article is missing

- Confirm the date range includes its activity.
- Search for alternate state or article naming.
- Check that the article belongs to the State by State program.
- Allow recent GA4 information time to finalize.

### Numbers changed after an earlier report

- Confirm identical dates and filters.
- Check when each report was refreshed.
- Use finalized periods for recurring reporting when possible.
- Record the original and current values before escalating.

### The dashboard will not open

- Use the live link above.
- Refresh the browser or try a private window.
- Check [Streamlit Community Cloud](https://share.streamlit.io/) for an app status message.
- Send the visible error and approximate time to the Streamlit owner.

## Ongoing maintenance

- Record the selected dates and refresh time when sharing results.
- Keep GA4, Meta, Google Ad Manager, Streamlit, and repository access assigned to current SME staff.
- Treat sponsor-opportunity results as planning estimates.
- Escalate credential, source-mapping, deployment, and code changes to the assigned technical owner.

*** Delete File: VideoDash/README.md
