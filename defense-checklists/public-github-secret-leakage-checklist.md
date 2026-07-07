# Public GitHub Repositories and Secret Leakage Checklist

> **Proje:** siber-savunma-atlas · **Kapsam:** Geliştiriciler, Öğrenciler, KOBİ ve Açık Kaynak Ekipleri · **Dil:** Türkçe  
> **Son Güncelleme:** Temmuz 2026 

---

## Executive Summary

Herkese açık GitHub depolarında yanlışlıkla paylaşılan API anahtarları, veritabanı parolaları, OAuth token'ları ve bulut kimlik bilgileri; saldırganlar tarafından dakikalar içinde tespit edilip kötüye kullanılabilir. Bu tür sızıntılar yalnızca bireysel geliştiricileri değil, bağlı oldukları organizasyonları, müşterilerini ve kullandıkları bulut altyapısını da doğrudan riske atar.

Bu belge, herkese açık depolarda gizli bilgi sızıntısını önlemeye yönelik savunma odaklı bir kontrol listesi sunmaktadır. Geliştiriciler, öğrenciler, açık kaynak katkıcıları ve küçük-orta ölçekli ekipler tarafından doğrudan uygulanabilecek pratik adımlardan oluşmaktadır. Belge; saldırı yöntemlerini değil, yapılandırma kontrollerini, araç kullanımını ve olay müdahale sırasını kapsar.

Bir sır bir kez herkese açık bir depoya gönderildiğinde, kısa süre sonra silinmiş olsa dahi, tehlikeye girmiş kabul edilmelidir. Bu nedenle önleme; tespit ve müdahaleden çok daha az maliyetlidir.

---

## Context

Git; değişiklikleri zaman damgasıyla birlikte saklayan ve bu geçmişi varsayılan olarak koruyan bir versiyon kontrol sistemidir. Bu tasarım, işbirliğini kolaylaştırmakla birlikte bir güvenlik açısını da beraberinde getirir: depoya bir kez gönderilen her içerik — sonradan silinmiş olsa dahi — Git geçmişinde iz bırakır ve bu iz teknik bilgiye sahip herhangi biri tarafından erişilebilir durumdadır.

Herkese açık depolarda gizli bilgi sızıntısını özellikle riskli kılan birkaç etken vardır. Birincisi, otomatik tarama araçları GitHub üzerindeki commit akışını sürekli izler ve yeni eklenen sırları dakikalar içinde tespit eder. İkincisi, bir deponun "herkese açık" olarak yanlışlıkla yapılandırılması — ya da başlangıçta özel olan bir deponun sonradan kamuya açılması — geçmişteki tüm sızıntıları anında erişilebilir kılar. Üçüncüsü, fork mekanizması nedeniyle bir depo kamuya açıldıktan sonra içeriğin tamamıyla kaldırılması teknik olarak güvence altına alınamaz.

GitHub Secret Scanning, GitGuardian ve benzeri araçların yaygınlaşması; sızıntı tespitini hızlandırmakla birlikte bu araçlara erişimin yalnızca savunma tarafıyla sınırlı olmadığını unutmamak gerekir. Güvenli yazılım geliştirme pratiğinin temel kuralı, sırların depoya hiçbir zaman ulaşmamasıdır — tespit edilip temizlenmesine değil.

---

## Türkiye Relevance

Türkiye'deki yazılım geliştirme topluluğu, açık kaynak katkıcıları, üniversite öğrencileri ve erken aşama startup'lar GitHub'u yoğun biçimde kullanmaktadır. Bu kullanım yaygınlıkla birlikte güvenlik alışkanlıklarındaki boşlukları da gündeme getirir.

**Öğrenciler ve bireysel geliştiriciler:** Ders projeleri, portfolio depoları ve hackathon çalışmaları sıkça herkese açık olarak paylaşılır. Bu depolarda yer alan `.env` dosyaları, sabit kodlanmış API anahtarları veya veritabanı bağlantı bilgileri; kullanım bittikten çok sonra bile erişilebilir kalmaya devam edebilir. İş başvurularında paylaşılan GitHub profilleri bu riskin görünürlüğünü daha da artırır.

