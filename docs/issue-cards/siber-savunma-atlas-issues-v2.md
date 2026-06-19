# siber-savunma-atlas — Issue Kartları (v2)

**v1'den farklar:** Issue 1 trend-report'a taşındı ve Tier 2'ye düştü · metodoloji ağırlığı içerik türüne göre 3 katmana ayrıldı · checklist/defensive-lesson için ayrı Safety Checklist · Ransomware-as-Cover'da attribution dili sıkılaştırıldı · "Suggested Starting Sources" → "Suggested Source Types to Verify" · Methodology dosyası maintainer-written ilk commit olarak geliyor, issue olarak beklemiyor · Contributor Rights / No Ownership Claim maddesi eklendi · Wave 1/2/3 açılış sıralaması tanımlandı.

---

## A. Metodoloji Ağırlık Katmanları (tüm issue'lar buna göre sınıflandı)

| Katman | İçerik türleri | Gereksinim |
|---|---|---|
| **Hafif** (Tier 1) | checklist, defensive-lesson | Verified Facts/Assessment ayrımı YOK. Ayrı, basit bir Safety Checklist kullanılır (aşağıda Tip B). Admiralty metadata YOK. |
| **Orta** (Tier 2) | sector-risk-note (attribution-sensitive olmayanlar) | Verified Facts/Assessment ayrımı VAR. Source Reliability/Information Reliability sözel ölçekte (Yüksek/Orta/Düşük), Admiralty A-F/1-6 kodu zorunlu değil. |
| **Ağır** (Tier 2 trend-report / Tier 3) | incident-brief, threat-trend-report, attribution-sensitive sector-risk-note | Verified Facts/Assessment ayrımı VAR. Tam Admiralty Scale metadata zorunlu: `source_reliability` (A–F), `information_reliability` (1–6), `confidence_code` (örn. B2), `estimative_probability`, `independent_sources_count`, `archived_sources_count`. |

## B. İki Safety Checklist Tipi

**Tip A — Olgu/yargı içeren türler (incident-brief, trend-report, sector-risk-note, methodology):**
- [ ] Exploit/PoC yok
- [ ] Malware örneği yok
- [ ] C2 kurulumu yok
- [ ] Gerçek hedef/kurban bilgisi yok
- [ ] Credential/leaked data yok
- [ ] Jailbreak/bypass prompt yok
- [ ] Politik attribution teknik kaynak olmadan yok
- [ ] Kaynak ve arşiv linkleri var
- [ ] Verified Facts / Analyst Assessment ayrımı var
- [ ] Contributor Rights / No Ownership Claim onaylandı (bkz. PR template)

**Tip B — Pratik/uygulamalı türler (checklist, defensive-lesson):**
- [ ] Kaynaklar eklendi
- [ ] Öneriler uygulanabilir ve somut
- [ ] Ürün/marka reklamı yok
- [ ] Gerçek credential/leaked data yok
- [ ] Exploit/PoC veya çalışan kötüye kullanım adımı yok
- [ ] Contributor Rights / No Ownership Claim onaylandı (bkz. PR template)

## C. Contributor Rights / No Ownership Claim (PR template'e sabit madde olarak eklenir)

> Katkı sağlayan kişi içerikte görünür credit alır (PR'da contributor olarak listelenir, README'deki Contributors bölümüne eklenir). Katkı, **bu reponun lisansına tabidir** (*subject to the repository license*) ve o lisansın izin verdiği ölçüde organize edilebilir, yayınlanabilir, arşivlenebilir ve rapor/eğitim materyali/veri seti/araç/ürün gibi türev çalışmalarda kullanılabilir. Katkı sağlamak ortaklık, gelir payı, ürün sahipliği veya lisans kapsamının dışında bir hak talebi doğurmaz.

Her PR, bu maddeyi onaylayan bir checkbox içermeden merge edilmez.

## D. Açılış Sırası (Wave Yapısı)

