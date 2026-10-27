# Odds sources and processing methods for accurate 1X2 probabilities (Europe/Spain): evidence for ORÁCULO 1X2 / La Quiniela now that football-data.co.uk has dropped Pinnacle

How to read the "OA" (own analysis) items. They are a reproducible computation I ran on 27 Oct 2026 on football-data.co.uk CSVs. Scope: 20 leagues (SP1, SP2, E0–E3, EC, SC0, SC1, D1, D2, I1, I2, F1, F2, N1, B1, P1, T1, G1), seasons 2012/13–2026/27, 104,930 matches with results. Files follow the pattern `https://www.football-data.co.uk/mmz4281/{season}/{div}.csv`, and the column key is [notes.txt](https://www.football-data.co.uk/notes.txt).
- Labels: PS/PSC = Pinnacle pre-closing/closing; Avg/AvgC = market average; Max/MaxC = market maximum; BFE/BFEC = Betfair Exchange; B365 = Bet365; BW = bwin ("Bet&Win"); BV = BetVictor (incl. former VC); WH = William Hill; IW = Interwetten; BFD = Betfred; 1XB = 1xBet; BF = Betfair Sportsbook. A trailing "C" means closing.
- "Pre-closing" odds are collected on Friday afternoon for weekend games and on Tuesday afternoon for midweek games ([notes.txt](https://www.football-data.co.uk/notes.txt)).
- De-vig methods: multiplicative ("mult"), additive, power, Shin, odds-ratio ("or").
- Metrics: RPS (ordered H<D<A), log-loss (LL, natural log) and hit rate of the argmax sign.
- Comparisons are paired differences (source − reference) on the same matches, so negative = better. "±" is the 95% half-width from cluster-robust standard errors, with clusters = league×season×ISO-week (≈ a jornada).
- The scripts are in a temporary scratchpad (`/tmp/claude-0/-home-user-umbralstudio-apps-github-io/db5fef1a-9578-5e30-892b-7c2f81795a0f/scratchpad/scripts/odds_accuracy.py` and `calib_flips.py`). The methods above are enough to re-run the analysis.
- OA claims below cite a representative data file, e.g. [SP1 2025/26 CSV](https://www.football-data.co.uk/mmz4281/2526/SP1.csv).

## 1. Which odds source is most accurate (Pinnacle vs consensus vs max odds vs Betfair Exchange vs Asian sharp books vs high-margin retail), by how much, in Spain, and are second divisions or women's leagues less efficient?

### Takeaway
Once margins are removed properly (power method), Pinnacle closing, Betfair Exchange closing and the football-data market average are statistically indistinguishable: differences are ≤0.0001 RPS over 10k–46k matches in 2019/20–2025/26. Single retail books are about 0.00015–0.0004 RPS worse. Spain (SP1/SP2) shows the same ordering with wider confidence intervals. Second divisions differ mainly through higher margins, more draws and lower predictability, not through a larger sharp-vs-consensus gap. I found no rigorous accuracy evidence for women's leagues, Asian sharp books or Spanish-licensed books.

### Cited Findings
- OA, all 20 leagues, 2019/20–2025/26, closing sources vs Pinnacle closing (both power-devigged) — [OA: football-data CSVs](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - Market average AvgC: +0.00004 ±0.00006 RPS (N=46,553; LL +0.0003 ±0.0002; hit 50.57% vs 50.58%).
  - Betfair Exchange BFEC: −0.00006 ±0.00020 (N=10,180, available from 2024/25).
  - Market maximum MaxC: +0.00010 ±0.00007.
  - BetVictor +0.00006 ±0.00009; Betfair Sportsbook +0.00014 ±0.00026; Bet365 +0.00019 ±0.00008 (LL +0.0010 ±0.0004); 1xBet +0.00020 ±0.00020 (N=7,321); bwin +0.00021 ±0.00010; Interwetten +0.00027 ±0.00011; William Hill +0.00038 ±0.00015.
- OA, same comparison for pre-closing (Friday/Tuesday) odds vs Pinnacle pre-closing — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - Avg|power +0.00004 ±0.00004 (N=46,398); Max|power +0.00008 ±0.00005; BetVictor +0.00007 ±0.00007.
  - Bet365 +0.00015 ±0.00007; 1xBet +0.00017 ±0.00013; William Hill +0.00021 ±0.00010; bwin +0.00022 ±0.00009.
  - Betfair Exchange pre-closing BFE|power +0.00035 ±0.00029 (N=9,697): the exchange is good at the close but not on Friday.
- OA, Spain only (SP1+SP2), 2019/20–2025/26 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv):
  - Closing vs PSC: AvgC|power +0.00008 ±0.00015 (N=5,434); MaxC +0.00004 ±0.00019; BFEC −0.00001 ±0.00038 (N=1,227); Bet365 +0.00017 ±0.00021; bwin +0.00023 ±0.00026; BetVictor +0.00027 ±0.00023.
  - Pre-closing vs PS: Avg|power +0.00013 ±0.00012; Max +0.00013 ±0.00014; Bet365 +0.00008 ±0.00021.
  - Betfair Exchange pre-closing in Segunda is poor: BFE|mult +0.00177 ±0.00127 and BFE|power +0.00091 ±0.00120 (N=596). Its Friday booksum in SP2 is 1.051, against 1.008–1.009 at the close, i.e. thin liquidity days before kickoff.
- OA, user-style weighted consensus (Pinnacle and market average double-weighted, plus all individual books, power) vs Pinnacle pre-closing, 2012/13–2025/26: +0.00007 ±0.00003 RPS (N=97,569; LL +0.0003 ±0.0001). Spain: +0.00009 ±0.00009 (N=11,265). Consensus without Pinnacle: +0.00013 ±0.00004 (all leagues) — [OA](https://www.football-data.co.uk/mmz4281/1819/SP1.csv).
- OA, mean booksum (1 + margin), 2019/20–2025/26 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - SP1: PSC 1.027, BFEC 1.006, AvgC 1.048, B365C 1.056.
  - SP2: PSC 1.033, BFEC 1.008, AvgC 1.071, B365C 1.065, bwin 1.089.
  - In 2026/27 files the market-average booksum is 1.065 (SP1) and 1.091 (SP2) for pre-closing odds. Paddy Power is 1.075/1.108 and SKB (undocumented in notes.txt, presumably Sky Bet) 1.073/1.129.
- OA, league-level gaps vs PSC (2019/20–2025/26, power) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv):
  - Market average AvgC−PSC: SP1 +0.00003 ±0.00021; SP2 +0.00013 ±0.00021; largest in Scotland-2 (SC1) at +0.00066 ±0.00043 and Greece (G1) at +0.00039 ±0.00034.
  - Bet365 B365C−PSC: SP1 +0.00005 ±0.00029; SP2 +0.00027 ±0.00031; up to +0.00095 ±0.00045 in Greece, with Bundesliga-2 (D2) +0.00049, Turkey (T1) +0.00048 and Netherlands (N1) +0.00044.
  - Predictability: Pinnacle closing RPS is 0.1910 in SP1 vs 0.2089 in SP2.
- In 5,478 Big-Five matches (incl. Spain) over three seasons, the Betfair exchange gave more accurate predictions than bookmakers. Betting where bookmaker odds exceeded exchange-implied odds earned above-average and sometimes positive returns — [Franck, Verbeek & Nüesch 2010, IJF 26(3) (SSRN abstract)](https://doi.org/10.2139/ssrn.1503350); [IJF DOI](https://doi.org/10.1016/j.ijforecast.2010.01.004).
- Across 51 online bookmakers and >16,000 English matches since 2010, odds were "generally not biased" (no favourite–longshot or outcome-type bias in aggregate). Individual bookmakers were not efficient and did not fully use the information in competitors' odds — [Elaad, Reade & Singleton 2020, Finance Research Letters 35](https://doi.org/10.1016/j.frl.2019.09.006).
- With odds from 41 bookmakers on 11 major European leagues over 11 years, efficiency differs by market: using best odds, 8 markets are efficient and 3 show exploitable inefficiencies. The abstract does not name the leagues — [Angelini & De Angelis 2019, IJF 35(2)](https://doi.org/10.1016/j.ijforecast.2018.07.008).
- Bundesliga, three seasons (678–837 games): prediction markets and betting odds were equally accurate and both beat tipsters. Combining forecasts helped (slightly with weighting, substantially with a rule-based combination) — [Spann & Skiera 2009, J. Forecasting 28(1)](https://ideas.repec.org/a/jof/jforec/v28y2009i1p55-72.html).
- Spain-specific bias evidence, which conflicts:
  - Odds on Spanish top-flight football respond to fan support, so supporters of the more popular club get better terms (similar for Scotland) — [Forrest & Simmons 2008, Applied Economics 40(1)](https://doi.org/10.1080/00036840701522895); [Lancaster eprint](https://eprints.lancs.ac.uk/id/eprint/44748).
  - Contradicted by Štrumbelj, who "provide[s] evidence against the reported bias of bookmakers favoring better supported teams", attributing it to misinterpretation, and shows basic normalisation yields biased probabilities — [Štrumbelj, J. Sports Economics](https://doi.org/10.1177/1527002513519329).
- La Liga vs EPL: with Shin's method, implied probabilities are unbiased in the EPL. In La Liga, both normalisation and Shin show favourite bias (favourites win more often than implied) — [Koning & Zijm 2022, Annals of Operations Research](https://doi.org/10.1007/s10479-022-04722-3).
- On Spanish football odds, bookmakers ("experts") forecast results better than football-pools bettors (the crowd), and the Spanish betting market shows a favourite–longshot bias — [García, Pérez & Rodríguez 2016, MPRA 69687](https://mpra.ub.uni-muenchen.de/69687).
- Asian handicap vs 1X2: for a large sample of European matches, the 1X2 market shows "a strong pattern of favourite-longshot bias". The Asian handicap market, converted with a new method, "can generate efficient forecasts" for the same matches — [Hegarty & Whelan, "Forecasting Soccer Matches With Betting Odds: A Tale of Two Markets", IJF 41(2) 2025 / CEPR DP17949](https://ideas.repec.org/p/cpr/ceprdp/17949.html).
- Women's football (indirect only): bookmaker-consensus forecasts for the FIFA Women's World Cup adjust outright odds for overround, which one of these pages reports as averaging 8.6%, and average on the log-odds scale — [Zeileis et al. 2019](https://eeecon.uibk.ac.at/~zeileis/news/fifawomen2019/); [Zeileis et al. 2023](https://eeecon.uibk.ac.at/~zeileis/news/fifawomen2023/).

### Inferences
- The Pinnacle advantage over a power-devigged market average is economically tiny: about 0.00004 RPS at close and before close (pooled), and +0.00007 ±0.00003 over 2012/13–2025/26 for a user-style weighted consensus. This is the same size as the user's own consensus gap (0.20051 vs 0.20043 ≈ 0.00008).
- The ranking is: Pinnacle ≈ exchange at close ≈ de-vigged broad average > max odds > single retail books. This matches Elaad et al. (aggregation beats individual books) and Franck et al. (exchange > bookmakers).
- Spanish-licensed retail books were not measured. Given their typically higher margins and the retail-book results above, they should be expected to be no better than Bet365/bwin (untested).
- "Second divisions less efficient" is weakly supported:
  - In SP2 the gaps between sources are slightly larger and n.s.
  - Margins are clearly higher (market average ~7–9% vs ~5–6.5%).
  - Lower-profile leagues (SC1, G1, T1, N1, D2) show the clearest retail-vs-sharp gaps.
- Spain-specific bias evidence is mixed: favourite bias in La Liga (Koning & Zijm, and OA section 3) vs disputed sentiment/fan-support bias.

### Gaps
- No peer-reviewed or reproducible accuracy comparison found for Asian sharp books (SBOBet, Singbet/Crown), Spanish-licensed books (none are in football-data), or women's leagues (Liga F, WSL, NWSL, Frauen-Bundesliga). Three targeted searches found nothing.
- Joseph Buchdahl's own "Wisdom of the Crowd"/Pinnacle closing-line analyses and Pinnacle's "Betting Resources" articles could not be retrieved, so they are not cited directly.
- The full texts of Štrumbelj (2014, IJF, https://doi.org/10.1016/j.ijforecast.2014.02.008) and Štrumbelj & Šikonja (2010, IJF, https://doi.org/10.1016/j.ijforecast.2009.10.005) were not accessible; their bookmaker-by-bookmaker results are not reported here.
- The 1xBet history in football-data covers only 2024/25, and Betfair Exchange only 2024/25 onwards, so their comparisons rest on ~7–10k matches.

## 2. Timing: how much does accuracy improve from early (days-before) odds to closing odds, and what drives it?

### Takeaway
Moving from football-data's Friday/Tuesday Pinnacle odds (PS) to Pinnacle closing (PSC) improves RPS by about 0.00095 (LL by about 0.003) on 97.5k matches. That is roughly 20–25× the Pinnacle-vs-consensus gap and about 10× the user's model edge. The gain grows with lead time (Friday-evening games ≈ +0.0007, Monday games ≈ +0.0018) and is similar in Spain (SP1+SP2 +0.00085 ±0.00045).

### Cited Findings
- OA, all leagues 2012/13–2025/26, PS vs PSC (power): RPS 0.20405 vs 0.20309, d = +0.00095 ±0.00015 (N=97,535); LL +0.0031 ±0.0005; hit rate 50.00% vs 50.25% — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv).
- OA, by league group (12/13–25/26) — [OA](https://www.football-data.co.uk/mmz4281/2425/SP2.csv):
  - SP1: +0.00096 ±0.00057 (N=5,121; hit 54.23% → 54.70%).
  - SP2: +0.00077 ±0.00068 (N=6,138; hit 46.29% → 46.59%).
  - SP1+SP2: +0.00085 ±0.00045, LL +0.0026 ±0.0015.
  - Top-5 leagues +0.00073 ±0.00027; second tiers +0.00078 ±0.00028.
- OA, by kickoff weekday (weekend odds are collected Friday afternoon) — [OA](https://www.football-data.co.uk/mmz4281/2425/E0.csv):
  - All leagues: Friday +0.00069 ±0.00038; Saturday +0.00093 ±0.00022; Sunday +0.00100 ±0.00033; Monday +0.00183 ±0.00080.
  - SP1+SP2: Friday +0.00033 ±0.00113; Saturday +0.00045 ±0.00074; Sunday +0.00092 ±0.00074; Monday +0.00239 ±0.00228.
- OA, other sources over the same horizon (all leagues 2019/20–2025/26): Avg→AvgC +0.00110 ±0.00021; Max→MaxC +0.00108 ±0.00021; Bet365 +0.00105 ±0.00024; Betfair Exchange +0.00130 ±0.00046 — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv).
- OA, early sharp vs late soft: Friday Pinnacle is worse than the closing market average by +0.00104 ±0.00022 RPS, and worse than closing Bet365 by +0.00089 ±0.00025 — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv).
- OA, sign changes: the Friday Pinnacle favourite differs from the closing favourite in 3.81% of SP1 matches and 7.62% of SP2 matches (5.63% all leagues). When they disagree, the closing sign wins more often: SP1 42.1% vs 29.7% (n=195); SP2 39.3% vs 35.3% (n=468) — [OA](https://www.football-data.co.uk/mmz4281/2425/SP2.csv).
- OA, Over/Under 2.5, Pinnacle pre vs closing: LL +0.0025 ±0.0005, Brier +0.0012 ±0.0003 (N=46,301) — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv).
- Real-time odds (Odds-API.com) on 1,120 EPL games, 2022/23–2024/25: predictive power improves gradually towards kickoff. "Most of the useful information is available by a day or two before a game", but new information is still absorbed in the final hour — [Whelan, UCD lecture notes, Spring 2026](https://www.karlwhelan.com/Teaching/BettingMarkets/10.EfficienciesandFavourite-LongshotBias.pdf).
- Bookmakers adjust quickly to news such as injuries to star players (evidence cited from Australian rules football) and in-game events. When home advantage halved during COVID ghost games, Asian handicap lines priced the change "pretty much perfectly" once enough data existed (Hegarty & Whelan) — [Whelan, UCD lecture notes](https://www.karlwhelan.com/Teaching/BettingMarkets/10.EfficienciesandFavourite-LongshotBias.pdf).
- Bookmaker forecasts became increasingly effective over a 5-year period of intensifying competition (~10,000 English games) — [Forrest, Goddard & Simmons 2005, IJF](https://doi.org/10.1016/j.ijforecast.2005.03.003).
- Anomaly: in 2025/26 (only matches up to Pinnacle's removal, N=2,831), PS→PSC improved by just +0.00034 ±0.00070. Every alternative closing source scored better than PSC (AvgC −0.00044 ±0.00057, BFEC −0.00056 ±0.00060, bwin −0.00050, Betfred −0.00051; each n.s.) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv).

### Inferences
- For this system, timing dominates source choice. Odds taken Saturday morning for Sunday/Monday games should lose part of the ~0.0009–0.0024 RPS (Spain, Sunday/Monday) that separates Friday odds from the close. How much is recovered by Saturday morning cannot be measured with football-data, which has only two snapshots.
- In correct signs, Friday→closing is worth about +0.25pp hit rate overall (+0.47pp SP1, +0.30pp SP2), i.e. about +0.07 correct signs per 14-match coupon (see section 6).
- The 2025/26 anomaly suggests football-data's last half-season of "Pinnacle closing" may not have been a true closing snapshot, or it is chance. Either way, 2025/26 PSC is a weak gold standard.
- Late information (team news, lineups, market money) is the plausible driver: the gain grows with lead time and appears for every source. Football-specific measurement of lineup effects is missing (see Gaps).

### Gaps
- I found no rigorous football study isolating the effect of official lineup announcements or injury news on pre-match 1X2 accuracy. Searches returned only practitioner/promotional pages.
- There are no intermediate time-stamped odds in football-data (Friday vs close only), so the Saturday-morning point on the curve is unknown.
- Pinnacle's own closing-line articles could not be retrieved.

## 3. De-vigging: which method is most accurate for 3-way football markets, does it differ for low- vs high-margin books, and what about favourite–longshot and draw biases (incl. Spain)?

### Takeaway
For football 1X2, power ≈ additive > Shin ≈ odds-ratio > multiplicative. The gain over multiplicative is negligible for Pinnacle and exchange odds (≈0.00005 RPS) but meaningful for high-margin books and averages (0.00011–0.00029 RPS). Power marginally beats Shin. Multiplicative leaves a classic favourite–longshot bias, which power largely removes. However, power slightly under-predicts draws (by ~0.3pp overall and 0.6–0.8pp in second tiers), and La Liga (and Serie A) favourites remain slightly underpriced.

### Cited Findings
- OA, gain over multiplicative, RPS (all leagues, 12/13–25/26; LL in parentheses) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - Pinnacle closing (N=98,353): additive/power −0.00005 ±0.00002; Shin −0.00004 ±0.00002; odds-ratio −0.00004 ±0.00001 (LL −0.0002 for each).
  - Market average closing (N=50,999): power −0.00017 ±0.00007 (LL −0.0007 ±0.0003); additive −0.00017; Shin −0.00014 ±0.00005; odds-ratio −0.00013 ±0.00004.
  - Retail books, power: Bet365 closing −0.00014 ±0.00007; bwin closing −0.00021 ±0.00007; William Hill −0.00020 ±0.00006; Interwetten closing −0.00026 ±0.00009; Betfred closing −0.00029 ±0.00021.
  - Max odds and exchange closing: −0.00001 to −0.00002, i.e. irrelevant when booksum ≈ 1.
  - Spain (SP1+SP2): market average closing power −0.00024 ±0.00018; bwin closing −0.00028 ±0.00021; Pinnacle closing −0.00007 ±0.00007.
- OA, Shin vs power directly (2019/20–2025/26): Pinnacle closing +0.00001 ±0.00001; Bet365 closing +0.00002 ±0.00002; market average closing +0.00003 ±0.00002, i.e. power marginally better. Odds-ratio vs power: +0.00002 to +0.00004 — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv).
- OA, illiquid exchange quotes are an exception. For Friday Betfair Exchange odds (wide spreads), power is not better on LL (+0.0008 ±0.0009 vs mult) while Shin is neutral (LL +0.0000 ±0.0004). In SP1+SP2, Friday BFE improves with power (−0.00051 ±0.00035 RPS) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv).
- OA, favourite–longshot bias, observed minus implied by implied-probability bin (all outcomes stacked, 2019/20–2025/26) — [OA](https://www.football-data.co.uk/mmz4281/2425/E0.csv):
  - PSC|mult: −1.7pp below 0.10, +2.7pp at 0.6–0.7, +3.3pp at 0.7–0.8.
  - PSC|power: −0.8pp, +1.1pp and +1.7pp in the same bins.
  - B365C|mult: −2.1pp, +3.5pp and +3.3pp; B365C|power: −0.6pp, +0.7pp and +0.4pp.
- OA, calibration slope of logit(outcome) on logit(implied), 12/13–25/26, with 95% cluster-bootstrap CIs; slope > 1 means favourites are underpriced — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv):
  - All leagues: PSC|mult 1.056 [1.038, 1.074]; PSC|power 1.015 [0.999, 1.029].
  - SP1: PSC|mult 1.067 [1.006, 1.133]; PSC|power 1.028 [0.967, 1.085].
  - SP2: PSC|power 1.042 [0.964, 1.142].
  - Others: Serie A PSC|power 1.075 [1.014, 1.131]; EPL 1.013 [0.955, 1.064]; Bundesliga 0.939 [0.878, 1.009].
- OA, Spain favourites: SP1 matches whose Pinnacle-closing favourite had implied 65–75% won 74.1% vs 69.5% implied, +4.6pp ±3.5 (n=607). Other SP1 bands were n.s. — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv).
- OA, draws (observed − implied p(D), 12/13–25/26) — [OA](https://www.football-data.co.uk/mmz4281/2425/SP2.csv):
  - All leagues: observed 26.50%. PSC|mult +0.08 ±0.27pp; PSC|power +0.34 ±0.27; Shin +0.23; odds-ratio +0.25; Avg|power +0.59 ±0.26; B365C|mult +0.31 ±0.38; B365C|power +0.89 ±0.38.
  - Second tiers: observed 29.24%. PSC|mult +0.60 ±0.52; PSC|power +0.76 ±0.52; Avg|power +1.20 ±0.51.
  - SP1: observed 25.45%. PSC|power +0.37 ±1.13.
  - SP2: observed 30.12%. PSC|mult +0.46 ±1.09; PSC|power +0.60 ±1.09; Avg|power +1.02 ±1.06.
  - By bin (all leagues): when PSC p(D) is 0.31–0.34, draws occur 33.6% vs 32.1% implied (+1.5 ±1.0pp); below 0.18, −0.6 ±0.8pp.
- The power method never yields probabilities outside 0–1 and allows for favourite–longshot bias. On three large bookmaker datasets from different sports it "universally outperforms the multiplicative method and outperforms or is comparable to the Shin method". Shin and additive are equivalent for two outcomes — [Clarke, Kovalchik & Ingram 2017, Am. J. Sports Science 5(6)](https://doi.org/10.11648/j.ajss.20170506.12).
- Basic normalisation produces biased probabilities. Differences between BN, regression and Shin probabilities can be large enough to change conclusions — [Štrumbelj, J. Sports Economics](https://doi.org/10.1177/1527002513519329). Štrumbelj (2014) is cited as finding that Shin improves on basic normalisation in RPS — [secondary: Egidi, Pauli & Torelli, arXiv 1802.08848](https://arxiv.org/pdf/1802.08848); [Štrumbelj 2014 DOI](https://doi.org/10.1016/j.ijforecast.2014.02.008).
- Shin is unbiased for the EPL but La Liga favourites win more often than either normalisation or Shin implies — [Koning & Zijm 2022](https://doi.org/10.1007/s10479-022-04722-3).
- Method catalogue in the R `implied` package:
  - Methods: basic, `wpo` (margin weights proportional to odds, from Buchdahl's "Wisdom of the Crowd" document), `or` (Cheung), `power` (which Buchdahl's document calls "logarithmic"), `additive`, `bb`, `shin` and `jsd`.
  - The basic method "tend[s] to be the least accurate", stated without evidence, and additive can give negative probabilities.
  - Source: [implied vignette](https://rdrr.io/cran/implied/f/vignettes/introduction.Rmd).
- Other packages: the Python `shin` package implements Shin's method ([GitHub mberk/shin](https://www.github.com/mberk/shin)). The penaltyblog docs only state that "several algorithms, including Shin's method" are provided ([penaltyblog implied docs](https://penaltyblog.readthedocs.io/en/latest/implied/index.html)).
- Favourite–longshot bias in UK fixed-odds football betting, for results and correct scores — [Cain, Law & Peel 2000, SJPE](https://doi.org/10.1111/1467-9485.00151). It persists in modern online fixed-odds markets and is explained by bettor disagreement plus bookmaker risk aversion — [Whelan, Economica](https://doi.org/10.1111/ecca.12500).
- On 453,765 soccer bets (2005–2025, football-data), average payouts fall with odds, and normalised probabilities overestimate longshots and underestimate favourites — [Whelan, UCD lecture notes 2026](https://www.karlwhelan.com/Teaching/BettingMarkets/10.EfficienciesandFavourite-LongshotBias.pdf).
- New (April 2026, not peer reviewed): on 90,014 football matches from 5 bookmakers, a new odds-only method beat multiplicative/Shin/power for most (not all) bookmakers. A GLM with a single favourite–longshot parameter beat multinomial and logistic GLMs — [Goto, Takeishi & Yairi, arXiv 2604.17194](https://arxiv.org/abs/2604.17194).

### Inferences
- The user's choice of power is supported. For Pinnacle it barely matters; for the consensus/average fallback it matters about 3× more than the Pinnacle-vs-average gap itself.
- Additive is practically tied with power in 3-way football (odds ≥ ~1.1), but can go negative on extreme longshots.
- Draw and favourite residual biases are small but systematic:
  - Power under-predicts draws, especially in second tiers (p ≈ 0.05 pooled) and in high-p(D) matches.
  - La Liga and Serie A strong favourites look slightly underpriced even after power.
  - A post-hoc calibration layer (e.g., a draw intercept per division, or a single favourite–longshot slope fitted walk-forward) is the evidence-consistent fix. Expected gains are of the order of 0.00002–0.00010 RPS (inference from the bin sizes, not tested).

### Gaps
- No public, peer-reviewed head-to-head of all methods (power, Shin, odds-ratio, wpo, jsd) on football 1X2 with confidence intervals was found; OA fills this for football-data books.
- Clarke et al. do not name the sports in the abstract.
- I did not test the `jsd`, `bb` or Goto et al. methods.

## 4. Without Pinnacle in football-data 2026/27, what is the best proxy for training/backtesting and live use, how big is the gap vs Pinnacle, and what are the risks of mixing sources?

### Takeaway
football-data's Pinnacle columns stop in early-to-mid January 2026: the last rows with Pinnacle odds are 12 Jan 2026 in SP1/SP2. The 2026/27 files contain no Pinnacle 1X2, O/U or AH columns. The best like-for-like proxy with long history is the power-devigged market average (Avg/AvgC). It is statistically indistinguishable from Pinnacle (≈ +0.00004 RPS pooled; +0.00008 to +0.00013 in Spain, n.s.), and its O/U 2.5 equivalent is also near-identical. Mixing sources shifts probabilities far less (mean absolute difference ~1.4–1.7pp) than mixing timings (~6pp). The bigger risks are changes in what football-data's Avg/Max actually contain, and the illiquidity of exchange prices days before kickoff.

### Cited Findings
- OA, 2026/27 headers (SP1, SP2, E0): no PSH/PSCH, P>2.5/PC>2.5 or PAHH/PCAHH. 1X2 odds, pre-closing and closing, are present for B365, BFD, BV, BW, PP, SKB, Max, Avg and BFE. O/U 2.5 and Asian handicap odds are present only for B365, Max, Avg and BFE. New HxG/AxG columns were added — [SP1 2026/27 CSV](https://www.football-data.co.uk/mmz4281/2627/SP1.csv); [SP2 2026/27 CSV](https://www.football-data.co.uk/mmz4281/2627/SP2.csv); [notes.txt](https://www.football-data.co.uk/notes.txt).
- OA, last 2025/26 Pinnacle rows: SP1 12 Jan 2026 (189 of 380 matches); SP2 12 Jan 2026 (196/462); EPL 8 Jan; Bundesliga 15 Jan; Serie A 15 Jan; Ligue 1 4 Jan — [SP1 2025/26 CSV](https://www.football-data.co.uk/mmz4281/2526/SP1.csv).
- OA, history coverage in Spain: Avg/Max, Bet365 and bwin have ~100% coverage from 2012/13 (as Betbrain averages before 2019/20). Closing averages run from 2019/20, Betfair Exchange from 2024/25 and 1xBet only in 2024/25 — [OA](https://www.football-data.co.uk/mmz4281/2425/SP1.csv).
- OA, proxy accuracy (power), all leagues 2019/20–2025/26 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - Pre-closing vs PS: Avg +0.00004 ±0.00004; Max +0.00008 ±0.00005; the 6 books present in 2026/27 ("Cons26") +0.00009 ±0.00006; BFE+Avg geometric blend +0.00013 ±0.00018; BFE +0.00035 ±0.00029.
  - Closing vs PSC: AvgC +0.00004 ±0.00006; MaxC +0.00010 ±0.00007; Cons26C +0.00009 ±0.00008; BFEC −0.00006 ±0.00020; BFEC+AvgC −0.00010 ±0.00018.
  - Over 2012/13–2025/26, Avg vs PS: +0.00006 ±0.00003 (N=97,556).
- OA, 2025/26 only (closest to the 2026/27 book mix, N≈2,835 pre): Avg +0.00006 ±0.00026; Cons26 +0.00000 ±0.00026; Betfred −0.00011 ±0.00031; Bet365 +0.00016 ±0.00031; BFE +0.00029 ±0.00047 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv).
- OA, Over/Under 2.5 proxies (2019/20–2025/26) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - Closing vs Pinnacle closing: market average LL +0.0002 ±0.0002; Bet365 +0.0001 ±0.0002; Betfair Exchange +0.0004 ±0.0006.
  - Pre-closing market average vs Pinnacle pre-closing: +0.0001 ±0.0001.
  - SP1+SP2: market average closing +0.0001 ±0.0004.
- OA, football-data's market average changed composition. Its booksum rose from 1.048 (SP1, 2019–26 average) to 1.065 in 2025/26 and 2026/27, and from 1.073 to 1.091 (SP2). The closing maximum moved from 0.997 to 1.024 (SP1) and 1.010 to 1.043 (SP2), i.e. fewer sharp books in Max — [OA](https://www.football-data.co.uk/mmz4281/2627/SP1.csv).
- OA, distribution shift vs Pinnacle (mean p_proxy − p_Pinnacle in pp for H/D/A; MAD = mean of the summed absolute differences), all leagues 2019/20–2025/26 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - Market average closing vs PSC: +0.05/−0.26/+0.21, MAD 1.64.
  - Betfair Exchange closing: −0.15/+0.28/−0.13, MAD 2.05.
  - BFEC+AvgC blend: −0.03/−0.01/+0.05, MAD 1.73.
  - Bet365 closing (power): +0.32/−0.54/+0.22, MAD 2.75.
  - Friday vs closing Pinnacle: +0.11/−0.21/+0.11, MAD 6.00 (95th percentile 14.9).
  - Spain: market average closing dD −0.41pp; Bet365 closing dD −0.78pp; Friday vs closing Pinnacle MAD 6.27.
- OA, 2026/27 to date (no Pinnacle; SP1+SP2 N=220, all leagues N=1,868) — [SP1 2026/27](https://www.football-data.co.uk/mmz4281/2627/SP1.csv):
  - Closing all-league RPS: Cons26C 0.20473, MaxC 0.20474, BFEC 0.20475, AvgC 0.20479, B365C 0.20506.
  - Pre-closing: Avg 0.20563, Bet365 0.20592, BFE 0.20678. The exchange is again weakest before the close.
- Individual books do not fully use competitors' information, which favours aggregation — [Elaad, Reade & Singleton 2020](https://doi.org/10.1016/j.frl.2019.09.006). Bookmaker-consensus forecasting de-vigs each book and averages on the log-odds scale — [Leitner, Zeileis & Hornik 2010, IJF](https://doi.org/10.1016/j.ijforecast.2009.10.001); method description at [Zeileis et al.](https://eeecon.uibk.ac.at/~zeileis/news/fifawomen2023/).
- Asian handicap odds can be converted into efficient 1X2-type forecasts — [Hegarty & Whelan 2025](https://ideas.repec.org/p/cpr/ceprdp/17949.html). football-data 2026/27 still carries AH lines (Avg/Max/B365/BFE, incl. closing) — [SP1 2026/27 CSV](https://www.football-data.co.uk/mmz4281/2627/SP1.csv).
- The Kaunitz et al. strategy treated bookmakers' own consensus odds as the probability estimate and was profitable in a 10-year closing-odds simulation, a 6-month minute-by-minute simulation and 5 months of real-money betting. The authors also report bookmaker discrimination against winning clients — [Kaunitz, Zhong & Kreiner 2017, arXiv 1710.02824](https://arxiv.org/abs/1710.02824).

### Inferences
- For training/backtesting history, use the power-devigged Avg (pre-closing) as the market baseline for the whole history (2012/13–present). This gives one consistent series with no structural break in January 2026, and it is the least-shifted proxy (MAD ~1.4–1.6pp). Pinnacle can be kept as a secondary feature where it exists.
- Avoid Max odds as baseline: slightly worse, and its composition changed sharply. Avoid single retail books: worse, and their draw probabilities after power are about 0.5–0.8pp lower.
- Betfair Exchange is an excellent closing proxy but a poor early one (Friday SP2 booksum ~1.05). A geometric BFE+Avg blend removes most of the exchange's mean bias, but is only usable from 2024/25.
- Live use: the timing mismatch matters more than source mismatch. The live input (Saturday-morning odds) is later than football-data's Friday "pre-closing" and earlier than "closing", so the backtest built on Friday odds is conservative relative to live.
- If live Pinnacle is still used, blending it with the live market average costs nothing in accuracy (PS+Avg geometric vs PS: +0.00001 ±0.00002) and makes live inputs statistically closer to an Avg-based history.
- The new HxG/AxG columns are a possible model input, not an odds proxy.

### Gaps
- I found no published accuracy study of football-data's new 2025/26+ market-average composition (which books it includes), or of Asian-handicap-derived 1X2 probabilities vs Pinnacle on 2026/27 data. The Hegarty & Whelan method was not replicated here.
- Live-API odds (Saturday morning) could not be evaluated against football-data history.

## 5. Can models (Elo, xG, Dixon–Coles, ML) beat closing sharp odds in football, and which market–model combinations help?

### Takeaway
No credible evidence shows public-data models beating closing sharp 1X2 odds on accuracy. Bookmaker odds beat every entry in the 2017 Soccer Prediction Challenge (RPS 0.2020 vs the winner's 0.2063), beat Elo in every large comparison, and Elo adds ~0 information on top of odds. The documented "wins" are betting-profit results that exploit mispricing, best-odds shopping, specific markets or decorrelation, not better probabilities. Gains from combining models with markets, where shown, are small. This is consistent with the user's −0.00010 RPS (CI crossing 0) from half-strength departures.

### Cited Findings
- 2017 Soccer Prediction Challenge (206-match test set; training data of over 200,000 matches). Table 1.2 of the survey reports — [Bunker, Yeung & Fujii 2024, arXiv 2403.07669](https://arxiv.org/pdf/2403.07669):
  - Bookmaker odds: RPS 0.2020, accuracy 0.5194.
  - Elo ordered logit (post-challenge): 0.2035.
  - XGBoost + Berrar ratings (post-challenge): 0.2054.
  - Winner, XGBoost + pi-ratings: 0.2063, accuracy 0.5243.
  - Constantinou's hybrid Bayesian network: 0.2083.
  - k-NN + pi-ratings: 0.2149.
  - The survey states bookmaker predictions "outperformed the top-performing submissions" and that odds "have proven difficult to beat". It notes that Baboota & Kaur's tuned gradient boosting could not beat odds-based predictions.
  - Razali et al.'s CatBoost + pi-ratings is reported at RPS 0.1925 on the Open International Soccer Database; whether it is comparable with the challenge test set is unclear.
  - Challenge papers: [Hubáček, Šourek & Železný 2019, Machine Learning 108](https://doi.org/10.1007/s10994-018-5704-6) (also questions the monotonicity assumption behind RPS; [abstract](https://mlanthology.org/mlj/2019/hubacek2019mlj-learning)); [Dubitzky et al. 2019](https://doi.org/10.1007/s10994-018-5726-0); [Berrar, Lopes & Dubitzky 2019](https://doi.org/10.1007/s10994-018-5747-8).
- On ~10,000 English games, bootstrapped statistical models with many variables failed to beat the odds-setters — [Forrest, Goddard & Simmons 2005](https://doi.org/10.1016/j.ijforecast.2005.03.003).
- Elo-based ordered-logit predictions were significantly worse than bookmaker-odds benchmarks — [Hvattum & Arntzen 2010, IJF 26(3), DOI 10.1016/j.ijforecast.2009.10.002 (via review)](https://graham-kendall.com/blog/?p=611).
- About 15,000 matches 2007/08–2016/17 (EPL, Bundesliga, Spanish Primera, Serie A plus European cups; results from football-data; odds averaged across bookmakers and basic-normalised): betting odds had the best predictive quality. An odds-based Elo ("ELO-Odds") was significantly worse than the odds but better than goal-based Elo — [Wunderlich & Memmert 2018, PLoS ONE 13(6)](https://doi.org/10.1371/journal.pone.0198668).
- 151,254 matches in 11 European countries incl. Spain: regressing outcome on Elo gives R² 0.0911, on normalised average-odds probabilities R² 0.1213. Adding Elo to odds raises R² by only 0.0003 — [Whelan, UCD lecture notes 2026](https://www.karlwhelan.com/Teaching/BettingMarkets/10.EfficienciesandFavourite-LongshotBias.pdf).
- Betting returns are not a valid measure of forecast accuracy; profitability and accuracy must be assessed separately — [Wunderlich & Memmert 2020, IJF 36(2)](https://ideas.repec.org/a/eee/intfor/v36y2020i2p713-722.html) (as described by [arXiv 2306.01740](https://arxiv.org/pdf/2306.01740) and [Wunderlich's dissertation](https://fis-db.dshs-koeln.de/ws/portalfiles/portal/6465170/Dissertation_Wunderlich.pdf)).
- Systematic profits are possible with an inferior price-predicting model if it is trained to be decorrelated from the market — [Hubáček & Šír 2023, IJF 39(2)](https://doi.org/10.1016/j.ijforecast.2022.02.001).
- Combining historical data and odds: a hierarchical Bayesian Poisson model whose scoring rates are convex combinations of history-based parameters and odds was applied to nine years of top European leagues to predict the tenth season — [Egidi, Pauli & Torelli 2018, Statistical Modelling](https://doi.org/10.1177/1471082x18798414). Combining forecasts improved accuracy in the Bundesliga — [Spann & Skiera 2009](https://ideas.repec.org/a/jof/jforec/v28y2009i1p55-72.html).
- Shots and corners beat goals as inputs: "GAP" ratings built on them gave about +0.8% profit per bet over 12 years in the O/U 2.5 market of 10 European leagues — [Wheatcroft 2020, IJF 36(3)](https://doi.org/10.1016/j.ijforecast.2019.11.001). Historical precedent: a Dixon–Coles Poisson model was profitable against 1995–96 English odds — [Dixon & Coles 1997](https://doi.org/10.1111/1467-9876.00065).
- Scoring rules: RPS is commonly recommended for football because it is "sensitive to distance" ([Constantinou & Fenton 2012, JQAS](https://doi.org/10.1515/1559-0410.1418)). Wheatcroft's simulations find the Ignorance (log) score outperforms both RPS and Brier — [Wheatcroft 2021, JQAS 17(4)](https://doi.org/10.1515/jqas-2019-0089).
- OA, combining sources: geometric blends add nothing measurable to Pinnacle — PSC+AvgC +0.00000 ±0.00003, PSC+BFEC −0.00006 ±0.00010, PS+Avg +0.00001 ±0.00002 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv).

### Inferences
- The user's −0.00010 RPS (95% CI −0.00022…+0.00001) is at the top of what the literature would lead one to expect from public-data models on top of sharp odds. Shrinking departures (half-weight) is the evidence-consistent design.
- Larger gains from new model features are unlikely, but improvement on the market's known residuals (draw underestimation, La Liga favourite bias, early-odds staleness) is plausible.
- Because RPS is criticised (Wheatcroft) and the user's goal is correct signs, model acceptance should also be judged on log-loss and on argmax hit rate (paired, block-bootstrapped by jornada). Changes that alter RPS without flipping signs do not change Quiniela hits.
- xG: football-data now includes HxG/AxG (2026/27), but I found no rigorous study showing xG-based 1X2 forecasts beating closing odds. Wheatcroft's O/U result suggests shot-based inputs can add information mainly in totals markets.

### Gaps
- The 2023 Soccer Prediction Challenge results (Yeung et al., Machine Learning 113, DOI 10.1007/s10994-024-06608-w) and Constantinou's Dolores paper could not be accessed for exact RPS figures.
- I found no peer-reviewed study testing xG models against Pinnacle closing 1X2 odds in La Liga/Segunda.

## 6. Implications for a 14-match pool: draw calibration, draw mispricing in Spanish leagues, and how many correct signs are realistic from market favourites?

### Takeaway
Picking the market favourite gives about 7.3 correct signs out of 14 on a coupon of 10 Primera + 4 Segunda matches (SD ≈1.9). Ten or more correct happens in ~12% of coupons, 12+ in ~1%, and 14/14 in ~0.01% (about 1 in 9,000). Draws are almost never the most likely outcome (0.4–0.6% of Primera matches, ~2.6% of Segunda). Markets slightly under-price draws, more so in Segunda and in tight, low-scoring matches. That is too little to make "X" the argmax in more than a handful of matches per season.

### Cited Findings
- OA, hit rate of the argmax, 2012/13–2025/26 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv):
  - Pinnacle closing: SP1 54.73% (mean p_max 54.04%); SP2 46.69% (mean p_max 46.27%).
  - Pinnacle Friday: SP1 54.23%; SP2 46.30%.
- OA, simulated 14-match coupons (10 SP1 + 4 SP2, 200,000 random draws from realised outcomes) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv):
  - Friday Pinnacle favourite: mean 7.27, SD 1.87. P(≥9)=25.6%, P(≥10)=11.5%, P(≥11)=3.9%, P(≥12)=0.92%, P(≥13)=0.15%, P(14)=0.011%.
  - Closing Pinnacle favourite: mean 7.34. P(≥10)=12.2%, P(≥12)=1.04%, P(14)=0.011%.
- OA, the draw as argmax (Pinnacle closing): 0.42% of matches overall, 0.55% in SP1, 2.56% in SP2 (Friday odds: 0.25% SP1, 1.19% SP2). Realised draw rates: SP1 25.45%, SP2 30.12% — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv).
- OA, draw under-pricing in Spain, observed minus implied — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv):
  - SP1: +0.37 ±1.13pp (PSC|power) and +0.10 (PSC|mult).
  - SP2: +0.60 ±1.09pp (PSC|power) and +1.02 ±1.06pp (Avg|power).
  - Second tiers pooled: +0.76 ±0.52pp (PSC|power), significant.
  - SP2 matches with PSC p(D) of 0.28–0.31: +1.5 ±1.8pp.
- OA, Spanish favourites priced at 65–75% won 4.6pp more often than implied (±3.5, n=607) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv). This is consistent with La Liga favourite bias in [Koning & Zijm 2022](https://doi.org/10.1007/s10479-022-04722-3).
- The highest-probability outcome is "almost always" a non-draw, and draws are hard to predict, which is why some studies drop or merge them — [Bunker, Yeung & Fujii 2024](https://arxiv.org/pdf/2403.07669).
- Football-pools (Quiniela) bettors forecast worse than bookmakers — [García, Pérez & Rodríguez 2016](https://mpra.ub.uni-muenchen.de/69687).
- OA, where sources disagree on the sign, the closing market is more often right. Friday vs closing Pinnacle in SP1: closing sign right 42.1% vs 29.7% (n=195). Market average closing vs PSC in SP2: PSC right 35.6% vs 26.4% (n=87) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv).

### Inferences
- To maximise expected correct signs, the optimal pick in each match is the argmax of the best probability estimate. Draw under-pricing of ~0.5–1.5pp only flips the argmax where p(D) is within ~1pp of the leading outcome: a few Segunda matches per season, essentially none in Primera.
- Departures from the market should be allowed to flip a sign only when they exceed the market's own uncertainty: a sign-flip rule tested on hit rate, not on RPS.
- The realistic ceiling is about 7.3–7.5 correct signs per coupon on average for league-only coupons. Model gains of ~0.0001 RPS translate into hundredths of a sign per coupon (inference from the RPS→hit-rate ratio seen in Friday→closing: −0.00095 RPS ≈ +0.25pp hit rate).
- Liga F, Copa del Rey and international matches are not in football-data. Their favourite hit rates and draw rates may differ (e.g., Copa ties with large quality gaps have more extreme favourites).

### Gaps
- No market-accuracy evidence was found for Liga F, Copa del Rey (incl. extra-time/penalties rules vs 90-minute 1X2 settlement) or international friendlies/qualifiers. Pleno al 15 exact-goal categories were not analysed beyond O/U 2.5.
- Within-jornada correlation of outcomes (weather, refereeing, calendar) is ignored in the coupon simulation.

## 7. Synthesis: concrete, evidence-backed recommendations for ORÁCULO 1X2 v3.2

### Takeaway
Timing is the largest controllable lever. Then use a consistent, power-devigged broad market average as the historical (and, blended with Pinnacle, live) baseline. Keep half-strength departures, add a small draw/favourite calibration layer, and judge changes on correct signs and log-loss as well as RPS. Expect about 7.3 correct signs per league-only coupon.

### Cited Findings
- Friday→closing: −0.00095 ±0.00015 RPS (all leagues), growing with lead time (Monday +0.0018), vs Pinnacle−Avg ≈ +0.00004 — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv); [Whelan 2026 notes](https://www.karlwhelan.com/Teaching/BettingMarkets/10.EfficienciesandFavourite-LongshotBias.pdf).
- The power-devigged average is ≈ Pinnacle (pre +0.00004 ±0.00004; closing +0.00004 ±0.00006), and its O/U 2.5 equivalent too (LL +0.0001 to +0.0002) — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv).
- Power beats multiplicative by 0.00011–0.00029 on averages and retail books, and marginally beats Shin — [OA](https://www.football-data.co.uk/mmz4281/2526/SP1.csv); [Clarke et al. 2017](https://doi.org/10.11648/j.ajss.20170506.12).
- Residual biases: draws under-predicted (second tiers +0.76 ±0.52pp) and La Liga favourites underpriced — [OA](https://www.football-data.co.uk/mmz4281/2526/SP2.csv); [Koning & Zijm 2022](https://doi.org/10.1007/s10479-022-04722-3); [Hegarty & Whelan 2025](https://ideas.repec.org/p/cpr/ceprdp/17949.html).
- Odds are hard to beat; combinations add little — [Bunker et al. 2024](https://arxiv.org/pdf/2403.07669); [Forrest et al. 2005](https://doi.org/10.1016/j.ijforecast.2005.03.003); [Wunderlich & Memmert 2018](https://doi.org/10.1371/journal.pone.0198668); [Spann & Skiera 2009](https://ideas.repec.org/a/jof/jforec/v28y2009i1p55-72.html).

### Inferences
1. Timing first.
   - Keep running as late as the Quiniela deadline allows.
   - In backtests, the market baseline should be football-data's pre-closing columns (PS / Avg, Friday or Tuesday), not closing ones, to match the live information set.
   - Report results by lead time (Fri/Sat/Sun/Mon), since the market's staleness grows with lead time.
   - Never train departure weights against closing-odds baselines and then apply them to early odds.
2. History baseline after Pinnacle's exit.
   - Rebuild the market series for 2012/13–2026/27 from power-devigged `Avg` (pre-closing; `BbAv` before 2019/20) as the primary baseline. Its accuracy loss vs Pinnacle is ≈ 0.00004–0.00006 RPS pooled (Spain ≈ 0.0001, n.s.).
   - Keep PS/PSC only as an auxiliary feature or diagnostic up to 12 Jan 2026.
   - Do not switch the baseline column mid-history (structural break). If Pinnacle is kept where available, add a source indicator so departures are learned per source.
3. Live baseline. Blend live Pinnacle (if the APIs still deliver it) with the live market average geometrically: no measurable accuracy cost (+0.00001 ±0.00002), and closer to the Avg-based history.
   - Without Pinnacle, use the de-vigged average of available books.
   - Use Betfair Exchange only when liquid (e.g., booksum ≤ ~1.02), never as the sole early source for Segunda.
   - Do not use Max odds or a single retail/Spanish-licensed book as baseline.
4. De-vig.
   - Keep power for averages and soft books; for Pinnacle and exchange the choice is immaterial. Prefer power over Shin.
   - Add a walk-forward calibration layer on top of the de-vigged market: a division-level draw intercept, especially Segunda, where power under-predicts draws by ~0.6–1.0pp, and a single favourite–longshot slope, especially Primera.
   - Validate it by log-loss and hit rate. Expected effect is small (≈ 10⁻⁴ RPS) — an inference, untested.
5. Over/Under for implied goals: replace Pinnacle O/U 2.5 with power-devigged `Avg>2.5/Avg<2.5`, which is near-identical (pre LL +0.0001 ±0.0001).
6. Model fusion.
   - Keep half-strength departures. The evidence says public-data models do not beat sharp closing odds on accuracy, and the measured edge (−0.00010) is at the plausible maximum.
   - Restrict sign flips (vs the market argmax) to cases where the model's shift clearly exceeds the market's noise, and test that rule on correct signs with a block bootstrap by jornada.
7. Candidate new market signals to test, not proven for 1X2: Asian-handicap-derived probabilities (Hegarty & Whelan show AH forecasts are efficient while 1X2 has favourite–longshot bias) using football-data's Avg/BFE AH columns. Also the new HxG/AxG columns as model features.
8. Expectations and evaluation.
   - Typical performance from market favourites is ~7.3 correct signs per 10+4 league coupon (P(≥10) ≈ 12%, P(14) ≈ 0.01%).
   - Track the system's hit rate against that baseline, and against the "closing-odds oracle" hit rate (+0.07 signs per coupon), which bounds what better timing alone could deliver.

### Gaps
- None of the recommendations was tested on the user's own pipeline or live API odds.
- The size of the calibration-layer gains and the value of Asian-handicap-derived 1X2 probabilities are untested.
- Liga F, Copa and international matches lack accuracy evidence.