**KOBİ'ler ve startup'lar:** Küçük ekiplerde güvenlik rolleri çoğunlukla net biçimde ayrılmamıştır. Geliştirici aynı zamanda sistem yöneticisi ve DevOps sorumlusu olabilir. Bu durumda güvenli yapılandırma pratiklerinin bilinmemesi; bulut faturası şoklarına, veri ihlallerine ve müşteri güven kaybına yol açabilir.

**KVKK yükümlülükleri:** Türkiye'de 6698 sayılı Kişisel Verilerin Korunması Kanunu kapsamında, bir GitHub deposunda kullanıcı verilerine erişim sağlayan kimlik bilgilerinin sızması doğrudan bir veri ihlali sayılabilir. Bu durum KVKK bildirimi yükümlülüğünü ve idari yaptırım riskini beraberinde getirir. Bulut API anahtarlarının açıkta kalması ise hem müşteri verilerini hem de organizasyonun altyapısını tehlikeye atar.

**Açık kaynak toplulukları:** Türkiye'de büyüyen açık kaynak ekosisteminde katkıcılar, güvenli geliştirme pratiklerini erken benimsemek hem bireysel itibar hem de topluluk güvenliği açısından kritik bir sorumluluktur. Kötü yapılandırılmış bir fork veya test deposu, ana projeyi de dolaylı biçimde olumsuz etkileyebilir.

---

## Practical Checklist

### 1. Depo Oluşturulmadan Önce

- [ ] **Deponun görünürlük ayarı, içerik kararından önce belirlenir.**  
  Yeni bir depo oluştururken varsayılan görünürlüğü organizasyonunuzun politikasına göre ayarlayın. Herkese açık olarak başlatılması planlanan bir depo için bile ilk commit'ten önce hangi içeriklerin dahil edileceği gözden geçirilmelidir. Bir depo özel olarak başlatılıp sonradan kamuya açılacaksa, tüm geçmiş commit'ler o ana kadar yapılmış sızıntılar dahil erişilebilir hale gelir.

- [ ] **`.gitignore` dosyası, ilk commit'ten önce oluşturulur ve gizli bilgi içerebilecek tüm dosya türlerini kapsar.**  
  GitHub'ın önerdiği dile ve çerçeveye özel `.gitignore` şablonlarını başlangıç noktası olarak kullanın. Buna ek olarak `.env`, `.env.local`, `.env.production`, `*.pem`, `*.key`, `config/secrets.*`, `credentials.json` gibi yaygın gizli dosya adlarını açıkça listeleyin. `.gitignore` dosyasının kendisinin de depoya eklendiğinden ve tüm ekip üyelerinin sisteminde geçerli olduğundan emin olun.

- [ ] **Gizli bilgiler için bir yönetim yöntemi, kod yazılmadan önce belirlenir.**  
  Sırlar doğrudan kod içine veya yapılandırma dosyalarına yazılmamalıdır. Ortam değişkenleri, şifreli vault çözümleri (HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, GitHub Actions Secrets) veya yerel `.env` dosyaları — depo dışında yönetilmek koşuluyla — kabul edilebilir yaklaşımlardır. Hangi yöntemin kullanılacağı ekip içinde açıkça kararlaştırılmalı ve belgelenmelidir.

---

### 2. Geliştirme Sürecinde

- [ ] **Her commit gönderilmeden önce, değiştirilen dosyalar gizli bilgi açısından gözden geçirilir.**  
  `git diff --staged` komutuyla hangi içeriklerin commit'e dahil edildiğini her seferinde kontrol edin. Bu alışkanlık, özellikle hızlı geliştirme dönemlerinde otomatik araçlarla desteklenmelidir. Bir dosyayı `.gitignore`'a eklemek, o dosyanın daha önce izlenmişse takip edilmesini otomatik olarak durdurmaz; `git rm --cached` ile izlemeyi açıkça kaldırın.

