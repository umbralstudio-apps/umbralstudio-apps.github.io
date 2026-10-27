# Live pre-match odds sources for Spanish football (1X2 and O/U 2.5) for ORÁCULO 1X2 / La Quiniela, as of 27 Oct 2026

Scope: live and pre-match odds access from Google Colab for LaLiga EA Sports, LaLiga Hypermotion, Copa del Rey, Liga F and international matches. Historical CSVs and academic accuracy studies are out of scope; other researchers cover them.

Labels used below:
- "Own measurement" means a direct HTTP test from this research session on 27 Oct 2026. The session's egress IP was Google LLC (AS396982), geolocated to Columbus, Ohio, US, per [ipinfo.io](https://ipinfo.io/json). That is a reasonable proxy for a Colab VM, but it is not a Colab VM.
- "Vendor claim" means a figure published by a company that sells the product, or by its competitor.
- "Search snippet" means the claim came from a search-result summary and the page itself was not opened.

---

## 1. Pinnacle in 2025–2026: the API closure, how aggregators still get Pinnacle prices, whether Pinnacle is legal in Spain, sharpness and margins

### Takeaway
Pinnacle closed its official API to the public on 23 July 2025. Aggregators now get Pinnacle prices in two ways:
- **From Pinnacle's public website.** The Odds API says this openly, and warns that these odds "may incur a delay".
- **From undisclosed commercial or scraped feeds.** This applies to OddsPapi and to Pinnacle-only resellers.

Pinnacle's public website JSON still served LaLiga, Segunda and Copa del Rey prices, with stake limits, without login on 27 Oct 2026. It served no Liga F matches.

Pinnacle is not licensed in Spain: it is absent from the DGOJ register.

Its LaLiga 1X2 margin is about 3–4% within a week of kickoff and about 2.9% near kickoff (vendor measurement). Its margin is higher on Segunda (about 5%) and much higher on early Copa del Rey ties (about 9%, with small limits).

### Cited Findings

**The API closure**
- Pinnacle's own documentation repository says: "Access to Pinnacle API suite has been closed for the general public since July 23rd, 2025." It continues: "We offer bespoke data services for select high value bettors & commercial partnerships. We also support academics and pregame handicapping projects." Applicants email a use case to api@pinnacle.com — [Pinnacle API docs (GitHub)](https://github.com/pinnacleapi/pinnacleapi-documentation).
- The same repository describes the legacy API's terms — [Pinnacle API docs (GitHub)](https://github.com/pinnacleapi/pinnacleapi-documentation):
  - a funded account was required;
  - a maximum of 2 distinct IP addresses per client;
  - odds endpoints limited to 1 request per 2 minutes per endpoint per sportId, with HTTP 429 on excess.
