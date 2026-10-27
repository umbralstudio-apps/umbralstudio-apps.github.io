# Odds and data sources for La Quiniela's non-LaLiga matches (Liga F, Copa del Rey with lower-division clubs, national-team breaks, other SELAE inclusions) — status at 27 Oct 2026

Method note for the report writer: SELAE (loteriasyapuestas.es), RFEF (rfef.es), FBref, BeSoccer and Transfermarkt all blocked automated fetches from the research sandbox (HTTP 403, Akamai or Cloudflare). Where a claim comes from a search-engine summary of a blocked page, it is marked "(via search summary)". The statistics marked "computed" were calculated by this researcher on 27 Oct 2026 from BetExplorer's public season pages (average 1X2 odds across the bookmakers BetExplorer tracks, plus final scores with AET/AfP flags). They are descriptive only. BetExplorer's visible bookmaker set depends on the visitor's location: the sandbox was served US/Brazil-targeted promos, so a Spanish IP may see a different set.

## 1. Liga F odds: who publishes them, how early, and how efficient they are

### Takeaway
the-odds-api has no Liga F key, so for odds the system depends on OddsPapi plus scraping. Liga F matches do eventually get odds (98% of 2025/26 matches have average odds on BetExplorer, up from 66% in 2024/25). But they are priced late: four days before matchday 9 (31 Oct–2 Nov 2026), none had odds, while LaLiga and Segunda already showed 7–15 bookmakers. Margins are about twice LaLiga's (≈10% vs ≈5% overround on average odds).