- [ ] **Pre-commit hook'ları veya yerel tarama araçları, geliştirici ortamında etkinleştirilir.**  
  `gitleaks`, `truffleHog`, `detect-secrets` gibi araçlar commit gönderilmeden önce içerikleri tarar ve gizli bilgi tespit ettiğinde işlemi durdurur. Bu araçları `pre-commit` framework'ü aracılığıyla ekip genelinde zorunlu hale getirin. Araç yapılandırmasını (`.gitleaks.toml`, `.pre-commit-config.yaml` gibi) deponun kendisinde tutun; böylece yeni ekip üyeleri aynı kontrolleri otomatik olarak devralır.

- [ ] **CI/CD pipeline'ında otomatik gizli bilgi taraması çalıştırılır.**  
  Her pull request veya merge işleminde gizli bilgi taraması yapan bir adım ekleyin. GitHub Advanced Security, GitGuardian veya açık kaynak alternatifleri bu amaçla kullanılabilir. Tarama sonuçları PR onay sürecinin bir parçası haline getirilmeli; tarama başarısız olduğunda birleştirme (merge) engellenmeli ve ilgili kişiler bilgilendirilmelidir.

- [ ] **GitHub Secret Scanning ve push protection özellikleri etkinleştirilir.**  
  GitHub; bilinen API anahtarı formatlarını otomatik olarak tespit eden yerleşik bir tarama özelliği sunar. Organizasyon veya depo ayarlarından "Secret scanning" ve "Push protection" seçeneklerinin açık olduğunu doğrulayın. Push protection; bilinen bir gizli bilgi formatı içeren bir commit'in depoya gönderilmesini otomatik olarak engeller.

- [ ] **Kişisel erişim token'ları (PAT) ve servis hesabı kimlik bilgileri, yalnızca gerekli izinlere sahip olacak şekilde yapılandırılır.**  
  Token oluştururken en az yetki (principle of least privilege) ilkesini uygulayın. Yalnızca belirli bir repo için okuma erişimine ihtiyaç varsa, tüm organizasyona yazma yetkisi veren bir token kullanmayın. Token'lara son kullanma tarihi belirleyin ve bu tarihleri takip edin. Kullanılmayan token'ları derhal iptal edin.

---

### 3. Depo Yönetiminde

- [ ] **Deponun işbirlikçi listesi ve erişim izinleri düzenli aralıklarla gözden geçirilir.**  
  Artık aktif olmayan katkıcıların erişimini kaldırın. Fork'ların ve bağlı uygulamaların listesini inceleyin. Organizasyon düzeyinde SAML SSO veya iki faktörlü doğrulama (2FA) zorunluluğunu devreye alın. Eski bir çalışanın erişiminin kaldırılması, o kişinin yerel olarak klonlamış olduğu içerikleri ortadan kaldırmaz; bu nedenle ayrılan kişilerin kullanmış olduğu token'lar ve kimlik bilgileri ayrıca yenilenmelidir.

- [ ] **Eski branch'ler, etiketler (tag) ve kapatılmış pull request'ler periyodik olarak temizlenir.**  
  Git geçmişinin yalnızca ana branch'te değil, tüm ref'lerde erişilebilir olduğunu unutmayın. Silinmiş gibi görünen bir branch, `git reflog` veya ağ (network) görünümü üzerinden erişilebilir kalabilir. Artık gerekli olmayan branch'leri depoya yazma yetkisi olan kişiler tarafından silin ve bu temizliği düzenli bir alışkanlık haline getirin.

- [ ] **Demo ve test depoları, üretim altyapısıyla aynı güvenlik standartlarında yönetilir.**  
  "Bu sadece bir demo" ya da "test ortamı" gerekçesiyle gizli bilgi yönetiminde taviz verilmemelidir. Demo depoları çoğunlukla gerçek API anahtarları veya bağlantı bilgileriyle doldurulur ve bu durum üretim ortamı kadar ciddi bir risk oluşturur. Demo amaçlı sahte (mock) veya kısıtlı yetkili kimlik bilgileri kullanın; gerçek kimlik bilgilerini bu depolardan tamamen uzak tutun.

---

### 4. Olay Müdahalesi (Incident Response)

