# La Quiniela (SELAE) 2026/27: official data, rules, public pick percentages ("porcentajes"), mirrors, historical data, and how ORÁCULO 1X2 can use them

Research date: 27 October 2026. Scope: Quiniela-specific sources only (bookmaker odds and football statistics are covered elsewhere). Notation: "[unverified]" = could not be confirmed against a primary document in this session; "[via search snippet]" = the text came from the search engine's extraction of an official PDF/page that returned HTTP 403 to direct fetches from this research environment (see Q1). "Own test" = HTTP probe run by this researcher from a cloud/datacenter IP on 27 Oct 2026.

## Q1. What official data does SELAE / loteriasyapuestas.es publish for La Quiniela, in what form, and is datacenter/cloud traffic blocked?

### Takeaway
SELAE publishes everything the system needs: the jornada list and order (results / "comprobar" pages), per-jornada sales-closing notices, suspension and substitution notices, results, escrutinio and prizes per category, recaudación and bote (press-release PDFs), Elige 8 results, season calendars, the normas, and official "porcentajes de signos pronosticados" (statistics PDFs). It all comes as HTML pages, PDFs, an embeddable results widget and an RSS variant of the escrutinio pages; the JSON endpoints under `/servicios/` are undocumented. The whole domain sits behind an Akamai-style WAF. In own tests on 27 Oct 2026, every SELAE URL tried (HTML, `/servicios/` JSON, widget, RSS, PDF) returned **HTTP 403 "Access Denied"** from a datacenter IP, while the main mirror sites returned 200.