### Cited Findings
- the-odds-api soccer keys for Spain are only `soccer_spain_la_liga`, `soccer_spain_segunda_division` and `soccer_spain_copa_del_rey`. There is no Liga F, Primera Federación or Copa de la Reina key. The only women's keys are `soccer_germany_bundesliga_women`, `soccer_uefa_champs_league_women` and `soccer_fifa_world_cup_womens`. The page says "These sports are covered by the API when in season" and "All usage plans give access to all available sports." — [the-odds-api sports list](https://the-odds-api.com/sports-odds-data/sports-apis.html) (full key list re-checked by grepping the page on 27 Oct 2026)
- OddsPapi (blog dated 20 Aug 2026), measured on LaLiga:
  - Unfiltered `/odds` calls return 174–192 bookmakers per fixture, 160 of them with a complete 1X2.
  - Spanish-licensed books present include `888sport.es`, `betway.es`, `bwin.es`, `codere.es`, `leovegas.es`, `paf.es`, `pokerstars.es`, `winamax.es`, and `bet365.es` on 3 of 4 fixtures.
  - Median three-way margin: Pinnacle 2.93%, `betfair-ex` 0.71%, `codere.es` 4.36%, `betway.es` 13.73%. Polymarket and Kalshi are also in the feed.
  - API: base `https://api.oddspapi.io/v4`, `apiKey` query parameter; `tournaments?sportId=10`; `fixtures` with `from`/`to` (window capped at 10 days) and a `hasOdds` filter; `odds?fixtureId=`; `historical-odds` limited to 3 bookmakers per call. Historical odds are available on the free tier back to the opening line. HTTP 429 responses carry `retryMs`.
  - Its tournament catalogue lists Primera Federación and Segunda Federación, but the article does not discuss Liga F or Copa del Rey — [OddsPapi blog, "La Liga Odds API: 192 Books…"](https://oddspapi.io/blog/?p=3654)
- One OddsPapi page says it tracks 1,372 football tournaments, including women's football among lower-tier and youth competitions. Liga F is not named, and coverage "resolves per fixture, not per league" (via search summary; exact page not pinned) — [OddsPapi API page](https://oddspapi.io/api); [OddsPapi blog](https://oddspapi.io/blog/?p=2479)
- OddsPortal has a Liga F page, which says next matches "will appear here as soon as bookmaker betting odds become available" (via search summary) — [OddsPortal Liga F](https://www.oddsportal.com/football/spain/liga-f-women/)
- **Computed, BetExplorer Liga F 2025/26:**
  - 240 matches (30 rounds × 8), 236 (98%) with average 1X2 odds.
  - Mean overround of the average odds 10.0% (median 10.0%).
  - 90-minute signs 1/X/2 = 39% / 21% / 40%.
  - The favourite won 61% of matches (implied 59%); draws 21% (implied 22%).
  - Favourites with implied probability ≥70% won 58/65 = 89% (implied 82%).
  - Source: [BetExplorer Liga F 2025/26 results](https://www.betexplorer.com/football/spain/liga-f-women-2025-2026/results/)
- **Computed, BetExplorer Liga F 2024/25:**
  - Only 158/240 matches (66%) had average odds; overround 10.0%.
  - Favourite won 56% (implied 58%); draws 22% (implied 22%).
  - Favourites ≥70% won 28/38 = 74% (implied 84%).
  - Source: [BetExplorer Liga F 2024/25 results](https://www.betexplorer.com/football/spain/liga-f-women-2024-2025/results/)
- **Computed comparison, LaLiga 2025/26:**
  - 380/380 matches with odds; average-odds overround 5.0%.
  - Signs 49% / 24% / 27%; favourite won 54% (implied 50%).
  - Source: [BetExplorer LaLiga 2025/26 results](https://www.betexplorer.com/football/spain/laliga-2025-2026/results/)
- **Observed timing (BetExplorer fixtures pages, Tue 27 Oct 2026, 09:29 UTC):**
  - Liga F: no odds for any match on 31 Oct (0/4), 1 Nov (0/3) or 2 Nov (0/1) — [BetExplorer Liga F fixtures](https://www.betexplorer.com/football/spain/liga-f-women/fixtures/)
  - LaLiga, same dates: 10/10 matches with odds (7–8 bookmakers); 6–8 Nov already had 3 bookmakers — [BetExplorer LaLiga fixtures](https://www.betexplorer.com/football/spain/laliga/fixtures/)
  - LaLiga 2: 31 Oct–2 Nov 11/11 with odds (13–15 bookmakers) — [BetExplorer LaLiga 2 fixtures](https://www.betexplorer.com/football/spain/laliga2/fixtures/)
- The previous Liga F round already showed average odds. These were the four Liga F matches in Quiniela J16 (25 Oct 2026), positions 11–14:
  - Logroño–Badalona: 2.55/3.27/2.56 (result 1-0)
  - Dep. A Coruña–Alavés: 1.83/3.47/3.86 (2-1)
  - Eibar–Madrid CFF: 3.06/3.22/2.19 (2-2)
  - Real Madrid–Costa Adeje Tenerife: 1.36/4.81/6.35 (3-2)
  - Sources: [BetExplorer Liga F](https://www.betexplorer.com/football/spain/liga-f-women/); [El Periódico de Ceuta, Quiniela J16](https://elperiodicodeceuta.es/resultado-la-quiniela-jornada-16-2026-27)
- No study specifically on the efficiency of women's football betting markets was found. A general Journal of Sports Economics paper finds that apparent inefficiencies show up in single seasons but are not persistent, and warns that significant single-season effects appear even under full efficiency. This is relevant to small Liga F samples — [Bielefeld record (JSE 2023)](https://pub.uni-bielefeld.de/record/2983980)

### Inferences
- The "no odds when the system runs" problem is mostly timing, not missing coverage: Liga F closing odds exist for nearly all matches. A second run close to the Quiniela close (Friday evening or Saturday morning) should recover most Liga F prices. Separately, BetExplorer's history (2022/23–2025/26) can calibrate a "synthetic odds" model for early runs.
- A ≈10% average-odds overround (vs ≈5% in LaLiga) means a larger and less uniform margin to remove. The de-vig method (multiplicative vs power/Shin) matters more in Liga F. Pinnacle or exchange prices, where available through OddsPapi, should be preferred over averages.
- On one round's sample, SELAE's Liga F picks in J16 avoided the most lopsided games (Barcelona–Granada at 1.01 was not chosen; three of the four chosen had a favourite priced at 1.83 or longer). So Liga F slots tend to be genuinely uncertain, and good probabilities matter.
- Liga F's raw home and away win rates were almost equal in 2025/26 (39% vs 40%). The Dixon-Coles home-advantage parameter for Liga F should be estimated separately and is probably small, not borrowed from men's football.

### Gaps
- Whether Pinnacle and Betfair Exchange price Liga F, how early, and with what limits or liquidity: not verifiable (BetExplorer's per-match bookmaker endpoint returned 404; OddsPortal is JavaScript-rendered).
- OddsPapi's Liga F tournament ID and its per-fixture coverage and lead time were not verified (it needs an API key). The user's own logs are the best evidence.
- API-Football's Liga F league ID and its odds coverage were not verified; [api-football.com/coverage](https://www.api-football.com/coverage) returned 403. Check with `GET /leagues?country=Spain`.
- The exact hour when Liga F odds appear (Thursday? Friday?) was not measured; only a single snapshot four days before was observed.

## 2. Liga F data: official sources, stats/xG, historical datasets, women's club ratings

### Takeaway
There is no free CSV or API equivalent of football-data.co.uk for Liga F. The practical sources are en.ligaf.es (official, reachable), Wikipedia season pages, and BetExplorer season pages (results plus average odds, one page per season). FBref lost all Opta advanced stats on 20 Jan 2026. FotMob and Sofascore have rich data but their unofficial APIs were blocked or changed from a cloud IP. The only serious women's club rating is the Opta Power Rankings (2,500+ women's clubs), which is interactive only, with no download.

### Cited Findings
- Wikipedia's Liga F page says:
  - The league was "granted professionalised league status" on 10 June 2020 and became "fully professional" from 2021–22, cut from 18 to 16 teams.
  - Barcelona won 2022/23–2025/26 (2025/26: 87 points, Real Madrid 72).
  - Season pages exist: "2026–27 Liga F", "2025–26 Liga F", "2024–25 Liga F", "2023–24 Liga F", "2022–23 Liga F", "2021–22 Primera División (women)".
  - Source: [Wikipedia: Liga F](https://en.wikipedia.org/wiki/Liga_F)
  - Other sources may date the professional status to 2021; this was not cross-checked.
- BetExplorer's 2025/26 Liga F page lists 240 matches in 30 rounds (16 teams). Its 2026/27 page shows the 16 current clubs: Barcelona, Real Madrid, Atlético, Real Sociedad, Athletic, Sevilla, Granada, Valencia, Eibar, Espanyol, Logroño, Madrid CFF, Dep. A Coruña, Alavés, Badalona, Costa Adeje Tenerife. Its season selector goes back to 2021/22 and earlier — [BetExplorer Liga F 2025/26](https://www.betexplorer.com/football/spain/liga-f-women-2025-2026/results/); [BetExplorer Liga F current](https://www.betexplorer.com/football/spain/liga-f-women/)
- en.ligaf.es returned HTTP 200 to a scripted request from the cloud sandbox on 27 Oct 2026 — [en.ligaf.es](https://en.ligaf.es/)
- FBref: on 20 January (2026), Sports Reference removed advanced statistics "effective immediately". Stats Perform said it terminated FBref's access for violating the agreement's terms. The women's game was hit hardest: FBref had added 10 women's competitions after moving to Opta in 2022. Scores and top-scorer tables remain. The article is dated 4 Feb 2026. Suggested alternatives: Opta Analyst, Understat, OneFootball, WhoScored, Forza, Sofascore, FotMob. The article says Opta's Analyst site shows only two women's competitions — [The IX](https://www.theixsports.com/the-ix-soccer/fbrefs-loss-advanced-stats-womens-soccer-data-accessibility/)
- FBref still hosts Liga F club pages (e.g., Levante Women 2024/25) — [FBref Levante Women](https://fbref.com/en/squads/0f4738a8/2024-2025/Levante-Women-Stats). A scripted request to an FBref Liga F schedule URL returned 403 from the sandbox on 27 Oct 2026.
- Opta Power Rankings (article dated 27 Jul 2026):
  - Covers "over 13,500 men's domestic football teams" from "183 different FIFA member countries and 562 unique domestic leagues", plus "over 2,500 women's clubs".
  - Scale 0–100, updated daily.
  - Women's view: `?type=womens`. No downloadable data is offered.
  - Source: [The Analyst – Opta Power Rankings](https://theanalyst.com/articles/who-are-the-best-football-team-in-the-world-opta-power-rankings); [women's view](https://theanalyst.com/articles/who-are-the-best-football-team-in-the-world-opta-power-rankings?type=womens)
- A press reproduction of Opta's women's top 30 lists Barcelona 100.00, Bayern 96.14, Chelsea 94.47, Man City 93.59. It is dated "Monday 24 August", probably 2026 but unconfirmed — [UnoTV](https://www.unotv.com/deportes/america-entra-al-top-30-de-los-mejores-clubes-femeniles-del-mundo-segun-opta/)
- Opta's supercomputer combines betting-market odds with the Power Rankings to produce match probabilities (via search summary) — [The Analyst supercomputer explainer](https://theanalyst.com/2024/05/opta-supercomputer-premier-league-2023-24-predictions)
- No public Elo for women's clubs (ClubElo-style) was found. Search results only turned up Opta, video-game ratings and individual-player Elo sites — [Opta via UnoTV](https://www.unotv.com/deportes/america-entra-al-top-30-de-los-mejores-clubes-femeniles-del-mundo-segun-opta/); [wazygoose (player Elo, irrelevant)](https://wazygoose.com/Leagues/EloRankings/44/673/northern-ladies-league-elo-ratings-league-ending-16-may-2025)
- Scripted tests from the sandbox on 27 Oct 2026:
  - `https://api.sofascore.com/api/v1/unique-tournament/17073/seasons` → 403.
  - `https://www.fotmob.com/api/leagues?id=8968` → 404.
  - Sofascore's and FotMob's public web pages for Spanish competitions do exist — [Sofascore Primera Federación](https://www.sofascore.com/tournament/football/spain/primera-federacion/17073); [FotMob Primera Federación](https://www.fotmob.com/en-GB/leagues/8968/stats/primera-federacion/teams)

### Inferences
- The most robust Liga F history for Colab is BetExplorer, at one HTTP request per season (results plus average closing odds), joined to Wikipedia or ligaf.es for team names and standings. This gives about 960 matches (2022/23–2025/26) with market prices, enough to fit a market-implied strength model (for example Elo or Bradley–Terry on de-vigged odds). That would likely beat Poisson/Dixon-Coles built only from standings when odds are missing.
- Opta's women's ratings could serve as a manual or semi-automated prior: map the 0–100 score to a rating gap, then calibrate on BetExplorer odds. With no API, it is a weekly manual step, not a pipeline.
- xG for Liga F is no longer freely available through FBref. FotMob and Sofascore web pages may show it, but scraping them from Colab is fragile. Treat xG as optional.

### Gaps
- Whether ligaf.es exposes a JSON or API endpoint (fixtures, results) was not checked beyond a 200 on the home page.
- No free, maintained Liga F CSV dataset (Kaggle or GitHub) was located or verified.
- Whether FotMob or Sofascore currently show Opta xG for Liga F matches was not verified.
- Opta's women's Power Rankings for individual Liga F clubs (beyond Barcelona) could not be extracted.

## 3. Copa del Rey: format for 2025/26–2026/27, and which result counts for the Quiniela sign

### Takeaway
Every tie is single-leg until the semi-finals, which are two-legged, and the lower-category club hosts until the quarter-finals. The first round of 2026/27 is being played 27–29 Oct 2026 (Quiniela J17 = Copa). Crucially for the model, lottery sources citing SELAE's norma 40ª say the Quiniela sign uses the result when the referee ends the match, extra time included and penalties excluded. Bookmaker 1X2 markets settle at 90 minutes, so the two do not match.

### Cited Findings
- **2026/27 format (RFEF news; via search summary, direct fetch blocked):**
  - 116 participants; 112 enter the first round as 56 single-leg ties played 27–29 Oct (nominal date 28 Oct).
  - The 4 Supercopa clubs enter in the round of 32.
  - Draw on 5 Oct 2026 at the Ciudad del Fútbol, with 4 pots by category. When two clubs of the same category meet, the first one drawn hosts.
  - 10 first-round clubs come from regional categories via a two-legged preliminary round (stated as 26 Sep–4 Oct).
  - Second round on 2 Dec 2026.
  - Sources: [RFEF – distribución de grupos](https://rfef.es/es/noticias/conocida-la-distribucion-de-los-grupos-para-el-sorteo-de-la-primera-eliminatoria); [RFEF – 56 eliminatorias](https://rfef.es/es/noticias/56-eliminatorias-emplazadas-para-vivir-la-fiesta-de-la-copa); [RTVC – Atlético Paso v Córdoba](https://rtvc.es/atletico-paso-recibira-cordoba-cf-primera-eliminatoria-copa-del-rey-2026-27/)
  - Conflict: BetExplorer lists preliminary-round legs on 11 Oct 2026 (e.g., Unión Güímar–Hortaleza 3:3 AET; Prat–El Espinar Sant Rafel 5:0) — [BetExplorer Copa del Rey](https://www.betexplorer.com/football/spain/copa-del-rey/)
- **2026/27 calendar:**
  - First round 28 Oct 2026; second round 2 Dec; round of 32 16 Dec; round of 16 6 Jan 2027; quarter-finals 13 Jan; semi-finals 10 Feb and 3 Mar (two legs); final 24 Apr 2027 at La Cartuja (third year in a row, agreement covering 2026–2028).
  - The lower-category club hosts "hasta los cuartos de final".
  - Source: [El Gol Digital](https://www.elgoldigital.com/futbol/copa-del-rey/copa-del-rey-2026-27-calendario-fechas-final-cartuja/)
- BetExplorer's 2026/27 fixtures show the first round split as 18 ties on 27 Oct, 24 on 28 Oct and 14 on 29 Oct — [BetExplorer Copa fixtures](https://www.betexplorer.com/football/spain/copa-del-rey/fixtures/)
- 2025/26 used the same structure: a 56-tie single-match first round on 28–30 Oct 2025, with Barcelona, Real Madrid, Atlético and Athletic (the Supercopa clubs) exempt (via search summary) — [RFEF 2025/26 first round](https://rfef.es/es/noticias/56-eliminatorias-partido-unico-con-horario-decidido-para-la-primera-ronda-de-la-copa-del)
- BetExplorer's stage structure confirms the format in 2023/24–2025/26: preliminary (1/128), then 1/64 (55–56 ties), 1/32 (28), 1/16 (16), 1/8 (8), quarter-finals (4) as single matches, two-legged semi-finals, and the final. Results carry AET/AfP flags (computed) — [BetExplorer Copa 2025/26](https://www.betexplorer.com/football/spain/copa-del-rey-2025-2026/results/)
- **Quiniela rule:** "sí, cuenta [la prórroga] en la Quiniela"; "únicamente no se cuentan los penaltis".
  - TuLotero cites norma 40ª ("para determinar el acierto de cada pronóstico se considerará como resultado de cada partido que interviene en el concurso…" the result when the referee ends the match). A TuLotero reply dated 28 Apr 2025 says the same applies to the Pleno al 15. Page updated 18 Apr 2024 — [TuLotero](https://tulotero.es/cuenta-la-prorroga-en-la-quiniela/)
  - The same reading appears in other lottery-agency explainers — [La Fortuna de Montserrat](https://www.lafortunademontserrat.es/blog/resultados-de-la-quiniela.htm); [Loterías 1 Fuengirola](https://www.loterias1fuengirola.com/blog/cuenta-la-prorroga-en-la-Quiniela.htm)
  - A forum puts it as "La quiniela no entiende de eliminatorias, entiende de partidos" — [foro1x2](http://www.foro1x2.com/viewtopic.php?t=47499)
  - An official SELAE notice quoting norma 40ª ("…el obtenido en el terreno de juego en el momento en que el árbitro lo dé por finalizado") exists, but the PDF returned 403; quoted via search summary — [SELAE aviso (PDF)](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/SUSPENSI%C3%93N%20PARTIDO%20DINAMARCA%20UCRANIA%20JDA%2066.pdf)
- By contrast, bookmaker cup bets "cuentan solo los 90 minutos" (informal forum source) — [laps4 forum](https://www.laps4.com/comunidad/goto/post?id=4176919)
- **Computed, BetExplorer Copa 1/64 + 1/32 + 1/16 rounds, 2023/24–2025/26 (n=297 ties with odds):**
  - 68 (23%) went to extra time. 39 of those (57%) were decided in extra time, and the favourite won 29 of them (74%). The other 29 (43%) went to penalties.
  - Quiniela signs (extra time counts, penalties = X): 1/X/2 = 22% / 10% / 69%.
  - The 90-minute market implied 19% / 22% / 58%.
  - Sources: [2025/26](https://www.betexplorer.com/football/spain/copa-del-rey-2025-2026/results/); [2024/25](https://www.betexplorer.com/football/spain/copa-del-rey-2024-2025/results/); [2023/24](https://www.betexplorer.com/football/spain/copa-del-rey-2023-2024/results/)
- **Computed, first round (1/64) only, 3 seasons (n=166):**
  - 38 (23%) were level at 90 minutes; 16 went to penalties.
  - Quiniela X only 16/166 = 9.6%, against an average implied 90-minute draw of about 21%.
  - Quiniela 1 = 33/166 = 19.9%; 2 = 117/166 = 70.5%.
  - By season: 2025/26 21/12/66%; 2024/25 18/5/76%; 2023/24 20/11/69% — same sources as above.

### Inferences
- **This is probably the largest single fixable error in Copa jornadas (J17, J26, J30).** Feeding de-vigged 90-minute 1X2 odds straight into a Quiniela forecast overstates X by about 12 points and understates the favourite. A simple transformation using the pooled rates (q_pen ≈ 0.43, s_fav ≈ 0.74):
  - P_Q(X) = P90(X)·q_pen
  - P_Q(fav) = P90(fav) + P90(X)·(1−q_pen)·s_fav
  - P_Q(dog) = P90(dog) + P90(X)·(1−q_pen)·(1−s_fav)
  - Applied to the first-round average implied 17/21/62, it gives about 20/9/71. That matches the observed 19.9/9.6/70.5.
- Because P_Q(X) is rarely above 12–13% in single-leg Copa ties, X should almost never be the chosen sign there. The same logic applies to Elige 8 picks and a Copa Pleno al 15 (extra-time goals count).
- For the two-legged semi-finals, the Quiniela still scores each leg as a match, so extra time in a second leg only matters if that leg is level at 90 minutes.

### Gaps
- The official text of norma 40ª and any SELAE norm on extra time could not be read directly (SELAE returns 403). The user should confirm on loteriasyapuestas.es before changing the model. Another researcher covers the general rules.
- Which of the 56 first-round ties SELAE put on J17 (28 Oct), and whether any are Tuesday matches, was not found.

## 4. Copa del Rey: odds for early-round ties with Federación and regional clubs (availability, timing) and upset evidence

### Takeaway
Odds for modest Copa ties do exist eventually: all 166 first-round ties in 2023/24–2025/26 have average odds on BetExplorer, and even regional preliminary ties often do. But they appear very late. On 27 Oct 2026 at 09:29 UTC, the 18 ties played that day had 10–12 bookmakers, while the 38 ties on 28–29 Oct had none. In the history, the market was well calibrated or even conservative on strong favourites. There is no evidence that "Copa magic" is underpriced.

### Cited Findings
- **Observed, BetExplorer fixtures, 27 Oct 2026 09:29 UTC:** 27 Oct ties 18/18 with odds (10–12 bookmakers); 28 Oct 0/24; 29 Oct 0/14 — [BetExplorer Copa fixtures](https://www.betexplorer.com/football/spain/copa-del-rey/fixtures/)
- Same-day examples (average odds):
  - Cuarte–Girona 14.80/6.63/1.16
  - Pinatar–Elche 38.26/14.61/1.03
  - Sestao–Espanyol 6.18/4.20/1.46
  - Calamocha–CE Europa 4.29/3.64/1.74
  - Castellonense–Almería 6.60/4.33/1.43
  - Source: [BetExplorer Copa del Rey](https://www.betexplorer.com/football/spain/copa-del-rey/)
- 2026/27 preliminary-round ties with average odds include San José–Auriense 1.94/3.46/3.35, Tedeón–Anaitasuna 180/15.5/1.01 and Ceuta 6 de Junio–Lebrijana 300/11.5/1.02 — [BetExplorer Copa del Rey](https://www.betexplorer.com/football/spain/copa-del-rey/)
- **Computed, odds coverage:**
  - 2025/26: 126 of 137 Copa matches (92%) had odds; all 11 without were preliminary-round legs (e.g., Campanario–CD Yuncos, Deportivo Getxo–Betis Valladolid).
  - 2024/25: 125/126 (only Dolorense–Manises missing).
  - 2023/24: 125/126 (Unionistas–Villarreal, round of 32, missing).
  - Average-odds overround: 6.9%, 7.3% and 6.0%.
  - Sources: [2025/26](https://www.betexplorer.com/football/spain/copa-del-rey-2025-2026/results/); [2024/25](https://www.betexplorer.com/football/spain/copa-del-rey-2024-2025/results/); [2023/24](https://www.betexplorer.com/football/spain/copa-del-rey-2023-2024/results/)
- **Computed, calibration (all rounds, 90 minutes):**
  - Favourites with implied probability ≥70% won 28/32 (88%, implied 84%) in 2025/26, 30/36 (83%, implied 82%) in 2024/25, and 30/33 (91%, implied 83%) in 2023/24.
  - Draws at 90 minutes: 25%, 22% and 26%, against implied 22%, 23% and 23%.
  - Same sources as above.
- **Computed, first round 90-minute results:**
  - Home underdog wins in 90 minutes: 16% (2025/26), 13% (2024/25), 13% (2023/24), against an implied ≈17–18%.
  - Including wins in extra time, underdog "1" signs rose to 18–21% (section 3).
  - Same sources as above.
- **Anecdotal upset evidence:**
  - 2022/23 first round: Cádiz (3-2 at Real Unión) and Almería (2-0 at Arenteiro) were the only LaLiga sides eliminated (via search summary) — [Soccerway](https://es.soccerway.com/noticias/real-union-y-arenteiro-se-cargan-a-cadiz-y-almeria-unicos-de-primera-eliminados-en-copa/Ig6a9HcE)
  - Under the new format, Alavés was the first LaLiga club eliminated by a Tercera side "in almost four decades" (via search summary) — [Goal](https://www.goal.com/es/noticias/alaves-la-primera-victima-de-la-nueva-copa-del-rey/k7jwrkoz7ich125ttxyd9o5mz)
- the-odds-api has a `soccer_spain_copa_del_rey` key ("with scores"). Its coverage of early-round ties against Federación or regional clubs, and how early, was not testable without a key — [the-odds-api sports list](https://the-odds-api.com/sports-odds-data/sports-apis.html)

### Inferences
- The fallback trigger ("no odds → Copa Elo by category") fires mainly because the system runs before bookmakers price the minor ties, not because markets never exist. Re-running on the morning of each matchday (or hourly near the deadline) and querying OddsPapi with `hasOdds` should convert many fallbacks into market prices. This only helps when the Quiniela's close comes after the first prices appear; for Thursday ties in a Wednesday-dated jornada, it may not.
- When a fallback is unavoidable, calibrate it on BetExplorer's ~166 historical first-round ties: implied probability as a function of the category pairing (LaLiga at Segunda Federación, Segunda at Tercera, and so on, with categories from RFEF or Futbolme). That is a better-grounded replacement for an Elo-by-category guess. Then apply the extra-time transformation from section 3.
- The calibration data says the market slightly underrates strong favourites in Copa ties, rather than overrating them. So the system's "half-departure" from the market should not tilt towards cup upsets.

### Gaps
- Which bookmakers (Pinnacle? bet365.es? Betfair Exchange?) price these ties first, and how many hours before kick-off: not measurable without per-match bookmaker data (BetExplorer's per-match endpoint returned 404). OddsPapi's `historical-odds` endpoint could answer this per fixture (opening-line timestamps).
- The observation is a single snapshot from a non-Spanish IP. Spanish-licensed books may price earlier than BetExplorer's visible set.
- No academic study of Spanish cup upset rates by category gap was found.

## 5. Copa del Rey: data and ratings for lower-division clubs (Primera, Segunda and Tercera Federación, regional)

### Takeaway
ClubElo, the system's current cup fallback, looked broken from the sandbox on 27 Oct 2026: the snapshot API returned 502 on every attempt, the Fixtures API reports "deactivated", and the website sits behind a Cloudflare challenge. It also historically covers only top divisions (coverage of Spain's third tier could not be checked because of the outage). For lower-division data, BetExplorer (results plus odds for Primera RFEF and Segunda RFEF groups) and Futbolme were reachable. RFEF, BeSoccer and Transfermarkt blocked scripted access. FotMob and Sofascore have Federación pages but their APIs were blocked. Opta Power Rankings (13,500 men's teams, 562 leagues) is the most plausible professional rating covering these clubs, but this is not verified and it has no API.

### Cited Findings
- **ClubElo tests from the sandbox, 27 Oct 2026:**
  - `http://api.clubelo.com/2026-10-26`, `/2026-10-25`, `/2026-10-01` and `/2026-06-01` → HTTP 502.
  - `http://api.clubelo.com/Barcelona` (club history) → 502.
  - `https://api.clubelo.com/...` → connection reset.
  - `http://api.clubelo.com/Fixtures` → "Fixtures API deactivated".
  - `clubelo.com/ESP` → redirect to HTTPS, then Cloudflare "Just a moment…" (403).
  - Source: [api.clubelo.com/Fixtures](http://api.clubelo.com/Fixtures); [clubelo.com/ESP](http://clubelo.com/ESP)
- **Computed, BetExplorer Segunda RFEF (4th tier) Group 1 2025/26:**
  - 306 matches, 276 (90%) with average odds; overround 10.2%.
  - Signs 42% / 27% / 31%; favourite won 44% (implied 47%).
  - Source: [BetExplorer Segunda RFEF G1 2025/26](https://www.betexplorer.com/football/spain/segunda-rfef-group-1-2025-2026/results/)
- A Primera RFEF Group 1 results page also exists, with average odds (270 odds cells in the current season) — [BetExplorer Primera RFEF G1](https://www.betexplorer.com/football/spain/primera-rfef-group-1/results/)
- **Observed, 27 Oct 2026:** Primera RFEF G1 and Segunda RFEF G1 fixtures for 31 Oct–1 Nov had no odds yet — [Primera RFEF G1 fixtures](https://www.betexplorer.com/football/spain/primera-rfef-group-1/fixtures/); [Segunda RFEF G1 fixtures](https://www.betexplorer.com/football/spain/segunda-rfef-group-1/fixtures/)
- FotMob has Primera Federación league pages and Segunda Federación match pages. Its pages advertise "Real-time extensive stats powered by Opta: … xG …", which may be generic text (via search summary) — [FotMob Primera Federación](https://www.fotmob.com/en-GB/leagues/8968/stats/primera-federacion/teams); [FotMob Sabadell–Sestao](https://www.fotmob.com/en-GB/matches/sabadell-vs-sestao/18rdkz)
- Sofascore has a Primera Federación tournament page (ID 17073) — [Sofascore](https://www.sofascore.com/tournament/football/spain/primera-federacion/17073). Its API returned 403 from the sandbox.
- **Scripted HTTP status from the sandbox, 27 Oct 2026:**
  - futbolme.com: 301 to the non-www host (reachable).
  - besoccer.com: 403.
  - transfermarkt.es: 405.
  - int.soccerway.com: 307 to www.soccerway.com (site restructured).
  - rfef.es: Cloudflare challenge (403).
  - Sources: [Futbolme](https://futbolme.com/); [BeSoccer](https://www.besoccer.com/); [Transfermarkt](https://www.transfermarkt.es/); [Soccerway](https://www.soccerway.com/); [RFEF](https://rfef.es/es/noticias/competiciones-masculinas/copa-del-rey)
- Opta Power Rankings cover 13,500+ men's teams in 562 domestic leagues and 183 countries, updated daily. The page does not list which Spanish tiers are included — [The Analyst](https://theanalyst.com/articles/who-are-the-best-football-team-in-the-world-opta-power-rankings)

### Inferences
- The ClubElo dependency is now a reliability risk as well as a coverage risk: even LaLiga clubs' ratings may be unavailable when the Copa fallback needs them. Cache the last good ClubElo snapshot, or derive club strength from market odds (BetExplorer or OddsPapi history) instead.
- For category labels and current form of Federación clubs, BetExplorer group pages (one request per group per season) give results plus odds. Futbolme is a reachable Spanish alternative for tables. RFEF is authoritative but impractical to scrape.

### Gaps
- Whether ClubElo's outage is temporary or specific to cloud IPs (Colab may behave the same or differently) is unknown. The user should test from Colab.
- Whether Opta Power Rankings include Primera, Segunda or Tercera Federación clubs, and whether its data can be pulled programmatically: not verified.
- Futbolme's data formats and terms were not inspected.

## 6. International matches in the Quiniela: competitions used and best odds/ratings sources

### Takeaway
For 2026/27, SELAE's provisional calendar names only the Nations League (M) as the "other competition" in break jornadas. These are J9 (27 Sep), J10 (30 Sep), J11 (4 Oct), J21 (15 Nov) and J22 (18 Nov), always mixed with Segunda and Liga F on the Sundays. The user's existing `soccer_uefa_nations_league` key covers it. World Football Elo (eloratings.net) TSV files were reachable and current, making them the best free rating fallback.

### Cited Findings
- **SELAE-branded provisional calendar 2026/27** ("Este calendario es PROVISIONAL…"):
  - J9 27/09: Segunda J7 + Liga F J5 + Nations League (M).
  - J10 30/09 (Wednesday): "Nations League (M) / Otras".
  - J11 04/10: Segunda J8 + Liga F J6 + Nations League (M).
  - J21 15/11: Segunda J14 + Liga F J11 + Nations League (M).
  - J22 18/11: "Nations League (M)" + "Champions League (F)".
  - Source: [SELAE calendar PDF (hosted by El Quinielista)](https://www.elquinielista.com/Quinielista/web/pdfs/CALENDARIO_La_Quiniela.pdf)
- Conflict on J21: Quinielafutbol.info lists "Primera, Liga F, Nations League" and says the Spanish national team is always included when it plays in FIFA windows — [Quinielafutbol.info](https://www.quinielafutbol.info/bases-del-juego/calendario-la-quiniela.html). Maxiloto agrees with the PDF (Segunda + Liga F + NL) and warns that SELAE does not confirm NL matches for 18/11 — [Maxiloto](https://www.maxiloto.es/blog/calendario-de-la-liga-de-futbol-profesional.htm)
- The same PDF's Quinigol calendar puts Nations League matchdays on 24/09 (Thursday), 30/09, 12/11 (Thursday), 15/11 and 17/11 (Tuesday) — [SELAE calendar PDF](https://www.elquinielista.com/Quinielista/web/pdfs/CALENDARIO_La_Quiniela.pdf)
- eloratings.net serves plain TSV files:
  - `World.tsv` (current ratings; row 1 is Spain at 2287, then Argentina 2175 and England 2146).
  - `latest.tsv` (recent results, latest dated 2026-10-06).
  - `2026.tsv`.
  - All returned HTTP 200 to a scripted request on 27 Oct 2026. Teams use 2-letter codes (ES, AR, EN…).
  - Source: [eloratings World.tsv](https://www.eloratings.net/World.tsv); [eloratings latest.tsv](https://www.eloratings.net/latest.tsv)
- the-odds-api international keys: `soccer_uefa_nations_league`, `soccer_fifa_world_cup_qualifiers_europe`, `soccer_uefa_euro_qualification`, `soccer_fifa_world_cup` and others. There is no friendlies key — [the-odds-api sports list](https://the-odds-api.com/sports-odds-data/sports-apis.html)
- Precedents for national-team matches in the Quiniela:
  - Qatar 2022: Spain's matches were the Pleno al 15 in jornadas 24–26 (via search summary) — [Moncloa.com](https://www.moncloa.com/2022/11/24/millonapp-sobre-jugar-la-quiniela-online-del-mundial-de-futbol-qatar-2022-1725220/)
  - A June 2024 jornada had Spain–Croatia (Euro 2024) as match 15 — [Periódico de Ibiza](https://www.periodicodeibiza.es/noticias/sorteos-loterias/2024/06/16/2185403/quiniela-resultado-del-domingo-junio-2024-2.html)

### Inferences
- National-team matches are well-priced, liquid markets. The-odds-api plus OddsPapi as backup should cover NL matches days in advance, so international slots are a minor weakness compared with Liga F and Copa.
- eloratings.net is the natural no-odds fallback, and a prior for "Otras" (friendlies). It is free, current and needs one request.
- Euro 2028 qualifying (key `soccer_uefa_euro_qualification`) presumably takes over in 2027 break jornadas. This is unverified.

### Gaps
- The actual competitions in 2025/26 break jornadas (World Cup qualifiers in Sep/Oct/Nov 2025, friendlies or play-offs in March 2026, World Cup 2026 jornadas in June/July 2026) could not be verified: SELAE pages were blocked and searches returned nothing specific.
- What "Otras" means in J10 (30 Sep 2026) is unknown.
- Whether Opta publishes national-team power ratings was not verified. The FIFA ranking was not evaluated.

## 7. Other competitions SELAE includes now (2026/27), and how to source their odds

### Takeaway
Beyond LaLiga, Segunda, Liga F, Copa and the Nations League, the 2026/27 calendar includes European club competitions (midweek), the UEFA Women's Champions League (J22), the Copa de la Reina (J31) and the Premier League (J32, 27 Dec). Liga F appears in 14 of the 32 jornadas up to 27 Dec 2026, so it is a recurring, not an occasional, weakness.

### Cited Findings
- **SELAE provisional calendar 2026/27:**
  - Champions League (J5, 09/09).
  - "Europa League (M)" (J7, 16/09).
  - "Champions / Europa / Conference League (M)" in J13, J15, J19, J24 and J28 (J28 also Liga F J13).
  - Copa del Rey in J17 (28/10), J26 (02/12) and J30 (16/12, "Copa del Rey / Otras").
  - "Copa de la Reina" in J31 (20/12).
  - "Premier League (M) / Otras" in J32 (27/12).
  - Liga F matchdays 1–14 appear in J3, J4, J6, J8, J9, J11, J14, J16, J18, J20, J21, J23, J28 and J29.
  - Source: [SELAE calendar PDF](https://www.elquinielista.com/Quinielista/web/pdfs/CALENDARIO_La_Quiniela.pdf)
- Midweek jornadas on 14 and 21 Oct 2026 listed European club matches (Oporto, Liverpool, Manchester City, Real Madrid) (via search summary; page blocked) — [SELAE escrutinio 21 Oct 2026](https://www.loteriasyapuestas.es/es/la-quiniela/escrutinios/la-quiniela-premios-y-ganadores-del-21-de-octubre-de-2026)
- the-odds-api has `soccer_uefa_champs_league_women` and `soccer_epl`, but no Copa de la Reina or Primera Federación key — [the-odds-api sports list](https://the-odds-api.com/sports-odds-data/sports-apis.html)
- Liga F J8 (Quiniela J16) took 4 of the 14 slots (positions 11–14) — [El Periódico de Ceuta](https://elperiodicodeceuta.es/resultado-la-quiniela-jornada-16-2026-27)

### Inferences
- Two cheap fixes for the user's key list: add `soccer_uefa_champs_league_women` (J22) and `soccer_epl` (J32). Copa de la Reina early rounds pair Liga F and lower women's clubs: odds will be late and thin, so the extra-time transformation plus OddsPapi or BetExplorer apply, as for the Copa del Rey.
- Primera Federación does not appear as a regular column in 2026/27. If it appears under "Otras", OddsPapi (whose catalogue lists it) and BetExplorer (results plus odds, late pricing) are the sources.

### Gaps
- The January–May 2027 calendar was not yet published at the time of the sources.
- The BetExplorer slug for Copa de la Reina (tried `copa-de-la-reina-2025-2026`) redirected away, so its odds coverage is unverified.
- Whether SELAE used Primera Federación or foreign leagues in 2025/26 special jornadas was not verified.

## 8. Ranked shortlist per competition, with concrete benefit and risk for ORÁCULO 1X2 v3.2

### Takeaway
The highest-value changes are mostly about timing and correct use of data rather than new subscriptions:
1. Convert 90-minute odds to Quiniela signs for cup ties (extra time counts, penalties = X).
2. Re-run close to the Quiniela close, because Liga F and Copa odds appear late.
3. Replace the ClubElo-based fallback with ratings calibrated on historical market odds (BetExplorer and OddsPapi).
4. Add two the-odds-api keys (women's Champions League, Premier League).

### Cited Findings
- Copa extra-time effect: Quiniela X ≈10% vs 90-minute implied ≈22% (n=297, computed) — [BetExplorer Copa 2025/26](https://www.betexplorer.com/football/spain/copa-del-rey-2025-2026/results/); rule per [TuLotero](https://tulotero.es/cuenta-la-prorroga-en-la-quiniela/)
- Late pricing on 27 Oct 2026: Liga F, Federación leagues and next-day Copa ties had 0 odds, while LaLiga and Segunda had 7–15 bookmakers — [BetExplorer Liga F fixtures](https://www.betexplorer.com/football/spain/liga-f-women/fixtures/); [BetExplorer Copa fixtures](https://www.betexplorer.com/football/spain/copa-del-rey/fixtures/)
- ClubElo returned 502 and its Fixtures API is deactivated — [api.clubelo.com/Fixtures](http://api.clubelo.com/Fixtures)
- OddsPapi: 10-day fixture window, `hasOdds` filter, historical odds on the free tier (3 bookmakers per call), Pinnacle at 2.93% median margin — [OddsPapi blog](https://oddspapi.io/blog/?p=3654)

### Inferences
**Liga F (ranked)**
1. **OddsPapi** (already integrated).
   - Benefit: widest book set (Pinnacle and exchanges where priced). Its `historical-odds` endpoint can also show when Liga F lines open, to schedule runs.
   - Risk: a 250 requests/month budget against 14 Liga F jornadas through December; per-fixture coverage unverified; prices arrive late.
2. **Late re-run** on Friday evening or Saturday morning, plus a check of OddsPortal or BetExplorer fixtures.
   - Benefit: turns most "no odds" cases into market prices; 98% of 2025/26 Liga F matches ended up with odds.
   - Risk: Liga F kick-offs from Saturday 12:00 leave a narrow window before the Quiniela closes.
3. **BetExplorer season pages** as the history and calibration set (2022/23–2025/26, about 960 matches with average closing odds).
   - Benefit: a market-implied strength model that beats standings-based Poisson when odds are missing; Liga F-specific home advantage and draw rates (21–22%).
   - Risk: scraping and terms of use, a geo-dependent bookmaker set, HTML changes, no API.
4. **Opta women's Power Rankings**.
   - Benefit: an independent professional rating covering every Liga F club.
   - Risk: interactive only, no download, so a manual weekly step; mapping 0–100 to probabilities needs calibration.
5. **en.ligaf.es** (official tables) plus **Wikipedia season pages**.
   - Benefit: reachable, authoritative fixtures and standings.
   - Risk: no odds or xG; Wikipedia edits can lag.
6. Lower priority:
   - FBref: scores only since 20 Jan 2026, and 403 to cloud IPs.
   - FotMob and Sofascore: rich data, but APIs returned 403/404 from the cloud.
   - the-odds-api: no Liga F key.

**Copa del Rey with lower-division clubs (ranked)**
1. **Extra-time transformation** of any 90-minute probabilities (q_pen ≈ 0.43, favourite wins ≈74% of ties decided in extra time).
   - Benefit: removes a ~12-point overstatement of X in J17, J26 and J30.
   - Risk: the rule should be confirmed against the official norma 40ª text, and the parameters come from 68 extra-time ties, so they are noisy.
2. **OddsPapi with `hasOdds`, re-polled on matchday**.
   - Benefit: earliest and widest prices.
   - Risk: about 17 requests per jornada, and minor ties may still be unpriced before the close.
3. **the-odds-api `soccer_spain_copa_del_rey`**.
   - Benefit: cheap, already integrated.
   - Risk: coverage of Federación-host ties unverified.
4. **BetExplorer Copa pages** (2023/24–2025/26 history; same-day prices with 10–12 bookmakers).
   - Benefit: a calibration set for a category-pairing fallback (about 166 first-round ties), plus same-day prices for late runs.
   - Risk: same scraping risks as above; prices appear only on matchday.
5. **Category fallback recalibrated on market history**, replacing ClubElo.
   - Benefit: removes the dependency on a failing API.
   - Risk: categories must be kept current (RFEF blocks scraping; Futbolme or BetExplorer group pages work).
6. **Opta Power Rankings** as a cross-check.
   - Benefit: may cover Federación clubs (13,500 teams).
   - Risk: lower-tier coverage unverified; no API.

**International breaks (ranked)**
1. **the-odds-api `soccer_uefa_nations_league`** (plus qualifiers keys).
   - Benefit: already integrated; liquid markets priced well ahead.
   - Risk: no friendlies key for "Otras".
2. **OddsPapi** for friendlies and "Otras".
   - Benefit: covers what the-odds-api lacks.
   - Risk: request budget.
3. **eloratings.net TSV** (`World.tsv`, `latest.tsv`).
   - Benefit: free, current (to 6 Oct 2026), one request, a strong no-odds fallback.
   - Risk: 2-letter team codes need a mapping table; unofficial site.
4. FIFA ranking or Opta: not recommended or not verified as additions.

**Other SELAE inclusions**
- Add `soccer_uefa_champs_league_women` (J22) and `soccer_epl` (J32).
  - Benefit: free coverage with keys already supported.
  - Risk: none significant.
- Copa de la Reina (J31): OddsPapi or BetExplorer plus the extra-time transformation.
  - Risk: thin and late markets.

### Gaps
- None of the timing recommendations were checked against the exact closing time of each Quiniela jornada; that is covered by the rules researcher.
- The cost in OddsPapi requests of probing opening times with `historical-odds` was not quantified.