Bir gizli bilginin herkese açık bir depoya ulaştığı tespit edildiğinde aşağıdaki sıra izlenmelidir:

- [ ] **1. Sızan sırrı derhal iptal edin veya yenileyin (revoke / rotate).**  
  Bu adım her şeyden önce ve gecikmeksizin atılmalıdır. Sızan bir sır; Git geçmişinden silinmemiş olsa dahi, eski değeri artık geçersizse kötüye kullanılamaz. Sırrı geçmişten silmeden önce iptal etmek, saldırganın erişim penceresini kapatır. Sızan bilginin tehlikeye girmiş olduğunu varsayın — kısa süre sonra fark edilmiş olsa bile.

- [ ] **2. Sırrın kullanılıp kullanılmadığını kontrol edin.**  
  İlgili servis sağlayıcısının (AWS, GitHub, Google Cloud vb.) erişim günlüklerini inceleyin. Sızan kimlik bilgisiyle yapılan her isteği zaman damgasıyla kayıt altına alın. Yetkisiz bir işlem tespit edilirse, bu adımı bir güvenlik olayı olarak ele alın ve organizasyonun olay müdahale sürecini başlatın.

- [ ] **3. Günlükleri ve erişim geçmişini inceleyin.**  
  Sızan sırrın kaç kez kullanıldığını, hangi IP adreslerinden erişim sağlandığını ve bu erişimlerin beklenen kullanım kalıplarıyla örtüşüp örtüşmediğini değerlendirin. Bu inceleme hem olayın kapsamını anlamak hem de yasal veya düzenleyici bildirim yükümlülüğünü değerlendirmek açısından gereklidir.

- [ ] **4. Sırrı depo geçmişinden uygun araçlarla kaldırın.**  
  `git filter-repo` veya BFG Repo Cleaner araçlarını kullanarak sırrı Git geçmişinden temizleyin. Bu işlem geçmişi yeniden yazdığından tüm katkıcıların yerel kopyalarını güncelleme ihtiyacı doğurur. Temizleme tamamlandıktan sonra GitHub desteğiyle önbelleğe alınmış görünümlerin kaldırılmasını talep edin. **Bu adımın tek başına yeterli olmadığını ve sırrın iptal edilmesinin yerini tutmadığını unutmayın.**

- [ ] **5. Olayı belgeleyin ve kontrolleri güncelleyin.**  
  Sızıntının nasıl gerçekleştiğini, hangi adımların atıldığını ve alınan önlemleri yazılı olarak kayıt altına alın. Aynı hatanın tekrarlanmaması için hangi süreçlerin veya araçların güncellenmesi gerektiğini belirleyin. Gerektiğinde ekip içinde kısa bir bilgilendirme yapın.

---

## Common Mistakes

**`.env` dosyalarını commit'lemek:** Bu dosyalar ortam değişkenlerini saklarken kolaylık sağlar; ancak `.gitignore`'a eklenmediğinde veya izleme listesinden çıkarılmadığında kolayca depoya dahil olur. `.env` dosyalarının hiçbir koşulda commit'lenmemesi gerekir. Şablon olarak `.env.example` dosyası tutulabilir; bu dosya gerçek değer içermemeli, yalnızca hangi değişkenlerin gerekli olduğunu göstermelidir.

**Bir dosyayı silmenin Git geçmişinden kaldırdığını varsaymak:** `git rm` veya dosyayı silerek yeni bir commit göndermek, o dosyanın önceki commit'lerde erişilebilir olmaya devam etmesini engellemez. Git geçmişi doğrusal ve kalıcıdır; geçmişi yeniden yazmak için `git filter-repo` gibi özel araçlar gerekir ve bu işlem tüm katkıcıları etkiler.

**Aşırı yetkilere sahip kişisel erişim token'ları (PAT) kullanmak:** Tek bir göreve yönelik token oluşturulurken kolaylık amacıyla tüm izinler seçilir. Bu token daha sonra sızarsa saldırgan geniş bir yetki alanına erişmiş olur. Her token yalnızca ihtiyaç duyduğu izinleri içermeli, son kullanma tarihi belirlenmeli ve görevi sona erdiğinde iptal edilmelidir.