| Wave | İçerik | GitHub'da ne zaman açılır |
|---|---|---|
| **Wave 1** | **GitHub'da issue olarak açılacak: 4 adet** (Tier 1). Methodology dosyası issue değildir, ilk commit'te repoya hazır olarak eklenir. | **Şimdi** |
| **Wave 2** | sector-risk-notes (4) + trend-reports (2) | Wave 1 issue'larından en az biri merge olduktan sonra |
| **Wave 3** | incident-brief + attribution-sensitive (2) | Wave 2'den en az 2 katkıcı Tier 2'ye ulaştıktan sonra |

---

# WAVE 1 — Şimdi Açılacak

**GitHub'da issue olarak açılacak: aşağıdaki 4 kart.** Issue 5 (methodology) bir GitHub issue'su değildir, ayrı alt başlıkta "ilk commit dosyası" olarak yer alıyor.

## Issue 1 (W1)

**Issue Title:** [CHECKLIST] Public GitHub Repositories and Secret Leakage Checklist

**Repository:** siber-savunma-atlas

**Content Type:** defense-checklist

**Trust Tier:** Tier 1 — Hafif metodoloji

**Goal:** Geliştiricilerin/küçük ekiplerin GitHub'da herkese açık repolarda yanlışlıkla API key, token, parola veya bağlantı dizesi sızdırmasını önlemek için uygulanabilir bir kontrol listesi üretmek.

**Scope:** Yaygın sızıntı türleri (commit geçmişinde unutulan secret, .env dosyası, hardcoded credential), önleyici araçlar (pre-commit hook, secret scanning, gitignore disiplini), sızıntı tespit edilirse yapılacaklar.

**Out of Scope:** Gerçek sızdırılmış bir secret/token örneği, belirli bir reponun/şirketin teşhiri, aktif olarak kötüye kullanılabilecek arama sorgusu (dork) listesi.

**Required Output:** `defense-checklists/public-github-secret-leakage-checklist.md`

**Required Sections:** Context, Checklist Items (madde madde, uygulanabilir), Why This Matters, Sources. *(Verified Facts/Analyst Assessment ayrımı bu içerik türünde zorunlu değil.)*

**Source Requirements:** En az 2 bağımsız kaynak (araç/yöntem önerileri için). Admiralty metadata gerekmiyor.

**Research Method Notes:** Bu içerik olay analizi değildir, doğrudan uygulanabilir bir kontrol listesidir; önerilen her araç/yöntem için kaynak gösterilmelidir.

**Suggested Source Types to Verify:** GitHub'ın resmi secret scanning dokümantasyonu (source to verify), OWASP Secrets Management Cheat Sheet (source to verify), GitGuardian/TruffleHog gibi açık kaynak araçların resmi dokümantasyonu (source to verify).

**Labels:** `defense-checklist`, `Tier-1`, `good-first-issue`, `wave-1`

**Acceptance Criteria:** En az 8 uygulanabilir checklist maddesi; her araç önerisi kaynaklı; gerçek sızıntı örneği yok; maintainer onayı.

**Safety Checklist:** Tip B (yukarıdaki Bölüm B)

---

## Issue 2 (W1)

**Issue Title:** [CHECKLIST] KOBİ Siber Hijyen Minimum Kontrol Listesi

**Repository:** siber-savunma-atlas

**Content Type:** defense-checklist

**Trust Tier:** Tier 1 — Hafif metodoloji

**Goal:** Türkiye'deki KOBİ'ler için bütçe/personel kısıtlarını göz önünde bulundurarak uygulanabilir, minimum düzeyde siber hijyen kontrol listesi üretmek.

**Scope:** MFA, yedekleme, yama yönetimi, parola politikası, e-posta güvenliği, çalışan farkındalığı gibi düşük maliyetli ama etkili kontroller; öncelik sıralaması.

**Out of Scope:** Kurumsal/büyük ölçekli güvenlik mimarisi önerileri, belirli bir ürün/marka reklamı.

