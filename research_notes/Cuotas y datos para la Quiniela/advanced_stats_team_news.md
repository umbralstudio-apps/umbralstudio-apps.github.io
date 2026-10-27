# Advanced match statistics (xG) and team-news sources for Spanish football (LaLiga EA Sports, LaLiga Hypermotion, Liga F): status at 27 Oct 2026 and evidence on predictive value

Method note: claims marked **[direct check]** come from HTTP requests I made on 2026-10-27 from a cloud datacenter IP (this research sandbox, browser User-Agent, no cookies). That IP is **not Google Colab**, but Colab also runs on datacenter IPs, so treat these results as a good proxy, not proof. Odds sources are out of scope here.

## 1. xG / advanced-stats providers: coverage by competition, data provider, access, 2026 status, history

### Takeaway
As of 27 Oct 2026 only two free sources give current, machine-readable xG for Spanish men's football. **Understat** covers Primera only, uses its own neural-net model, has every season since 2014/15, and was updated to 26 Oct 2026. **FotMob** uses Opta xG and covers LaLiga from 2019/20, LaLiga Hypermotion from 2022/23 and most Copa del Rey rounds; it has **no Liga F xG**. FBref deleted all Opta advanced data on 20 Jan 2026. Sofascore, WhoScored, FBref and FootyStats refuse datacenter requests. For Liga F, the only free xG is StatsBomb open data for one season (2023/24), which is useful for history only.