**Sızdırılan sırları yenilememek (rotate etmemek):** Sızıntı fark edildiğinde bazı ekipler yalnızca dosyayı geçmişten silip işi bitmiş saymaktadır. Oysa sır silinmeden önce herhangi bir süre boyunca erişilebilir durumdaysa tehlikeye girmiş kabul edilmelidir. İptal ve yenileme her zaman birinci adım olmalıdır.

**Sadece manuel incelemeye güvenmek:** Gizli bilgi sızıntılarının büyük çoğunluğu; dikkatli gözden geçirme yerine otomatik araçlar tarafından tespit edilmektedir. Manuel inceleme tamamlayıcı bir katmandır, ancak tek başına yeterli değildir. Pre-commit hook'ları ve CI entegrasyonu, insan hatasına bağımlılığı önemli ölçüde azaltır.

**Eski commit'leri ve branch'leri görmezden gelmek:** Güvenlik incelemesi çoğunlukla mevcut durum üzerinden yapılır; ancak eski branch'ler, etiketler ve kapatılmış pull request'ler de Git geçmişinin bir parçasıdır. Sızıntı aramalarında yalnızca varsayılan branch değil tüm ref'ler taranmalıdır.

**Herkese açık demo depolarını "düşük riskli" olarak değerlendirmek:** Demo ve eğitim amaçlı depolar sıklıkla gerçek API anahtarları veya bağlantı bilgileriyle yapılandırılır ve ardından kamuya açılır. "Sadece bir demo" gerekçesi, üretim etkisi olan bir kimlik bilgisinin sızmasını hafifletmez. Demo ortamları için kısıtlı yetkili veya sahte (mock) kimlik bilgileri kullanılmalıdır.

---

## What This Content Deliberately Excludes

Bu belge aşağıdaki içerikleri kasıtlı olarak dışlamaktadır:

- Gerçek API anahtarları, token'lar, parolalar veya kimlik bilgileri
- Sızdırılan kimlik bilgilerinin nasıl kötüye kullanılacağına dair talimatlar
- Hedef ya da kurban örnekleri
- Sömürme (exploitation) adımları veya senaryoları
- Bulut altyapısı suistimal (abuse) iş akışları
- Kimlik bilgisi toplama (credential harvesting) yöntemleri
- Ofansif tarama (offensive scanning) araçlarının nasıl kullanılacağına dair rehberlik
- Bu kontrol listesinin gizli bilgi sızıntısını yüzde yüz engellediğine dair her türlü iddia

Bu belgenin amacı; saldırı yöntemlerini tanıtmak değil, geliştiricilerin ve ekiplerin güvenli geliştirme alışkanlıklarını somut adımlarla benimsemesine yardımcı olmaktır.

---

## Defensive Takeaways

**Sırlar depoya ulaşmadan önce engellenmelidir.** Tespit ve müdahale; önlemenin yerini tutmaz ve her zaman daha maliyetlidir. Pre-commit hook'ları, `.gitignore` yapılandırması ve CI entegrasyonu; savunmanın çekirdeğini oluşturur.

**Bir sır bir kez herkese açık hale geldiğinde tehlikeye girmiş kabul edilmelidir.** Kısa süre sonra fark edilmiş veya birkaç dakika sonra silinmiş olması, bu gerçeği değiştirmez. Otomatik tarama araçları depoları sürekli izler ve yeni içerikler dakikalar içinde işlenir.

**Olay müdahalesinde sırayı doğru kurun.** Geçmişi temizlemek değil, sırrı iptal etmek ilk adımdır. Sırrı geçerli ve aktif bırakarak yalnızca Git geçmişini temizlemek; saldırganın erişimini kapatmaz.

**En az yetki ilkesini token yönetiminin temeli yapın.** Her token, servis hesabı ve erişim anahtarı yalnızca ihtiyaç duyduğu izinlere sahip olmalı, son kullanma tarihi belirlenmeli ve kullanılmadığında derhal iptal edilmelidir.