**Required Output:** `defense-checklists/kobi-siber-hijyen-minimum-kontrol-listesi.md` (Türkçe, `language: "tr"`)

**Required Sections:** Context, Checklist Items (öncelik sırasına göre), Why This Matters, Sources.

**Source Requirements:** En az 2 bağımsız kaynak. Admiralty metadata gerekmiyor.

**Research Method Notes:** Liste maddeleri genel best-practice kaynaklarından derlenir, uydurulmaz.

**Suggested Source Types to Verify:** CISA Cyber Essentials (source to verify), NCSC (UK) Small Business Guide (source to verify), ENISA KOBİ siber güvenlik rehberleri (source to verify), USOM/BTK genel güvenlik tavsiyeleri (source to verify).

**Labels:** `defense-checklist`, `Tier-1`, `good-first-issue`, `wave-1`

**Acceptance Criteria:** En az 10 madde, önceliklendirilmiş; en az 2 kaynak; maintainer onayı.

**Safety Checklist:** Tip B

---

## Issue 3 (W1)

**Issue Title:** [DEFENSIVE-LESSON] MFA Alone Is Not Enough Against Session Hijacking

**Repository:** siber-savunma-atlas

**Content Type:** defensive-lesson

**Trust Tier:** Tier 1 — Hafif metodoloji

**Goal:** "MFA açtım, güvendeyim" yanılgısını düzeltmek; session/cookie hijacking, AiTM phishing gibi MFA'yı atlayan tekniklerin var olduğunu kavram düzeyinde açıklamak ve ek kontrol önerisi vermek.

**Scope:** MFA'nın koruduğu/korumadığı senaryoların kavramsal açıklaması, ek savunma katmanları (token binding, conditional access, oturum süresi kısıtlama).

**Out of Scope:** AiTM phishing kit kurulum adımları, session hijacking için çalışan araç/script, gerçek saldırı örneğinin teknik detayı.

**Required Output:** `defensive-lessons/mfa-alone-not-enough-session-hijacking.md`

**Required Sections:** The Lesson, Why It's Commonly Misunderstood, Real-World Illustration (genel, isimsiz örnek), Recommended Control, Sources.

**Source Requirements:** En az 2 bağımsız kaynak. Admiralty metadata gerekmiyor.

**Research Method Notes:** "Real-World Illustration" belirli bir olayın detaylı anlatımı değil, kavramı somutlaştıran genel bir örnektir.

**Suggested Source Types to Verify:** Microsoft AiTM phishing/token theft tehdit raporları (source to verify), CISA phishing-resistant MFA rehberleri (source to verify), NIST SP 800-63B kimlik doğrulama rehberi (source to verify).

**Labels:** `defensive-lesson`, `Tier-1`, `good-first-issue`, `wave-1`

**Acceptance Criteria:** Kavram doğru ve net açıklanmış; en az 2 kaynak; en az 2 uygulanabilir ek kontrol; teknik istismar adımı yok; maintainer onayı.

**Safety Checklist:** Tip B

---

## Issue 4 (W1)

**Issue Title:** [DEFENSIVE-LESSON] Backups Are Not a Ransomware Strategy Unless Tested

**Repository:** siber-savunma-atlas

**Content Type:** defensive-lesson

**Trust Tier:** Tier 1 — Hafif metodoloji

**Goal:** "Yedeğimiz var, güvendeyiz" yanılgısını düzeltmek; test edilmemiş yedeklerin ransomware krizinde işe yaramama riskini açıklamak ve test/kurtarma disiplini önerisi vermek.

**Scope:** Yedeklemenin var olması ile çalışır olması arasındaki fark, yaygın başarısızlık noktaları, test disiplini önerileri.

**Out of Scope:** Belirli bir ransomware ailesinin yedek hedefleme tekniğinin teknik detayı, gerçek bir kurumun olay anlatımı.