### Cited Findings
**Pages and URL patterns (official)**
- Per-jornada results pages follow the pattern `/es/la-quiniela/resultados/la-quiniela-resultados-del-DD-de-MES-de-AAAA`. For 2026/27 they exist in es/en/gl/ca/va, e.g. 30 Aug 2026 and 13 Sep 2026. — [SELAE results 13-sep-2026](https://www.loteriasyapuestas.es/es/la-quiniela/resultados/la-quiniela-resultados-del-13-de-septiembre-de-2026); [SELAE results 30-ago-2026 (en)](https://www.loteriasyapuestas.es/en/la-quiniela/resultados/la-quiniela-resultados-del-30-de-agosto-de-2026)
- Escrutinio ("premios y ganadores") pages follow `/es/la-quiniela/escrutinios/la-quiniela-premios-y-ganadores-del-DD-de-MES-de-AAAA`. An **RSS variant** exists by appending `.formatoRSS`. — [SELAE escrutinio 21-oct-2026](https://www.loteriasyapuestas.es/es/la-quiniela/escrutinios/la-quiniela-premios-y-ganadores-del-21-de-octubre-de-2026); [SELAE escrutinio RSS example (10-ago-2025)](https://www.loteriasyapuestas.es/es/la-quiniela/escrutinios/la-quiniela-premios-y-ganadores-del-10-de-agosto-de-2025.formatoRSS)
- Official embeddable results widget: SELAE's "últimos sorteos" page tells third-party sites to call `/f/loterias/resultados/quiniela.html?game_id=LAQU&fecha_sorteo=aaaammdd`, where game_id is the game (LAQU = La Quiniela) and fecha_sorteo is the draw date. — [SELAE resultados-últimos-sorteos](https://www.loteriasyapuestas.es/es/resultados-ultimos-sorteos)
- A "comprobar" page shows the current boleto. It lists Liga F fixtures with an "(F)" suffix, e.g. "Logroño (F) - Badalona W. (F)" and "Real Madrid (F) - Tenerife (F)" [via search snippet]. — [SELAE comprobar](https://www.loteriasyapuestas.es/es/resultados/quiniela/comprobar)
- **Press releases ("Notas de prensa") per jornada (PDF)** carry the winning combination, winners and prize per category, Elige 8 results and the bote announcement:
  - J12 (11 Oct 2026): combination X-2-1-X-1-1-X-X-1-1-1-1-2-1; 32 tickets with 14 at 17,500.75 €; no Pleno al 15 winner, so a BOTE; 1,623 Elige 8 winners. — [NP 11_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_11_10_26.pdf)
  - J13 (Wed 14 Oct 2026): combination 1-1-1-2-2-X-1-2-1-1-2-X-2-X; no winners of Pleno al 15 or of 14. — [NP 14_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_14_10_26.pdf)
  - J15 (Wed 21 Oct 2026): 4 tickets with 14 at 45,666.15 €; Pleno al 15 rolled over; 10 hits paid 0 €. The next draw (25 Oct) was announced as "un único acertante de Catorce Aciertos con Pleno al 15 podría ganar 2.500.000,00 euros". The note misprints its own date as "21 de septiembre". — [NP 21_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_21_10_26.pdf)
  - Escrutinio for J14 (18 Oct 2026): Pleno al 15 had 18 winners at ≈80,778 €; 50 winners with 14 at ≈11,162 €. — [SELAE escrutinio 18-oct-2026](https://www.loteriasyapuestas.es/es/la-quiniela/escrutinios/la-quiniela-premios-y-ganadores-del-18-de-octubre-de-2026)
  - Elige 8 on 9 Sep 2026: 9,284 winning bets with 8 hits. — [NP 9_09_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_9_09_26.pdf)
- **"Avisos de interés"** (HTML index plus PDFs) holds per-jornada **sales-closing notices** ("Horario de venta / Aviso cierre"), e.g. J4 (5–6 Sep 2026) and J72 of 2025/26 (11–12 Jul 2026). It also holds **suspension notices**, e.g. J7 (16 Sep 2026), and Rayo Vallecano–Athletic Club in J12 2026/27, suspended at 0-0 after objects were thrown, so match 1's sign was X. — [Avisos de interés](https://www.loteriasyapuestas.es/es/avisos-de-interes); [Aviso cierre J4 2026/27](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/Aviso%20cierre%20La%20Quiniela%20jornada%20%204%C2%AA%20y%20El%20QuiniGol%20jornada%20%204%C2%AA%20de%205%20-%206%20de%20Septiembre%20de%202026.pdf); [Aviso cierre J72](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/Aviso%20cierre%20La%20Quiniela%20jornada%2072%C2%AA%20y%20El%20QuiniGol%20jornada%2084%C2%AA%20de%2011%20-%2012%20de%20Julio%20de%202026.pdf); [Suspensión J7 16-sep-2026](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/SUSPENSION%20PARTIDO%20JORNADA%207%C2%AA%20DE%20LA%20QUINIELA%2016%20DE%20SEPTIEMBRE%202026.pdf); [Suspensión Rayo–Athletic J12](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/SUSPENSION%20RAYO%20VALLECANO-ATHLETIC%20CLUB%20QUINIELA%20JORNADA%2012%20TDA%2026-27.pdf)
- **Season calendars (PDF).** The 2025/26 calendar has the columns "Número | Fecha | 1ª | 2ª | Otras | Posibles", i.e. how many Primera, Segunda and other matches each jornada is planned to contain. A summer-2026 calendar exists, and the Ayuda page lists "La Quiniela: Calendario temporada 2026-27". The provisional calendars warn that jornadas may consist wholly or partly of matches from competitions not normally included. — [Calendario 25-26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/CALENDARIO_Quiniela_Temp_25-26.pdf); [Calendario verano 2026](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/CALENDARIO_VERANO_QUINIELA_2026.pdf); [Ayuda / calendarios](https://www.loteriasyapuestas.es/es/centro-de-ayuda/centro-de-informacion-y-ayuda)
- **Normas and guides (PDF):** 2015-16 normas, 2019-20 normas, "Normas de la Quiniela y Elige8 Octubre 2019", the "Guía del Quinielista", a help PDF on condicionadas, and an official page on reducidas. — [Normas 19/20](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Normativa%20Quiniela/NORMAS_LA_QUINIELA_TEMPORADA_19_20.pdf); [Normas Quiniela y Elige8 Oct 2019](https://www.loteriasyapuestas.es/f/loterias/documentos/normativa/Normativa%20de%20los%20juegos/Normas_de_la_Quiniela_y_Elige8_Octubre_2019.pdf); [Guía del Quinielista](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/guia_del_quinielista.pdf); [Ayuda Condicionadas](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Ayuda%20Condicionadas.pdf); [Quinielas reducidas](https://www.loteriasyapuestas.es/es/paginas-informativas/quinielas-reducidas-maximiza-tus-posibilidades)
- **Official percentages of signs bet ("Estadísticas de pronósticos", PDF):** Quiniela files exist for 2014-15 ("TANTOS POR CIENTO DE LOS SIGNOS PRONOSTICADOS") and 2018-19 ("Pronos 1x2 Jda 59_18_19"). Quinigol files exist for 2025-26 and 2026-27; the 2026-27 J11 file is dated 30/09/2026 and counts bets up to 28-09-26. Details in Q3. — [Quiniela 2014-15](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Pronosticos_10_14-15%201x2%20S.pdf); [Quiniela 2018-19](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Temporada%202018_2019/Pronos%201x2%20Jda%20%2059_18_19.pdf); [Quinigol 2026-27 J11](https://www.loteriasyapuestas.es/f/loterias/documentos/El%20Quinigol/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Temporada%202026_2027/pronosQNG_11_26_27_L.pdf)
- Official online play exists at juegos.loteriasyapuestas.es. — [Jugar La Quiniela (SELAE)](https://juegos.loteriasyapuestas.es/jugar/la-quiniela/apuesta/?access=subhome&lang=es)
- SELAE also hosts older result pages, e.g. 30 Sep 2012. — [SELAE 2012 escrutinio](https://www.loteriasyapuestas.es/en/la-quiniela/resultados/la-quiniela-premios-y-ganadores-del-domingo-30-de-septiembre-de-2012)

**Blocking (own tests, 27 Oct 2026, datacenter IP, browser User-Agent)**
- HTTP/2 **403** with a 405–531-byte "Access Denied … You don't have permission to access … Reference #18.xxxx" page pointing to `https://errors.edgesuite.net/…`. This is Akamai's standard edge-error format [Akamai attribution is an inference from the edgesuite.net domain]. The 403 came back for all of these:
  - [/es/resultados/quiniela](https://www.loteriasyapuestas.es/es/resultados/quiniela)
  - [/servicios/proximosv3?game_id=LAQU&num=2](https://www.loteriasyapuestas.es/servicios/proximosv3?game_id=LAQU&num=2)
  - [/servicios/buscadorSorteos?game_id=LAQU&celebrados=true&fechaInicioInclusiva=20261001&fechaFinInclusiva=20261027](https://www.loteriasyapuestas.es/servicios/buscadorSorteos?game_id=LAQU&celebrados=true&fechaInicioInclusiva=20261001&fechaFinInclusiva=20261027)
  - [/es/la-quiniela](https://www.loteriasyapuestas.es/es/la-quiniela)
  - the [widget](https://www.loteriasyapuestas.es/f/loterias/resultados/quiniela.html?game_id=LAQU&fecha_sorteo=20261025)
  - the [.formatoRSS escrutinio](https://www.loteriasyapuestas.es/es/la-quiniela/escrutinios/la-quiniela-premios-y-ganadores-del-25-de-octubre-de-2026.formatoRSS)
  - a [suspension PDF](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/SUSPENSION%20PARTIDO%20JORNADA%207%C2%AA%20DE%20LA%20QUINIELA%2016%20DE%20SEPTIEMBRE%202026.pdf)
- From the same IP these returned 200: eduardolosilla.es, quinielafutbol.info, quiniela15.com, loterias1fuengirola.com (after redirect), pronosticosfiablesquiniela.es and lotoideas.com. resultados-futbol.com/quiniela returned 403 (9 bytes). — Own test; [eduardolosilla porcentajes](https://www.eduardolosilla.es/quiniela/ayudas/porcentajes); [quinielafutbol próximas](https://www.quinielafutbol.info/proximas-jornadas-de-la-quiniela.html); [resultados-futbol quiniela](https://www.resultados-futbol.com/quiniela)
- A web search for documentation of `/servicios/buscadorSorteos` or any JSON service found none. The only official integration documentation surfaced was the HTML widget instructions. — [SELAE resultados-últimos-sorteos](https://www.loteriasyapuestas.es/es/resultados-ultimos-sorteos)
- A readable copy of SELAE's normas (2017-18 edition) is hosted on the Ministry of Hacienda's site, which is not behind SELAE's WAF. — [Hacienda repository: Normas La Quiniela 2017-18](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf)
- A 2013-era open-source scraper, dmiro/betEScraper, exposed SELAE Quiniela/Primitiva data as JSON/XML/CSV through a REST layer. Its examples date from 2013. — [GitHub dmiro/betEScraper](https://github.com/dmiro/betEScraper)

### Inferences
- The block covers static PDFs and the widget, not just the JSON. It is therefore IP- or bot-reputation based, so changing endpoints won't help from Colab.
- Legitimate workarounds:
  1. Run the SELAE fetch from the user's own residential connection (home PC, Raspberry Pi or local Jupyter), at a low rate with a normal client, and push a JSON snapshot to Google Drive or GitHub for Colab to read.
  2. Keep mirrors as the primary source inside Colab and use SELAE as a post-hoc validator (e.g. compare the official combination and prizes when the home job runs).
  3. Read normas from the Hacienda copy.
- Evading the WAF with rotating residential proxies may breach SELAE's terms; not recommended.
- The press-release PDFs are the most information-dense official artefact: combination, winners per category, Elige 8, and the bote for the next jornada in one place. They are the best item to archive weekly.
- The per-jornada "Aviso cierre" PDF is the authoritative closing time. Mirrors give different times (see Q2/Q6).

### Gaps
- The JSON schemas of `/servicios/proximosv3` and `buscadorSorteos` couldn't be inspected (403), and no public documentation was found.
- No official SELAE statement about blocking cloud IPs, or any whitelist or API programme, was found.
- The official app and SELAE's social-media accounts were not researched (time budget).

## Q2. Rules for 2026/27 and how jornadas are composed (Primera, Segunda, Liga F, Copa, international); changes 2024–2026

### Takeaway
The core economics have been stable since at least the 2017-18 normas: 0.75 € per bet; 55% of gross takings to prizes, split 16% (14 hits) / 7.5% (13) / 7.5% (12) / 7.5% (11) / 9% (10), plus 7.5% for the Categoría Especial (14 + Pleno al 15). A cascade and minimum-prize rules apply, and SELAE chooses which later concurso receives a bote. Elige 8 costs 0.50 € and has its own 55% pool. A J16 2026/27 payout check confirms the 16% share is still applied. The big 2026/27 change is the permanent inclusion of Liga F: SELAE decides weekly how many matches, with at least one guaranteed and four in recent jornadas. It follows a Real Decreto approved by the Consejo de Ministros on 5 May 2026. The season also has frequent midweek jornadas (Copa del Rey) and summer/international jornadas.

### Cited Findings
**Price and prize pool (normas 2017-18, current numbering)**
- Norma 5ª: "El precio de cada apuesta queda fijado en 0,75 Euros". Norma 6ª: 55% of gross takings go to prizes, within art. 15 of Orden EHA/3081/2011 (BOE nº 277, 17 Nov 2011). Of this, 47.5% goes to the five ordinary categories and 7.5% to the Categoría Especial. — [Hacienda copy of SELAE normas 2017-18](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf)
- Norma 7ª: Primera (14 hits) 16%, Segunda (13) 7.5%, Tercera (12) 7.5%, Cuarta (11) 7.5%, Quinta (10) 9% of gross takings, each shared equally. The same table (with P15 at 7.5%) appears in SELAE's Guía del Quinielista. — [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf); [Guía del Quinielista](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/guia_del_quinielista.pdf)
- Cascade and minimum-prize rules (norma 7ª):
  - With no 14-hit winner, the Primera fund goes to the Especial "del concurso que designe SELAE".
  - With no winner in Segunda, its fund flows down to Tercera, then Cuarta, then Quinta, and finally to the Especial.
  - No lower category may pay more than a higher one; if one would, their funds are merged.
  - If a Cuarta, Tercera or Segunda prize would be under 1 €, it goes unpaid and its fund cascades upward.
  - If a Quinta (10-hit) prize would be under 1.50 €, it goes unpaid and the fund goes to the Especial of the concurso SELAE designates.
  - J15 2026/27 is an example: 10 hits paid 0 €. — [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf); [NP 21_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_21_10_26.pdf)
- Norma 8ª (Categoría Especial): 7.5% of gross takings is shared equally among bets that win Primera **and** get the exact goals of the Pleno al 15, which is not one of the 14 base matches. With no winner, the fund goes to the same category "del concurso que designe SELAE". — [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf)

**Pleno al 15**
- It can be predicted 16 ways: goals per team of 0, 1, 2 or M (3 or more). It is outside the combinatorics of the 14, and its sign only counts if the bet reaches Primera (14 hits) [via search snippet]. — [Guía del Quinielista](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/guia_del_quinielista.pdf); [SELAE cómo jugar](https://www.loteriasyapuestas.es/es/centro-de-ayuda/como-se-juega/como-jugar-a-la-quiniela)

**Elige 8**
- A 0.50 € add-on to a Quiniela bet played by the direct method. The player picks 8 of the 14 matches (P15 excluded), and their existing predictions are played. Doubles or triples among those 8 make it a multiple Elige 8 bet.
- Own fund: 55% of Elige 8 takings, shared equally among the bets with the **highest number of hits**. If nobody hits 8, 7-hit bets are paid, and so on. Probability of 8 hits with one simple bet: 1 in 6,561 [via search snippet]. — [SELAE cómo jugar](https://www.loteriasyapuestas.es/es/centro-de-ayuda/como-se-juega/como-jugar-a-la-quiniela); [Normas Quiniela y Elige8 Oct 2019](https://www.loteriasyapuestas.es/f/loterias/documentos/normativa/Normativa%20de%20los%20juegos/Normas_de_la_Quiniela_y_Elige8_Octubre_2019.pdf)
- Elige 8 does not appear in the 2017-18 normas text but does in the October 2019 normas. Inference: it was introduced around 2019 [unverified launch date]. — [Hacienda normas 2017-18](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf); [Normas Oct 2019](https://www.loteriasyapuestas.es/f/loterias/documentos/normativa/Normativa%20de%20los%20juegos/Normas_de_la_Quiniela_y_Elige8_Octubre_2019.pdf)

**Methods: simple, multiple, reducidas, condicionadas**
- The normas regulate simple, direct multiple (dobles/triples), Múltiple Reducido (norma 22ª) and Múltiple Condicionado (norma 23ª). Official reduction tables include:
  - 4 triples: 81 bets reduced to 9
  - 7 dobles: 128 reduced to 16
  - 8 triples: 6,561 reduced to 81
  - 11 dobles: 2,048 reduced to 132
  - others reduced to 24 and 64 bets
- In the condicionado method, the player sets conditions on a group of doubles and triples (worked examples: 6 dobles + 2 triples giving 232, 256 or 136 resulting bets). — [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf); [Ayuda Condicionadas](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Ayuda%20Condicionadas.pdf)

**Match validity, substitution, suspended and unplayed matches**
- Norma 37ª: a match's result is void if it starts before 12:00 of the day before the jornada date, or after 24:00 of the day after it (peninsular time). Older normas used 15:00; the exact edition was not verified, and it appears in the 1995–2009 BOE resolutions returned by search. — [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf); [BOE-A-2009-12204](https://www.boe.es/buscar/doc.php?id=BOE-A-2009-12204)
- Norma 38ª A:
  - If SELAE learns officially before 24:00 on the Thursday of the week before the jornada, it designates a substitute match and announces it.
  - Otherwise (B), uncomputed matches are decided by **draw**: 100 balls, red = 1, blue = X, yellow = 2. The number of balls of each colour equals the **percentages of signs bet by participants in the central system**, which SELAE publishes before the draw.
  - Rounding ties favour 1 over X/2 and X over 2.
  - For an uncomputed Pleno al 15, each team gets its own 100-ball drum (white = 0, red = 1, yellow = 2, green = M), weighted by the public's per-team goal percentages. — [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf)
  - Conflict: a search summary of the 2019-20 normas says the substitution trigger is official knowledge before 24:00 of the *previous day* (norma 39ª after renumbering) [via search snippet; unverified]. — [Normas 19/20](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Normativa%20Quiniela/NORMAS_LA_QUINIELA_TEMPORADA_19_20.pdf)
- The result that counts is the score when the referee ends the match, including extra time, or the score at suspension, even if sports bodies later annul it [via search snippet, 2019 normas]. Example: Rayo–Athletic, J12 2026/27, suspended at 0-0, gave X. — [Normas Oct 2019](https://www.loteriasyapuestas.es/f/loterias/documentos/normativa/Normativa%20de%20los%20juegos/Normas_de_la_Quiniela_y_Elige8_Octubre_2019.pdf); [Suspensión Rayo–Athletic](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/SUSPENSION%20RAYO%20VALLECANO-ATHLETIC%20CLUB%20QUINIELA%20JORNADA%2012%20TDA%2026-27.pdf)

**Closing time**
- Each jornada has its own official "Horario de venta / Aviso cierre" PDF; the J4 2026/27 notice gives closing hours of 14:00 and 16:15 [via search snippet]. Mirror sites state that sales close "poco antes del inicio del primer partido".
- For J17, quiniela15 states "Cierra el 27/10/2026 a las 20:00". eduardolosilla shows its own earlier internal cut-offs (18:30 for DNP peñas, 19:00 for individual players). — [Aviso cierre J4](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/Aviso%20cierre%20La%20Quiniela%20jornada%20%204%C2%AA%20y%20El%20QuiniGol%20jornada%20%204%C2%AA%20de%205%20-%206%20de%20Septiembre%20de%202026.pdf); [quinielafutbol próximas](https://www.quinielafutbol.info/proximas-jornadas-de-la-quiniela.html); [quiniela15](https://www.quiniela15.com/); [eduardolosilla](https://www.eduardolosilla.es/)

**Legal form of the rules**
- Until about 2009 the annual normas were published in the BOE (e.g. the 2003-04 and 2009-10 resolutions). The current SELAE normas say "Estas normas se publicarán en la página web de SELAE".
- A BOE search found no 2024–2026 resolution amending La Quiniela. Norma 1ª allows matches from "competiciones autorizadas por la Real Federación Española de Fútbol u otras instituciones de ámbito nacional o internacional". — [BOE-A-2003-15238](https://www.boe.es/buscar/doc.php?id=BOE-A-2003-15238); [BOE-A-2009-12204](https://www.boe.es/buscar/doc.php?id=BOE-A-2009-12204); [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf)

**Liga F (change in 2026/27)**
- Ara (24 Aug 2026): "Starting this week, the F League will be included in the Quiniela". Four Liga F matches were added: Athletic Club–Badalona, Eibar–Espanyol, Alavés–Valencia, Real Madrid–Atlético. — [Ara](https://en.ara.cat/sports/historic-step-in-the-f-league-the-quiniela-is-now-reality_25_5831066.html)
- Yogonet (27 Aug 2026): this is the first time Liga F enters La Quiniela, with four matches from Liga F's matchday 1 of 2026-27.
  - Legal basis: a Real Decreto approved by the Consejo de Ministros on 5 May.
  - SELAE "decide cada semana cuántos partidos de Liga F aparecen, con un mínimo de uno garantizado".
  - The men's league's share of the tax revenue falls from 45.50% to 30.50%, and Liga F gets 15%, estimated by El Mundo at up to ≈5 M€ a year. — [Yogonet](https://www.yogonet.com/latinoamerica/noticias/2026/08/27/110398-espana-la-liga-f-debuta-en-la-quiniela-y-recibira-el-15-de-la-recaudacion-de-las-apuestas)
- EFE via Infobae (16 Sep 2026): Liga F matches are in all jornadas this season, permanently ("un mecanismo permanente en nuestro marco normativo", minister of Hacienda Arcadi España).
  - Distribution of the Impuesto sobre Actividades de Juego from football mutual bets: 30.50% LNFP, 4.55% RFEF, 49.95% diputaciones (via the CCAA), 15% Liga Profesional de Fútbol Femenino.
  - Campaign "Ahora con el fútbol femenino", in La Quiniela's 80th-anniversary season. — [Infobae/EFE](https://www.infobae.com/espana/agencias/2026/09/16/los-partidos-de-la-liga-f-llegan-a-la-quiniela-para-siempre/)
- Liga F 2026-27 runs from 29 Aug 2026 to 23 May 2027 with 16 teams. — [Wikipedia 2026–27 Liga F](https://en.wikipedia.org/wiki/2026%E2%80%9327_Liga_F)

**Observed 2026/27 composition**
- J16 (Sun 25 Oct 2026): 7 LaLiga EA Sports, 3 LaLiga Hypermotion and 4 Liga F matches; Pleno al 15 Barcelona–Real Madrid (1-2); recaudación 3,380,010.75 €; 15 winners with 14. — [quinielafutbol.info](https://www.quinielafutbol.info/)
- J16 Liga F results as listed: Edf Logroño 1-0 Badalona Women, Deportivo (F) 2-1 Alavés Femenino, Eibar (F) 2-2 Madrid CFF, Real Madrid (F) 3-2 Tenerife (F). — [quiniela15](https://www.quiniela15.com/)
- J17 (nominal date Wed 28 Oct 2026; matches Tue 27 to Thu 29): Copa del Rey and Segunda matches, e.g. RSD Alcalá–Las Palmas (Tue 20:00) and At. Calatayud–Osasuna (Thu 19:00); Pleno al 15 Recreativo de Huelva–Rayo. — [eduardolosilla](https://www.eduardolosilla.es/); [quiniela15](https://www.quiniela15.com/); [quinielafutbol próximas](https://www.quinielafutbol.info/proximas-jornadas-de-la-quiniela.html)
- J18 (Sat 31 Oct to Mon 2 Nov 2026), 7 Primera + 3 Segunda + 4 Liga F:
  - Primera: Levante–At. Madrid, Rayo–Celta, Betis–Málaga, Barcelona–Alavés, Getafe–Sevilla, Racing–Real Madrid, Elche–Valencia
  - Segunda: Eibar–Almería, Eldense–Granada, Burgos–Castellón
  - Liga F: Alavés (F)–Real Sociedad (F), Madrid CFF (F)–Deportivo (F), Sevilla (F)–Real Madrid (F), Tenerife (F)–Athletic Club (F)
  - Pleno al 15: Athletic–Real Sociedad, 1 Nov 21:00. — [quinielafutbol próximas](https://www.quinielafutbol.info/proximas-jornadas-de-la-quiniela.html)
- Season structure: J1 of 2026/27 was 16 Aug 2026. The 2025/26 season ran to at least J74 (26 Jul 2026), through a summer-2026 calendar of international/World Cup-period jornadas. A dedicated Qatar 2022 World Cup Quiniela calendar also existed. — [NP 9_8_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_9_8_26.pdf); [NP 26_07_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_26_07_26.pdf); [Calendario verano 2026](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/CALENDARIO_VERANO_QUINIELA_2026.pdf); [Calendario Mundial 2022](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/CALENDARIO%20MUNDIAL_AD2022.pdf)
- 2026/27 midweek jornadas seen so far: Wed 9 Sep (J5 [unverified number]), Wed 16 Sep (J7), Wed 14 Oct (J13), Wed 21 Oct (J15), Wed 28 Oct (J17). — [NP 9_09_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_9_09_26.pdf); [Suspensión J7](https://www.loteriasyapuestas.es/f/loterias/web_corporativa/Comunicacion/Avisos_de_interes/SUSPENSION%20PARTIDO%20JORNADA%207%C2%AA%20DE%20LA%20QUINIELA%2016%20DE%20SEPTIEMBRE%202026.pdf); [NP 14_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_14_10_26.pdf); [NP 21_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_21_10_26.pdf)

### Inferences
- **The prize split is confirmed for 2026/27 by arithmetic.** For J16: 16% × 3,380,010.75 € / 15 winners = 36,053.45 €, exactly the published 14-hit prize (Fuengirola prize table, Q6). Also 3,380,010.75 / 0.75 = 4,506,681 bets, an integer, consistent with 0.75 €.
- Estimated volumes in Oct 2026: weekend jornadas ≈ 3.4–3.5 M€, ≈ 4.5–4.7 M bets. Midweek J15 ≈ 1.14 M€ (4 × 45,666.15 / 0.16), ≈ 1.5 M bets. These are derived from the 16% rule; small errors are possible from rounding.
- **The bote does not automatically roll to the next jornada.** It goes to "el concurso que designe SELAE". J16 had no Pleno al 15 winner, yet quinielafutbol.info and Fuengirola show "no bote" for the midweek J17. The likely explanation is that SELAE assigns rollovers to selected (often weekend) jornadas. The system should read the bote from each press release rather than assume it carries over.
- **Liga F must be modelled every jornada (≥1 match, 4 typical so far).** The count is set weekly by SELAE, so the system should parse the composition rather than hard-code 14 men's matches.
- Expect team-name variants such as "Badalona W." / "Badalona Women" / "Badalona (F)" and "Alavés Femenino" / "Alavés (F)". Team-by-team cross-checking needs a gender-aware alias table.
- **Suspended and unplayed matches:** a match suspended after kick-off keeps its score at suspension. A match not played inside the validity window is settled by a draw weighted by the public's percentages. For a match with postponement risk s, a calibrated sign distribution is (1 − s)·p_model + s·q_public (q = official % of signs). This is the one place where public percentages directly change the *hit-probability* of a sign.
- Midweek Copa jornadas pair lower-division home sides with top-flight teams. They have smaller pools (fewer bets), so 14-hit prizes vary a lot, from 4 winners at 45,666 € to 32 winners at 17,500 € in October 2026.

### Gaps
- The full 2026/27 normas PDF (if a new edition exists) could not be opened (403). The rules above come from the 2017-18 edition (Hacienda copy) plus 2019-20 search extracts and 2026 payout data.
- The number and BOE reference of the May 2026 Real Decreto were not found.
- The minimum number of bets per paper ticket and the maximum dobles/triples in direct multiples were not verified.
- The exact current substitution deadline (Thursday of the previous week vs. 24:00 of the previous day) conflicts between editions.
- The official 2026/27 calendar PDF (planned 1ª/2ª/Liga F/Otras per jornada) was not retrieved.

## Q3. Public pick percentages ("porcentajes"): does SELAE publish them, which sites republish them, methodology, timing, accuracy?

### Takeaway
Yes. SELAE computes the "tantos por ciento de los signos pronosticados" from its central system and publishes them **daily, at the close of each day's admission** (normas). It uses them to settle unplayed matches and puts them in "Estadísticas de pronósticos" PDFs. The only scrape-friendly republisher found is **eduardolosilla.es** (quinielista.es now 301-redirects there). It shows three series side by side: **% LAE** (official SELAE data, updated daily), **% Quinielista** (its own users' bets, hourly) and **% Real** (Betfair/bookmakers, hourly). The other sites in the user's pipeline (quinielafutbol.info, quiniela15, pronosticosfiablesquiniela, loterias1fuengirola) do not publish population percentages. No study of how close the last pre-close % LAE snapshot is to the final distribution was found.

### Cited Findings
- 2019-20 normas: "Diariamente, cuando se cierra la admisión de apuestas, Loterías publicará los tantos por ciento de los signos pronosticados por los participantes hasta ese momento" [via search snippet]. — [Normas 19/20](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Normativa%20Quiniela/NORMAS_LA_QUINIELA_TEMPORADA_19_20.pdf)
- A 2018-19 SELAE statistics PDF ("Plantilla de Boletos de 1X2") says the figures are updated daily with the percentages bet up to that moment [via search snippet]. — [Pronos 1x2 Jda 59_18_19](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Temporada%202018_2019/Pronos%201x2%20Jda%20%2059_18_19.pdf)
- The draw for uncomputed matches uses these percentages "registrados en el sistema central", and SELAE must publish them before the draw (norma 38ª). — [Hacienda normas](https://www.hacienda.gob.es/DocLeyes/REPOSITORIO%20NORMATIVA/58018anexo.pdf)
- Format of SELAE's statistics PDFs (Quinigol 2026/27 J11): per-match percentage per option, colour-coded (most chosen in blue, next two in green, least in red). "Calculados con las apuestas realizadas hasta la fecha indicada al pie": the document is dated 30/09/2026 and covers bets to 28-09-26. Older Quiniela 1X2 PDFs carry the heading "TANTOS POR CIENTO DE LOS SIGNOS PRONOSTICADOS" (2014-15), and one "pronos1X2_10M" file covers a 2013 Champions League jornada. — [Quinigol 2026-27 J11](https://www.loteriasyapuestas.es/f/loterias/documentos/El%20Quinigol/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Temporada%202026_2027/pronosQNG_11_26_27_L.pdf); [Quiniela 2014-15](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Pronosticos_10_14-15%201x2%20S.pdf); [pronos1X2_10M](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/pronos1X2_10M.pdf); [Quinigol 2025-26 J58](https://www.loteriasyapuestas.es/f/loterias/documentos/El%20Quinigol/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Temporada%202025_2026/Pronos_QNG_58_25-26_J.pdf)
- **eduardolosilla.es/quiniela/ayudas/porcentajes** (J17 2026/27):
  - "% QUINIELISTA": bets of the site's users, "se actualizan cada hora" (last update 27/10/2026 10:20).
  - "% LAE": "datos oficiales de LAE actualizados diariamente" (last update 27/10/2026 07:24).
  - "% REAL": "Probabilidad real (Betfair/Casas de apuestas)", hourly (09:57).
  - An "Evolución porcentajes" chart is listed but showed no data. — [eduardolosilla porcentajes](https://www.eduardolosilla.es/quiniela/ayudas/porcentajes)
  - Example values (1/X/2):

    | Match | % Quinielista | % LAE | % Real |
    |---|---|---|---|
    | RSD Alcalá–Las Palmas | 10/7/83 | 19/15/66 | 17/21/62 |
    | Alcoyano–Mallorca | 10/7/83 | 20/17/63 | 12/18/70 |
    | Arosa–Pontevedra | 21/23/56 | 29/27/44 | 22/26/52 |

    — [eduardolosilla porcentajes](https://www.eduardolosilla.es/quiniela/ayudas/porcentajes)
- The same site offers "estimación" of prizes (shown after a bet is built), escrutinio, bote, reducidas/condicionadas/optimizadas tools, and file upload of columns. — [eduardolosilla](https://www.eduardolosilla.es/)
- https://www.quinielista.es/ returns 301 to https://www.eduardolosilla.es/ (own test via fetch). — [quinielista.es](https://www.quinielista.es/)
- quinielafutbol.info's main page has no betting percentages. — [quinielafutbol.info](https://www.quinielafutbol.info/)
- quiniela15 shows no public percentages, only "Sis."/"Usu." columns (system and users' picks). — [quiniela15](https://www.quiniela15.com/)
- pronosticosfiablesquiniela.es describes "porcentajes, signos recomendados y nivel de confianza", but no figures or source are visible in its static HTML. — [pronosticosfiablesquiniela](https://pronosticosfiablesquiniela.es/)
- loterias1fuengirola shows "Tip del Experto" figures (e.g. 79% quinielista vs 74% real) with no source. — [loterias1fuengirola](https://www.loterias1fuengirola.com/jugar-quiniela-online)
- Practitioner use (apuestas-deportivas.es, 2019–2020 seasons): "estimación de porcentajes LAE al cierre" is compared with "porcentajes reales" to classify signs as "más caros" or "más rentables", e.g. Valencia–Osasuna with "una estimación cercana al 73% de apuestas para el 1". — [apuestas-deportivas.es J44](https://www.apuestas-deportivas.es/?p=28969)
- Practitioner formula (Emprendedores, 29 May 2025):
  - Expected winners ≈ (public probability of the winning column) × total bets.
  - "Clonismo" (players with similar methods playing the same columns) makes real prizes lower than such forecasts, especially in "rentable" jornadas.
  - In the Pleno al 15, scores like 1-1, 2-1 and 1-2 are heavily played, while 0-0, 1-0 and 0-1 often carry value. Example: Peña Q84's 0-0 Barcelona–Villarreal Pleno al 15 worth 1.8 M€. — [Emprendedores](https://emprendedores.es/noticias-de-empresa/la-quiniela-azar-y-asimetria/)
- Comparable pool: Swedish Stryktipset guides compare public "streck" with odds to find over-bet favourites, and warn that streck change up to the deadline. — [hurbra.se Stryktipset 8 Aug 2026](https://hurbra.se/stryktipset-8-augusti-2026/)

### Inferences
- **Use % LAE, not % Quinielista, as the population distribution.** On J17, the site's engaged online users put 83% on Las Palmas while the whole SELAE population had 66%. A site-user sample would badly overstate concentration and so mis-estimate co-winners and prizes.
- **% LAE is a daily snapshot.** The 07:24 stamp on closing day means the final hours of sales are missing. The system should store every daily snapshot to (a) learn the typical drift between the last pre-close snapshot and the final distribution, and (b) build its own history. No public archive was found (Q5).
- In this single J17 sample, % LAE gave the draw less than the market did in two of three matches (15 vs 21; 17 vs 18), but it did not uniformly over-bet favourites. In two Copa ties (Alcoyano–Mallorca, Arosa–Pontevedra) the population over-bet the lower-division home side. Systematic conclusions need the multi-season data the system does not yet have.
- **Pipeline:** scrape eduardolosilla's porcentajes page (200 from datacenter) for % LAE and % Real. Optionally fetch the official SELAE statistics PDF from a home IP to validate that eduardolosilla's "% LAE" equals SELAE's numbers.

### Gaps
- The exact URL and file naming of the 2026/27 La Quiniela 1X2 statistics PDFs was not found; only Quinigol 2026/27 files surfaced.
- How SELAE counts doubles and triples in the percentages (per bet or per marked sign) is undocumented in the sources found.
- No accuracy study of the last published % LAE versus the final at-close distribution exists in the sources found.
- Sample size and representativeness of eduardolosilla's "% Quinielista" are not stated.

## Q4. Evidence: are pool bettors biased, do contrarian strategies raise expected value, and how do jackpots and prize structure change the optimal strategy?

### Takeaway
Across pari-mutuel football pools (Austrian Toto, Korea's sports lottery, US NFL pick'em pools), the crowd over-bets favourites and likely outcomes. Long-shot or "differentiated" hits therefore pay more per hit. In large pools, EV-optimal picks beat score-maximising picks by large factors: Clair & Letscher report "often by orders of magnitude", and 3.4–28× better than random in a 170,000-entrant pool. Spanish research shows Quiniela demand behaves like lotto: strongly jackpot-driven, with habit, halo and jackpot-fatigue effects. That means more competing bets when botes are big. No peer-reviewed backtest of a profitable contrarian strategy for La Quiniela itself was found. With a 45% takeout, positive EV realistically needs both large public mispricing and a bote.

### Cited Findings
- **Clair & Letscher (2007), Operations Research 55(6):1163–1177.**
  - "Teams that are popularly perceived as 'favorites' gain a disproportionate share of entries. In large pools there can be a significant advantage to picking upsets that differentiate your picks from the crowd". Their strategies "significantly outperform strategies based on maximizing score or number of correct picks—often by orders of magnitude".
  - On 2004-05 online NFL pools: "pool participants overbet favorites"; "In larger (thousands of players) pools, crowd avoidance is essential—picking all favorites is one of the few losing bets".
  - With N = 170,000, random picks averaged an expected weekly return of 23.4, and the optimal picks were 3.4–28× better than random. The optimal picks went against the ESPN pool favourites 63% of the time (9.5 games/week) and against the Massey ratings in 44% of games (6.6 underdogs/week). Expected return of optimal picks: 16–74 (average 41) at N = 170,000 and 2.26–7.17 (average 3.87) at N = 50.
  - Optimal play is more conservative in small pools and uses more upsets in large ones. — [Operations Research DOI](https://pubsonline.informs.org/doi/10.1287/opre.1070.0448); [PDF (Berkeley course copy)](https://www.stat.berkeley.edu/~aldous/157/Papers/clair.pdf); [Authors' page](https://cs.slu.edu/~clair/pools)
  - The same paper cites Metrick (1996) on 1993 NCAA pools, where top seeds were over-backed. — [Clair & Letscher PDF](https://www.stat.berkeley.edu/~aldous/157/Papers/clair.pdf)
- **Hauser, Koenig & Krylova (2000), "Gamblers' Rationality in Parimutuel Soccer Betting", IHS Economics Series 87.** Data: Austrian Toto and Torwette 1996–99, 90 rounds.
  - Because a rollover is fairly likely, it is optimal to "overbet favourite outcomes" relative to their probability.
  - Actual gamblers over-bet favourites even more than the optimum: probable results are chosen too often, improbable ones too rarely. — [EconPapers](https://econpapers.repec.org/RePEc:ihs:ihsesp:87); [IDEAS](https://ideas.repec.org/p/ihs/ihsesp/87.html)
- **Chung & Hwang (2010), Southern Economic Journal 76(4):884–905.** Korea's pari-mutuel soccer lottery vs. UK bookmakers (EPL score bets).
  - Lottery participants put more money on high-probability outcomes than bookmaker odds imply.
  - So winning long-odds bets pay more in the pool than at bookmakers, and short-odds bets pay less. — [IDEAS](https://ideas.repec.org/a/wly/soecon/v76y2010i4p884-905.html); [Korea Univ. record](https://scholar.korea.ac.kr/handle/2021.sw.korea/116764)
- **Forrest & Pérez (2015), "Just Like the Lottery? Player Behaviour and Anomalies in the Market for Football Pools", Journal of Gambling Studies 31(2):471–482 (DOI 10.1007/s10899-013-9423-4).** 23 years of Spanish pools sales data show "strong sensitivity of sales to the size of jackpot on offer, significant habit effects, a halo effect … and a tendency to jackpot fatigue". Pools players appear to "share common psychological and cognitive traits" with lotto players. Open-access copy: hdl 10651/33594. — [DOI](https://doi.org/10.1007/s10899-013-9423-4); [Semantic Scholar record (abstract)](https://api.semanticscholar.org/graph/v1/paper/DOI:10.1007/s10899-013-9423-4?fields=title,abstract,year,venue); [Open access (Univ. Oviedo)](http://hdl.handle.net/10651/33594)
- **García & Rodríguez (2007), "The Demand for Football Pools in Spain: The Role of Price, Prizes, and the Composition of the Coupon", Journal of Sports Economics 8(4):335–354.** Fixture-level data 1972-73 to 2002-03 (working paper UPF 825). The **jackpot model fits better than the effective-price model**, and the presence of First Division matches in the coupon affects demand. — [UPF WP 825](https://econ-papers.upf.edu/en/onepaper.php?id=825); [Uniovi record](https://portalinvestigacion.uniovi.es/documentos/5e78ca8c2999521b3d11f056?lang=en)
- **Rodríguez, García & Pérez (EASM 2011).** Lottery-demand phenomena (lotto fever, prize fatigue, conscious selection, gambler's fallacy, halo) also show up in Quiniela demand. "A naïve explanation … could be that the introduction of a rollover rule made the (football) pools more like lotto". The paper cites García, Pérez & Rodríguez (2008), "Football pools sales: How important is a football club in the top divisions?", Int. J. Sports Finance 3:119–126, and Forrest (1999), "The past and future of the British football pools", J. Gambling Studies 15:161–176. — [EASM 2011 abstract PDF](https://www.easm.net/download/2011/bae3e8955b97f8696852aa5b1e1f2acb.pdf)
- **Pujol (2009), "Football Betting as a Cyclical Learning Process", Univ. Navarra WP 05/09.** Quiniela data 1970–2000 in a probability-matching framework; bettors' performance improves progressively, interpreted as learning. — [IDEAS](https://ideas.repec.org/p/una/unccee/wp0509.html)
- **Stryktipset (Sweden), Stockholm University bachelor thesis (2012), "Jakten på den optimala Stryktipsstrategin".** Regressions of the public's bets on outcome probabilities found no Stryktipset system with EV above the stake, but found odds-market bets with expected profit. Student thesis; limited evidence [via search snippet]. — [SU report 2012:7](https://www2.math.su.se/matstat/reports/seriec/2012/rep7/abstract.pdf)
- General pari-mutuel theory:
  - Snowberg & Wolfers (JPE 2010) attribute the horse-racing favourite–longshot bias mainly to probability misperception. — [IZA DP 4884](https://iza.org/publications/dp/4884/imprint)
  - Ottaviani & Sørensen note that pari-mutuel lotto-type games always produce a *reverse* favourite–longshot bias. — [Ottaviani & Sørensen PDF](https://web2.econ.ku.dk/sorensen/papers/pvfom.pdf)
- Prize dispersion in La Quiniela, October 2026: the 14-hit prize ranged from ≈11,162 € (50 winners, J14) and 17,500.75 € (32 winners, J12) to 36,053.45 € (15 winners, J16) and 45,666.15 € (4 winners, J15). — [SELAE escrutinio 18-oct](https://www.loteriasyapuestas.es/es/la-quiniela/escrutinios/la-quiniela-premios-y-ganadores-del-18-de-octubre-de-2026); [NP 11_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_11_10_26.pdf); [NP 21_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_21_10_26.pdf); [quinielafutbol.info](https://www.quinielafutbol.info/)
- Elige 8 dispersion: 9,284 winners (9 Sep 2026) vs. 1,623 winners (11 Oct 2026) sharing the same 55% pool rule. — [NP 9_09_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_9_09_26.pdf); [NP 11_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_11_10_26.pdf)
- Benchmark for "hits": a 2018 UB/UPC bachelor thesis (multinomial GAM on Primera matches in Quiniela format) hit 51.18% in training and 54.94% in validation. Seasons were unspecified, and it made no market comparison. — [UB dipòsit 2445/124322](https://diposit.ub.edu/dspace/handle/2445/124322)

### Inferences
- **Maximising hits and maximising EV are different objectives.** Public percentages do not change the probability of a sign, except through the draw rule (Q2). They change what a hit is worth. With the system's tiny accuracy edge (RPS 0.20033 vs 0.20043; 50.6% vs 50.5% of signs), the payout channel is likely the larger lever.
- **Cost-free use under the current goal:** when two signs have near-equal model probability, pick (or double) the one with the lower % LAE. Expected hits are unchanged and the expected prize rises.
- **Approximate EV math** (derived here; standard Poisson pari-mutuel approximation, not taken from a cited source). For a column c with model probabilities p_i and public shares q_i, N bets, and category fund F_k (e.g. F_1 = 0.16 × recaudación):
  - Expected co-winners ≈ λ = N·Π q_i.
  - Expected prize if you hit ≈ F_k·(1 − e^(−λ))/λ.
  - For the 14-hit category with λ ≫ 1: EV ≈ 0.16 × 0.75 € × Π(p_i/q_i) = 0.12 € × Π(p_i/q_i). Value multiplies across matches.
  - The Especial adds roughly 0.05625 € × Π(p_i/q_i) × (p_P15/q_P15), plus the share of any bote.
  - "Clonismo" (correlated public picks) makes the independence assumption optimistic (Emprendedores, Q3).
- **Pool size:** with ≈1.5–4.7 M bets per jornada (Q2), La Quiniela is far into Clair & Letscher's "large pool" regime for the 14-hit and Especial categories, where differentiation pays. For 10–12 hits, many co-winners make the prize nearly invariant to differentiation, and the cascade and minimum rules can zero them out.
- **Jackpots:** a bote raises only the Especial's EV, and SELAE chooses where it goes. Botes also attract more bets (Forrest & Pérez), which dilutes the ordinary categories proportionally but not the fixed bote. Hauser et al.'s result (rollovers push optimal play toward favourites) and Clair & Letscher's (large pools push toward upsets) differ because of rollover mechanics. The system should solve its ticket optimisation numerically per jornada rather than adopt a blanket "contrarian" rule [inference].
- **Pleno al 15** (16 combos, per-team goal percentages published by SELAE when it has to draw a P15) is where public bias (high-scoring scorelines over-played, per practitioners) and dispersion are greatest. Value there only pays out if the 14 are also hit.
- **Elige 8:** every bet with the top number of hits shares one pool, so the prize per winner depends on how many others also hit. Favourite-heavy Elige 8 picks win mostly in "many winners" states (e.g. 9,284 vs 1,623 winners). The same contrarian logic applies, weighted by state.

### Gaps
- No peer-reviewed study specific to Italian Totocalcio or the UK pools' public-pick bias was found. Forrest (1999) was found only as a citation.
- No Quiniela-specific backtest of contrarian vs. favourite strategies using official % LAE was found; this is the key missing evidence.
- No peer-reviewed Svenska Spel / Stryktipset efficiency study was found (only a 2012 student thesis).
- The full text of García et al. (2008) and the size of the "big club" effect on percentages were not retrieved.

## Q5. Historical Quiniela databases (jornadas, results, prizes, percentages over many seasons)

### Takeaway
No clean, ready-made public dataset (Kaggle or GitHub) covering many seasons of La Quiniela was found. The richest accessible history is eduardolosilla.es "Histórico 1X2": seasons 2003/04 to 2026/27, with signs, Pleno al 15, recaudación, bote and prizes per category, but no teams. SELAE's own per-jornada pages and press-release PDFs are authoritative but blocked from Colab. No public multi-season archive of percentages exists, so the system must start archiving % LAE itself.

### Cited Findings
- eduardolosilla "Histórico 1X2":
  - Season selector from TEMPORADA 26/27 back to 03/04.
  - Per jornada: row of 1/X/2 signs plus a Pleno al 15 token (e.g. "M2", "0M"), Recaudación, Bote, and amounts for "Al 15" through "Al 10".
  - No team names, no percentages, no download; season tabs without URL parameters.
  - A separate "Histórico" page covers per-match history. — [eduardolosilla histórico 1X2](https://www.eduardolosilla.es/quiniela/ayudas/historico-1X2); [eduardolosilla histórico](https://www.eduardolosilla.es/quiniela/ayudas/historico)
- quinielafutbol.info: per-jornada pages with results, combination, prize table (Pleno al 15 to 5ª plus Elige 8), recaudación, number of bets and total prizes. It has an archive and mentions history back to 1946, but the archive's depth and format were not verified. — [quinielafutbol.info archive](https://www.quinielafutbol.info/resultados/jornadas-de-la-quiniela.html); [quinielafutbol.info](https://www.quinielafutbol.info/)
- SELAE official: per-jornada results and escrutinio pages go back at least to 2012 (e.g. 30 Sep 2012). Press-release PDFs were seen from 2023 onward (e.g. 5 Mar 2023). "Estadísticas de pronósticos" PDFs exist for 2013, 2014-15 and 2018-19. Calendars exist from 2023-24 onward. — [SELAE 2012](https://www.loteriasyapuestas.es/en/la-quiniela/resultados/la-quiniela-premios-y-ganadores-del-domingo-30-de-septiembre-de-2012); [NP 5_3_23](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_DE_LA_QUINIELA_DE_FECHA_5_3_23.pdf); [Calendario 23-24](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Calendarios/CALENDARIO_Quiniela_Temp_23-24.pdf); [Quiniela pronos 2018-19](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Estad%C3%ADsticas%20de%20pron%C3%B3sticos/Temporada%202018_2019/Pronos%201x2%20Jda%20%2059_18_19.pdf)
- lotoideas.com offers full downloadable result histories (Excel, OpenDocument, PDF, CSV, TSV) for Primitiva, Bonoloto, Euromillones, El Gordo, EuroDreams and Lototurf, but **not** for La Quiniela. For the Quiniela it has reduction systems (2010–2012 posts) and a "Adaptador de Pronósticos". — [lotoideas Quiniela](https://www.lotoideas.com/categoria/la-quiniela/); [lotoideas Primitiva histórico](https://www.lotoideas.com/primitiva-resultados-historicos-de-todos-los-sorteos/)
- GitHub: only dmiro/betEScraper (2013-era SELAE scraper with REST/JSON/XML/CSV output) was found; it is likely broken against today's site. — [dmiro/betEScraper](https://github.com/dmiro/betEScraper)
- Kaggle: searches returned no Quiniela dataset. — [search returned only news pages, e.g. Menorca.info](https://www.menorca.info/actualidad/sorteos-loterias/2025/10/05/2485303/comprobar-quiniela-resultado-del-domingo-octubre-2025.html)
- Regional press (Última Hora, Periódico de Ibiza, Menorca.info) publish weekly HTML tables of matches, signs, scores and prizes per category, noting that only the organiser's list is official. — [Última Hora Sep 2025](https://www.ultimahora.es/noticias/sorteos-loterias/2025/09/21/2474983/comprobar-quiniela-resultado-del-domingo-septiembre-2025-2.html); [Menorca.info Oct 2025](https://www.menorca.info/actualidad/sorteos-loterias/2025/10/05/2485303/comprobar-quiniela-resultado-del-domingo-octubre-2025.html)
- Academic datasets (not public) cover 1972-73 to 2002-03 fixture-level sales (García & Rodríguez), 23 years of sales (Forrest & Pérez) and 1970–2000 bettor performance (Pujol). — [UPF WP 825](https://econ-papers.upf.edu/en/onepaper.php?id=825); [Forrest & Pérez DOI](https://doi.org/10.1007/s10899-013-9423-4); [Pujol IDEAS](https://ideas.repec.org/p/una/unccee/wp0509.html)
- A Universitat de València peña site hosts 2019/20 member-pick sheets. One jornada shows members picked 58.8% "1", 19.9% "X" and 21.3% "2" [small private sample; exact sheet unverified]. — [uv.es/quiniela](https://www.uv.es/quiniela/index_archivos/sheet013.htm)

### Inferences
- For backtesting payout-aware strategies, the eduardolosilla history (2003/04+) provides combination, recaudación and prizes per category. Joined with match lists from SELAE pages or press PDFs (fetched from a home IP), it gives realised co-winner counts (fund ÷ prize). That is a proxy for how "popular" each winning column was, even without % data.
- Historical % LAE is the missing piece. Archiving the daily eduardolosilla % LAE snapshot, ideally also the SELAE statistics PDFs, from now on is the only practical way to build it.

### Gaps
- Depth and machine-readability of quinielafutbol.info's archive was not verified.
- No public multi-season archive of official percentages was found.
- No Kaggle dataset was found; a direct Kaggle site search was not possible with the available tools.

## Q6. Reliable mirror/secondary sites for the official jornada and results — evaluation and ranked shortlist

### Takeaway
eduardolosilla.es and quinielafutbol.info are the strongest Colab-reachable mirrors. eduardolosilla adds official % LAE, % Real and estimación; quinielafutbol.info adds clean composition text, kickoff times, prize tables and recaudación. quiniela15.com is a useful third check for the list and closing time. loterias1fuengirola.com, one of the user's five current sources, now redirects and was mixing two jornadas on 27 Oct 2026, so it should be demoted. pronosticosfiablesquiniela.es is a tipster site, not a list source. resultados-futbol.com blocks datacenter IPs. lotoideas.com and elgordo.com add nothing for the official list.

### Cited Findings
- **eduardolosilla.es** (200 from datacenter, own test):
  - J17 list with day and time of each match; Pleno al 15 Recreativo de Huelva–Rayo.
  - Its own closing deadlines: Tue 27/10 at 18:30 (DNP peñas) and 19:00 (individual players).
  - Pending botes, escrutinio, estimación, live scores, histórico, % LAE/% Quinielista/% Real.
  - No documented API. Its footer reads "Administración de Loterías Nº 1 en internet desde 2003". — [eduardolosilla](https://www.eduardolosilla.es/); [porcentajes](https://www.eduardolosilla.es/quiniela/ayudas/porcentajes); [histórico 1X2](https://www.eduardolosilla.es/quiniela/ayudas/historico-1X2)
- **quinielafutbol.info** (200):
  - Next-jornadas page: J17 dated Wed 28 Oct 2026; J18 with all 15 matches, dates and kickoff times, "(F)" markers, and a prose description of the composition (7 LaLiga, 3 Hypermotion, 4 Liga F, Pleno al 15 Athletic–Real Sociedad 01/11 21:00).
  - States "no hay bote acumulado" for J17 and that the calendar "se actualiza diariamente".
  - Results pages include prize tables, recaudación and number of bets. — [quinielafutbol próximas](https://www.quinielafutbol.info/proximas-jornadas-de-la-quiniela.html); [quinielafutbol.info](https://www.quinielafutbol.info/)
- **quiniela15.com** (200): a self-described "comunidad no oficial de quinielistas".
  - J17 list (Segunda + Copa del Rey) with times; "Cierra el 27/10/2026 a las 20:00"; live results of J16 including Liga F scores.
  - Bote text "Hay un bote de 2.500.000 € para esta jornada" attached to J16. — [quiniela15](https://www.quiniela15.com/)
- **loterias1fuengirola.com** (200 after redirect):
  - The user's URL `/quiniela.php` now returns **301** to `/jugar-quiniela-online`.
  - On 27 Oct 2026 the title said "Jornada 17" while the selector said "18". The JS-driven form listed J18's matches (Levante–At. Madrid … Tenerife (F)–Athletic Club (F)), and the Pleno al 15 (Athletic–Real Sociedad) rendered as two separate entries. Meanwhile the editorial text described J17's Copa ties.
  - It showed "Sin Bote!". Its last result (25/10/26) was "2211X11XXX11X1" plus Pleno al 15 "1-2".
  - Its prize table: Pleno al 15 0 €; 14 36,053.45 €; 13 455.12 €; 12 36.94 €; 11 5.61 €; 10 1.63 €; Elige 8 94.33 €.
  - It identifies as "Administración de Loterías nº 1 … Peralta Fuengirola SL" and uses SELAE logos "a modo meramente identificativo"; no receptor number is shown. — [loterias1fuengirola (redirect source)](https://www.loterias1fuengirola.com/quiniela.php); [loterias1fuengirola jugar-quiniela-online](https://www.loterias1fuengirola.com/jugar-quiniela-online)
- **pronosticosfiablesquiniela.es** (200): a tipster site ("QuinielaLab") with self-reported accuracy (e.g. 182/210 signs; J15 14/14). Its header says "Jornada 17", but the static HTML shows 14 rows without team names, and its latest analysis was J15. — [pronosticosfiablesquiniela](https://pronosticosfiablesquiniela.es/)
- **resultados-futbol.com/quiniela**: 403 to the datacenter IP (own test). — [resultados-futbol quiniela](https://www.resultados-futbol.com/quiniela)
- **elgordo.com**: `/es/resultados/quiniela` redirected to the generic `/es/resultados` (200). Quiniela coverage was not verified (own test). — [elgordo resultados](https://www.elgordo.com/es/resultados/quiniela)
- **lotoideas.com**: no Quiniela history; systems and tools only. — [lotoideas Quiniela](https://www.lotoideas.com/categoria/la-quiniela/)
- **Regional press**: weekly results and prize tables with an "only the official list is valid" disclaimer. — [Última Hora](https://www.ultimahora.es/noticias/sorteos-loterias/2025/09/21/2474983/comprobar-quiniela-resultado-del-domingo-septiembre-2025-2.html)
- **Inconsistencies observed on 27 Oct 2026:**
  - J17 bote: quinielafutbol.info and Fuengirola say none. quiniela15's 2.5 M€ text refers to J16, matching SELAE's 21 Oct note announcing 2.5 M€ for 25 Oct.
  - Closing time: quiniela15 says 20:00; eduardolosilla's internal cut-offs are 18:30/19:00; the official per-jornada aviso was not readable from here. — [quinielafutbol próximas](https://www.quinielafutbol.info/proximas-jornadas-de-la-quiniela.html); [quiniela15](https://www.quiniela15.com/); [NP 21_10_26](https://www.loteriasyapuestas.es/f/loterias/documentos/Quiniela/Notas%20de%20prensa/NOTA_DE_PRENSA_LA_QUINIELA_21_10_26.pdf); [eduardolosilla](https://www.eduardolosilla.es/)

### Inferences
- Key the cross-check on (jornada number, nominal date) **before** comparing teams, because a mirror may show the next jornada's form while the current one is still open (Fuengirola case). Reject any source whose match count is not 15 or whose Pleno al 15 does not parse as one pairing.
- Treat closing times from sales points (eduardolosilla, Fuengirola) as **earlier internal deadlines**. The official time comes from SELAE's per-jornada "Aviso cierre" PDF, fetched from a home IP; failing that, use quiniela15's or quinielafutbol.info's stated close, cross-checked against the first kickoff.
- Read the bote only from SELAE press releases, or from mirrors that quote them for the specific jornada number. Generic "bote" banners go stale.

#### Ranked shortlist of Quiniela-specific sources for ORÁCULO 1X2 (benefit / risk)

| Rank | Source | Concrete benefit for the system | Concrete risk |
|---|---|---|---|
| 1 | **SELAE official**: results/comprobar/escrutinio pages, Notas de prensa PDFs, Avisos de interés (cierre/suspensión), Estadísticas de pronósticos PDFs, calendars, normas | Ground truth: list and order, official closing time, substitutions and suspensions, combination, prizes, recaudación, bote destination, official % of signs | Akamai 403 from Colab/datacenter (confirmed 27 Oct 2026, incl. `/servicios/` JSON, widget, RSS, PDFs). Undocumented JSON. Needs a home-IP fetch job; WAF evasion may breach terms |
| 2 | **eduardolosilla.es** (+ quinielista.es redirect) | Only Colab-reachable source of **official % LAE** (daily), plus % Real (hourly), own-user %, prize estimación, escrutinio, list with times, 2003/04+ history with recaudación and prizes per category | Commercial sales point; HTML can change without notice; internal deadlines earlier than official; % LAE is a daily snapshot (stale at close); no API or ToS clarity on scraping |
| 3 | **quinielafutbol.info** | Clean 15-match list with dates, times, "(F)" markers and prose composition; next-jornada preview; prize tables with recaudación and bets; claims daily calendar updates | No percentages; independent site of unverified provenance; bote statements generic; archive depth unverified |
| 4 | **quiniela15.com** | Third independent list; explicit closing timestamp; live results incl. Liga F; community signals | Unofficial community; bote banner can refer to a previous jornada; possible layout changes |
| 5 | **Regional press** (Última Hora / Periódico de Ibiza / Menorca.info) | Results and prize-table backup with HTML tables | Post-event only; publication delays; disclaimers |
| 6 | **loterias1fuengirola.com** (now `/jugar-quiniela-online`) | Sales-point prize table that matched SELAE arithmetic for J16 | 301 redirect from the configured URL; mixed J17/J18 content; "Sin Bote!" banner; JS-driven form; Pleno al 15 rendering issue. Demote to tertiary |
| 7 | **pronosticosfiablesquiniela.es** | None for official data (tipster content only) | No team names in static HTML; stale analysis; self-reported accuracy. Drop from the official-list consensus |
| 8 | **resultados-futbol.com / elgordo.com / lotoideas.com / GitHub betEScraper** | Marginal (lotoideas tools; old scraper code) | 403 to datacenter (resultados-futbol); redirect to generic page (elgordo); no Quiniela history (lotoideas); 2013-era code (betEScraper) |
| — | **Evidence base for strategy**: Clair & Letscher 2007; Hauser et al. 2000; Chung & Hwang 2010; Forrest & Pérez 2015; García & Rodríguez 2007 | Justifies payout-aware ticket construction (value ratio p/q, crowd avoidance in large pools, bote effects) | None is a Quiniela-specific contrarian backtest; Hauser vs Clair imply different directions depending on rollover structure, so validate on the system's own % LAE archive |

### Gaps
- The terms of service and robots.txt of eduardolosilla.es and quinielafutbol.info, and the update latency (minutes after SELAE publishes the list), were not measured.
- Marca/AS Quiniela pages were not located by search, so not evaluated. SELAE social media and the official app were not evaluated.
- Whether quinielafutbol.info's composition text and times are copied from SELAE or compiled independently is unknown.