**Demo ve test ortamları, güvenlik açısından üretim ortamıyla aynı standartta ele alınmalıdır.** "Düşük riskli" olarak sınıflandırılan depolar, gerçek kimlik bilgileri içerdiğinde bu sınıflandırma geçerliliğini yitirir.

**Güvenli geliştirme alışkanlıkları; araçlarla desteklenmeli, ekip içinde paylaşılmalı ve belgelenmeli** — tek bir kişinin bilgisinde kalmak yerine organizasyonel bir pratik haline getirilmelidir.

---

## Sources

1. **GitHub Docs — Secret Scanning**
   - Source title: About Secret Scanning
   - Publisher / organization: GitHub, Inc.
   - URL: [https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: GitHub'ın yerleşik gizli bilgi tarama özelliğini ve push protection mekanizmasını belgeleyen birincil kaynaktır. Hangi token formatlarının otomatik olarak tespit edildiği ve uyarıların nasıl yapılandırılacağı bu belgede açıklanmaktadır.

2. **OWASP — Secrets Management Cheat Sheet**
   - Source title: Secrets Management Cheat Sheet
   - Publisher / organization: OWASP Foundation
   - URL: [https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Gizli bilgi yönetiminin yaşam döngüsünü — oluşturma, saklama, dağıtım, yenileme ve iptal — kapsamlı biçimde ele alan, uygulamaya yönelik bir referans belgedir.

3. **NIST SP 800-57 — Recommendation for Key Management**
   - Source title: Recommendation for Key Management, Part 1: General
   - Publisher / organization: National Institute of Standards and Technology (NIST)
   - URL: [https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final](https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Kriptografik anahtarlar ve kimlik bilgileri için yaşam döngüsü yönetimi ilkelerini tanımlayan temel standarttır. En az yetki ve dönemsel yenileme gibi ilkelerin teknik dayanağını sağlar.

4. **git-filter-repo — Resmi Dokümantasyon**
   - Source title: git-filter-repo Documentation
   - Publisher / organization: newren (GitHub Projesi)
   - URL: [https://github.com/newren/git-filter-repo](https://github.com/newren/git-filter-repo)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Git geçmişinden hassas içeriklerin kaldırılması için Git ekibinin önerdiği araçtır. Olay müdahalesi sırasında geçmiş temizleme adımı bu araçla gerçekleştirilir.

5. **Gitleaks — Açık Kaynak Gizli Bilgi Tarama Aracı**
   - Source title: Gitleaks
   - Publisher / organization: gitleaks (GitHub Projesi)
   - URL: [https://github.com/gitleaks/gitleaks](https://github.com/gitleaks/gitleaks)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Pre-commit hook'u ve CI pipeline entegrasyonu için yaygın biçimde kullanılan, açık kaynak gizli bilgi tarama aracıdır. Bu kontrol listesindeki otomatik tarama adımlarının referans uygulamasını sağlar.

6. **KVKK — Kişisel Verilerin Korunması Kanunu**
   - Source title: 6698 Sayılı Kişisel Verilerin Korunması Kanunu
   - Publisher / organization: Kişisel Verileri Koruma Kurumu (KVKK)
   - URL: [https://www.kvkk.gov.tr/Icerik/6649/6698-SAYILI-KANUN](https://www.kvkk.gov.tr/Icerik/6649/6698-SAYILI-KANUN)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Türkiye'de kişisel verilere erişim sağlayan kimlik bilgilerinin sızması durumunda geçerli olan yasal çerçeveyi tanımlar. Veri ihlali bildirimi ve idari yaptırım konularında bağlayıcı hükümler içerir.

7. **CWE-312 — Cleartext Storage of Sensitive Information**
   - Source title: CWE-312: Cleartext Storage of Sensitive Information
   - Publisher / organization: MITRE Corporation
   - URL: [https://cwe.mitre.org/data/definitions/312.html](https://cwe.mitre.org/data/definitions/312.html)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Gizli bilgilerin şifrelenmemiş biçimde depolanmasını tanımlayan standarttır. Bu kontrol listesindeki güvenli yapılandırma maddelerinin teknik sınıflandırma dayanağını oluşturur.


