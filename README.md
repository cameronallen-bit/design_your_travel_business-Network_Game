# Design Your Travel Business (concept beta)

A one-minute phone page for the Avoya Travel Network. Pick a specialty, your clients, your hours, your workspace and your signature touch, then name the agency. You leave with a shareable agency card ("Booked from my kitchen table, mornings only."), a line for every pick on how Avoya backs it, how the network works, and an optional two-step form for the recruiting team.

Built on the advisor quiz's engine ([could_you_be_a_TA-Network_Game](https://github.com/cameronallen-bit/could_you_be_a_TA-Network_Game)): the REST store, the retry outbox, attribution, cohorts, the form and the admin page. One self-contained `index.html`, no build step for the site and no dependencies for visitors (the admin page loads the Firebase SDK; the ad pixel loads only if an ID is set). The illustrations are original, drawn in code for this page.

## Links

| What | Address |
| --- | --- |
| The designer | https://cameronallen-bit.github.io/design_your_travel_business-Network_Game/ |
| Pilot link (staff, friends and family; counted) | `…/?c=pilot` |
| Advisor link (working Avoya advisors; kept out of the crowd numbers) | `…/?c=advisor` |
| Test mode (real database, nothing counts, leads marked test) | `…/?test=1` |
| Demo mode (nothing leaves the browser) | `…/?demo=1` (add `&seed=200` to preview the crowd lines) |
| Admin page | `…/?role=admin` (demo data: `…/?role=admin&demo=1`) |
| Share previews | `…/r/ocean.html`, `river`, `luxury`, `expedition`, `tours`, `resorts`, `lastminute`, `accessible` (each forwards to the designer with the shared design) |

## Setup still to do

1. **Database rules.** Firebase console, project `price-is-fright`, Realtime Database, Rules. Inside `"rules"`, beside the `priceIsFright` block (and Choc Trivia's, and the quiz's `advisorQuiz` once it's in), paste the `"agencyDesigner": { … }` block from `database.rules.json`. Leave out its two root lines (`".read": false`, `".write": false`). Publish. Until then the page works end to end, but counters, designs and leads are refused (each visitor's device keeps them and retries later).
2. **Admin sign-in.** Authentication, Sign-in method, Google, Enable (already done if the quiz's admin works). Settings, Authorized domains, add `cameronallen-bit.github.io`. Open `?role=admin`, sign in, copy your user ID from the page, and in the database add `agencyDesigner/admins/<your user ID>` = `true`.
3. **Before ads:** the network team's sign-off on every "With Avoya" line and the network steps, legal's on the consent wording, the flexibility framing and privacy coverage, the ad category, and the Meta Pixel ID (`ANALYTICS.metaPixelId`, empty now). Move to an Avoya-owned Firebase project and an Avoya address (then set `APP.siteUrl` and, for the card's footer, `APP.cardUrlLabel`).

## Files

- `index.html`: the designer and the admin page. The config is at the top of the script: `FIREBASE_CONFIG`, `APP`, `OPTIONS_VERSION` and `STEPS` (every pick, its card phrase and its "With Avoya" line with sources), `NAME_BITS` (name ideas), `NETWORK_STEPS`, `FORM`, `LEAD_SINK`, `ANALYTICS`.
- `r/*.html`: the eight share previews (their own title and image, then on to the designer).
- `img/`: link-preview images, the logo, `BRAND.md` (colors and type from AvoyaNetwork.com) and `SOURCES.md` (where every "With Avoya" line comes from).
- `database.rules.json`: the rules.

## Updating

Edit `index.html`, then in this repo: Add file, Upload files, drop it in, commit. Pages redeploys in about a minute. Rewording a line is an edit; adding, removing or renaming an option bumps `OPTIONS_VERSION`, which starts fresh counters.