- odds-api.io (blog, 1 Feb 2026) writes "In July 2025, Pinnacle shut down public API access." It says some large API providers kept access while others are losing it. odds-api.io itself replaced Pinnacle with Betfair Exchange, SingBet, Polymarket and Kalshi — [odds-api.io blog](https://odds-api.io/blog/pinnacle-api-shutdown-alternatives).

**How aggregators source Pinnacle now**
- The Odds API lists `pinnacle` only in its `eu` region, with the note: "Odds come from a public website and may incur a delay" — [The Odds API bookmaker list](https://the-odds-api.com/sports-odds-data/bookmaker-apis.html).
- **Conflict.** OddsPapi's comparison (12 Mar 2026) claims The Odds API has "No Pinnacle, Singbet, or Betfair Exchange" and only about 40 soft books — [OddsPapi blog](https://oddspapi.io/blog/?p=2498). This is contradicted by The Odds API's own list, which shows `pinnacle`, `betfair_ex_eu`, `betfair_ex_uk`, `matchbook` and `smarkets` — [The Odds API bookmaker list](https://the-odds-api.com/sports-odds-data/bookmaker-apis.html).
- A dev.to article (mid-2026) compares three alternatives — [dev.to](https://dev.to/ryankr/pinnacle-killed-its-public-api-heres-how-to-get-pinnacle-odds-in-2026-with-code-39pe). The author says "no affiliate links", but the examples are built on pinnapi, so a vendor tie is likely.
  - OpticOdds: custom quote, "reportedly starting in the high hundreds per month".
  - pinnapi: $99–$229/month; free tier of 100 REST requests/day; Pinnacle only; SSE/WebSocket push.
  - The Odds API: "scraped from Pinnacle's public website, with a documented delay".

**Pinnacle on LaLiga (OddsPapi measurements, vendor claim)** — all from [OddsPapi LaLiga post, 20 Aug 2026](https://oddspapi.io/blog/la-liga-odds-api/):
- On 11 Aug 2026, Pinnacle was on 7 of 8 opening-round LaLiga fixtures, with 1X2 margins of 3.23%–4.41%.
- OddsPapi calls Pinnacle "the sharp reference on La Liga".
- Re-measured on 24 Aug 2026, Pinnacle's median LaLiga three-way margin was 2.93%, ranking 17th of 160 books.
- Tighter on that day: Betfair Exchange 0.71%, sx.bet 1.12%, Polymarket 1.50%, Kalshi 1.51% and 1xBet 1.57%.
- Pinnacle's Asian handicap margin on Sevilla v Rayo was as low as 2.36% at −0.25.
- Pinnacle's base limits on that fixture were $1,500 on 1X2 and Asian handicap and $1,000 on goals O/U. It opened 40 days out at a $250 limit.

**Own measurement: Pinnacle public website JSON, about 09:30 UTC on 27 Oct 2026, no login, Google US IP**
- The league list returned these Spanish leagues with offers — [league list](https://guest.api.arcadia.pinnacle.com/0.1/sports/29/leagues?all=true):

  | League | Pinnacle id | Matchups listed |
  |---|---|---|
  | Spain - La Liga | 2196 | 21 |
  | Spain - Segunda Division | 2432 | 11 |
  | Spain - Copa del Rey | 2462 | 17 |
  | Spain - Primera Division Women (Liga F) | 2468 | 0 |
  | Spain - Primera Federacion | 220076 | 0 |

- **LaLiga** — [LaLiga markets](https://guest.api.arcadia.pinnacle.com/0.1/leagues/2196/markets/straight):
  - 20 regular-time matches, 30 Oct–8 Nov.
  - Prices are in American format (e.g. +378 / −161 / +373). Each market carries a `limits` field (maxRiskStake).
  - Median 1X2 overround was 4.66% (range 3.27–5.73%).
  - Matches within 6 days of kickoff: 9 matches, median 3.75%, stake limit 3,000.
  - Matches more than 6 days out: 11 matches, median 5.07%, limits 500–3,000.
  - Median O/U 2.5 overround was 4.31%.
- **Segunda** — [Segunda markets](https://guest.api.arcadia.pinnacle.com/0.1/leagues/2432/markets/straight):
  - 11 matches, 31 Oct–2 Nov.
  - Median 1X2 overround 5.00% (range 4.90–5.65%); stake limit 600.
  - Median O/U 2.5 overround 4.34%.
- **Copa del Rey first round** — [Copa markets](https://guest.api.arcadia.pinnacle.com/0.1/leagues/2462/markets/straight), [Copa matchups](https://guest.api.arcadia.pinnacle.com/0.1/leagues/2462/matchups):
  - 17 ties on 27 Oct, for example Cuarte v Girona, Manacor v Villarreal and Recreativo Huelva v Rayo Vallecano.
  - 14 of the 17 had a three-way price.
  - Median 1X2 overround 9.21% (range 9.13–12.48%); stake limits 125–250.
  - Median O/U 2.5 overround 6.43%.
- **Main total line.** Pinnacle's main (non-alternate) total was exactly 2.5 in only 4 of 20 LaLiga matches, 7 of 11 Segunda matches and 5 of 17 Copa ties. The other main lines ranged from 2.0 to 4.5, including quarter lines. A 2.5 line existed as main or alternate in 18 of 20, 11 of 11 and 14 of 17 respectively — same endpoints as above.

**Spain licence**
- Pinnacle does not appear among the 78 operators in the DGOJ licensed-operator register (fetched 27 Oct 2026) — [DGOJ Buscador de operadores](https://www.ordenacionjuego.es/operadores-juego/operadores-licencia/operadores).
- Affiliate directories list Spain among countries whose residents cannot join Pinnacle (search snippet; secondary source) — [StatsDrone](https://statsdrone.com/affiliate-programs/pinnacle-sports-affiliates/).
- Pinnacle holds a Maltese remote gaming licence (search snippet) — [Wikipedia](https://en.wikipedia.org/wiki/Pinnacle_Sports).

### Inferences
- **The Pinnacle feed is fragile.** The Odds API's own wording confirms that its Pinnacle column is now scraped from the public site. If Pinnacle hardens that site, both The Odds API and any direct use lose Pinnacle at the same moment.
  - The notebook should log `last_update` per bookmaker.
  - It should fall back automatically when `pinnacle` is missing or stale.
- **Timing matters a lot for the margin.** Margins shrink and limits rise towards kickoff. A Saturday-morning pull is roughly 0–3 days before LaLiga kickoffs, where the margin is about 3.75% or lower. Matches more than 6 days out sit around 5%, so fetching earlier in the week degrades the base probabilities.
- **Copa del Rey early rounds are a weak market.** A 9% Pinnacle margin with 125–250 stake caps carries far less information than LaLiga prices. A multi-book consensus, or a heavier weight on Elo/model, may be as good there. This should be validated with RPS on past Copa rounds.
- **The O/U 2.5 line needs explicit handling.** With Pinnacle, "totals" is usually not 2.5, so an API's featured `totals` market often returns 2.25, 2.75 or 3.0.
  - The notebook must either select the alternate 2.5 line explicitly,
  - or convert the main Asian line into an implied goal expectation (for example via Poisson) instead of assuming 2.5.
- **Liga F (and Primera Federación) have no Pinnacle price.** Neither had a single Pinnacle matchup 4 days before the weekend. Expect no Pinnacle price for Liga F Quiniela matches at Saturday-morning time.

### Gaps
- No Pinnacle statement found on whether its public website endpoints may be used programmatically. Their terms of use were not reviewed.
- Not checked whether pinnacle.com is geo-blocked for Spanish residential IPs.
- No independent measurement of The Odds API's actual Pinnacle delay. Only the vendor's "may incur a delay" exists.
- PS3838 (a Pinnacle-linked Asian route) and PinnOdds appeared in searches ([sharproute guide](https://sharproute.net/guides/ps3838-api-access/), [pinnodds](https://pinnodds.com/pinnacle-odds-api)) but were not evaluated. They are vendor or agent pages, and their legality for a Spanish resident is doubtful.
- Whether Pinnacle is the most accurate LaLiga/Segunda market is not established here; the researcher on accuracy studies covers it.

---

## 2. the-odds-api.com: coverage, bookmakers, costs, limits, historical data, reliability

### Takeaway
The Odds API is the most mature, best-documented low-cost API covering Pinnacle plus two exchanges on LaLiga, Segunda and Copa del Rey.

Its limits:
- It has no Liga F key.
- It has no Spanish-licensed books.
- Its Pinnacle data is scraped and may be delayed.
- Its featured `totals` is the main line only.

The free 500 credits per month are enough for weekly runs. Historical odds (since June 2020, 5-minute snapshots since Sept 2022) need a paid plan.

### Cited Findings

**Sport keys**
- Spanish keys: `soccer_spain_la_liga` ("La Liga - Spain"), `soccer_spain_segunda_division` ("La Liga 2 - Spain") and `soccer_spain_copa_del_rey` ("Copa del Rey").
- There is no Liga F (Spanish women's) key and no Supercopa key — [The Odds API sports list](https://the-odds-api.com/sports-odds-data/sports-apis.html).
- National-team keys: `soccer_fifa_world_cup_qualifiers_europe`, `soccer_uefa_nations_league`, `soccer_uefa_euro_qualification`, `soccer_fifa_world_cup`, `soccer_fifa_world_cup_womens` and `soccer_uefa_european_championship`. No friendlies key is listed — [sports list](https://the-odds-api.com/sports-odds-data/sports-apis.html).

**Bookmakers by region** — [The Odds API bookmaker list](https://the-odds-api.com/sports-odds-data/bookmaker-apis.html)
- `eu`: onexbet (1xBet), sport888, betclic_fr, betanysports, betfair_ex_eu, betonlineag, betsson, codere_it, betvictor, coolbet, everygame, gtbets, leovegas_se, marathonbet, matchbook, mybookieag, nordicbet, pinnacle, pmu_fr, tipico_de, unibet_fr, unibet_it, unibet_nl, unibet_se, williamhill, winamax_de, winamax_fr.
- `uk`: sport888, betano_uk, betfair_ex_uk, betfair_sb_uk, betfred_uk, betvictor, betway, boylesports, casumo, coral, grosvenor, ladbrokes_uk, leovegas, livescorebet, matchbook, paddypower, skybet, smarkets, unibet_uk, virginbet, williamhill.
- There is no Spain region, and no `.es` book. The Codere entry is Italy's `codere_it`.
- Reliability notes on the same page:
  - Delisting is rare.
  - "Occasionally a bookmaker might disappear from the API response", usually resolved within hours to days.
  - The Pinnacle entry carries the public-website delay caveat.

**Pricing** (USD per month) — [The Odds API home](https://the-odds-api.com/)

| Plan | Price | Credits per month | Bookmakers |
|---|---|---|---|
| Starter | Free | 500 | "Most bookmakers" |
| 20K | $30 | 20,000 | All |
| 100K | $59 | 100,000 | All |
| 5M | $119 | 5,000,000 | All |
| 15M | $249 | 15,000,000 | All |

**Credit costs** — [The Odds API v4 docs](https://the-odds-api.com/liveapi/guides/v4/)
- `/odds` costs 1 credit per region per market.
- `/sports` and `/events` are free. `/scores` costs 1 credit, or 2 with `daysFrom`.
- Responses with empty data are free.
- "Every group of 10 bookmakers is the equivalent of 1 region". When both are given, `bookmakers` overrides `regions`.
- The per-event endpoint `/events/{eventId}/odds` costs unique markets returned × regions.

**Historical odds** — [The Odds API v4 docs](https://the-odds-api.com/liveapi/guides/v4/)
- Data available from 6 June 2020.
- Snapshots every 10 minutes at first, every 5 minutes from September 2022.
- Cost: 10 credits × markets × regions.
- "This endpoint is only available on paid usage plans."
- **Conflict.** OddsPapi says historical data is reachable on the free tier at 10× cost — [OddsPapi blog](https://oddspapi.io/blog/the-odds-api-free-tier-limits/). The official docs say paid plans only.

**Update intervals** — [The Odds API update intervals](https://the-odds-api.com/sports-odds-data/update-intervals.html)
- Featured markets (h2h, spreads, totals): 60 s pre-match, 40 s in-play.
- Betting exchanges: 20 s pre-match, 10 s in-play.
- The interval starts shrinking 6 hours before kickoff.

**Markets** — [The Odds API markets](https://the-odds-api.com/sports-odds-data/betting-markets.html)
- For soccer, `h2h` includes the draw.
- "Spreads and totals markets are mainly available for US sports and bookmakers at this time."
- `alternate_totals`, `btts`, `draw_no_bet` and `h2h_3_way` are additional markets, served one event at a time through `/events/{eventId}/odds`.

### Inferences
- **Weekly cost on the current setup.** A typical run calls 3 sport keys × 2 markets (h2h, totals) × 1 region, which is 6 credits. The free 500 credits cover about 80 such runs a month. Adding `uk` doubles the cost.
- **A better configuration at the same price.** Pass `bookmakers=` with up to 10 sharp or low-margin keys instead of `regions=eu`. Ten keys cost the same as one region and can mix EU and UK books. For example: pinnacle, betfair_ex_eu, betfair_ex_uk, matchbook, smarkets, marathonbet, onexbet, williamhill, betsson, sport888.
- **The O/U 2.5 line.** The featured totals will often be Pinnacle's main Asian line rather than 2.5 (see Section 1). Pulling `alternate_totals` per event costs credits per event, so converting the main line is cheaper.
- **Backfilling Pinnacle closing odds.** The football-data 2026/27 files lack Pinnacle, and the 20K plan ($30) can fill that gap. A LaLiga season has about 38 rounds × about 10 kickoff slots = about 380 snapshot calls. At 2 markets × 10 credits each, that is about 7,600 credits per league-season.
- **No Liga F, and unknown early-Copa coverage.** Whether early Copa ties appear depends on which books the API scrapes.

### Gaps
- No independent 2025–2026 uptime or latency reports for The Odds API's Pinnacle or Betfair feeds were found.
- No live test with an API key was possible, so it is unconfirmed that `pinnacle` actually appears today in `soccer_spain_*` responses.
- Unknown which Betfair pool `betfair_ex_eu` reflects (international .com or Spain .es).

---

## 3. OddsPapi (oddspapi.io): operator, books, Spanish coverage, limits, prices, data-quality issues

### Takeaway
OddsPapi's free tier is the broadest no-cost source:
- 250 requests per month.
- Every bookmaker, including Pinnacle, SBOBet, Singbet and Betfair Exchange.
- Nine Spanish-licensed books on LaLiga.
- Free historical odds, with stake limits on every snapshot.

The trade-offs:
- It is a marketing-heavy vendor that appears to belong to 55 Tech, with no published SLA.
- Its bookmaker counts are inconsistent.
- It ships clone and internal feeds that can triple-count Pinnacle.
- Its payloads are very large.
- On paid self-serve plans Pinnacle is "contact us" only.

Liga F and Copa del Rey coverage are unverified.

### Cited Findings

**Operator**
- OddsPapi's "About" link points to 55-tech.com — [What is OddsPapi (2 Mar 2026)](https://oddspapi.io/blog/?p=2479).
- 55 Tech's site carries an "OddsPapi fixtures and odds" testimonial and describes a "300-source feed" — [55 Tech](https://55-tech.com).
- The founding date was not found.

**Bookmakers**
- Sharps named: Pinnacle, SBOBet and "Singbet (Crown)". Exchanges named: Betfair Exchange and Matchbook — [What is OddsPapi](https://oddspapi.io/blog/?p=2479).
- Counts vary between posts: "350+" ([What is OddsPapi](https://oddspapi.io/blog/?p=2479)), 370 ([OddsPapi blog](https://oddspapi.io/blog/the-odds-api-free-tier-limits/)), 372 ([OddsPapi blog](https://oddspapi.io/blog/api-football-alternative/)) and 381 ([OddsPapi blog](https://oddspapi.io/blog/betsapi-alternative/)).
- On 8 Sep 2026: 357 slugs in the catalogue, 282 with live odds, and 170 live feeds that are neither flagged clones nor internal test slugs. OddsPapi warns: "Skip the four internal feeds in any consensus, or Pinnacle counts three times" — [OddsPapi enterprise pricing post](https://oddspapi.io/blog/enterprise-odds-feed-pricing/).

**Spanish coverage** — [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/)
- LaLiga is tournamentId 8. The Spain category lists twelve tournaments, including LaLiga 2, Primera Federación and Segunda Federación.
- Opening round, 11 Aug 2026: 16–17 books per fixture, mostly US books.
- 24 Aug 2026: 174–192 books per fixture, 160 of them with a complete 1X2.
- Spanish-licensed books with live LaLiga odds: 888sport.es, betway.es, bwin.es, codere.es, leovegas.es, paf.es, pokerstars.es and winamax.es on all four fixtures checked; bet365.es on three; marathonbet on two. betfair.es and goldenpark.es were absent.

**Data-quality issues** — [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/)
- "17 slugs -> 12 independent quotes". Byte-identical clone groups such as betparx/ballybet/betrivers/fourwinds report `cloneOf: null`.
- A 429 rate-limit body is valid JSON, so naive code can read it as "this fixture has no odds".
- The `/fixtures` window is capped at 10 days, and `to` is a midnight-UTC instant.
- `hasOdds` must be checked before calling `/odds`.
- `/markets` ignores `sportId`.

**Historical odds** — [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/)
- Free; three bookmakers per call; no market filter.
- One fixture with three books returned 8.33 MB. OddsPapi advises sleeping about 4.5 s between calls.
- Pinnacle snapshots include the stake limit.
- A full board for one fixture (262 books) can reach 28 MB — [OddsPapi enterprise pricing post](https://oddspapi.io/blog/enterprise-odds-feed-pricing/).

**Pricing** — [OddsPapi enterprise pricing post (8 Sep 2026)](https://oddspapi.io/blog/enterprise-odds-feed-pricing/)
- Formula: (bookmakers + sports) × request tier.
- Sports: soccer $5 per month.
- Bookmaker feeds: $10, $20 or $30 per month each.
- Request tiers:

  | Tier | Multiplier | Requests per month (approx.) |
  |---|---|---|
  | Normal | ×1 | 5,000 |
  | Dev | ×2 | 100,000 |
  | Pro | ×5 | 500,000 |
  | Ultra | ×10 | 1.5M |

- "Nine feeds, Pinnacle among them, show as locked with a contact link instead of a price."
- WebSocket and live odds sit on the B2B plan.
- The pricing page disclaims: "The goal is to cover all odds being on the bookmakers sites, but this is not always guaranteed" — [OddsPapi pricing](https://oddspapi.io/en/pricing).

**What the feed does not carry**
- No scores and no stats. Fixtures carry `externalProviders` IDs (Sofascore, Betradar, OpticOdds, Flashscore, Pinnacle) that can be used as join keys — [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/).

### Inferences
- **Request budget per jornada.** Expect roughly 15–20 requests per Quiniela jornada (one `/odds` call per fixture plus lookups). 250 requests per month covers about 4–5 jornadas if historical pulls are avoided in the same month.
- **Building a consensus.** Deduplicate by price tuple and drop internal or test slugs. Otherwise the consensus over-weights clone feeds and Pinnacle.
- **Risk that free Pinnacle disappears.** Pinnacle cannot be bought self-serve on OddsPapi's paid plans. Its presence on the free tier may therefore be revoked without notice.
- **Value for Copa del Rey and Primera Federación.** The catalogue includes Primera and Segunda Federación tournaments, so OddsPapi is the most plausible API source for lower-division Copa sides. This must be verified per match.

### Gaps
- Liga F and Copa del Rey tournament IDs and actual book counts were not verified, and no Liga F mention was found.
- No independent reliability or uptime data, and no information on where OddsPapi sources Pinnacle.
- The company's legal identity and jurisdiction were not confirmed.

---

## 4. API-Football (api-sports.io): odds coverage, free-plan restrictions, prices, reliability

### Takeaway
API-Football is strong for fixtures, IDs and stats, including Liga F and lower divisions, but weak for odds:
- Its odds are pre-match snapshots from a limited set of books.
- Per a competitor's reading of its docs, odds are updated about once a day.
- Free plans are season-restricted.

Its website sits behind a Cloudflare challenge, though the API host is reachable from datacenter IPs. Official odds details could not be read in this session.

### Cited Findings
- **Free plan.** 100 requests per day; access to all endpoints; "limited in terms of available seasons" (search snippets) — [API-Football pricing](https://www.api-football.com/pricing), [API-Football beginner's guide](https://www.api-football.com/news/post/how-to-get-started-with-api-football-the-complete-beginners-guide).
- **Bookmakers endpoint.** The beginner's guide advises calling the bookmakers endpoint once and caching it — [beginner's guide](https://www.api-football.com/news/post/how-to-get-started-with-api-football-the-complete-beginners-guide).
- **Paid prices.** Pro $19 per month (7,500 requests/day) and Ultra $29 per month (75,000 requests/day), per OddsPapi's reading of the pricing page (competitor, 22 Jul 2026) — [OddsPapi blog](https://oddspapi.io/blog/api-football-alternative/).
- **Odds endpoint.** OddsPapi says it is "pre-match only and, per its own documentation, is updated once a day with a recommended one call per day". It says bookmakers are "a limited set" — [OddsPapi blog](https://oddspapi.io/blog/api-football-alternative/).
- **Odds window (other sport).** API-Football's own NFL guide says pre-match odds are provided 1–7 days before the game, with 7-day history. That is for American football, not soccer — [API-Football NFL guide](https://www.api-football.com/news/post/how-to-get-started-with-api-nfl-the-complete-beginners-guide).
- **Seasons on the free plan.** A third-party integration guide advises verifying free-plan season access with a live key — [Bruin docs](https://getbruin.com/docs/ingestr/soccer-sources/api-football.html).
- **Access from a datacenter IP (own measurement).** Both www.api-football.com/pricing and the documentation returned Cloudflare "Just a moment..." (HTTP 403). `https://v3.football.api-sports.io/status` returned the API's JSON error "Missing application key" — [API-Football pricing](https://www.api-football.com/pricing), [API status endpoint](https://v3.football.api-sports.io/status).

### Inferences
- Treat API-Football as a fixtures, IDs, results and Liga F data layer, and as a last-resort odds backup.
- A once-daily snapshot from an unknown set of books is a poor substitute for a Saturday-morning Pinnacle or exchange price.

### Gaps
- The official odds documentation could not be read (Cloudflare block, and the Wayback Machine was unreachable). Still unconfirmed for soccer:
  - the current bookmaker list, including whether Pinnacle survived July 2025;
  - the days-before-kickoff window;
  - the update frequency;
  - which seasons the 2026 free plan allows.

---

## 5. Betting exchanges: Betfair Spain, liquidity, API access, and Matchbook/Smarkets/Betdaq/Orbit

### Takeaway
Betfair is the only licensed betting exchange in Spain, and its Spanish exchange appears to be a separate, thinner pool. The official Betfair API is a poor fit for Colab:
- It blocks US IPs.
- Read-only use with the live key is not permitted.
- The delayed key lags 1–180 s and hides traded volume.
- Live-key activation now costs £499.

Exchange prices are better taken through The Odds API (`betfair_ex_eu`, `betfair_ex_uk`, `matchbook`, `smarkets`) or OddsPapi. Betfair Exchange had the tightest LaLiga margin measured (0.71%).

### Cited Findings

**Licensing in Spain**
- Filtering the DGOJ register by "Apuestas deportivas cruzadas" (the exchange licence) returns exactly one operator: BETFAIR INTERNATIONAL SPAIN SA (betfair.es) — [DGOJ register, licence filter 71](https://www.ordenacionjuego.es/operadores-juego/operadores-licencia/operadores?licences=71).
- Matchbook, Smarkets and Betdaq do not appear among the 78 licensed operators — [DGOJ register](https://www.ordenacionjuego.es/operadores-juego/operadores-licencia/operadores).

**Spanish exchange API** — [Betfair docs: Betting on Spanish Exchange (v19, 13 Mar 2026)](https://betfair-developer-docs.atlassian.net/wiki/spaces/1smk3cen4v3lu3yomq5qye0ni/pages/2687649/Betting+on+Spanish+Exchange)
- Spanish Exchange accounts register at betfair.es and need their own app key.
- Login goes through `identitysso.betfair.es` or `identitysso-cert.betfair.es`.
- Calls then go to the UK endpoints (api.betfair.com), which "automatically return the markets that are available to Spanish Exchange customers".
- The Stream API is available to Spain customers.

**Separate pool (anecdotal)** — [Bet Angel forum](https://forum.betangel.com/viewtopic.php?t=11112)
- A 2020 post says the Spanish exchange is "completely separate", open only to Spanish residents, with limited markets.
- A 2023 Spanish user cited 16k matched on a City match versus 66k on the main exchange.

**App keys** — [Betfair docs: Application Keys (v143, 7 May 2026)](https://betfair-developer-docs.atlassian.net/wiki/spaces/1smk3cen4v3lu3yomq5qye0ni/pages/2687105/Application+Keys)
- Each account gets one Live key and one Delayed key.
- The Delayed key gives "delayed Betfair price data… variable between 1-180 second snapshots". It does not return `totalMatched` or EX_ALL_OFFERS.
- The Live key needs full KYC, completed testing and "the £499 activation fee".
- "Read-only access using the Live App Key isn't permitted."
- App keys are "for personal betting purposes only". Commercial use needs Betfair's approval.
- **Conflict on the fee.** Older documentation versions in search results cited £299 — [Betfair docs (search snippet)](https://betfair-developer-docs.atlassian.net/wiki/x/GA8p). The current page says £499.
- Betfair restates that read-only access with the live key is not permitted and that the delayed key should be used instead (updated 22 Aug 2026) — [Betfair support: read-only access](https://support.developer.betfair.com/hc/en-us/articles/25033076334748-What-is-read-only-Betfair-API-access).

**Blocked IP regions** — [Betfair support: restricted IP regions (updated 21 Sep 2026)](https://support.developer.betfair.com/hc/en-us/articles/28271961503516-Which-IP-regions-are-restricted-from-accessing-the-Betfair-API)
- Requests from these regions are "automatically blocked": China, France, Germany, Greece, Cyprus, Netherlands, North Korea, India, Iran, Iraq, Singapore, Turkey, UAE and USA.
- In some regions the API instead returns no markets.
- Spain is not listed.

**Exchange prices without the Betfair API**
- The Odds API carries `betfair_ex_eu`, `betfair_ex_uk`, `matchbook` and `smarkets` — [The Odds API bookmaker list](https://the-odds-api.com/sports-odds-data/bookmaker-apis.html). Exchange odds refresh every 20 s pre-match — [The Odds API update intervals](https://the-odds-api.com/sports-odds-data/update-intervals.html).
- On LaLiga (24 Aug 2026) Betfair Exchange's median three-way margin was 0.71%, first of 160 books — [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/).
- Kalshi and Polymarket also price LaLiga ([OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/)):
  - Kalshi had $2,916 behind the 1X2 and $3,506 behind O/U 2.5 on Sevilla v Rayo.
  - Both widen sharply far from kickoff: Kalshi was at 14% nine days out.

### Inferences
- **Colab and the Betfair API.** Colab runs on Google infrastructure, and this session's Google IP geolocated to the US. If a Colab VM geolocates to a restricted region (the US and the Netherlands are both on the list), a Betfair API login from Colab will fail. The terms also bar a read-only live-key setup in any case.
- **Exchange data in the ensemble.** Use exchange data via aggregators as a second sharp anchor next to Pinnacle, weighted by liquidity.
- **Thin markets.** On Segunda, Liga F and Copa minnows, exchange prices are probably thin or wide, so their back/lay mid can be noisy.
- **Kalshi and Polymarket.** They are not licensed in Spain (absent from the DGOJ register). They can still serve as consensus inputs via OddsPapi near kickoff, filtered by depth.

### Gaps
- No current (2025–2026) matched-volume figures for LaLiga, Segunda or Liga F on Betfair (.com or .es).
- Orbit and Betdaq API terms, and Smarkets public API access, were not verified.
- Whether `betfair_ex_eu` in The Odds API reflects the .com pool is undocumented.

---

## 6. Other odds data providers with LaLiga/Segunda coverage

### Takeaway
Paid feeds that publish prices and claim Pinnacle:
- Goalserve: $250 per month for soccer pre-match.
- pinnapi: $99–$229 per month, Pinnacle only, with a vendor-tied source.
- SportsGameOdds: $99–$499 per month.

Other options:
- SportMonks: €29 + €15 per month for 5 leagues with an odds add-on of "50+ bookmakers". Books are not named.
- odds-api.io: from £49 per month for 2 bookmakers, with free keys paused and Pinnacle dropped.
- BetsAPI: paid only, Bet365-centric.
- OpticOdds, OddsJam, Sportradar, Genius, LSports and OddsMatrix: sales-gated enterprise feeds, overkill for this project.

### Cited Findings

**SportMonks** — [SportMonks pricing](https://www.sportmonks.com/football-api/plans-pricing)

| Plan | Price per month | Leagues |
|---|---|---|
| Starter | €29 | 5 |
| Growth | €99 | 30 |
| Pro | €249 | 120 |
| Enterprise | Custom | All |

- Odds & Predictions bundle: €15 per month, "50+ bookmakers", "150+ markets", pre-match and in-play.
- Premium Odds Feed: from €129 per month.
- Historical add-on: from €29.
- Pinnacle and Betfair are not named.
- The premium odds feed is powered by TXOdds and keeps pre-match history up to 7 days after kickoff (search snippet) — [SportMonks docs](https://docs.sportmonks.com/v3/endpoints-and-entities/endpoints/premium-odds-feed).

**odds-api.io** — [odds-api.io pricing](https://odds-api.io/pricing), [odds-api.io blog](https://odds-api.io/blog/pinnacle-api-shutdown-alternatives)

| Plan | Price per month | Bookmakers |
|---|---|---|
| Solo | £49 | 2 |
| Starter | £99 | 5 |
| Growth | £179 | 10 |
| Pro | £229 | 15 |

- Every plan includes 5,000 requests per hour. WebSocket costs 2× the plan price.
- The blog says "New free Odds-API.io keys are paused", claims "415+" bookmakers, and says Pinnacle was replaced by Betfair Exchange, SingBet, Polymarket and Kalshi.

**BetsAPI (competitor's description)** — [OddsPapi blog](https://oddspapi.io/blog/betsapi-alternative/)
- Bet365-first, with BWin, Betfair, Sbobet, 1xBet and William Hill through separate endpoints.
- 3,600 requests per hour.
- No free tier; a $1 one-day trial.

**OpticOdds and OddsJam**
- OpticOdds: no public price — [OddsPapi blog](https://oddspapi.io/blog/?p=2498). "Reportedly starting in the high hundreds per month" — [dev.to](https://dev.to/ryankr/pinnacle-killed-its-public-api-heres-how-to-get-pinnacle-odds-in-2026-with-code-39pe).
- OddsJam API: sales-only. One review says Pinnacle and Bet365 are absent — [sportsapis.dev](https://sportsapis.dev/apis/odds-jam). Other comparison sites claim Pinnacle is included. The claims conflict and are unresolved.

**SportsGameOdds** — [OddsPapi blog](https://oddspapi.io/blog/?p=2498), [SportsGameOdds comparison](https://sportsgameodds.com/compare/opticodds)
- $99–$499 per month, Pinnacle included, 7-day trial.
- A free tier with 9 books and a 10-minute delay (search snippet, from SportsGameOdds' own comparison page).

**Enterprise feeds** — [OddsPapi enterprise pricing post](https://oddspapi.io/blog/enterprise-odds-feed-pricing/)
- Read on 8 Sep 2026, Sportradar, Genius Sports, LSports and OddsMatrix publish no price.
- Sportradar Odds Comparison: "140+ global bookmakers".
- OddsMatrix: "Over 150 bookmaker suppliers"; pull access limited to one request per 30 s.
- OddsPapi also says LaLiga sells data rights to Sportradar and Genius — [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/).

**Goalserve** — [Goalserve prices](https://www.goalserve.com/en/sport-data-feeds/odds-api/prices)
- Soccer Pregame Odds: $250 for 1 month, $1,000 for 6 months, $1,500 for 12 months.
- Named bookmakers include Bet365, Pinnacle, Marathonbet, Betfair and Unibet.
- Pre-match refresh every 30 s; trial on request.
- The page is inconsistent on the bookmaker count (20+, 30+ or 50+).

### Inferences
- **Only escalate if the cheap sources fail.** The Odds API plus OddsPapi together cover LaLiga, Segunda and Copa with Pinnacle and exchanges at roughly zero cost. Escalate only if Pinnacle disappears from both.
- **Cheapest published fallback that claims Pinnacle.** Goalserve's $250 per month soccer plan. Verify its Pinnacle source, delay and Copa or Liga F coverage on a trial first.
- **SportMonks.** Useful mainly if its fixtures and stats layer is also wanted. Its odds books are unspecified.

### Gaps
- No primary information on iSports or an Oddspedia API.
- No trials run on any paid feed.
- No Liga F coverage data for any provider in this section.

---

## 7. Odds-comparison websites for manual checks (OddsPortal, BetExplorer, Oddschecker, Flashscore, Sofascore, Oddspedia, Spanish comparators)

### Takeaway
Two sites load from a Google datacenter IP and suit the Saturday-morning manual cross-check:
- **OddsPortal**, for broad multi-book comparison. Its terms forbid scraping or automated requests without consent.
- **Flashscore.es**, for Spanish-licensed books on LaLiga, and plausibly Liga F and Copa.

BetExplorer also loads. Oddschecker, Oddspedia and Sofascore's API block datacenter requests.

### Cited Findings

**OddsPortal terms** — [OddsPortal terms](https://www.oddsportal.com/terms/)
- Signed by Livesport s.r.o., Prague, 9 Oct 2023.
- "You must not burden our server… with automated requests."
- Content may not be used by "embedding, aggregating, scraping or recreating it without our express consent."
- No extraction of database content; no commercial use.
- Odds are "presented for reporting and comparison purposes."

**Own measurement from a Google US IP, 27 Oct 2026**

| Site | Result | Notes |
|---|---|---|
| [OddsPortal LaLiga](https://www.oddsportal.com/football/spain/laliga/) | HTTP 200 | Next.js app; odds are not in the static HTML |
| [OddsPortal Pinnacle page](https://www.oddsportal.com/bookmaker/pinnacle/) | HTTP 200 | Page exists |
| [BetExplorer LaLiga](https://www.betexplorer.com/football/spain/laliga/) | HTTP 200 | |
| [Flashscore.es LaLiga EA Sports 2026/2027](https://www.flashscore.es/futbol/espana/laliga-ea-sports/) | HTTP 200 | HTML names bet365, 1xBet, Retabet, Sportium, Winamax, William Hill, Betway and bwin |
| [Oddschecker](https://www.oddschecker.com/football/spain/la-liga) | HTTP 403 | Cloudflare "Attention Required!" |
| [Oddspedia](https://www.oddspedia.com/es/futbol/espana/laliga) | HTTP 403 | Cloudflare "Just a moment..." |
| [Sofascore API](https://www.sofascore.com/api/v1/unique-tournament/8/seasons) | HTTP 403 | JSON error |
| [elcomparador.com](https://www.elcomparador.com/) | HTTP 503 | |

### Inferences
- **What Flashscore.es is good for.** Seeing what Spanish-licensed books offer, especially for Liga F and Copa matches that APIs lack. Automating it probably carries terms risk too. OddsPortal's terms are signed by Livesport s.r.o., which as far as I know also runs Flashscore; that ownership was not verified in this session.
- **What OddsPortal is good for.** A human comparison of Pinnacle or Betfair against the API output, if those columns are shown to the viewer's region. That is unverified.
- **Oddschecker.** UK-focused and blocked from cloud IPs, so of little value for this system.

### Gaps
- Not verified whether OddsPortal or BetExplorer currently display Pinnacle prices, odds movement and closing odds to Spanish visitors after Pinnacle's 2025 API change.
- Flashscore's and BetExplorer's own terms were not read.
- No reliable Spanish-only odds comparator was verified (elcomparador returned 503).

---

## 8. Spanish-licensed bookmakers (DGOJ): who is licensed and who has the lowest LaLiga margins

### Takeaway
Licences on 27 Oct 2026:
- 78 operators in the DGOJ register.
- 47 hold the fixed-odds sports betting licence ("Apuestas deportivas de contrapartida").
- Only Betfair holds the exchange licence.
- Pinnacle is not licensed.

On LaLiga 1X2 (vendor measurement, Aug 2026), the tightest Spanish book was Codere at 4.36%. Most others sat between 5.7% and 13.7%. All were worse than Pinnacle's 2.93%. Spanish books are useful for coverage and consensus, not as the fair-value anchor.

### Cited Findings

**The 47 fixed-odds sports betting licensees**, with brands as listed — [DGOJ register, licence filter 72](https://www.ordenacionjuego.es/operadores-juego/operadores-licencia/operadores?licences=72):
- 888sport.es; Kirolbet (Artxibet 2022); Juegging; AdmiralBet; Betfair (apuestas.betfair.es); Betway.
- Casino Barcelona; Marca Apuestas (Casino Marbella Interactive: marcaapuestas.es, apuestas.marca.es); Casumo; Codere; Casino Gran Vía; Bet777; DAZN Bet; ebingo.
- Efbet; Retabet (Ekasa); bwin (Electraworks Ceuta); Casino Gran Madrid; Sol Casino; dafabet.es; Paston; TonyBet.
- Monopoly Casino; Botemanía; Pause and Play; Golden Park; bet365.es (Hillside New Media Malta); Betinia; Interwetten; Kaizen Gaming (no website listed).
- LeoVegas; Luckia; Mr Green; Aupabet; Paf (paf.es, speedybet.es); Betsson; Yosports (Rank); Yaass.
- Sportium; Olybet (Suertia); PokerStars Sports (TSG); Jokerbet; Versus; 1xbet.es (Wagerfair, S.A.); William Hill (WHG Ceuta); Winamax; ZEbet.

**Edge cases in the register**
- Marathonbet Spain, SA (marathonbet.es) and Betfred (Betwin360) are in the full list of 78 — [DGOJ register](https://www.ordenacionjuego.es/operadores-juego/operadores-licencia/operadores). Neither was returned by the fixed-odds sports filter — [DGOJ register, licence filter 72](https://www.ordenacionjuego.es/operadores-juego/operadores-licencia/operadores?licences=72).

**LaLiga margins (OddsPapi, 24 Aug 2026, four fixtures, median three-way margin; vendor claim)** — [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/)

| Book | Median 1X2 margin | Rank of 160 |
|---|---|---|
| pinnacle (reference) | 2.93% | 17th |
| codere.es | 4.36% | 34th |
| paf.es | 5.70% | 84th |
| bwin.es | 5.87% | 96th |
| winamax.es | 6.71% | 123rd |
| 888sport.es | 7.44% | 136th |
| leovegas.es | 9.72% | 152nd |
| betway.es | 13.73% | 156th |

- OddsPapi's conclusion: "the tightest Spanish book still charges 1.43 points more than the sharp."
- "1xbet" ranked 5th at 1.57%. Whether that is the .es or .com feed was not stated.
- On 11 Aug, Bet365's slug showed 9.54% on Sevilla v Rayo.

### Inferences
- **Fallback consensus when Pinnacle is missing** (Copa minnows, Liga F). Weight low-margin, independent feeds (Codere, Paf, bwin, Winamax, Marathonbet, 1xBet). Remove duplicated feeds before averaging.
- **Do not treat a Spanish-book average as Pinnacle-equivalent.** Its overround and favourite–longshot bias differ, so the power de-vig parameters may need recalibration per source.

### Gaps
- No margin data for Segunda or Liga F for any Spanish book.
- Sportium, Luckia, Kirolbet, Retabet, Marca Apuestas, Versus and Betfair Sportsbook were not measured.
- No DGOJ or press data on overround per league.

---

## 9. Accessibility from datacenter IPs (Google Colab)

### Takeaway
Reachable from a Google US IP:
- key-based odds APIs (The Odds API, OddsPapi, the API-Football API host);
- Pinnacle's public website JSON;
- OddsPortal, BetExplorer and Flashscore.es.

Blocked or restricted:
- Betfair's API (US IPs are on its restricted list);
- Oddschecker, Oddspedia and Sofascore's API (Cloudflare or 403);
- the API-Football website (Cloudflare);
- SELAE (per the user's note).

### Cited Findings
- **The test environment** was Google LLC AS396982, Columbus, Ohio, US — [ipinfo.io](https://ipinfo.io/json).
- **Reachable (HTTP 200):**
  - [Pinnacle public JSON](https://guest.api.arcadia.pinnacle.com/0.1/leagues/2196/matchups), no login;
  - [OddsPortal](https://www.oddsportal.com/football/spain/laliga/);
  - [BetExplorer](https://www.betexplorer.com/football/spain/laliga/);
  - [Flashscore.es](https://www.flashscore.es/futbol/espana/laliga-ea-sports/).
- **Reachable but answered with its own error:** the [API-Football API host](https://v3.football.api-sports.io/status) returned HTTP 403 with its JSON "Missing application key" error, not a Cloudflare page. The host is reachable; it rejected the call only because no key was sent.
- **Blocked or failing:**
  - [Oddschecker](https://www.oddschecker.com/football/spain/la-liga): 403 Cloudflare;
  - [Oddspedia](https://www.oddspedia.com/es/futbol/espana/laliga): 403 Cloudflare challenge;
  - [Sofascore API](https://www.sofascore.com/api/v1/unique-tournament/8/seasons): 403;
  - [API-Football website](https://www.api-football.com/pricing): Cloudflare 403;
  - [elcomparador.com](https://www.elcomparador.com/): 503.
- **Betfair** automatically blocks API requests from IPs geolocated to restricted regions, including the USA and the Netherlands — [Betfair support: restricted IP regions](https://support.developer.betfair.com/hc/en-us/articles/28271961503516-Which-IP-regions-are-restricted-from-accessing-the-Betfair-API).
- Betfair's fix for a wrongly geolocated IP is a correction request to MaxMind; it says it cannot whitelist manually (search snippet; exact article not opened) — [Betfair support: LOGIN_RESTRICTED_LOCATION](https://support.developer.betfair.com/hc/en-us/articles/360000406031-Why-am-I-receiving-the-LOGIN-RESTRICTED-LOCATION-error).

### Inferences
- **Check the VM's location in every run.** Before any Betfair or geo-sensitive call, log `requests.get('https://ipinfo.io/json')` from the notebook, because Colab VM location varies.
- **Keep the pipeline on key-based APIs.** That avoids Cloudflare, residential-proxy requirements and terms risk.

### Gaps
- No actual Colab VM was tested, and Colab's VM geolocation policy is undocumented in the sources found.
- No live calls with API keys were made to The Odds API or OddsPapi (no keys available).

---

## 10. Ranked shortlist for ORÁCULO 1X2 (synthesis of Sections 1–9)

### Takeaway
- **Primary:** keep The Odds API as the primary programmatic source, with Pinnacle as base and both Betfair exchanges as a second sharp anchor.
- **First backup:** OddsPapi free, which adds SBOBet, Singbet, Spanish books, lower-division coverage and free historical odds with stake limits.
- **Validation and last resort:** Pinnacle's public JSON, which carries unofficial-use risk.
- **Liga F:** no reliable Pinnacle or API price exists. Keep the model-first path and use Flashscore.es for manual checks.

### Cited Findings
All benefits and risks below rest on findings already cited in Sections 1–9:
- [The Odds API bookmakers](https://the-odds-api.com/sports-odds-data/bookmaker-apis.html), [v4 docs](https://the-odds-api.com/liveapi/guides/v4/), [sports list](https://the-odds-api.com/sports-odds-data/sports-apis.html)
- [OddsPapi LaLiga post](https://oddspapi.io/blog/la-liga-odds-api/), [OddsPapi enterprise pricing post](https://oddspapi.io/blog/enterprise-odds-feed-pricing/)
- [Pinnacle API closure notice](https://github.com/pinnacleapi/pinnacleapi-documentation), [Pinnacle public JSON](https://guest.api.arcadia.pinnacle.com/0.1/leagues/2196/markets/straight)
- [Betfair restricted IP regions](https://support.developer.betfair.com/hc/en-us/articles/28271961503516-Which-IP-regions-are-restricted-from-accessing-the-Betfair-API), [Betfair Application Keys](https://betfair-developer-docs.atlassian.net/wiki/spaces/1smk3cen4v3lu3yomq5qye0ni/pages/2687105/Application+Keys)
- [DGOJ register](https://www.ordenacionjuego.es/operadores-juego/operadores-licencia/operadores), [OddsPortal terms](https://www.oddsportal.com/terms/), [Goalserve prices](https://www.goalserve.com/en/sport-data-feeds/odds-api/prices)

### Inferences

**Best primary programmatic source**

1. **The Odds API.**
   - Suggested call: `bookmakers=pinnacle,betfair_ex_eu,betfair_ex_uk,matchbook,smarkets,marathonbet,onexbet,williamhill,betsson,sport888`, markets h2h and totals. Ten bookmakers cost one region-equivalent.
   - Benefits:
     - A documented, stable API with 60 s pre-match updates and 20 s for exchanges.
     - Pinnacle plus two exchange pools plus low-margin books in one schema.
     - Free 500 credits per month is enough for weekly use.
     - The $30 20K plan unlocks historical snapshots back to June 2020 (10-minute snapshots, 5-minute since September 2022). That can rebuild Pinnacle and exchange closing odds for 2025/26–2026/27, which football-data no longer supplies.
   - Risks:
     - Pinnacle is scraped from the public site and may be delayed. If Pinnacle hardens the site, the base disappears.
     - A competitor claims there is no Pinnacle at all. Verify that `pinnacle` is present and fresh in every response.
     - Featured totals are the main line (often 2.25, 2.75 or 3.0), not necessarily 2.5.
     - No Liga F; early-Copa coverage unknown; no Spanish books.

**Best backups**

2. **OddsPapi (free, 250 requests per month).**
   - Benefits:
     - Pinnacle, SBOBet, Singbet and Betfair Exchange, plus 9 Spanish-licensed books on LaLiga, for consensus and Spanish-market sanity checks.
     - The catalogue includes Primera and Segunda Federación tournaments, useful for Copa minnows.
     - Free historical odds back to the opening line, with Pinnacle stake limits that can be used as a confidence weight.
   - Risks:
     - The vendor publishes inconsistent bookmaker counts, and clone or internal slugs can triple-count Pinnacle unless deduplicated.
     - 429 responses look like empty data.
     - Payloads of 8–28 MB.
     - Pinnacle is "contact us" on paid tiers, so free Pinnacle could be withdrawn.
     - No SLA; the operator (55 Tech) is thinly documented; Liga F unverified.

3. **Pinnacle public website JSON (`guest.api.arcadia.pinnacle.com`), only as validation or last resort.**
   - Benefits:
     - The primary source itself, free and reachable from a Google IP.
     - Covers LaLiga, Segunda and Copa (17 first-round ties on 27 Oct 2026).
     - Exposes main and alternate total lines, including 2.5, and stake limits.
   - Risks:
     - Undocumented and unofficial; terms not reviewed; may break or be blocked at any time.
     - Prices are in American odds.
     - Pinnacle is unlicensed in Spain.
     - No Liga F or Primera Federación matchups at the time of checking.

4. **Betfair Exchange prices via The Odds API or OddsPapi (not the Betfair API).**
   - Benefits:
     - The tightest LaLiga margin measured (0.71%).
     - Independent of Pinnacle, so useful when Pinnacle is missing or stale.
   - Risks:
     - Thin liquidity outside top matches, so a noisy mid on Segunda, Liga F and Copa.
     - The direct Betfair API is a poor fit: US IPs blocked, read-only use with the live key not permitted, £499 activation, and a delayed key lagging 1–180 s without volume data.

5. **API-Football (paid backup).**
   - Benefits: fixtures, IDs and results across Liga F and lower divisions; join keys.
   - Risks: odds reportedly updated about daily from a limited set of books (secondary claim); free-plan season limits; Pinnacle presence unverified.

6. **Paid escalation, only if 1–3 all lose Pinnacle.**
   - Goalserve Soccer Pregame, $250 per month: names Pinnacle and Betfair; 30 s refresh; verify on a trial.
   - pinnapi, $99–$229 per month: Pinnacle only; the evidence comes from a likely affiliated source.
   - SportMonks €29 + €15, odds-api.io from £49 (no Pinnacle), and the enterprise feeds are lower value per euro for this use.

**Best manual-check websites (Saturday morning, by a human)**

1. **OddsPortal.**
   - Benefit: a broad cross-book view for LaLiga, Segunda and Copa; loads from cloud IPs.
   - Risk: its terms prohibit scraping and automation; whether Pinnacle is shown to Spanish visitors is unverified.
2. **Flashscore.es.**
   - Benefit: Spanish-licensed books (bet365, Sportium, Retabet, 1xBet, Winamax, William Hill, Betway, bwin) on the actual Quiniela fixtures, including the Liga F and Copa matches APIs miss.
   - Risk: soft-book margins of about 4–14%, so use it as a sanity check, not an anchor; Livesport terms.
3. **BetExplorer.**
   - Benefit: a secondary cross-check; loads from cloud IPs.
   - Risk: limited book visibility observed (only bet365 found in the static HTML).
4. **betfair.es exchange (logged-in Spanish account).**
   - Benefit: the only legal exchange view in Spain.
   - Risk: a separate, thinner pool than Betfair .com.
5. **Not recommended:** Oddschecker (UK books, Cloudflare-blocked), Oddspedia and Sofascore (blocked from cloud IPs).

**System-level recommendations**
- **Store provenance and freshness.** For every match, record the source (pinnacle / exchange / consensus / model-only), the timestamp and the overround. Then RPS can be evaluated per source and per competition, since Copa and Liga F behave very differently from LaLiga.
- **Dedupe the consensus.** Deduplicate identical price feeds before averaging, whatever the aggregator.
- **Size the market weight by competition.** For Copa early rounds (Pinnacle about 9% margin, $125–$250 limits), test giving the model more than half-weight relative to the market. For LaLiga near kickoff (about 3% margin, $3,000 limits), the current half-departure rule is well supported by the tiny RPS edge reported.

### Gaps
- Two parts of this ranking rest on vendor data: Pinnacle availability inside The Odds API today (not tested with a key), and OddsPapi's measurements.
- A one-week trial with both keys, logging per-book presence and `last_update` for every Quiniela match (LaLiga, Segunda, Copa, Liga F, internationals), would settle the remaining uncertainty.