**Required Output:** `defensive-lessons/backups-not-ransomware-strategy-unless-tested.md`

**Required Sections:** The Lesson, Why It's Commonly Misunderstood, Real-World Illustration (genel, isimsiz), Recommended Control, Sources.

**Source Requirements:** En az 2 bağımsız kaynak. Admiralty metadata gerekmiyor.

**Research Method Notes:** Genelleme iddiaları yalnızca kaynaklı bir rapor varsa kesin dille yazılır.

**Suggested Source Types to Verify:** CISA #StopRansomware yedekleme rehberleri (source to verify), NIST SP 800-184 siber olay kurtarma rehberi (source to verify), bağımsız güvenlik araştırma şirketlerinin ransomware kurtarma anket raporları (source to verify, ticari önyargıya dikkat).

**Labels:** `defensive-lesson`, `Tier-1`, `good-first-issue`, `wave-1`

**Acceptance Criteria:** En az 2 kaynak; immutable/offline yedek ve test disiplini önerisi net; gerçek olay verisi yok; maintainer onayı.

**Safety Checklist:** Tip B

---

## Issue 5 — İLK COMMIT DOSYASI, GitHub Issue Olarak Açılmaz

**Issue Title:** [METHODOLOGY] Verified Facts vs Analyst Assessment Guide *(referans amaçlı başlık — GitHub Issues sekmesinde görünmeyecek)*

**Repository:** siber-savunma-atlas

**Content Type:** methodology

**Trust Tier:** maintainer

**Durum:** Bu, dışarıdan bir katkıcının üstleneceği bir issue değildir. Repo açılışıyla birlikte **ilk commit'te** maintainer tarafından yazılmış halde repoda bulunur, çünkü diğer tüm Wave 2/3 issue'ları PR review sırasında bu dosyaya referans verir — sıralama tersine çevrilemez. GitHub'da görünür bir issue olarak açılırsa, başlığına `[MAINTAINER TASK]` öneki eklenir ve "assigned to: repo owner" olarak işaretlenir, "help wanted" etiketi almaz.

**Goal:** Katkıcıların "doğrulanmış olgu" ile "analist yorumu" arasındaki farkı somut örneklerle anlayabileceği, diğer tüm issue template'lerinin referans verdiği temel metodoloji rehberini üretmek.

**Scope:** İki kategorinin tanımı, en az 3 "önce/sonra" örneği (kurgusal), Estimative Language tablosu, Admiralty Scale'e kısa referans, hangi içerik türünün hangi metodoloji ağırlığını taşıdığını gösteren tablo (bkz. bu dosyanın A bölümü).

**Out of Scope:** Gerçek vaka detayı, Tamga'nın kendi yayınlanmış içeriğinden alınmış örnek.

**Required Output:** `methodology/facts-vs-assessment.md`

