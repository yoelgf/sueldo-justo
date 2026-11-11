Written by Claude in the chat for Yoel (curator) on 2026-11-12. Research note for the side project; summary in own words, sources linked.

# Spain job market: app ideas research (2026-11-12)

## Pain points found
- Overall unemployment falling (EPA Q2 2026 ~9.9%, ~2.5M people) but youth (<25) unemployment ~25% after Q3 2026, highest in the EU; ~35% of under-25s overqualified. Sources: https://www.bankinter.com/blog/economia/paro-espana-encuesta-epa · https://valenciaplaza.com/valenciaplaza/nacional/la-tasa-de-paro-juvenil-escala-hasta-el-254-tras-sumar-53600-desempleados-durante-el-verano · https://forbes.es/?p=846225
- Ghosting and ghost jobs: ~42% of candidates say they got no answer after applying (LinkedIn data); ~43% of recruiters admit keeping ghost offers. InfoJobs reviews complain about unverified companies/offers. Sources: https://www.rrhhdigital.com/despedido/793073/ghosting-en-procesos-de-seleccion/ · https://resufit.com/es/blog/ghost-jobs-como-detectar-ofertas-de-empleo-falsas/
- Fijos discontinuos: contracts ~6x since 2019 (218,908 in Sept 2026 vs 34,673 in Sept 2019); only ~17% of registered FD demandantes get contributory benefit. Sources: https://www.cuestioneslaborales.es/fijos-discontinuos-cifras-paro/ · https://www.que.es/2026/06/10/fijos-discontinuos-paro-17-por-ciento/
- Salary transparency (EU Directive 2023/970): sources disagree on whether salary ranges in job ads are already mandatory in Spain; Spain missed the 7 June 2026 transposition deadline. Confusion = opportunity. Sources: https://www.moncloa.com/2026/07/13/transparencia-salarial-prohibe-salario-negociar-ofertas-3398814/ · https://www.ineaf.es/tribuna/ley-de-transparencia-salarial/
- Housing blocks job mobility: young people turn down jobs in other cities because rent would eat the salary (avg rent ~98.7% of a young salary). Sources: https://www.merca2.es/2026/04/28/70-de-jovenes-espanoles-casa-padres-crisis-vivienda-2374105/ · https://www.elespanol.com/madrid/sociedad/20260531/fabiola-fabio-angustia-jovenes-relegados-vivir-padres-necesitan-salario-pagar-alquiler/1003744263093_0.html
- Convenio salary tables are hard to find; yearly tables often published separately and late. Source: https://www.cuestioneslaborales.es/cuanto-debo-cobrar-segun-convenio/
- Digital time-tracking decree (registro horario) still not in the BOE as of July 2026. Source: https://www.holded.com/es/blog/registro-horario-digital
- Estatuto del Becario approved by the Council of Ministers (March 2026) but stuck in parliament; Constitutional Court annulled the provision that mandated it. Source: https://www.legaltoday.com/?p=193414

## Ideas and Claude's scores (Yoel's 6 criteria, /30)
Without runtime Gen AI:
1. Vida laboral reader + paro planner (private, in-browser PDF parsing; days contributed, paro estimate, FD timeline) - 25
2. "¿Me compensa?" offer vs city calculator (net salary minus rent/transport; programmatic SEO; links to Litoral) - 23
3. Job-hunt tracker + ghost-job flags browser extension - 22 (scraping/ToS risk)
4. Simple digital fichaje for micro-businesses - 19 (moving deadlines, incumbents; same pattern as dropped Verifactu)
5. Prácticas review board - 15

With Gen AI allowed:
1. "¿Me pagan bien?" AI check of nómina/contract/finiquito against the convenio + Estatuto (RAG over convenios) - 26
2. B2B WhatsApp hiring assistant for small/seasonal businesses (pre-screening, salary-compliant ad text) - 23; only ~16% of Spanish companies use AI in hiring (https://www.cio.com/tendencias/solo-el-16-de-las-empresas-espanolas-emplean-la-ia-en-sus-procesos-de-seleccion)
3. Spanish Sprout without scraping (swipe + AI-tailored CV/carta, user submits) - 21
4. English job-interview voice practice for Spaniards - 19

Crowded already: generic AI auto-apply (LoopCV, JobCopilot say they cover InfoJobs/LinkedIn/Indeed) and AI interview simulators in Spanish.

Yoel's reaction: likes #3 (Spanish Sprout) and wants it combined with #1 (convenio checker). See 2026-11-12-combined-job-app-concept.md.