### Cited Findings
**Understat (free, own model; best long xG history for Primera)**
- Covers EPL, La Liga, Bundesliga, Serie A, Ligue 1 and RFPL. Its model: "we trained neural network prediction algorithms with the large dataset (>100,000 shots, over 10 parameters for each)" — [Understat](https://understat.com/) [direct check]
- **Still updated in 2026/27.** The LaLiga 2026 endpoint lists 380 fixtures, 99 played. The last one played was 2026-10-26, Sevilla 2–0 Osasuna (xG 0.87–0.76). The JSON comes from an AJAX endpoint that needs the header `X-Requested-With: XMLHttpRequest`, and it answered from a datacenter IP — [Understat getLeagueData/La_liga/2026](https://understat.com/getLeagueData/La_liga/2026) [direct check]
- **History from 2014/15.** The 2014/15 endpoint returns 380 played matches — [Understat getLeagueData/La_liga/2014](https://understat.com/getLeagueData/La_liga/2014) [direct check]. A comparison updated on 20 Oct 2026 also says seasons go back to 2014/15 and that there is no Segunda or Liga F — [StatPair, Best xG websites 2026](https://statpair.com/blog/best-xg-websites-2026-comparison)
- No xG for any women's competition — [The IX Sports, 4 Feb 2026](https://www.theixsports.com/the-ix-soccer/fbrefs-loss-advanced-stats-womens-soccer-data-accessibility/)
- **The site's delivery method changed around Jan 2026.** The R package ggfootball 0.3.0 says it "Migrated Understat scraper from HTML parsing to AJAX API calls" — [ggfootball NEWS (CRAN mirror)](https://ftp.fau.de/cran/web/packages/ggfootball/news/news.html)
- Described in June 2026 as one of the last free, high-quality xG sources, accessed by scraping — [Liam Henshaw, 15 Jun 2026](https://www.liamhenshaw.com/writing/where-to-find-football-data)

**FBref / Stathead (lost advanced data in Jan 2026)**
- On 20 Jan 2026 the provider sent a letter "terminating our access to their data feeds and requiring the deletion of their data". Sports Reference says "we have removed the provider's data from FBref and Stathead". It also says "FBref will continue to present the deep historic basic data we have for over one hundred competitions", and that any future advanced data "will certainly have a dramatically smaller scale" — [Sports Reference blog](https://www.sports-reference.com/blog/2026/01/fbref-stathead-data-update/)
- The removed data was xG, xA, PSxG and the other advanced metrics, after Stats Perform ended the agreement — [StatPair](https://statpair.com/blog/best-xg-websites-2026-comparison). The provider alleged a breach of the agreement, which Sports Reference disputes — [Awful Announcing](https://awfulannouncing.com/soccer/sports-reference-pulls-advanced-data-agreement-violation-dispute.html). The removal also covered women's data: Sports Reference is "especially upset by the massive step back this creates in access for women's advanced soccer data" — [Sports Reference blog](https://www.sports-reference.com/blog/2026/01/fbref-stathead-data-update/)
- From a datacenter IP FBref returns HTTP 403 with `cf-mitigated: challenge` (a Cloudflare bot challenge) — [FBref Segunda page](https://fbref.com/en/comps/17/Segunda-Division-Stats) [direct check]

**FotMob (free, Opta xG; the only free Segunda xG found)**
- FotMob names Opta as its source, and Sofascore and FotMob show the same xG — [with-bet Sofascore review, 23 Sep 2026](https://with-bet.com/tools/stats/sofascore)
- **LaLiga (league id 87), 2026/27:** team stats include "Expected goals", "xG difference" and "xG conceded". Player stats include xG, xG per 90, "Expected goals on target (xGOT)" and xA. The season list runs back to 2010/11 — [FotMob API leagues?id=87](https://www.fotmob.com/api/data/leagues?id=87) [direct check]
- **LaLiga Hypermotion (league id 140), 2026/27:** same xG categories, 462 fixtures, 121 finished. Match-level xG is present, e.g. FC Andorra–Burgos (26 Oct 2026) shows "Expected goals (xG)" 1.75–1.54 — [FotMob leagues?id=140](https://www.fotmob.com/api/data/leagues?id=140), [FotMob matchDetails 5868505](https://www.fotmob.com/api/data/matchDetails?matchId=5868505) [direct check]
- **xG history depth (checked season by season with `&season=`):** LaLiga season xG first appears in 2019/20 (none in 2016/17–2018/19). LaLiga2 xG first appears in 2022/23 (none in 2018/19–2021/22) — [FotMob leagues?id=140&season=2022/2023](https://www.fotmob.com/api/data/leagues?id=140&season=2022%2F2023) [direct check]
- **Liga F (league id 9907):** no xG in season stats for 2022/23–2026/27. The one match checked (Eibar–Madrid CFF, 25 Oct 2026) had no xG in its match details. FotMob does carry Opta-style volume stats for Liga F: "Shots on target per match", "Big chances", "Corners", "Touches in opposition box" — [FotMob leagues?id=9907](https://www.fotmob.com/api/data/leagues?id=9907) [direct check]
- **Copa del Rey (league id 138), 2025/26:** xG appears from round 1 through the final, e.g. Constancia–Girona (R1), Cultural Leonesa–Athletic (R16) and Atlético–Real Sociedad (final). Not every tie has it: Atlético Tordesillas–Burgos (R1) had none — [FotMob leagues?id=138](https://www.fotmob.com/api/data/leagues?id=138&season=2025%2F2026) [direct check]
- **The undocumented API has already moved.** `/api/leagues?id=140` returned 404, while `/api/data/leagues?id=…` works — [FotMob old path](https://www.fotmob.com/api/leagues?id=140) [direct check]
- **Terms of use:** "The use of automatic services (robots, crawler, indexing etc.) as well as other methods for systematic or regular use is not permitted." — [FotMob terms](https://www.fotmob.com/terms)
- Background (old): FotMob's live-xG launch announcement cited 23 competitions — [FotMob news](https://www.fotmob.com/topnews/3627-Live-xG-data-is-now-in-FotMob). In Feb 2026 FotMob was "the only app to display xG data for more than one" of the top five women's leagues (French D1, NWSL); Liga F is not named — [The IX Sports](https://www.theixsports.com/the-ix-soccer/fbrefs-loss-advanced-stats-womens-soccer-data-accessibility/)

**Sofascore (free app, Opta-like xG on top leagues, closed to scripts)**
- xG and xGOT appear on "top leagues". "There is no download button, no CSV and no Sofascore API for the public." The Pro tier sells AI insights with "data-driven result probabilities", and the reviewer found no published accuracy record for them — [with-bet review, 23 Sep 2026](https://with-bet.com/tools/stats/sofascore)
- For women's football it has xG for seven competitions (FBref had nine), and the WSL is the only top-five women's league among them — [The IX Sports](https://www.theixsports.com/the-ix-soccer/fbrefs-loss-advanced-stats-womens-soccer-data-accessibility/)
- Its API and homepage return HTTP 403 `{"error": {"code": 403, "reason": "Forbidden"}}` (server: Varnish) to datacenter requests — [Sofascore API](https://api.sofascore.com/api/v1/unique-tournament/54/seasons), [sofascore.com](https://www.sofascore.com/) [direct check]

**WhoScored:** covers only one women's league (WSL) — [The IX Sports](https://www.theixsports.com/the-ix-soccer/fbrefs-loss-advanced-stats-womens-soccer-data-accessibility/). Its homepage returns HTTP 403 to datacenter requests — [WhoScored](https://www.whoscored.com/) [direct check]

**Opta Analyst (theanalyst.com):** the site was reachable [direct check]. Its 2026-27 LaLiga supercomputer gives Barcelona 45.6%, Real Madrid 31% and Atlético 8.6% to win the title. The model estimates match probabilities "using betting market odds and Opta Power Rankings", so it is **not independent of the market** — [Opta Analyst, LaLiga 2026-27 projections](https://theanalyst.com/articles/la-liga-predictions-2026-27-opta-supercomputer-projections)

**StatsBomb / Hudl open data (free GitHub JSON, research only)**
- Spain coverage: **La Liga 2015/16 full season (380 matches)**; Barcelona/Messi-era seasons 2004/05–2020/21 (e.g. 2020/21 has only 35 matches); a few Copa del Rey matches; **Liga F 2023/24 full season (240 matches)**. The repo's latest `match_updated` is 2026-05-26 — [StatsBomb competitions.json](https://raw.githubusercontent.com/statsbomb/open-data/master/data/competitions.json), [Liga F 2023/24 matches](https://raw.githubusercontent.com/statsbomb/open-data/master/data/matches/182/281.json) [direct check]
- Not full current seasons — [StatPair](https://statpair.com/blog/best-xg-websites-2026-comparison); [Henshaw](https://www.liamhenshaw.com/writing/where-to-find-football-data)

**LaLiga official / data provenance**
- Stats Perform (Opta) "exclusively collects and manages live official data and player statistics from over 800 matches per season" under a deal to 2028 — [SVG Europe](https://www.svgeurope.org/blog/headlines/laliga-extends-data-and-streaming-deal-with-stats-perform-until-2028/). It also holds the exclusive international betting data and streaming rights for 2023-24 to 2027-28: 848 matches per season across the top two tiers — [SportBusiness](https://tech.sportbusiness.com/news/exclusive-stats-perform-retains-laliga-betting-rights-in-long-term-deal/)
- laliga.com has an "Avanzadas | LALIGA" page that references `opta_id` and "Beyond Stats", is served through `apim.laliga.com/public-service`, and mentions "HYPERMOTION, y Liga F Moeve". I did not see xG fields in the static HTML — [laliga.com/estadisticas-avanzadas](https://www.laliga.com/estadisticas-avanzadas) [direct check]
- laliga.com hosts 2026-27 Liga F match pages with "Previa" and "Alineaciones" tabs — [laliga.com Liga F match](https://www.laliga.com/partido/temporada-2026-2027-liga-femenina-madrid-cff-deportivo-alaves-5)

**FootyStats:** the Spain Segunda "Datasets & Excel Downloads" page exists, offering League, Matches, Teams and Players CSVs ("Registration not required" per a search snippet) — [FootyStats Segunda datasets](https://footystats.org/spain/segunda-division/datasets). It returned HTTP 403 to both WebFetch and curl from the datacenter [direct check]. I could not verify whether it has xG columns or what it costs.

**Paid platforms:** Hudl Wyscout, StatsBomb IQ and Opta/Stats Perform cost "thousands of pounds a year" — [Henshaw](https://www.liamhenshaw.com/writing/where-to-find-football-data). The Sportmonks xG add-on is covered in section 4. Advice not to mix providers' xG within one model — [StatPair](https://statpair.com/blog/best-xg-websites-2026-comparison)

### Inferences
- **Sample sizes (my arithmetic from the checks above):**
  - Understat Primera: 12 complete seasons (2014/15–2025/26), about 4,560 matches, plus 99 in 2026/27. Walk-forward backtests can start around 2015/16, so the 2009/10–2013/14 part of the user's validation window would have no xG.
  - FotMob/Opta Primera: about 2,660 matches (2019/20–2025/26).
  - FotMob/Opta Segunda: about 1,850 matches (2022/23–2025/26 at 462 per season), plus 121 this season. That is enough for current ratings but thin for fitting a separate residual model.
- **Provider consistency:** Opta is LaLiga's official collector for both tiers, so FotMob xG is the only *consistent* xG across Primera, Segunda and Copa. Combining Understat for Primera with FotMob for Segunda in one rating would mix two different xG models. The options are separate ratings per provider, or FotMob throughout at the cost of a shorter Primera history.
- **Liga F:** no current free xG exists. The practical upgrade is shot-volume, big-chance and corner ratings from FotMob (football-data.co.uk has no Liga F stats as far as I know; not verified here). StatsBomb's 2023/24 season is only useful to test offline whether shot-quality information helps Liga F.
- For a Colab pipeline, the reachable sources are Understat (AJAX JSON) and FotMob (JSON API). Scraping FBref, Sofascore, WhoScored and FootyStats should be expected to fail from datacenter IPs.

### Gaps
- Sofascore xG coverage of LaLiga Hypermotion and Liga F could not be checked (blocked). The IX's statement that the WSL is its only top-five women's league suggests Liga F has no Sofascore xG, but that is unconfirmed.
- Not verified:
  - WhoScored's current xG display.
  - Whether laliga.com's advanced stats include xG.
  - FootyStats xG columns and price.
  - The status of xGscore and Infogol in 2026 (the only Infogol results were 2021–23 Sporting Life articles).
- No terms of use found for Understat.
- FBref's remaining basic coverage of Segunda and Liga F after Jan 2026 could not be checked (Cloudflare).
- Background I did not re-check: FBref's earlier switch from StatsBomb to Opta data (around 2022).

## 2. Evidence: do xG ratings improve outcome forecasts over goals/shots ratings, and over market odds? Is xG priced in?

### Takeaway
Shot-quality and shot-volume information predicts future goals and results better than goals alone. Evidence that xG beats **de-vigged sharp 1X2 odds** is weak:
- An xG-only Bundesliga model did not beat bookmaker RPS.
- An in-play EPL study found PSxG adds very little and the exchange already "incorporates information beyond goals and shots".
- The reported betting profits are segment-specific (home wins, O/U) and vary by season.

For a system already anchored to Pinnacle with a 0.0001 RPS edge, expect any xG gain to be incremental and small.

### Cited Findings
- **Mead, O'Hare & McMenemy (2023, PLOS ONE):**
  - Setup: 2017-18 season, top five leagues, team totals over the previous six matches.
  - Next-match accuracy (EPL): shots 0.4635, goals 0.4948, the authors' xG 0.5208, StatsBomb xG 0.5365.
  - Pearson r with future average goals (all leagues): shots 0.456, goals 0.47, own xG 0.574, StatsBomb 0.502.
  - Conclusion: "the expected goals statistic is the superior indicator of a team performance".
  - Caveat: some table rows look duplicated (La Liga rows equal EPL rows) — [PMC10075453](https://pmc.ncbi.nlm.nih.gov/articles/PMC10075453/)
- **Brechot & Flepp (working paper):** xG "based on quantified scoring chances predicts future performance more accurately than recent match results" — [RePEc zrh:wpaper:374](https://econpapers.repec.org/RePEc:zrh:wpaper:374)
- **Wheatcroft (2021, Journal of Sports Analytics):** ratings that predict match statistics (GAP and Bivariate Attacking ratings, built on shots and corners) are "informative enough to provide information beyond that reflected in the odds", with a "long term and robust gambling profit" — [LSE Research Online](https://researchonline.lse.ac.uk/id/eprint/111495), [arXiv 2001.09097](https://arxiv.org/abs/2001.09097)
- **Wheatcroft (2020, International Journal of Forecasting):** in the O/U 2.5 market, GAP ratings built only on shots and corners (no goals) gave about 0.8% average profit per bet over twelve years — [LSE Research Online](https://researchonline.lse.ac.uk/id/eprint/103712), [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0169207019302559)
- **Wheatcroft & Sienkiewicz (2021):** a shot-success model combined with predicted shot counts "can increase the skill of forecasts of both the match outcome and of whether the total number of goals in a match will exceed 2.5", with "mixed evidence" against betting strategies — [arXiv 2101.02104](https://arxiv.org/abs/2101.02104)
- **Wilkens (2026, Journal of Sports Analytics; SSRN 2025):**
  - Setup: recent xG fed into a Skellam distribution with isotonic calibration, Bundesliga 2014/15–2024/25.
  - Accuracy: "the model was not able to outperform the bookmaker's predictions" on RPS, and bookmaker odds "exhibit superior statistical calibration".
  - Betting: simulated ROI about 10% at average odds and nearly 15% at best prices. Profits came mostly from home-win bets, away-win bets lost consistently, and results varied considerably by season — [SAGE](https://journals.sagepub.com/doi/10.1177/22150218261416681), [SSRN 5381388](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5381388)
- **Forcher, Forcher, Woll & Altmann (2025, Frontiers in Sports and Active Living):**
  - Setup: Bundesliga 2022/23–2024/25, 756 matches analysed, 80/20 split.
  - Pre-match RPS: EPV 0.194, xG 0.199, Elo baseline 0.202.
  - Betting odds 0.206 is quoted from a *different* study (Berrar et al. 2024), so it is **not a like-for-like comparison**.
  - Conclusion: "xG provides limited value in predicting the number of goals or match outcomes in the future compared to EPV" — [PMC12640942](https://pmc.ncbi.nlm.nih.gov/articles/PMC12640942/)
- **arXiv 2605.16066 (May 2026, in-play EPL, Betfair prices, PSxG from FBref):**
  - Betfair RPS 0.1254 versus 0.1294 for the best model.
  - PSxG moved an uncalibrated model's RPS only from 0.1353 to 0.1347. The authors call its out-of-sample impact "small", say "the market incorporates information beyond goals and shots that our covariates do not capture", and conclude "pre-match information dominates the accuracy gap".
  - The Kelly-staked ROI of 4.5% is preliminary (140 matches) — [arXiv 2605.16066](https://arxiv.org/html/2605.16066v1)
- **Goto, Takeishi & Yairi (Apr 2026):** on 90,014 matches, they argue standard GLMs "attempt to capture relationships that the Efficient Market Hypothesis already captures" — [arXiv 2604.17194](https://arxiv.org/abs/2604.17194)
- **Counter-view (opinion, Dec 2022):** "no xG model has been shown to be superior to Dixon-Coles in predicting the future" — [Laurence Shaw, The Conversation](https://theconversation.com/a-brief-history-of-statistics-in-football-why-actual-goals-remain-king-in-predicting-who-will-win-194314)
- **Stats & Snake Oil (2019):** an xG-fed Dixon-Coles model on EPL 2018/19 (Understat data) gave materially different probabilities from a goals-based one (Liverpool title 0.65 versus 0.829), but reported **no** scoring rule — [Stats and Snake Oil](https://www.statsandsnakeoil.com/2019/01/06/predicting-the-premier-league-with-dixon-coles-and-xg/). Method for feeding xG into Dixon-Coles via simulated scorelines — [Stats and Snake Oil 2018](https://www.statsandsnakeoil.com/2018/06/22/dixon-coles-and-xg-together-at-last/)
- **Market structure:** EPL bookmaker odds show favourite-longshot bias for exact scorelines, "which is not generally present for match results" — [Reading EMDP 2020-03](https://www.reading.ac.uk/web/files/economics/emdp202003.pdf)

### Inferences
- The only like-for-like pre-match magnitude I found is xG versus Elo: about 0.003 RPS (Forcher et al.). The user's model already includes shots, shots on target and corners ratings, which carry much of xG's information (Mead: shots r=0.456, xG r=0.57; Wheatcroft: shot and corner ratings beat odds in some markets). Adding xG to the ensemble will therefore probably improve the *model* component by well under 0.003 RPS. After the 50% shrink toward the market, the net change against the market should be of order 10⁻⁴–10⁻³ RPS, and could be zero. For 14 signs per jornada that is a small fraction of one extra correct sign per jornada.
- xG matters most where the market is weakest: early season, after promotions or relegations, and in Segunda, Copa and Liga F where liquidity is thinner. But xG coverage is thinnest in exactly those places (Segunda xG from 2022/23 only; no Liga F xG).
- The safest use of xG is as **one more rating input inside the existing walk-forward ensemble**, judged on out-of-sample RPS. It should not replace the shots ratings or override the market anchor.

### Gaps
- I found no study measuring the incremental value of xG ratings over **de-vigged Pinnacle closing 1X2 odds** in Spanish leagues, or for Segunda or Liga F at all.
- A claim that "Wunderlich (2025)" showed bookmaker odds beat points, goals and Elo across about 100,000 matches appeared only in a search snippet, and I could not trace a verifiable source.
- The Hubáček et al. experimental review of score-based models was not found.

## 3. Team news for Spanish football (injuries, suspensions, probable lineups): best sources, accuracy, coverage, timing versus the Quiniela close

### Takeaway
For Primera and Segunda, the most useful **pre-close** sources are:
- **RFEF Comité de Disciplina PDFs:** official suspensions, adopted on Wednesdays.
- **FotMob per-match "unavailable" lists:** injury or suspension, plus expected return, machine-readable days ahead.
- **Futbolfantasy:** probable XIs for LaLiga and LaLiga2, plus LaLiga injury and suspension lists updated daily with each player's percentage chance of starting.
- **Comuniate and Jornada Perfecta:** cross-checks; Jornada Perfecta also covers Segunda.

Self-reported probable-XI accuracy is about 82–86% of starting slots. Liga F has almost no structured team news.

### Cited Findings
- **RFEF (official suspensions)**
  - PDF header: "COMUNICACION PUBLICA DE LOS ACUERDOS DEL COMITÉ DE DISCIPLINA ADOPTADOS EL 14-10-2026 … Primera División … Temporada: 2026-2027 JORNADA:8 (11-10-2026)". It lists each player's amonestaciones by type. The body is now called **Comité de Disciplina**. 14 Oct 2026 was a Wednesday — [RFEF PDF J8](https://rfef.es/sites/default/files/sanciones/20261014_Primera_Division_J8.pdf) [direct check: the PDF downloads from a datacenter IP, but `rfef.es/es/noticias` returns a Cloudflare challenge 403]
  - The Comité de Disciplina "cerró el 21 de octubre [Wednesday] los acuerdos de la jornada 9": Bernal 4 matches, Djené 1 match, Vinícius already serving 4 matches from 14 Oct, Laporte pending the next meeting — [El Gol Digital, 23 Oct 2026](https://www.elgoldigital.com/futbol/sancionados-jornada-10-laliga-bernal-vinicius-clasico/)
  - A Segunda PDF series exists under the same path — [RFEF Segunda J15 PDF](https://rfef.es/sites/default/files/sanciones/Segunda_Division_J_15.pdf) (season not checked). The RFEF also has an archive of sanction notices — [RFEF sanciones](https://rfef.es/es/federacion/normativas-y-circulares/sanciones?page=794)
- **FotMob absences (checked 3 days before the match)**
  - Villarreal–Espanyol (30 Oct 2026) "unavailable" list: Pape Gueye (suspension, "Late October 2026"), Nathan Saliba (injury, "Early November 2026"), Carlos Romero (injury, "About 1-2 weeks"), Nicolas Pépé (injury, "Unknown"), Jofre Carreras (injury, "Doubtful"), Kike García (injury) — [FotMob matchDetails 5868120](https://www.fotmob.com/api/data/matchDetails?matchId=5868120) [direct check]
  - LaLiga2 Real Sociedad B–Girona listed two Girona players as doubtful — [FotMob matchDetails 5868522](https://www.fotmob.com/api/data/matchDetails?matchId=5868522) [direct check]
  - Liga F Granada–Atlético had empty lists — [FotMob matchDetails 5882331](https://www.fotmob.com/api/data/matchDetails?matchId=5882331) [direct check]
  - The pre-match lineup field is `lineupType: lastStarting11`, i.e. the last XI used, **not** a prediction [same checks]
- **Futbolfantasy**
  - Pages exist for LaLiga probable XIs, LaLiga2 probable XIs, LaLiga injuries and LaLiga suspensions. No Liga F or `/segunda/` page was found (404) — [Futbolfantasy LaLiga](https://www.futbolfantasy.com/laliga/posibles-alineaciones), [LaLiga2](https://www.futbolfantasy.com/laliga2/posibles-alineaciones), [lesionados](https://www.futbolfantasy.com/laliga/lesionados), [sancionados](https://www.futbolfantasy.com/laliga/sancionados) [direct check; reachable from a datacenter IP]
  - The injuries page shows "Actualizado el 27/10/2026" and says lists are "actualizados a diario. Se mostrará adjunto el porcentaje de titularidad de cada jugador" — [Futbolfantasy lesionados](https://www.futbolfantasy.com/laliga/lesionados) [direct check]
  - Example of late news: "Courtois se pierde el Clásico por gripe" (27 Oct 2026) — [Futbolfantasy](https://www.futbolfantasy.com/laliga/noticias/153491-courtois-se-pierde-el-clasico-por-gripe)
- **Probable-XI accuracy (all self-reported)**
  - Futbolfantasy claims "nuestro porcentaje de aciertos supera el 86%" — [Futbolfantasy Premier League page](https://www.futbolfantasy.com/premier-league/posibles-alineaciones)
  - Futbolfantasy's audit method: the reference XI is taken "justo antes de que se haga oficial la primera alineación", and a position with two options scores 0.70 or 0.30. For LaLiga J30 2020-21: "Aciertos totales … 163.18/198", "Previsibilidad total … 82%" (about 9.1 of 11 per team) — [Futbolfantasy J30 2020-21](https://www.futbolfantasy.com/laliga/noticias/82764-aciertos-y-previsibilidad-de-los-posibles-onces-de-la-jornada-30)
  - Comuniate, LaLiga J26 2025/26 (28 Feb 2026): average 86.36%, range 72.73–100% across the 8 teams listed. Its lineups are saved "70 minutos antes del primer partido de la jornada" — [Comuniate](https://www.comuniate.com/noticias/14020/porcentajes-de-aciertos-en-los-onces-posibles-de-la-jornada-32)
  - Sportmonks' model-based expected lineups claim La Liga 75%, against EPL 84%, Bundesliga and Serie A 87%, Eredivisie 88% — [Sportmonks, Jul/Aug 2025](https://www.sportmonks.com/blogs/premium-expected-lineups/)
- **Other sites**
  - Jornada Perfecta has a Segunda section — [Jornada Perfecta Segunda](https://www.jornadaperfecta.com/segunda/) [direct check]
  - Analítica Fantasy's probable-lineups page returned 403 to the datacenter request — [Analítica Fantasy](https://www.analiticafantasy.com/fantasy-la-liga/alineaciones-probables) [direct check]
  - Transfermarkt's LaLiga injury list was reachable (200), but the LaLiga2 list returned 405 — [Transfermarkt ES1](https://www.transfermarkt.es/laliga/verletztespieler/wettbewerb/ES1), [Transfermarkt ES2](https://www.transfermarkt.es/laliga2/verletztespieler/wettbewerb/ES2) [direct check]. Transfermarkt is a source of injury records, not performance data — [Henshaw](https://www.liamhenshaw.com/writing/where-to-find-football-data)
  - Liga F: laliga.com's 2026-27 Liga F match pages have "Previa" and "Alineaciones" tabs but no injury content was seen — [laliga.com Liga F](https://www.laliga.com/partido/temporada-2026-2027-liga-femenina-madrid-cff-deportivo-alaves-5)

### Inferences
- **What is known by a Saturday Quiniela close:**
  - Suspensions: Wednesday RFEF PDFs.
  - Medium and long-term injuries: FotMob, Futbolfantasy and Transfermarkt.
  - Probable XIs at about 82–86% slot accuracy.
  - Late doubts such as illness or rotation are only partly known.
  - Confirmed XIs exist only for matches that kick off before the close.
- Sharp odds by Friday or Saturday already reflect almost all of this public news. The analyst module's ±5-point cap and shadow mode are consistent with the evidence. The most defensible use is **error-catching**: detecting a market price taken before a big absence was announced, or a key player suspended in Copa or midweek. Systematic tilting is less defensible.
- FotMob's structured `unavailable` list (type plus expected return) is the cheapest machine-readable absence feature for Primera and Segunda. It can feed the analyst module or a logged absence-count feature for future backtesting, since FotMob does not appear to keep history of these lists.

### Gaps
- No independent, multi-season audit of probable-XI accuracy was found for Futbolfantasy, Comuniate, Jornada Perfecta or Analítica Fantasy. Accuracy for Segunda is unknown.
- No structured injury or suspension source was found for **Liga F**, and I did not verify which body publishes Liga F sanctions or when.
- Not verified: the terms of use of Futbolfantasy, Comuniate, Jornada Perfecta and Transfermarkt, and the official LaLiga Fantasy app's player-status data.

## 4. APIs for injuries, lineups and predictions; unofficial endpoints (stability, terms, datacenter blocking)

### Takeaway
- **Licensed, low cost:** API-Football (free 100 requests/day; $19–39/month) has injuries, lineups and predictions endpoints, but I could not verify its Spanish-league injury coverage. Sportmonks costs €29–249/month, plus a €24/month xG add-on, and sells expected lineups claiming only 75% accuracy for La Liga.
- **Unofficial, as of today:** FotMob JSON and Understat AJAX are reachable from a datacenter IP. Sofascore, WhoScored, FBref, FootyStats and api-football.com's own website block such requests.

### Cited Findings
- **API-Football**
  - Pricing per third parties: Free $0 (100 requests/day), Pro $19/month (7,500/day), Ultra $29/month (75,000/day), Mega $39/month (150,000/day). The free plan is limited in available seasons — [Bruin docs](https://getbruin.com/docs/ingestr/soccer-sources/api-football.html), [TheStatsAPI](https://thestatsapi.com/blog/best-football-api) (third-party; verify officially)
  - API-Football says all plans include all endpoints — [API-Football beginner's guide](https://www.api-football.com/news/post/how-to-get-started-with-api-football-the-complete-beginners-guide)
  - The Injuries endpoint returns "the list of players who potentially will not participate in a match". The predictions endpoint uses "6 different algorithms" — [API-Football endpoint news](https://www.api-football.com/news/category/endpoints)
  - api-football.com's coverage and documentation pages return a Cloudflare 403 to datacenter requests. The API host `v3.football.api-sports.io` returned 403 without a key, which is expected — [api-football.com/coverage](https://www.api-football.com/coverage) [direct check]
- **Sportmonks**
  - Plans: Starter €29/month (5 leagues), Growth €99 (30), Pro €249 (120), Enterprise custom (2,300+ leagues).
  - Add-ons: "xG & Pressure Index" €24/month; "Odds & Predictions" €15/month; Expected Lineups (no price shown). "Injuries & suspensions" is listed as a data feature — [Sportmonks pricing](https://www.sportmonks.com/football-api/plans-pricing/)
  - Expected-lineup endpoints: `/v3/football/expected-lineups/teams/{team_id}` and `/v3/football/expected-lineups/players/{player_id}`. Lower tiers get them "hours before kickoff" — [Sportmonks blog](https://www.sportmonks.com/blogs/premium-expected-lineups/)
- **Other B2B feeds:** Goalserve has predicted lineups "for selected leagues"; Enetpulse sells an injury and suspension service — [Goalserve](https://www.goalserve.com/en/sport-data-feeds/football-api/description/5), [Enetpulse](https://enetpulse.com/?p=9278)
- **Unofficial endpoints**
  - Sofascore: 403 (Varnish) and no public API — [Sofascore API](https://api.sofascore.com/api/v1/unique-tournament/54/seasons) [direct check], [with-bet](https://with-bet.com/tools/stats/sofascore)
  - FotMob: `/api/data/leagues` and `/api/data/matchDetails` return 200 with no key, while the old `/api/leagues` path is 404. Its terms forbid "systematic or regular use" — [FotMob terms](https://www.fotmob.com/terms) [direct check]
  - Understat: `getLeagueData` returns gzip JSON when called with the XMLHttpRequest header [direct check]. The soccerdata README warns that changes to scraped sites will break the package — [soccerdata fork](https://github.com/Kalaweksh/soccerdata)

### Inferences
- **For a Colab notebook:**
  - Licensed APIs (API-Football, Sportmonks) are the only options with stable contracts and terms.
  - FotMob and Understat work today but can break or be blocked without notice. FotMob's terms explicitly prohibit automated systematic use.
  - Sofascore and WhoScored should be assumed unusable from Colab.
- I found no published validation of the API-Football or Sportmonks "predictions" endpoints, so they should not be treated as independent signals against the market.

### Gaps
- Not verified (site blocked): API-Football coverage flags for injuries, lineups and statistics in La Liga, Segunda and Liga F, and current official prices.
- Sportmonks: whether La Liga 2 and Liga F are available in a plan, and whether its xG is its own model or Opta-derived.
- Whether FotMob or Understat behave differently from Colab IPs or under repeated polling.

## 5. Other signals: referee appointments, fixture congestion, travel, weather

### Takeaway
Since 2025/26, LaLiga referee designations are published only about 24 hours (one day) before each match, so they are **mostly unavailable at the Quiniela close**. I found no rigorous evidence that referees, travel, weather or congestion add predictive value beyond sharp odds. The only market-efficiency evidence on rest effects is older and English.

### Cited Findings
- **Referees:**
  - In Aug 2025 the CTA said it would announce "24 horas antes de cada partido los árbitros designados para dirigirlo" — [ESdiario, 15 Aug 2025](https://www.esdiario.com/deportes/250815/165044/fin-norma-impuesta-franco-arbitros-laliga-recuperan-nombre.html)
  - "La Liga anunció que las designaciones arbitrales se publicarán un día antes de la celebración del partido" — [Ara, 13 Aug 2025](https://es.ara.cat/deportes/futbol/protegeran-arbitros-liga-azote-semanal-florentino_1_5470097.html)
  - The list of six referee-related changes for 2026-27 (10-second substitutions, 5-second restart countdown and others) does not mention designation timing — [El Debate, 4 Aug 2026](https://www.eldebate.com/deportes/futbol/la-liga/20260804/seis-cambios-implementados-arbitros-cara-temporada-2627-liga_446690.html)
- **Congestion and timing:** in older English data, fixed-odds prices were compiled at least five days before kickoff, which left an edge from recent results that "seems to have narrowed (or disappeared altogether) over time" — [Goddard, Modelling football match results and the efficiency of fixed-odds betting](https://www.stat.berkeley.edu/~aldous/157/Papers/goddard.pdf)

### Inferences
- Referee data could only matter for Friday or early-Saturday matches and for card or penalty markets. For 1X2 signs its value is negligible.
- The user already models rest and fixture load, and Pinnacle prices move continuously, so Goddard's stale-price mechanism mostly does not apply today.

### Gaps
- I found no peer-reviewed test of whether 1X2 odds fully price referee assignment, fixture congestion after European games, travel or weather in Spanish football.
- Betting-blog claims on these topics were unsourced and are excluded.

## 6. Ranked shortlist for ORÁCULO 1X2 v3.2 (benefit / risk)

### Takeaway
The best ratio of value to effort is: (1) Understat xG ratings for Primera, (2) FotMob Opta xG for Segunda and Copa plus its structured absence lists, (3) RFEF Wednesday suspension PDFs, (4) Futbolfantasy (and Comuniate/Jornada Perfecta) for the analyst module. Every addition should be judged by walk-forward RPS against the market anchor, because the evidence suggests the market already prices most of this.

### Cited Findings
1. **Understat (Primera xG)**
   - Benefit: free, 2014/15 to now, own neural-net xG, current to 26 Oct 2026, reachable from a datacenter IP. It allows about 4,500+ backtestable Primera matches — [Understat](https://understat.com/), [getLeagueData](https://understat.com/getLeagueData/La_liga/2026) [direct check]
   - Risk: unofficial endpoint that already changed around Jan 2026 ([ggfootball NEWS](https://ftp.fau.de/cran/web/packages/ggfootball/news/news.html)); Primera only; xG largely priced in ([Wilkens 2026](https://journals.sagepub.com/doi/10.1177/22150218261416681); [arXiv 2605.16066](https://arxiv.org/html/2605.16066v1)).
2. **FotMob (Opta xG and absences)**
   - Benefit: the only free Segunda xG (2022/23 onward); Primera xG from 2019/20; Copa del Rey xG; Liga F shot and big-chance stats; per-match injury and suspension lists with expected return — [FotMob API](https://www.fotmob.com/api/data/leagues?id=140) [direct check]. Opta is LaLiga's official collector for both tiers — [SportBusiness](https://tech.sportbusiness.com/news/exclusive-stats-perform-retains-laliga-betting-rights-in-long-term-deal/)
   - Risk: the terms forbid automated "systematic or regular use" ([FotMob terms](https://www.fotmob.com/terms)); undocumented paths already changed (404 on the old path); short history; no Liga F xG; mixing it with Understat xG is inconsistent ([StatPair](https://statpair.com/blog/best-xg-websites-2026-comparison)).
3. **RFEF Comité de Disciplina PDFs (official suspensions)**
   - Benefit: authoritative and published on Wednesdays (14 and 21 Oct 2026), well before the close — [RFEF PDF](https://rfef.es/sites/default/files/sanciones/20261014_Primera_Division_J8.pdf), [El Gol Digital](https://www.elgoldigital.com/futbol/sancionados-jornada-10-laliga-bernal-vinicius-clasico/)
   - Risk: index pages sit behind Cloudflare [direct check]; file names are irregular (e.g. `Segunda_Division_J_15.pdf`); the PDFs need parsing; the information is already public and priced.
4. **Futbolfantasy (LaLiga and LaLiga2 XIs; LaLiga injuries and suspensions, daily, with chance of starting)**
   - Benefit: the richest Spanish team-news source for the Claude analyst; about 82–86% XI accuracy (self-reported) — [Futbolfantasy](https://www.futbolfantasy.com/laliga/lesionados), [audit J30](https://www.futbolfantasy.com/laliga/noticias/82764-aciertos-y-previsibilidad-de-los-posibles-onces-de-la-jornada-30)
   - Risk: no independent audit, terms unknown, no Liga F.
5. **Comuniate and Jornada Perfecta (consensus cross-check; Jornada Perfecta has Segunda)**
   - Benefit: a second opinion on XIs; Comuniate's 86.36% sample was taken 70 minutes before the first match — [Comuniate](https://www.comuniate.com/noticias/14020/porcentajes-de-aciertos-en-los-onces-posibles-de-la-jornada-32), [Jornada Perfecta Segunda](https://www.jornadaperfecta.com/segunda/)
   - Risk: LaLiga-centric, self-reported. Analítica Fantasy is blocked from datacenter IPs [direct check].
6. **Sportmonks (paid, licensed)**
   - Benefit: a documented and stable API with injuries, suspensions, expected lineups and an xG add-on (€29 + €24 per month) — [Sportmonks pricing](https://www.sportmonks.com/football-api/plans-pricing/)
   - Risk: cost; La Liga expected-lineup accuracy only 75% ([Sportmonks blog](https://www.sportmonks.com/blogs/premium-expected-lineups/)); Segunda and Liga F coverage unverified.
7. **API-Football (cheap, licensed)**
   - Benefit: injuries, lineups and predictions endpoints from $0–19/month — [API-Football news](https://www.api-football.com/news/category/endpoints), [Bruin](https://getbruin.com/docs/ingestr/soccer-sources/api-football.html)
   - Risk: Spanish injury coverage unverified; the predictions endpoint has no published validation.
8. **StatsBomb open data**
   - Benefit: free, full LaLiga 2015/16 and **Liga F 2023/24** event data to test offline whether shot-quality ratings help Liga F, or to calibrate a home-made xG — [StatsBomb open data](https://raw.githubusercontent.com/statsbomb/open-data/master/data/competitions.json)
   - Risk: no current seasons, so no live use.
9. **Transfermarkt injury lists**
   - Benefit: long injury histories that could be used to backtest absence features — [Transfermarkt ES1](https://www.transfermarkt.es/laliga/verletztespieler/wettbewerb/ES1)
   - Risk: the LaLiga2 page was blocked (405) [direct check]; scraping terms not verified.
10. **Avoid or deprioritise**
    - FBref for xG: deleted on 20 Jan 2026 and Cloudflare-blocked — [Sports Reference](https://www.sports-reference.com/blog/2026/01/fbref-stathead-data-update/)
    - Sofascore and WhoScored: blocked, no public API — [with-bet](https://with-bet.com/tools/stats/sofascore)
    - Opta supercomputer: an input already derived from betting odds — [Opta Analyst](https://theanalyst.com/articles/la-liga-predictions-2026-27-opta-supercomputer-projections)
    - Referee designations: published about 24 hours before each match — [esdiario](https://www.esdiario.com/deportes/250815/165044/fin-norma-impuesta-franco-arbitros-laliga-recuperan-nombre.html)
    - FootyStats: unverified and blocked — [FootyStats](https://footystats.org/spain/segunda-division/datasets)

### Inferences
- **Suggested experiments (no code changes made):**
  - Add an xG-based Poisson/Elo rating per provider to the existing ensemble: Understat for Primera, FotMob for Segunda.
  - Run it through the same walk-forward RPS protocol on the seasons where xG exists, comparing model+xG, model alone and the market on identical matches.
  - Keep the 50% shrink toward the market. Expect a gain in the 10⁻⁴–10⁻³ RPS range at best.
- Log FotMob absence lists and Futbolfantasy chance-of-starting snapshots at each run. That builds the history needed to later test, out of sample, whether the analyst's ±5-point adjustments add anything beyond the closing odds.
- **Liga F:** no xG and almost no structured team news, so stay closer to the market where odds exist. Use FotMob shot volumes, not xG.

### Gaps
- None of the rankings above is validated on the user's data. The expected gains are inferences from non-Spanish studies.
- API-Football and Sportmonks coverage of Segunda and Liga F, and FotMob's tolerance of regular polling from Colab, need a live check with keys or on Colab itself.