**Required Sections:** Purpose, Definitions, Worked Examples (3+ önce/sonra), Estimative Language Reference Table, Methodology Weight Tiers (Bölüm A'nın kopyası), Common Mistakes, Reviewer Checklist Reference.

**Source Requirements:** En az 2 kaynak (istihbarat/araştırma metodolojisi).

**Suggested Source Types to Verify:** MISP Project "Best Practices in Threat Intelligence" dokümantasyonu (source to verify), ABD İstihbarat Topluluğu ICD 203 estimative language standardı (source to verify), Bellingcat açık kaynak araştırma metodolojisi rehberleri (source to verify).

**Labels:** `methodology`, `maintainer-task`, `wave-1`

**Acceptance Criteria:** Repo public olduğu anda bu dosya zaten mevcut olmalı; sonradan eklenen her issue template'i buna link verir.

**Safety Checklist:** Tip A

---

# WAVE 2 — Wave 1'den en az 1 merge sonrası açılır

## Issue 6 (W2)

**Issue Title:** [TREND-REPORT] Crisis-Period Phishing and Smishing Risks in Türkiye

*(v1'de incident-brief olarak yanlış sınıflandırılmıştı — tek olay değil, tekrar eden desen incelediği için trend-report'a taşındı.)*

**Repository:** siber-savunma-atlas

**Content Type:** threat-trend-report

**Trust Tier:** Tier 2 — Ağır metodoloji (trend-report sınıfı Admiralty metadata gerektirir)

**Goal:** Türkiye'de kriz dönemlerinde artan phishing/smishing kampanyalarının ortak desenini belgelemek ve savunma dersi çıkarmak.

**Scope:** Kriz dönemi tuzak temaları, dağıtım kanalları, hedefleme deseni, kamuya açık vaka örnekleri, savunma önerileri.

**Out of Scope:** Çalışan phishing kit kodu, aktif dolandırıcılık URL'leri, gerçek mağdur verisi, herhangi bir politik attribution.

**Required Output:** `threat-trend-reports/crisis-period-phishing-smishing-turkiye.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (A–F), Information Reliability (1–6), Confidence Code, Estimative Probability, Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 3 bağımsız kaynak. Desen/motivasyon iddiaları en az 2 bağımsız kaynak gerektirir. `independent_sources_count` ve `archived_sources_count` metadata alanları zorunlu.

**Örnek metadata (donup kalmamak için):**
```yaml
source_reliability: "B"
information_reliability: "2"
confidence_code: "B2"
estimative_probability: "likely"
independent_sources_count: 3
archived_sources_count: 2
```

**Research Method Notes:** Verified Facts yalnızca çok kaynaklı desenleri içerir. Analyst Assessment'taki yorum cümleleri "Likelihood: [estimative language]" formatında işaretlenir.

**Suggested Source Types to Verify:** USOM/BTK güvenlik bildirimleri (source to verify), ENISA Threat Landscape raporları (source to verify), APWG dönemsel raporları (source to verify), Microsoft/Proofpoint phishing trend raporları (source to verify).

**Labels:** `threat-trend-report`, `Tier-2`, `help-wanted`, `wave-2`

**Acceptance Criteria:** 3+ bağımsız/arşivlenmiş kaynak; tam Admiralty metadata dolu; en az 3 savunma önerisi; maintainer onayı.

**Safety Checklist:** Tip A

---

## Issue 7 (W2)

**Issue Title:** [TREND-REPORT] AI-Enabled Fraud Trends — Consumer/KOBİ Angle

**Repository:** siber-savunma-atlas

**Content Type:** threat-trend-report

**Trust Tier:** Tier 2 — Ağır metodoloji

**Goal:** AI destekli dolandırıcılık tekniklerinin tüketici/KOBİ için anlamını açıklamak, farkındalık önerisi üretmek.

**Scope:** **Tüketici/KOBİ açısı** — "bu mesajı/aramayı nasıl tanırsın". `ai-safety-lab`'deki AI-fraud içeriği **builder/ürün açısını** ele alır, çakışmaz; PR açıklamasına bu ayrımı not edin.

**Out of Scope:** Deepfake üretim rehberi, gerçek dolandırıcılık örneği/transkript, mağdur anlatımı, AI ürün güvenliği teknik detayı.

**Required Output:** `threat-trend-reports/ai-enabled-fraud-trends-consumer-kobi.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (A–F), Information Reliability (1–6), Confidence Code, Estimative Probability, Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 3 bağımsız kaynak; trend istatistiği kaynaksız yazılmaz.

**Örnek metadata:**
```yaml
source_reliability: "B"
information_reliability: "2"
confidence_code: "B2"
estimative_probability: "likely"
independent_sources_count: 3
archived_sources_count: 3
```

**Research Method Notes:** "AI dolandırıcılığı artıyor" gibi iddialar yalnızca kaynaklı istatistikle Verified Facts'e girer.

**Suggested Source Types to Verify:** FTC/Europol AI destekli dolandırıcılık uyarıları (source to verify), ENISA AI tehdit raporları (source to verify), Microsoft/Google AI kötüye kullanım şeffaflık raporları (source to verify), BTK/USOM tüketici uyarıları (source to verify).

**Labels:** `threat-trend-report`, `Tier-2`, `help-wanted`, `wave-2`

**Acceptance Criteria:** 3+ bağımsız kaynak; tüketici/KOBİ açısı net; tam Admiralty metadata; maintainer onayı.

**Safety Checklist:** Tip A

---

## Issue 8 (W2)

**Issue Title:** [SECTOR-RISK] Municipalities and Public Service Data Risk

**Repository:** siber-savunma-atlas

**Content Type:** sector-risk-note

**Trust Tier:** Tier 2 — Orta metodoloji (attribution-sensitive değil)

**Goal:** Belediyelerin neden artan oranda hedef olduğunu açıklamak, sektöre özel savunma kontrolleri önermek.

**Scope:** Veri türleri, yaygın saldırı vektörleri, hizmet kesintisinin toplumsal etkisi, kontrol önerileri.

**Out of Scope:** Belirli bir belediyenin gerçek olay verisi, sızdırılmış vatandaş verisi örneği, teknik istismar adımları.

**Required Output:** `sector-risk-notes/municipalities/public-service-data-risk.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (Yüksek/Orta/Düşük — sözel ölçek, A-F kodu zorunlu değil), Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 2 bağımsız kaynak.

**Research Method Notes:** Sektörel genellemeler yalnızca kurumsal/akademik kaynakla Verified Facts'e girer.

**Suggested Source Types to Verify:** ENISA kamu sektörü tehdit raporları (source to verify), CISA Cross-Sector Cybersecurity Performance Goals (source to verify), Türkiye'de KVKK kamuya açık ihlal bildirimi istatistikleri (source to verify).

**Labels:** `sector-risk-note`, `Tier-2`, `help-wanted`, `wave-2`

**Acceptance Criteria:** 2+ bağımsız kaynak; 4+ kontrol önerisi; gerçek olay verisi yok; maintainer onayı.

**Safety Checklist:** Tip A

---

## Issue 9 (W2)

**Issue Title:** [SECTOR-RISK] Universities as Credential Theft Targets

**Repository:** siber-savunma-atlas

**Content Type:** sector-risk-note

**Trust Tier:** Tier 2 — Orta metodoloji

**Goal:** Üniversitelerin kimlik bilgisi hırsızlığı açısından neden hedef olduğunu açıklamak, savunma önerisi üretmek.

**Scope:** Akademik açıklık/güvenlik dengesi, hedeflenen veri türleri, yaygın vektörler, kurumsal savunma önerileri.

**Out of Scope:** Gerçek olay verisi, çalışan kimlik avı şablonu, sızdırılmış öğrenci/personel verisi.

**Required Output:** `sector-risk-notes/education-universities/credential-theft-targets.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (sözel ölçek), Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 2 bağımsız kaynak.

**Suggested Source Types to Verify:** EDUCAUSE siber güvenlik raporları (source to verify), SANS yükseköğretim tehdit özetleri (source to verify), ENISA sektörel tehdit raporları (source to verify).

**Labels:** `sector-risk-note`, `Tier-2`, `help-wanted`, `wave-2`

**Acceptance Criteria:** 2+ bağımsız kaynak; 4+ kontrol; maintainer onayı.

**Safety Checklist:** Tip A

---

## Issue 10 (W2)

**Issue Title:** [SECTOR-RISK] SMEs and Ransomware Readiness

**Repository:** siber-savunma-atlas

**Content Type:** sector-risk-note

**Trust Tier:** Tier 2 — Orta metodoloji

**Goal:** KOBİ'lerin ransomware'e karşı hazırlıksızlığını açıklamak, minimum hazırlık kontrollerini listelemek.

**Scope:** Kaynak kısıtları, yaygın giriş vektörleri, düşük maliyetli kontroller.

**Out of Scope:** Gerçek olay verisi, çalışan ransomware örneği, fidye müzakere detayları.

**Required Output:** `sector-risk-notes/smes/ransomware-readiness.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (sözel ölçek), Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 2 bağımsız kaynak.

**Suggested Source Types to Verify:** CISA Stop Ransomware küçük işletme rehberleri (source to verify), ENISA KOBİ tehdit raporları (source to verify), NCSC (UK) küçük işletme rehberleri (source to verify).

**Labels:** `sector-risk-note`, `Tier-2`, `help-wanted`, `wave-2`

**Acceptance Criteria:** 2+ bağımsız kaynak; 5+ kontrol; maintainer onayı.

**Safety Checklist:** Tip A

---

## Issue 11 (W2)

**Issue Title:** [SECTOR-RISK] Healthcare Sector Ransomware: Minimum Defensive Controls

**Repository:** siber-savunma-atlas

**Content Type:** sector-risk-note

**Trust Tier:** Tier 2 — Orta metodoloji

**Goal:** Sağlık kurumlarının yüksek etkili ransomware hedefi olma nedenini açıklamak, minimum savunma kontrolleri önermek.

**Scope:** BT/OT karışık ortam riski, hasta verisi hassasiyeti, hizmet kesintisinin can güvenliği etkisi, segmentasyon/yedekleme öncelikleri.

**Out of Scope:** Gerçek olay verisi, hasta verisi örneği, tıbbi cihaz istismar detayları.

**Required Output:** `sector-risk-notes/healthcare/ransomware-minimum-controls.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (sözel ölçek), Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 2 bağımsız kaynak; "can güvenliği etkisi" gibi güçlü iddialar için en az 2 kurumsal kaynak.

**Suggested Source Types to Verify:** HHS/HC3 sağlık sektörü tehdit raporları (source to verify), ENISA sağlık sektörü tehdit raporları (source to verify), CISA sağlık sektörü rehberleri (source to verify).

**Labels:** `sector-risk-note`, `Tier-2`, `help-wanted`, `wave-2`

**Acceptance Criteria:** 2+ bağımsız kaynak; 4+ kontrol; maintainer onayı.

**Safety Checklist:** Tip A

---

# WAVE 3 — Wave 2'den en az 2 katkıcı Tier 2'ye ulaştıktan sonra açılır

## Issue 12 (W3)

**Issue Title:** [INCIDENT-BRIEF] Ransomware-as-Cover: Why Destructive Attacks May Look Financial

**Repository:** siber-savunma-atlas

**Content Type:** incident-brief

**Trust Tier:** Tier 3 — Ağır metodoloji, attribution-sensitive

**Goal:** "Ransomware-as-cover" kavramını kamuya açık, çok kaynaklı vakalar üzerinden açıklamak; olay müdahale ekiplerinin motivasyonu fidye notuna bakarak otomatik sınıflandırmaması gerektiği dersini çıkarmak.

**Scope:** Kavramın tanımı, 1-2 kamuya açık ve geniş çapta belgelenmiş örnek (olay örgüsü/etki düzeyinde, teknik adım değil), erken sınıflandırma hatalarını önleyici kontrol listesi.

**Out of Scope:** Wiper'ın teknik çalışma mekanizması, henüz net kamuya açıklanmamış olayların spekülatif sınıflandırması. **Hiçbir devlet/aktör bu içerikte kesin fail olarak yazılamaz.** Yalnızca "public reporting has associated..." veya "open-source reports have linked..." formundaki temkinli dil kullanılabilir; "X did this" veya "X devleti bunu yaptı" formundaki kesin ifadeler PR'da reddedilir.

**Required Output:** `incident-briefs/ransomware-as-cover-destructive-attacks.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (A–F), Information Reliability (1–6), Confidence Code, Estimative Probability, Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 3 bağımsız kaynak; seçilen vaka için en az 2 farklı güvenlik şirketi/kurum raporu çapraz kullanılmalı. Tek kaynaklı motivasyon iddiası kabul edilmez.

**Örnek metadata (attribution-sensitive içerikte confidence genelde düşük/orta kalır, bu normaldir):**
```yaml
source_reliability: "B"
information_reliability: "3"
confidence_code: "B3"
estimative_probability: "roughly even chance"
independent_sources_count: 3
archived_sources_count: 2
attribution: "publicly reported"
```

**Research Method Notes:** Verified Facts yalnızca çok kaynaklı doğrulanmış gözlemleri içerir. Analyst Assessment'taki yorumlar "Likelihood: [estimative language]" formatında, olgu değil değerlendirme olarak yazılır.

**Suggested Source Types to Verify:** ESET Research wiper/destructive malware analizleri (source to verify), Mandiant/Google Cloud tehdit raporları (source to verify), CISA ortak uyarıları (source to verify).

**Labels:** `incident-brief`, `Tier-3`, `needs-sources`, `attribution-sensitive`, `wave-3`

**Acceptance Criteria:** Kavram doğru tanımlanmış; en az bir vaka 2+ bağımsız kaynakla desteklenmiş; attribution dili yalnızca temkinli formda; tam Admiralty metadata; maintainer onayı **zorunlu**.

**Safety Checklist:** Tip A

---

## Issue 13 (W3)

**Issue Title:** [SECTOR-RISK] Defense Industry Suppliers and Supply Chain Exposure

**Repository:** siber-savunma-atlas

**Content Type:** sector-risk-note (attribution-sensitive — Tier 3'e yükseltildi)

**Trust Tier:** Tier 3 — Ağır metodoloji, attribution-sensitive

**Goal:** Savunma sanayii tedarikçilerinin casusluk/tedarik zinciri operasyonları için neden hedef olduğunu genel düzeyde açıklamak, tedarik zinciri güvenliği önerileri üretmek.

**Scope:** Tedarik zinciri risk kategorileri (SBOM, kod imzalama, tedarikçi denetimi), alt yüklenici/ana yüklenici güven ilişkisi riski, genel sektörel öneriler.

**Out of Scope:** Belirli bir Türk savunma şirketinin adı, belirli bir geçmiş/devam eden olayın detaylı anlatımı, herhangi bir devlete kesin atıf, gerçek proje/ürün adı.

**Required Output:** `sector-risk-notes/defense-industry-suppliers/supply-chain-exposure.md`

**Required Sections:** Verified Facts, Analyst Assessment, Sources, Archived Sources, Source Reliability (A–F), Information Reliability (1–6), Confidence Code, Türkiye Relevance, Defensive Lessons.

**Source Requirements:** En az 3 bağımsız kaynak. Motivasyon/aktör iddiası en az 2 bağımsız kaynak gerektirir.

**Research Method Notes:** Bu not **genel tedarik zinciri risk kategorisi** üzerinedir, belirli şirket/vaka anlatımı değildir. Kamuya açık örnek kullanılacaksa yalnızca zaten çok kaynaklı, kategori-temsili örnekler kullanılır, Türkiye'ye özel hiçbir şirket/proje adı anılmaz.

**Suggested Source Types to Verify:** NIST SP 800-161 tedarik zinciri risk yönetimi rehberi (source to verify), CISA SBOM kaynakları (source to verify), ENISA tedarik zinciri tehdit raporları (source to verify).

**Labels:** `sector-risk-note`, `Tier-3`, `attribution-sensitive`, `needs-sources`, `wave-3`

**Acceptance Criteria:** Hiçbir gerçek şirket/proje adı yok; 3+ bağımsız kaynak; 4+ kontrol; maintainer onayı **zorunlu**, otomatik merge edilemez.

**Safety Checklist:** Tip A + ek madde: `[ ] Gerçek şirket/proje adı yok`
