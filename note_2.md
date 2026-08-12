# Note: California Proposition 99 — Causal Impact Analysis

## 1. Seçilmiş Metod

İki metod istifadə edildi və müqayisə edildi:

- **Difference-in-Differences (DiD)** — bütün 38 control ştatı bərabər çəki ilə "counterfactual" kimi istifadə edir.
- **Synthetic Control** — control ştatların çəkili kombinasiyasından (pre-period-da California-ya ən yaxın uyğunluğu tapan optimallaşdırma ilə) "sintetik California" qurur. Predictor kimi `retprice` və pre-1989 illərinin `cigsale` dəyərləri istifadə olundu (`lnincome`, `beer`, `age15to24` datada çoxlu boşluq — 16–55% missing — olduğu üçün çıxarıldı).

İkisi birlikdə istifadə edildi ki, nəticə tək bir metodun fərziyyəsinə bağlı qalmasın.

## 2. Assumption Checks (Fərziyyə Yoxlamaları)

**DiD — Parallel Trends:**
Pre-1989 dövründə California-da siqaret satışı illik ortalama -1.71% azalırdı, control ştatların ortalamasında isə -0.30%. Trend istiqaməti eynidir (hər ikisi azalır), amma sürət fərqlidir — bu, "təmiz" parallel trends deyil. Deməli sadə DiD ATT-si bir qədər yuxarı qiymətləndirilmiş ola bilər, çünki artıq əvvəldən mövcud olan sürətli azalma trendini də "effekt" kimi qeyd edə bilər.

**Synthetic Control — Pre-treatment Fit:**
Pre-treatment RMSPE = 6.63 paçka (California-nın orta satış səviyyəsi ~110-120 paçka olduğu üçün nisbətən kiçikdir). Bu, sintetik California-nın 1989-dan əvvəl real California-nı yaxşı təqlid etdiyini göstərir — Synthetic Control-un əsas fərziyyəsi (yaxşı pre-fit) təxminən ödənir.

## 3. Final ATT Qiymətləri

| Metod | ATT (paçka/il) | Qeyd |
|---|---|---|
| Difference-in-Differences | **-27.35** | Klasterlənmiş SE (ştat üzrə), p < 0.001 |
| Synthetic Control | **-20.18** | 1989–2000 ortalama gap |

İki qiymət arasındakı fərq (~26%) DiD-in bütün ştatları bərabər çəkiləndirməsi ilə izah olunur — Synthetic Control yalnız California-ya real bənzəyən ştatları (Utah 32.6%, New Mexico 10.6%, Connecticut 6.3%) yüksək çəki ilə seçir.

**Ən etibarlı qiymət kimi Synthetic Control ATT-si (-20.18 paçka/il) qəbul edilir**, çünki onun fərziyyəsi (pre-fit) kəmiyyətcə yoxlanılıb, DiD-in isə yox.

## 4. Placebo Test Nəticəsi

Eyni prosedur bütün 38 control ştata tətbiq edildi. Yalnız yaxşı pre-fit-ə malik ştatlar (California-nın pre-RMSPE-sindən 2 dəfədən çox pis olmayanlar, 34 ştat) müqayisəyə daxil edildi.

- California-nın post/pre RMSPE nisbəti: **3.28**
- Rank: **9 / 34** (1 = ən güclü effekt)
- Pseudo p-value: **0.265**

Bu, klassik Abadie (2010) tədqiqatındakı qədər ekstremal (rank 1) deyil. Əsas səbəb — bizim modeldə yalnız `retprice` istifadə edilib (orijinal tədqiqatda əlavə olaraq `lnincome`, `beer`, `age15to24` də istifadə olunurdu, bunlar datada boşluğa görə çıxarıldı). Buna baxmayaraq, California yaxşı-fit ştatlar arasında ən yüksək nisbətlərin ilk üçdə birində (top ~26%) qalır.

## 5. Honest Interpretation

**Nə deyə bilərik:**
- 1989–2000 arası California-da adam başına siqaret satışı, sintetik California ilə müqayisədə illik ortalama ~20 paçka aşağı olub.
- Fərq 1989-dan dərhal sonra başlayır və zamanla böyüyür — vaxt baxımından müdaxilə ilə üst-üstə düşür.
- Placebo nəticəsi (top ~26%) effektin tam təsadüfi olmadığına dəlalət edir.

**Nə deyə bilmərik:**
- Bu, effektin 100% yalnız Proposition 99-a görə olduğunun sübutu deyil. Pseudo p-value (0.265) klassik 0.05 həddindən yüksəkdir.
- Datadakı boşluqlara görə (lnincome, beer, age15to24) tam predictor dəsti istifadə edilə bilmədi — bu, Synthetic Control-un dəqiqliyini məhdudlaşdırır.
- Nəticə yalnız California-nın bu dövrdəki özünəməxsus şəraitinə aiddir, başqa kontekstə birbaşa ümumiləşdirilə bilməz.

**Əsas təhlükələr (threats to validity):**
1. **Eyni vaxtda baş verən digər siyasətlər** — 1990-cı illərdə California-da paralel tütünə-qarşı tədbirlər (ictimai yerlərdə siqaret qadağaları, media kampaniyaları) də olub; bunlar Proposition 99-un təsirindən ayırd edilə bilmir.
2. **Missing data** — üç predictordan (lnincome, beer, age15to24) yalnız retprice istifadə edilə bildi.
3. **Spillover effektlər** — sərhədyanı ştatlarda (məs. Nevada) California sakinləri ucuz siqaret ala bilərdi, bu, control ştatların "təmiz" olması fərziyyəsini poza bilər (SUTVA pozulması).
4. **Statistik gücün məhdudluğu** — yalnız 39 ştat/vahid olduğu üçün placebo-əsaslı inference-in gücü aşağıdır (pseudo p-value 0.05-dən çox uzaqdır).
