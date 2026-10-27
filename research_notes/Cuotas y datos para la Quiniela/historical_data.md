# Historical data layer for ORÁCULO 1X2 (Spain, Primera/Segunda): football-data.co.uk status and alternatives, as of 27 Oct 2026

Research date: 27 October 2026. I downloaded the CSVs and pages myself and parsed them only as data (nothing was executed). Wherever a figure is marked "my computation", it was computed from the cited CSV URLs. The football-data.co.uk Bluesky account quoted below is @12xpert, the profile linked from football-data's own pages ([data.php](https://www.football-data.co.uk/data.php)). Its posts are written in the first person by the site's operator.

## Q1. football-data.co.uk for SP1/SP2 2025/26 and 2026/27: columns present now, and what changed season by season

### Takeaway
SP1/SP2 2026/27 have 113 columns and no Pinnacle data at all. They now carry xG (HxG/AxG) and odds from Bet365, Betfred, BetVictor, Bwin, Paddy Power, Sky Bet, the market Max/Avg and the Betfair Exchange (BFE), each in pre-closing and closing versions. In 2025/26 the Pinnacle columns exist but are filled only up to 12 Jan 2026, and the site flags them as unreliable from 23 Jul 2025. The bookmaker set has changed every season, so code that reads these files must tolerate columns appearing and disappearing.

### Cited Findings
- **2026/27 SP1 (99 matches, 15/08/2026–26/10/2026) and SP2 (121 matches, 14/08/2026–26/10/2026): 113 columns each** (my computation; [SP1 2627](https://www.football-data.co.uk/mmz4281/2627/SP1.csv), [SP2 2627](https://www.football-data.co.uk/mmz4281/2627/SP2.csv)):
  - Results: Div, Date, Time, HomeTeam, AwayTeam, FTHG, FTAG, FTR, HTHG, HTAG, HTR.
  - **HxG, AxG (new)**, filled for 100% of rows.
  - Stats: HS, AS, HST, AST, HF, AF, HC, AC, HY, AY, HR, AR.
  - 1X2 pre-closing: B365, BFD (Betfred), BV (BetVictor), BW (Bet&Win/Bwin), PP (Paddy Power), SKB (Sky Bet), Max, Avg, BFE (Betfair Exchange).
  - O/U 2.5: B365, Max, Avg, BFE.
  - AH: AHh plus B365AH, MaxAH, AvgAH, BFEAH.
  - Closing ("C") versions of all of the above, including AvgC, BFEC, B365C>2.5, AvgC>2.5, BFEC>2.5 and AHCh.
  - **No PSH/PSD/PSA, PSCH/PSCD/PSCA, P>2.5, PC>2.5, PAHH or PCAHH columns exist.**
- 2026/27 fill rates (my computation, same files):
  - Every column is filled for SP1 except BFEAHH (98/99) and BWC (94/99).
  - SP2 has holes in BFEH (114/121), BFE>2.5 (102/121), BFEAHH (58/121) and BWCH (116/121).
  - B365, Max and Avg (pre-closing and closing) are 100% filled in both divisions.
- **2025/26 SP1/SP2: 131 columns** (my computation; [SP1 2526](https://www.football-data.co.uk/mmz4281/2526/SP1.csv), [SP2 2526](https://www.football-data.co.uk/mmz4281/2526/SP2.csv)):
  - 1X2 bookmakers: B365, BFD, BMGM (BetMGM), BV, BW, CL (Coral), LB (Ladbrokes), PS (Pinnacle), Max, Avg, BFE.
  - O/U and AH: B365, P (Pinnacle), Max, Avg, BFE.
  - Closing versions of all; no xG.
- **2024/25 SP1: 119 columns, a different bookmaker set** (my computation; [SP1 2425](https://www.football-data.co.uk/mmz4281/2425/SP1.csv)): B365, BW, BF (Betfair sportsbook), PS, WH (William Hill), 1XB (1xBet), Max, Avg, BFE.
- When each column family starts in SP1 (my computation from headers):
  - 2009/10–2011/12: Betbrain averages (BbAvH) only, no Pinnacle ([1112](https://www.football-data.co.uk/mmz4281/1112/SP1.csv)).
  - From 2012/13: PSH and PSCH ([1213](https://www.football-data.co.uk/mmz4281/1213/SP1.csv)).
  - From 2019/20: Avg/Max, AvgC and B365C replace Bb* ([1819](https://www.football-data.co.uk/mmz4281/1819/SP1.csv) vs [1920](https://www.football-data.co.uk/mmz4281/1920/SP1.csv)).
  - From 2024/25: BFE and BFEC (absent in [2324](https://www.football-data.co.uk/mmz4281/2324/SP1.csv)).
- The site's own description: "Since 2005/06 average and maximum prices ... have also been collected from Betbrain (from Oddsportal since 2019/20)". It also says: "Since 2019/20 I have collected two sets of odds. The first set is collected after market opening ... The second set are the closing odds ('C' included the data column headings). Closing home-draw-away odds are also available for Pinnacle bookmaker only back to 2012/13" — [data.php](https://www.football-data.co.uk/data.php).
- Announced bookmaker changes, from the operator's posts:
  - 2 Jun 2025: switch "to include only UK-regulated (plus Pinnacle)" bookmakers for 2025/26 — [post](https://bsky.app/profile/12xpert.bsky.social/post/3lqmjxdvv4k2g).
  - 25 Jul 2025: new 1X2 set "bet365, Betfred, BetMGM, Betvictor, Bwin, Coral, Ladbrokes, Pinnacle. Over/Under and Asian as before (bet365 and Pinnacle)" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3lusda3j7zc2r).
  - 31 Jul 2026: "Owing to unreliability of Coral and Ladbrokes odds via the oddsportal feed, I've switched them to Paddy Power (PP) and Skybet (SKB) for this season" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mrwilkcnlc2g).
  - 7 Aug 2026: "BetMGM odds will no longer be featured for this season" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3msi6ercyw222).
  - 3 Aug 2026: "the bigger divisions will now have xG included" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3ms7heyddjk2w).
  - Earlier attrition: William Hill "finally died on Oddportal" (27 Mar 2025, [post](https://bsky.app/profile/12xpert.bsky.social/post/3llew7565c22d)). 1xBet odds went missing after a toggle on OddsPortal (6 Dec 2024, [post](https://bsky.app/profile/12xpert.bsky.social/post/3lcnkmbzkuk2j)).
- The Avg/Max market columns are now an average over UK-only books. The 18 Jul 2025 post says: "now I've moved to UK only bookmakers, the average and maximum market odds for Russia are equivalent to Pinnacle's, since no UK bookmaker lists them" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3lua3r2ih2s2n).
- notes.txt has not been updated for 2026/27. It defines the BFE, BFD, BMGM, BV, CL, LB and PP codes and the "C" closing convention. It does not define HxG/AxG or the new "SKB" code (it lists only the old "SKH = Skybet"). It still describes Pinnacle (PSH, P>2.5, PAHH) — [notes.txt](https://www.football-data.co.uk/notes.txt).
- The Spain page lists, for 2026/27, "La Liga Primera Division (FT & HT results; match stats; match, total goals & AH odds)" and "La Liga Segunda Division (FT & HT results; match stats; match odds and total goals odds)" — [spainm.php](https://www.football-data.co.uk/spainm.php). The SP2 CSV nevertheless does contain AH columns ([SP2 2627](https://www.football-data.co.uk/mmz4281/2627/SP2.csv)).

### Inferences
- The notebook's Pinnacle-first market currently falls back to the consensus for every 2026/27 match, and also for 2025/26 matches after 12 Jan 2026. P>2.5 (implied goals) and PAHH have no Pinnacle equivalent. The nearest replacements in the files are AvgC>2.5/BFEC>2.5 and AvgCAHH/BFECAHH, with the AHh/AHCh line sizes.
- The "Avg" consensus is not stationary across the backtest window: Betbrain until 2018/19, OddsPortal mixed books 2019/20–2024/25, UK-only books without Pinnacle from 2025/26. A model trained on the gap between itself and "market" may see a regime shift in 2025/26 (see the margin figures in Q4).
- The new HxG/AxG columns let the notebook add an xG Poisson rating without another source. The xG provider is not stated anywhere I found; another researcher covers xG.

### Gaps
- I found no statement of who supplies the new HxG/AxG values, or whether they are pre-match-safe (they are post-match values).
- I found no published list of which bookmakers make up Avg/Max in 2026/27, nor how many books each average uses.

## Q2. Why and when the Pinnacle columns disappeared (link to Pinnacle's API closure)

### Takeaway
The cause is Pinnacle closing its public API on 23 Jul 2025. football-data takes Pinnacle prices through OddsPortal's feed, which went stale right away. OddsPortal dropped Pinnacle (and its archive) in Oct 2025 and Pinnacle came back only intermittently. The last Pinnacle odds in SP1/SP2 are for 12 Jan 2026, and the operator called the loss possibly "permanent" on 16 Jan 2026. Even the 2025/26 Pinnacle values that do exist are flagged by the site as "systematically out of date", and my check finds them measurably staler than in 2024/25.

### Cited Findings
- **Pinnacle's own documentation (primary source):** "Access to Pinnacle API suite has been closed for the general public since July 23rd, 2025." Pinnacle adds: "We offer bespoke data services for select high value bettors & commercial partnerships." The notice also mentions support for academics and pregame handicapping projects, with requests to api@pinnacle.com — [pinnacleapi-documentation (GitHub)](https://github.com/pinnacleapi/pinnacleapi-documentation). Third-party vendors give the same date ([pinnapi blog](https://pinnapi.com/blog/pinnacle-api-alternative-2026), [sportsapis.dev](https://sportsapis.dev/apis/pinnapi), [pinnodds blog](https://pinnodds.com/blog/pinnacle-api-shut-down-alternative); these have commercial interests).
- **football-data's site warning:** "Since 23/07/2025 Pinnacle's public API for odds delivery has become unreliable meaning their odds are systematically out of date relative to odds for other bookmakers, including both the pre-closing and closing odds. Consequently they should be used with caution when undertaking any betting analyses, and are no longer being included for the calculation of market average and maximum odds." — [data.php](https://www.football-data.co.uk/data.php).
- Timeline from the operator's posts:
  - 1 Aug 2025: "Pinnacle's odds are unreliable (and mostly out of date) since Oddsportal have still not fixed the problem with intermittent updates. They say they are working on it with Pinnacle" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3lvdigtbrws2l).
  - 15 Aug 2025: "Pinnacle's odds remain unreliable and are not included in the max/avg calculation" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3lwgtvxkpec2h).
  - 24 Oct 2025: "Pinnacle has now completely disappeared from Oddsportal. I am told it will be back in the future, but with the entire archive removed, it remains to be seen how credible that is" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3m3wnysf2hk2w). Pinnacle was then "suddenly back again (although still seem to be intermittent)" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3m3wzxunaks2s).
  - 31 Oct 2025: "Pinnacle odds now only available for the biggest divisions" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3m4ifcsb5wc2j).
  - 4 Nov 2025: "almost no Pinnacle odds for the lower league games, although bizarrely they are showing for the Spanish 2nd division game" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3m4sei3mg3c27).
  - **16 Jan 2026:** "Sadly, Pinnacle's odds have gone again from Oddsportal. Maybe it's permanent this time. ... there are other API sources available, although typically via subscription" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mcjy6cxqtk2v).
- **Exact cut-off in the files** (my computation; [SP1 2526](https://www.football-data.co.uk/mmz4281/2526/SP1.csv), [SP2 2526](https://www.football-data.co.uk/mmz4281/2526/SP2.csv)):
  - Last match with PSH/PSCH/P>2.5/PAHH: **12/01/2026** in both divisions.
  - SP1: Pinnacle present for 189/189 matches up to that date and 0 after (189/380 for the season).
  - SP2: present for only **196/231** matches up to that date (PSCH 198), and 196/462 for the season.
- **Staleness check** (my computation, de-vigged home-win probability; [SP1 2425](https://www.football-data.co.uk/mmz4281/2425/SP1.csv), [SP2 2425](https://www.football-data.co.uk/mmz4281/2425/SP2.csv), 2526 files above):
  - Mean |P(Pinnacle closing) − P(Betfair Exchange closing)|:
    - SP1: 0.0065 in 2024/25 → 0.0098 in 2025/26 (Aug–Jan).
    - SP2: 0.0060 → 0.0115.
    - Share of matches with a gap > 5 pp: 0% → 0.5% (SP1) and 0% → 2.0% (SP2).
  - Control, Bet365 closing vs BFE closing: stayed flat (SP1 0.0108 → 0.0093; SP2 0.0094 → 0.0082).
  - Pinnacle's own pre-closing→closing movement shrank in SP1 (0.0246 → 0.0153), consistent with prices that were not updating.
- Replacement columns: no column directly replaces PS*. BFE (Betfair Exchange) already existed from 2024/25 (see Q1). For tennis, the operator wrote on 7 Sep 2025: "Given the situation with Pinnacle's prices (no longer reliable), I've opted to include Betfair exchange odds with the files going forward" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3lybpehz3hk2e). For the extra leagues, bet365 was added on 15 Aug 2025 "in light of the out-of-date Pinnacle odds" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3lwgktex7xs2c).

### Inferences
- Treat PS*/P>2.5/PAHH from 23/07/2025 to 12/01/2026 as unreliable (the site says so, and the staleness check agrees). Excluding them, or replacing them with BFEC/AvgC, makes the market baseline consistent from 23/07/2025 onward. That is roughly 1,060 SP1+SP2 matches (842 in 2025/26 plus 220 in 2026/27 so far).
- Pinnacle prices before 23/07/2025 (2012/13–2024/25) are unaffected and remain the best free sharp history.
- OddsPortal is very unlikely to work as a backfill for Pinnacle history, because the operator reports that the whole Pinnacle archive was removed (single source; see Q5).

### Gaps
- I found no OddsPortal statement on removing the Pinnacle archive, or on whether it was restored. This rests only on the operator's 24 Oct 2025 post.
- I found no Pinnacle statement about whether "pregame handicapping projects" from Spain would qualify for bespoke data.

## Q3. Collection timing, update speed, fixtures.csv, data errors, availability risk, other Spanish competitions

### Takeaway
- Timing and freshness: pre-closing odds are a Friday afternoon (≤17:00 UK) or Tuesday (≤13:00 UK) snapshot. Closing odds are collected near kick-off, but the exact time is undocumented. Results are current within about a day (Monday 26/10/2026 games were already in the files on 27/10).
- fixtures.csv: still lists SP1/SP2 with odds, but without Pinnacle.
- Data quality: internally clean in my checks. The known problems are kick-off times and lines coming from OddsPortal's feed.
- Availability: the main operational risk. There were outages in Sep 2026 from bot traffic, and on tennis-data the operator removed the CSVs.
- Other Spanish competitions: football-data covers no Liga F, Copa del Rey or Primera Federación.

### Cited Findings
- Odds collection: "the odds are collected for the downloadable weekend fixtures on Fridays afternoons generally not later than 17:00 British Standard Time. Odds for midweek fixtures are collected Tuesdays not later than 13:00 British Standard Time." The page showed "Latest fixtures uploaded: 23/10/26 14:36 UK time" — [matches.php](https://www.football-data.co.uk/matches.php). The same rule appears in [notes.txt](https://www.football-data.co.uk/notes.txt).
- Update frequency: files are "at least updated twice weekly (Sunday nights and Wednesday nights)" — [data.php](https://www.football-data.co.uk/data.php). On 27/10/2026 the Spain page showed "Last updated: 26/10/26" ([spainm.php](https://www.football-data.co.uk/spainm.php)), and both 2026/27 files already contained the Monday 26/10/2026 matches (Sevilla–Osasuna in SP1, Andorra–Burgos in SP2) (my check of [SP1 2627](https://www.football-data.co.uk/mmz4281/2627/SP1.csv) and [SP2 2627](https://www.football-data.co.uk/mmz4281/2627/SP2.csv)).
- Midweek Spanish fixtures are announced on Tuesdays, e.g. 20 Oct 2026: "Midweek main leagues fixtures: E1, E2, E3, SC1 & SP1" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3myci3sjqek2g).
- **fixtures.csv still includes Spain with odds.** On 27/10/2026 it had 194 rows in 21 divisions, including 10 SP1 and 11 SP2 matches dated 23–26/10/2026. It has 94 columns: Referee, plus the same pre-closing bookmakers as the 2026/27 results (B365, BFD, BV, BW, PP, SKB, Max, Avg, BFE; O/U from B365/Max/Avg/BFE; AH from B365/Max/Avg/BFE). The closing columns are present but empty, and there is no Pinnacle (my computation; [fixtures.csv](https://www.football-data.co.uk/fixtures.csv)).
- Data-quality checks on SP1/SP2 2024/25–2026/27 (my computation, files above):
  - None found: rows with Max < Avg, Avg overround < 1, Bet365 overround > 1.15, BFE/BFEC overround < 0.99, FTR inconsistent with goals, HT goals > FT goals, or missing core stats.
  - One impossible stat: AST > AS for Huesca–Burgos 07/09/2024 (SP2).
  - Four SP1 2025/26 rows have no AHh.
  - 2026/27 BFEC overround ranges 1.0001–1.0129 (median 1.0049) in SP1 and 1.0000–1.017 (median 1.0082) in SP2.
- Known feed problems:
  - 14 Aug 2026: "the complete mess with Oddsportal's feed at the moment, including systematically incorrect kick-off times, and spontaneously jumping/disappearing lines" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mszxdqh2x22d).
  - Corrections are posted ad hoc, e.g. "Santa Clara v Nacional (P1) on 10th August had incorrect closing odds so these have been repopulated" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mte2gxvalc2e).
  - 6 Feb 2026: "Ladbrokes and Coral odds are now intermittently absent" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3me6yevffv22d).
- Dependency risk: "oddsportal which I use has become less and less reliable over time, so I can't know how long I will continue to offer the fixtures/results in the current way" (31 Jul 2026) — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mrwir2ly222g).
- Availability risk:
  - 8 Sep 2026: "if outside the UK, remove the www. in the url or use a UK VPN until the problem is resolved" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3muysxvca3c2y).
  - 15 Sep 2026: "all the problems I had recently with website availability" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mvki25wta22f).
  - 17 Sep 2026: "Hopefully access to it will be settling down" — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mvqq2up7222o).
  - On the sister site, "I've decided to remove all CSV files from Tennis-Data in an attempt to stop the automated and repeated heavy downloads that have, according to my host, causing the 503 error outages" (12 Sep 2026, [post](https://bsky.app/profile/12xpert.bsky.social/post/3mvcujab2s223)), blamed on "lazy data calls from AI hoovers and other bots" ([post](https://bsky.app/profile/12xpert.bsky.social/post/3mvglzrhruk2x)).
  - On 27/10/2026 the non-www URL https://football-data.co.uk/mmz4281/2627/SP1.csv returned HTTP 200 with the same 47,448 bytes as the www URL (my check).
- **No other Spanish competitions:** the Spain page lists only Primera and Segunda for every season ([spainm.php](https://www.football-data.co.uk/spainm.php)). The "Extra Leagues" are Argentina, Austria, Brazil, China, Denmark, Finland, Ireland, Japan, Mexico, Norway, Poland, Romania, Russia, Sweden, Switzerland and USA ([data.php](https://www.football-data.co.uk/data.php)). Russia was discontinued for 2026/27 ([post](https://bsky.app/profile/12xpert.bsky.social/post/3mssdefryjc2y)). So there is no Liga F, Copa del Rey, Supercopa or Primera Federación.
- The operator points heavier users to paid partners: TheStatsAPI ([thestatsapi.php](https://www.football-data.co.uk/thestatsapi.php)), Footiqo ([footiqo.php](https://www.football-data.co.uk/footiqo.php)) and OddsRelay, a live feed of more than 140 bookmakers with "Pinnacle, is coming soon" ([oddsrelay.php](https://www.football-data.co.uk/oddsrelay.php)).

### Inferences
- The Time column looks like UK local time, one hour behind Spanish time. 2026/27 SP1 kick-offs cluster at 13:00/15:15/17:30/20:00 (my count from [SP1 2627](https://www.football-data.co.uk/mmz4281/2627/SP1.csv)), and the Real Madrid–Barcelona match of 26/10/2025 is listed at 15:15 ([SP1 2526](https://www.football-data.co.uk/mmz4281/2526/SP1.csv)). That Clásico started at 16:15 Spanish time, but this comes from my background knowledge and was not verified in this session. Together with the Aug 2026 kick-off-time errors, rest-day features should take kick-off times from an official calendar rather than from this column.
- If the notebook re-downloads every season's CSV on each Colab run, it generates exactly the traffic the operator is fighting. Caching past seasons (for example in Google Drive) and re-fetching only the current season, with a non-www fallback URL, would lower both outage risk and the chance that CSVs are withdrawn.
- Pre-closing (Friday) odds are closer to the information available when a Quiniela slip is filled in than closing odds are. Backtests on closing odds may flatter accuracy compared with live use. This is a methodological caution, not a measured result.

### Gaps
- The exact capture time of the "closing" odds is not documented on the pages I read.
- I found no list of past corrections or errata beyond the ad-hoc Bluesky posts.

## Q4. Quantitative check: which remaining football-data columns best replace Pinnacle (power de-vig, RPS)

### Takeaway
Over 2019/20–2023/24 (4,185 matches), the market-average closing odds (AvgC) are the closest proxy to Pinnacle closing: mean |ΔP| is about 0.005, at a cost of about +0.0001 RPS. Betfair Exchange closing (BFEC) matched or beat Pinnacle closing in SP1 2024/25. For pre-match (Friday) odds in Segunda, avoid BFE: it is illiquid and clearly worse there, so use Avg or B365. The model's reported edge (0.20033 vs 0.20043, i.e. 0.0001) is the same size as these differences between data sources, so the baseline must be held constant when comparing.

### Cited Findings
All figures are my computation with the power method, on matches where every listed source is present. Source files are the SP1/SP2 CSVs for [1920](https://www.football-data.co.uk/mmz4281/1920/SP1.csv), [2021](https://www.football-data.co.uk/mmz4281/2021/SP1.csv), [2122](https://www.football-data.co.uk/mmz4281/2122/SP1.csv), [2223](https://www.football-data.co.uk/mmz4281/2223/SP1.csv), [2324](https://www.football-data.co.uk/mmz4281/2324/SP1.csv), [2425](https://www.football-data.co.uk/mmz4281/2425/SP1.csv), [2526](https://www.football-data.co.uk/mmz4281/2526/SP1.csv) and [2627](https://www.football-data.co.uk/mmz4281/2627/SP1.csv) (SP2 at the same paths with SP2.csv). Lower RPS is better.

**2019/20–2023/24 (no BFE yet; SP1 n=1,897, SP2 n=2,288)**

| Division | PSC | AvgC | B365C | PS | B365 | Avg |
|---|---|---|---|---|---|---|
| SP1 | **0.19248** | 0.19258 | 0.19261 | 0.19274 | 0.19293 | 0.19295 |
| SP2 | **0.20779** | 0.20792 | 0.20784 | 0.20873 | 0.20867 | 0.20882 |

- Mean |ΔP| vs PSC (average of home and away): AvgC 0.0050 (SP1) and 0.0058 (SP2); B365C 0.0078 and 0.0093.
- Median overround: PSC 1.025/1.031, AvgC 1.045/1.067, B365C 1.056/1.061.

**2024/25 (all sources present; SP1 n=380, SP2 n=462)**

| Division | BFEC | AvgC | B365C | PSC | PS | BFE (pre-closing) |
|---|---|---|---|---|---|---|
| SP1 | **0.18693** | 0.18704 | 0.18715 | 0.18720 | 0.18923 | 0.18951 |
| SP2 | 0.20322 | **0.20228** | 0.20362 | 0.20313 | 0.20367 | 0.21233 |

- In SP2, pre-closing BFE is far off Pinnacle: mean |ΔP| vs PSC 0.048, against about 0.027 for the bookmakers.
- BFEC median overround: 1.0055 (SP1) and 1.0074 (SP2).

**2025/26, Aug–Jan only (stale Pinnacle; n=188 per division)**

| Division | BFEC | B365C | AvgC | PSC |
|---|---|---|---|---|
| SP1 | **0.18568** | 0.18576 | 0.18590 | 0.18622 (worst closing) |
| SP2 | 0.23405 | 0.23527 | 0.23385 | **0.23311** |

**2025/26 + 2026/27 to 26 Oct, no Pinnacle (SP1 n=448, SP2 n=537)**

| Division | BFEC | AvgC | B365C | B365 | Avg | BFE |
|---|---|---|---|---|---|---|
| SP1 | **0.19112** | 0.19142 | 0.19148 | 0.19216 | 0.19217 | 0.19226 |
| SP2 | 0.21326 | **0.21318** | 0.21363 | 0.21337 | 0.21374 | 0.21665 |

- The consensus margin has risen since the move to UK-only books without Pinnacle. Median AvgC overround went from 1.045 to 1.061 in SP1 and from 1.067 to 1.090 in SP2. For B365C, 2025/26–2026/27 medians are 1.055 (SP1) and 1.079 (SP2).

### Inferences
- **Closing-odds anchor from 23/07/2025:** use BFEC when present, falling back to AvgC, then B365C. Over 4,185 matches, AvgC cost only about 0.0001 RPS against PSC. BFEC has the lowest margin, but has holes in SP2.
- **Pre-closing anchor:** use Avg or B365, and do not use BFE in Segunda.
- The model-vs-market comparison (0.20033 vs 0.20043) should be recomputed on the same matches with the same fallback baseline. A source switch alone moves market RPS by about 0.0001, which is the whole reported edge.
- The power method suits the higher-margin UK consensus. Exchange odds (overround about 1.005) need almost no de-vig.
- With n of a few hundred per season, differences of 0.0001–0.0005 are within noise. Only the 2019/20–2023/24 block is reasonably robust.

### Gaps
- I did not test O/U 2.5 replacements (AvgC>2.5, BFEC>2.5 vs PC>2.5), log-loss, or significance (e.g. Diebold–Mariano). The 2025/26 Aug–Jan comparison is small.
- I did not test what Betfair commission does to effective exchange odds.

## Q5. Historical odds archives that can fill the Pinnacle gap (OddsPortal, BetExplorer, Betfair Historical, the-odds-api, OddsPapi, TheStatsAPI, Footiqo, Kaggle/GitHub)

### Takeaway
No free archive still provides reliable Pinnacle prices for 2025/26–2026/27. For Pinnacle itself, the realistic paid options are:
- the-odds-api historical snapshots (since Jun 2020; 5-minute snapshots since Sep 2022; Pinnacle "from public website"; US$30–59/month);
- OddsPapi (claims a free historical tier back to the opening line);
- TheStatsAPI (US$50/month; Pinnacle/Bet365/BFE opening and closing, but its odds history is probably short).

For exchange prices, Betfair Historical Data runs since 2016 (BASIC is free, last traded price at 1-minute intervals; ADVANCED costs about £69/month for soccer). OddsPortal's Pinnacle archive is reportedly gone. BetExplorer still serves average odds in static HTML.

### Cited Findings
- **OddsPortal:**
  - It is football-data's odds source ("from Oddsportal since 2019/20") — [data.php](https://www.football-data.co.uk/data.php); acknowledged in [notes.txt](https://www.football-data.co.uk/notes.txt).
  - Pinnacle "completely disappeared from Oddsportal ... with the entire archive removed" (24 Oct 2025) — [post](https://bsky.app/profile/12xpert.bsky.social/post/3m3wnysf2hk2w); gone again on 16 Jan 2026 — [post](https://bsky.app/profile/12xpert.bsky.social/post/3mcjy6cxqtk2v).
  - The LaLiga results page answered HTTP 200 on 27/10/2026, but its static HTML contains no odds values and no "Pinnacle" string. Odds are rendered client-side (my check of [oddsportal LaLiga results](https://www.oddsportal.com/football/spain/laliga/results/)).
- **BetExplorer:** the LaLiga results page serves odds in static HTML: 100 `data-odd` cells on 27/10/2026 (my check of [betexplorer LaLiga results](https://www.betexplorer.com/football/spain/laliga/results/)). A Copa del Rey results page exists with only 4 odds cells so far ([betexplorer Copa](https://www.betexplorer.com/football/spain/copa-del-rey/results/)).
- **Betfair Historical Data (exchange):**
  - Tiers: "Basic (free): 1-minute intervals, last traded price, no volume"; Advanced: 1-second intervals, top 3 price ladder, volume; Pro: 50 ms ticks and the full ladder.
  - Covers "nearly all markets offered on the Exchange" since 2016. Delivered as data.tar containing .bz2 stream files. Free data must still be "purchased" (checked out at £0) on the site — [Betfair Data Scientists guide](https://betfair-datascientists.github.io/data/usingHistoricDataSite/).
  - A GitHub investigation dated 18 Oct 2026 found:
    - Coverage: Basic covers EPL match odds from May 2015, available about 5 days after settlement.
    - No competition filter (matches have to be identified by team names).
    - Delta-encoded last-traded price (LTP): in a sample, the draw's last trade was 43 minutes stale at T−1 min.
    - Licence: "personal, internal use only", with no onward distribution.
    - Rate card for soccer: Basic 0, Advanced 69, Pro 230 per month.
    — [Acusick1/odds #507](https://github.com/Acusick1/odds/issues/507). Betfair also offers bulk discounts for 12 months of one sport — [Betfair developer support](https://support.developer.betfair.com/hc/en-us/articles/360019984158-Are-bulk-purchase-discounts-available). Excel and Python tooling exists ([betfair/historic-data-workbook](https://github.com/betfair/historic-data-workbook)).
  - Access from Spain is unclear: an Oct 2026 forum thread on non-UK access gets no answer, and the poster writes "I can't open an account there" — [Bet Angel forum](https://forum.betangel.com/viewtopic.php?t=32489).
  - historicdata.betfair.com returned 403 to my non-browser request (my check).
- **the-odds-api (historical):**
  - "Historical odds data is available from June 6th 2020, with snapshots every 10 minutes"; "From September 2022, snapshots are at 5-minute intervals".
  - Cost: 10 credits per region per market. Endpoints: `/v4/historical/sports/{sport}/odds`, `/events` and `/events/{eventId}/odds`. Sport key `soccer_spain_segunda_division` ("La Liga 2 - Spain") appears in the docs — [v4 docs](https://the-odds-api.com/liveapi/guides/v4/).
  - Plans: Starter free (500 credits), 20K US$30, 100K US$59, 5M US$119, 15M US$249. **Conflict:** the homepage marks "Historical Odds" as included in every plan, including the free Starter ([the-odds-api.com](https://the-odds-api.com/)), while the docs say historical endpoints are "only available on paid usage plans" ([v4 docs](https://the-odds-api.com/liveapi/guides/v4/)).
  - Pinnacle (`pinnacle`) is in the eu region with the note "Odds are from public website which may incur a delay". Betfair Exchange is `betfair_ex_eu`/`betfair_ex_uk` — [bookmaker list](https://the-odds-api.com/sports-odds-data/bookmaker-apis.html).
- **OddsPapi** (vendor blog, 20 Aug 2026):
  - Free tier historical odds "back to the opening line": 3 bookmakers per call, about 4.5 s between calls. The example Pinnacle history held 32 snapshots from 6 Jul to 11 Aug 2026.
  - LaLiga opening round: Pinnacle on 7 of 8 fixtures; `betfair-ex` median three-way margin 0.71%; the best Spanish-licensed book, codere.es, at 4.36%. 174–192 bookmakers per fixture unfiltered.
  — [OddsPapi blog](https://oddspapi.io/blog/?p=3654). The pricing page published no tiers when I fetched it ([oddspapi pricing](https://oddspapi.io/en/pricing)).
- **TheStatsAPI** (football-data partner):
  - "Opening, current and closing betting odds for 1X2, ..., over/under, Asian handicap ... from Pinnacle, Bet365, Betfair Exchange, and Kambi operators, for both upcoming and historical games" — [football-data thestatsapi.php](https://www.football-data.co.uk/thestatsapi.php).
  - Its own homepage lists Bet365, Pinnacle, Paddy Power, Betfair *Sportsbook* and Kambi (a conflict over exchange vs sportsbook). It covers 150 competitions by default (up to 1,196 on request) and "10 years" of match data for major leagues, with xG.
  - Pricing: Starter US$50/month (100k requests), Growth US$129, Scale US$379; 7-day trial — [thestatsapi.com](https://www.thestatsapi.com/).
  - Its coverage page names La Liga but not Segunda, and lists odds as "where captured" — [coverage](https://www.thestatsapi.com/coverage).
  - The odds feature was still "coming in the coming weeks" on 2 Apr 2026 — [post](https://bsky.app/profile/12xpert.bsky.social/post/3miivpzvn2k2k).
- **Footiqo** (football-data partner): historical data from 2015/16 for €49.99. It covers "150,000+ matches across 60+ leagues" with "Opening & closing odds (1xBet) where available", xG, corners, cards, shots and referees. A bundle of all three datasets costs €99.99. Each is a one-time purchase that includes 4–8 weeks of updates — [footiqo.php](https://www.football-data.co.uk/footiqo.php).
- **Pinnacle official route:** bespoke data for "select high value bettors & commercial partnerships", with academics and pregame handicapping projects supported; contact api@pinnacle.com — [pinnacleapi-documentation](https://github.com/pinnacleapi/pinnacleapi-documentation). Third-party Pinnacle feeds (pinnapi, pinnodds, PS3838 routes) exist, but their claims are unverified ([pinnapi blog](https://pinnapi.com/blog/pinnacle-api-alternative-2026), [pinnodds](https://pinnodds.com/blog/pinnacle-api-shut-down-alternative)).
- **Kaggle/GitHub:** I found no Kaggle dataset with Pinnacle closing odds for LaLiga 2025/26–2026/27. Search turned up only FootyStats CSV pages and odds trackers without Pinnacle — [FootyStats datasets](https://footystats.org/dk/spain/la-liga/datasets).

### Inferences
- the-odds-api is the most practical paid way to rebuild Pinnacle pre-match and closing odds for 2025/26–2026/27, if its historical snapshots actually contain `pinnacle` for Spanish leagues after Jul 2025. Its Pinnacle data comes from the public website, so it may not depend on the closed API, but the "may incur a delay" note means it should be checked against BFEC.
- Rough cost: each historical call returns all events of a sport at one timestamp. One h2h+totals snapshot per kick-off slot is roughly 500 calls × 20 credits ≈ 10k credits per SP1+SP2 season. That suggests 1–2 months of the US$30/US$59 plan would backfill both seasons (my estimate, not vendor-confirmed).
- Betfair BASIC (LTP) is weak for the draw and in thin Segunda markets, given the 43-minute stale draw example. ADVANCED (top-3 ladder) is needed for a proper back/lay mid-price. football-data's BFEC already gives a free closing exchange price per match.
- A short non-commercial request to api@pinnacle.com, describing the project as a pregame forecasting model, is cheap and is the only official Pinnacle route.

### Gaps
- Not verified: the-odds-api historical coverage of `pinnacle` for `soccer_spain_la_liga`/`soccer_spain_segunda_division` after Jul 2025 (needs an API key), and the exact La Liga sport key.
- OddsPapi historical depth before Jul 2026 and Segunda coverage are unknown.
- TheStatsAPI's odds history start date and Segunda coverage are unknown.
- Whether Spanish (betfair.es) accounts can use historicdata.betfair.com is unknown.
- I could not confirm Betfair's current official annual prices.
- I did not check the terms of service of BetExplorer or OddsPortal.

## Q6. football-data.org (API): Spanish competitions, tiers, limits, odds/stats, prices in 2026

### Takeaway
The free tier includes Primera (PD) but not Segunda (SD is TIER_TWO, so a paid plan is required). Copa del Rey is TIER_THREE and there is no Liga F. The free plan allows 10 calls/min with delayed scores. Odds (pre-match 1X2) and statistics are €15/month add-ons on top of a plan. It is useful as a calendar/results/standings feed, not as an odds archive.

### Cited Findings
- The unauthenticated `GET /v4/competitions` call returned 190 competitions (my call to [api.football-data.org/v4/competitions](https://api.football-data.org/v4/competitions)):
  - Spain: PD "Primera Division" TIER_ONE (current season start 2026-08-16); SD "Segunda División" TIER_TWO (2026-08-16); CDR "Copa del Rey" TIER_THREE (currentSeason still starting 2025-09-27); LLP "La Liga Play-Offs" TIER_FOUR; SDE "Supercopa de España" TIER_FOUR.
  - There is no Spanish women's competition.
  - Tier counts: TIER_ONE 12 (BL1, BSA, CL, DED, EC, ELC, FL1, PD, PL, PPL, SA, WC), TIER_TWO 20, TIER_THREE 25, TIER_FOUR 133.
  - Match endpoints need a token: `/v4/competitions/PD/matches` returned 403 without one.
- Plans ([pricing](https://www.football-data.org/pricing)):
  - Free: €0, 12 competitions, 10 calls/min, "Scores delayed", "Schedules delayed".
  - Free w/ Livescores: €12, 20/min.
  - ML Pack Light: €29 (adds trend/form data and 10 seasons).
  - Free + Deep Data: €29, 30/min, lineups and bookings.
  - Standard: €49, 30 competitions, 60/min.
  - Advanced: €99, 50 competitions, 100/min.
  - Pro: €199, 100 competitions, 120/min.
  - Add-ons at €15/month each: "Odds Add-On: 40 competitions, pre-match home/draw/away odds", and a Statistic Add-On (corners, shots on/off goal, fouls, cards, possession, etc.). No base plan includes odds.
- Coverage page: "Access to data of these leagues & cups is free. Forever.", with "La Liga" listed under Spain in the free tier — [coverage](https://www.football-data.org/coverage).

### Inferences
- The 12 free competitions match the 12 TIER_ONE codes, so the free plan probably equals TIER_ONE. Segunda would then need at least Standard (€49), and Copa del Rey probably Advanced (€99). This mapping is inferred from the counts, not stated by the site.
- For the notebook, the free PD feed is a clean JSON source for Primera fixtures and kick-off changes. It does not help with Segunda or with odds history unless paid for.

### Gaps
- The bookmaker behind the Odds Add-On and how deep its history goes are not stated.
- The exact tier-to-plan mapping is not stated on the pages I read.

## Q7. Python/R libraries that aggregate these sources (2026 status)

### Takeaway
soccerdata (Python) is actively released (2026.43.0, 19 Oct 2026). Its football-data reader is fine, but its ClubElo reader is currently broken by the ClubElo outage, and FBref is hitting CAPTCHAs. penaltyblog (1.13.1, 5 Oct 2026) is maintained and is useful for models, ratings and RPS. worldfootballR (R) has been archived and unmaintained since Sep 2025.

### Cited Findings
- **soccerdata:**
  - Latest PyPI release 2026.43.0, uploaded 2026-10-19 (my query of [PyPI JSON](https://pypi.org/pypi/soccerdata/json)).
  - Docs list ClubElo, ESPN, FBref, FiveThirtyEight, Match History (Football-Data.co.uk), Sofascore, SoFIFA, Understat and WhoScored. The docs header still shows "v1.9.2.dev14" — [docs](https://soccerdata.readthedocs.io/en/latest/).
  - Open issues ([issues](https://github.com/probberechts/soccerdata/issues)):
    - #977 (23 Sep 2026): api.clubelo.com "502 Bad Gateway" for every path. Workaround: clubelo.com pages embed data only "from about September 2022". Labelled bug on 17 Oct 2026 and still open — [#977](https://github.com/probberechts/soccerdata/issues/977).
    - #967 (5 Aug 2026): FBref CAPTCHA.
    - #880 (24 Aug 2025): FBref team match stats missing La Liga league matches.
    - #974 (25 Aug 2026): WhoScored locale IndexError.
    - #979 (8 Oct 2026): proposal for a "Football Charts" reader (results, half-time scores and goal minutes for 93 leagues).
- **penaltyblog** 1.13.1 (5 Oct 2026, Python ≥3.10):
  - Scrapers: "Football Charts, Understat, Club Elo, and Fantasy Premier League", plus StatsBomb and Opta API connectors.
  - Models: Poisson, Bivariate Poisson, Dixon-Coles and Bayesian/hierarchical. Ratings: Elo, Massey, Colley and Pi. Also implied-odds (overround removal) and RPS tools — [PyPI](https://pypi.org/project/penaltyblog/).
  - The docs list FBRef, Understat, Club Elo and FPL as sources and make no mention of football-data.co.uk — [docs](https://penaltyblog.readthedocs.io/en/latest/).
- **worldfootballR:** "archived by the owner on Sep 18, 2025. It is now read-only" and "will no longer be maintained". Fotmob was dropped in v0.6.4 and the CRAN version is "very much out of date" — [GitHub](https://github.com/JaseZiv/worldfootballR).

### Inferences
- The notebook already reads football-data directly, so soccerdata's MatchHistory reader adds little, and it is equally exposed to the site's anti-bot measures.
- penaltyblog's pi-ratings and Dixon-Coles are a maintained cross-check for the notebook's own implementations. Its Club Elo scraper is presumably affected by the same api.clubelo.com outage (not tested).
- Avoid worldfootballR for new work.

### Gaps
- I could not read GitHub release notes directly (API access to these repos is not enabled in this session).
- penaltyblog's specific de-vig methods (power, Shin and so on) are not listed on the pages I fetched.

## Q8. Results/fixtures/standings references (laliga.com, BDFutbol, worldfootball.net, Transfermarkt, RSSSF, Soccerway)

### Takeaway
- For the current calendar and kick-off-time changes, the authoritative source is laliga.com. Its calendar pages load match data client-side, so they are not trivially machine-readable.
- football-data.org's free PD feed is the easiest programmatic alternative for Primera.
- Many reference sites (BDFutbol, worldfootball.net, clubelo.com, Transfermarkt) now block non-browser clients, which limits use from Colab. RSSSF and Soccerway are reachable.

### Cited Findings
- laliga.com calendar pages returned HTTP 200 ([LaLiga EA Sports calendario](https://www.laliga.com/laliga-easports/calendario), [LaLiga Hypermotion calendario](https://www.laliga.com/laliga-hypermotion/calendario)). The embedded Next.js `__NEXT_DATA__` (about 6 KB) holds only keys such as `competition`, `calendarCompetitions` and `latestMatchesInfo`, with no match dates (my check). Fixtures are loaded client-side.
- HTTP status from this cloud environment on 27/10/2026 with a browser user-agent (my checks):
  - 403: [bdfutbol.com](https://www.bdfutbol.com/es/), [worldfootball.net](https://www.worldfootball.net/), [clubelo.com](https://clubelo.com/).
  - 202 with an empty body (bot challenge): [transfermarkt.es](https://www.transfermarkt.es/).
  - 200: [rsssf.org](https://www.rsssf.org/), [soccerway.com](https://www.soccerway.com/).
  - WebFetch was also refused by BDFutbol (403).
- Soccerway is live but redesigned. 2026 Trustpilot reviews criticise the redesign (e.g. a removed match calendar) rather than reporting a shutdown — [Trustpilot](https://es.trustpilot.com/review/soccerway.com).
- football-data.co.uk's own match-stat sources are "BBC, Flashscore, ESPN Soccer, Bundesliga.de, Gazzetta.it and Football.fr", and results come from XScores — [notes.txt](https://www.football-data.co.uk/notes.txt).

### Inferences
- For history, football-data.co.uk (SP1 since 1993/94, SP2 since 1996/97, per [spainm.php](https://www.football-data.co.uk/spainm.php)) plus RSSSF for deep archives is enough for Primera/Segunda results.
- Kick-off times should come from laliga.com (manually, or via a headless browser) or from football-data.org PD, not from football-data.co.uk's Time column.

### Gaps
- I could not verify BDFutbol's or worldfootball.net's current coverage or status (both blocked).
- I found no documented public LaLiga data API.
- I did not research how far ahead LaLiga announces kick-off times.

## Q9. Ratings for matches without odds (ClubElo, Opta Power Rankings, others)

### Takeaway
The api.clubelo.com dependency is broken today: every path returns 502, the Fixtures endpoint says "Fixtures API deactivated", and the site blocks bots. The notebook's Elo fallback for cup matches will fail until this changes. Opta Power Rankings (daily, hierarchical Elo with xG, more than 13,500 men's and 2,500 women's clubs) is the best external cross-league rating, but it has no documented API. For international matches, eloratings.net's TSV still downloads.

### Cited Findings
- ClubElo, 27/10/2026 (my checks):
  - [http://api.clubelo.com/2026-10-26](http://api.clubelo.com/2026-10-26) → HTTP 502; `/RealMadrid` → 502; the https variant is reset by the peer.
  - [http://api.clubelo.com/Fixtures](http://api.clubelo.com/Fixtures) returns the body "Fixtures API deactivated".
  - [clubelo.com](https://clubelo.com/) → 403.
  - soccerdata #977 says every path has returned 502 since at least 23 Sep 2026. Registration for a possible authenticated API "isn't open yet" (the reporter's inference). Pages carry rating history only from about Sep 2022 — [#977](https://github.com/probberechts/soccerdata/issues/977).
- Opta Power Rankings:
  - "a hierarchical Elo-based rating system". Elo change is "80% ... from the actual scoreline and 20% from xG" (100% scoreline when there is no xG).
  - A team's rating is the sum of team, league, country and continent levels. "The Power Rankings are updated daily".
  - Coverage: more than 13,500 men's and 2,500 women's teams (separate runs), "190 different countries" and "over 600 unique domestic leagues", including lower divisions — [methodology](https://theanalyst.com/articles/power-rankings-your-club-ranked/).
  - A 27 Jul 2026 article gives "183 FIFA member countries and 562 domestic leagues" (inconsistent with the methodology page) and no download or API URL — [Opta Power Rankings article](https://theanalyst.com/articles/who-are-the-best-football-team-in-the-world-opta-power-rankings).
- eloratings.net (national teams): [World.tsv](https://www.eloratings.net/World.tsv) returned HTTP 200 (30.6 KB). Its first row is "1 1 ES 2287 …" (Spain ranked 1st) (my check).

### Inferences
- The notebook already computes Elo with goal margin and pi-ratings from football-data results, so its own ratings are the most robust fallback for Primera/Segunda clubs.
- Copa del Rey ties against Primera Federación or lower clubs need an external or cross-league rating. Opta (no API; scraping its interactive table would need checking) is the main candidate, and it is also the only one here covering women's clubs (relevant to Liga F).
- eloratings.net suits the international matches in Quiniela jornadas.

### Gaps
- I do not know whether ClubElo's outage is temporary or a move to authenticated or paid access; there is no official statement.
- I did not test whether Opta's ranking table is backed by a fetchable JSON endpoint, or what its terms of use are.

## Q10. Ranked shortlist of historical sources for ORÁCULO 1X2, with concrete benefit and risk

### Takeaway
Keep football-data.co.uk as the backbone. From 23/07/2025, re-anchor the market on BFEC→AvgC→B365C for closing odds and Avg/B365 for pre-closing odds. Then, if budget allows, buy a short the-odds-api (or OddsPapi or TheStatsAPI) historical pull to rebuild Pinnacle for 2025/26–2026/27 and check it against BFEC. Replace the ClubElo dependency.

### Cited Findings
1. **football-data.co.uk SP1/SP2 + fixtures.csv (free; keep as backbone).**
   - Benefit: the longest free history (SP1 1993/94, SP2 1996/97), stats, and now xG; closing odds for B365, Avg/Max and BFE; Pinnacle 2012/13–Jul 2025; results updated within about a day ([spainm.php](https://www.football-data.co.uk/spainm.php), [SP1 2627](https://www.football-data.co.uk/mmz4281/2627/SP1.csv), [data.php](https://www.football-data.co.uk/data.php)).
   - Risk: no Pinnacle after 12/01/2026, and Pinnacle flagged unreliable from 23/07/2025 ([data.php](https://www.football-data.co.uk/data.php)); bookmaker set changes every season; dependence on OddsPortal; incorrect kick-off times ([post](https://bsky.app/profile/12xpert.bsky.social/post/3mszxdqh2x22d)); outages and possible CSV withdrawal ([post](https://bsky.app/profile/12xpert.bsky.social/post/3mvcujab2s223)).
2. **Betfair Exchange closing (BFEC) inside football-data (free) as the Pinnacle substitute.**
   - Benefit: about 0.5% margin, and RPS equal to or better than PSC in SP1 2024/25 (Q4, my computation).
   - Risk: holes in SP2 (BFEAHH 58/121 in 2026/27); pre-closing BFE is unreliable in Segunda (Q4).
3. **the-odds-api historical (US$30–59/month).**
   - Benefit: Pinnacle and Betfair Exchange snapshots every 5 min since Sep 2022 (10 min since Jun 2020), so pre-match odds at the exact Quiniela decision time could be rebuilt ([docs](https://the-odds-api.com/liveapi/guides/v4/), [bookmakers](https://the-odds-api.com/sports-odds-data/bookmaker-apis.html)).
   - Risk: Pinnacle comes "from public website which may incur a delay"; plan access to historical data is stated inconsistently ([homepage](https://the-odds-api.com/) vs docs); Spanish coverage after Jul 2025 is not verified.
4. **OddsPapi historical (claimed free tier).**
   - Benefit: Pinnacle and `betfair-ex` line histories back to the opening line ([blog](https://oddspapi.io/blog/?p=3654)).
   - Risk: vendor claims only; unknown depth; 3 bookmakers per call; throttling.
5. **TheStatsAPI (US$50/month, 7-day trial; endorsed by football-data).**
   - Benefit: Pinnacle/Bet365/BFE opening and closing odds plus xG through one JSON API ([thestatsapi.php](https://www.football-data.co.uk/thestatsapi.php), [thestatsapi.com](https://www.thestatsapi.com/)).
   - Risk: odds launched around spring 2026 ([post](https://bsky.app/profile/12xpert.bsky.social/post/3miivpzvn2k2k)), so history is likely short; Segunda coverage unconfirmed; inconsistent bookmaker lists.
6. **Betfair Historical Data (BASIC free; ADVANCED about £69/month for soccer).**
   - Benefit: real exchange prices since 2016 ([guide](https://betfair-datascientists.github.io/data/usingHistoricDataSite/)).
   - Risk: BASIC is LTP only, with stale draws; heavy parsing; licence limited to personal use ([#507](https://github.com/Acusick1/odds/issues/507)); access from Spain unclear ([forum](https://forum.betangel.com/viewtopic.php?t=32489)).
7. **Pinnacle bespoke data (api@pinnacle.com).**
   - Benefit: the only official Pinnacle source, open to "pregame handicapping projects" and academics ([pinnacleapi-documentation](https://github.com/pinnacleapi/pinnacleapi-documentation)).
   - Risk: discretionary; may require a funded account.
8. **football-data.org (PD free; SD and CDR paid; odds add-on €15).**
   - Benefit: a clean JSON calendar, results and standings feed with kick-off changes for Primera ([pricing](https://www.football-data.org/pricing), [competitions](https://api.football-data.org/v4/competitions)).
   - Risk: Segunda behind a paywall; 10 calls/min; not an odds archive.
9. **Footiqo (€49.99 one-off).**
   - Benefit: 1xBet opening and closing odds plus xG from 2015/16 ([footiqo.php](https://www.football-data.co.uk/footiqo.php)).
   - Risk: 1xBet is not a sharp-market reference; Spanish league coverage not itemised; static purchase.
10. **Ratings for matches without odds: own Elo/pi plus Opta Power Rankings plus eloratings.net.**
    - Benefit: daily Opta coverage of lower and women's divisions ([methodology](https://theanalyst.com/articles/power-rankings-your-club-ranked/)); a working TSV for national teams ([World.tsv](https://www.eloratings.net/World.tsv)).
    - Risk: ClubElo's API is currently down ([#977](https://github.com/probberechts/soccerdata/issues/977)); Opta has no API.
11. **Libraries:** soccerdata (maintained; ClubElo reader broken) and penaltyblog (maintained) are acceptable; worldfootballR is archived ([soccerdata issues](https://github.com/probberechts/soccerdata/issues), [penaltyblog](https://pypi.org/project/penaltyblog/), [worldfootballR](https://github.com/JaseZiv/worldfootballR)).
12. **OddsPortal/BetExplorer scraping (last resort).**
    - OddsPortal's Pinnacle archive is reportedly removed and its odds are client-rendered ([post](https://bsky.app/profile/12xpert.bsky.social/post/3m3wnysf2hk2w); my check of [OddsPortal](https://www.oddsportal.com/football/spain/laliga/results/)).
    - BetExplorer serves static average odds that could cover Copa del Rey ([BetExplorer](https://www.betexplorer.com/football/spain/laliga/results/)).
    - Risk: terms of service and legality (not checked), and fragility.

### Inferences
- Immediate, zero-cost actions:
  1. Mark PS*/P>2.5/PAHH as missing from 23/07/2025.
  2. Use BFEC→AvgC→B365C (closing) and Avg/B365 (pre-closing) as the market anchor, and AvgC>2.5/BFEC>2.5 for implied goals.
  3. Re-evaluate the model-vs-market RPS on the same baseline.
  4. Cache football-data files and add a non-www fallback URL.
  5. Replace api.clubelo.com with the notebook's own ratings (plus Opta for lower-division cup opponents and eloratings.net for national teams).
- Paid upgrade, worth it only if the Pinnacle anchor is believed to add more than about 0.0001 RPS over AvgC/BFEC: a 1–2 month the-odds-api historical pull (Pinnacle plus Betfair Exchange, h2h plus totals) for SP1/SP2 2025/26–2026/27, validated against BFEC.

### Gaps
- No source offers a verified, complete Pinnacle pre-match and closing history for Spanish football after 23/07/2025. Each candidate needs a sample pull to confirm coverage, especially for Segunda.
