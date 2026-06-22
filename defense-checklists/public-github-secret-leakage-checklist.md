# GitHub'da Gizli Bilgi Sızıntısını Önleme Kontrol Listesi

> **Siber Savunma Atlası** | Savunma Kontrol Listeleri Serisi  
> Kategori: Kaynak Kodu Güvenliği · Sürüm: 1.0 · Dil: Türkçe

---

## Context

Herkese açık GitHub depoları, yazılım geliştirme ekosisteminin temel yapı taşlarından biridir. Ancak bu depolar; dikkat edilmediğinde API anahtarları, veritabanı bağlantı dizeleri, kimlik doğrulama token'ları ve parolalar gibi son derece hassas bilgilerin istemeden dünyayla paylaşılmasına zemin hazırlayabilir.

Gizli bilgilerin kaynak koduna gömülmesi, bireysel geliştiricilerin ve küçük ekiplerin sıklıkla düştüğü bir güvenlik tuzağıdır. Bir commit'e eklenen sır, depo geçmişinden silinse dahi izler bırakabilir; otomatik tarama botları bu bilgileri dakikalar içinde tespit edebilir.

Bu kontrol listesi; yazılımcılara ve küçük ekiplere, gizli bilgilerin herkese açık GitHub depolarına sızmasını **önlemek** için uygulanabilir, adım adım bir savunma çerçevesi sunar.

---

## Checklist Items

### 🔧 Geliştirme Ortamı Yapılandırması

- [ ] **Ortam değişkeni dosyalarını `.gitignore`'a ekle**  
  `.env`, `.env.local`, `.env.production` gibi tüm ortam değişkeni dosyaları, depo başlatılırken `.gitignore` dosyasına eklenmelidir. Boş bir `.gitignore` ile başlamak yerine dilin/framework'ün resmi şablonu kullanılmalıdır.

- [ ] **Gizli bilgileri kaynak koda doğrudan yazma; ortam değişkeni kullan**  
  Bağlantı dizeleri, API anahtarları ve kimlik bilgileri hiçbir zaman kod dosyasının içine sabit değer (hardcode) olarak yazılmamalıdır. Bunun yerine `os.environ.get("VAR_NAME")` veya benzeri dil yapıları tercih edilmelidir.

- [ ] **Şablon yapılandırma dosyası (`.env.example`) oluştur ve depoya ekle**  
  Gerçek değerler içermeyen, yalnızca hangi değişkenlerin gerektiğini gösteren bir `.env.example` dosyası depoya eklenmeli; ekip üyeleri bu dosyayı kopyalayarak kendi yerel ortamlarını oluşturmalıdır.

- [ ] **Gizli yönetim servisi kullan (Secret Manager)**  
  Bulut tabanlı projelerde gizli bilgiler; AWS Secrets Manager, Google Secret Manager veya HashiCorp Vault gibi özel servisler aracılığıyla yönetilmeli, kod deposuyla doğrudan ilişkilendirilmemelidir.

---

###  Commit Öncesi Koruma Katmanı

- [ ] **`pre-commit` hook ile otomatik tarama yap**  
  [git-secrets](https://github.com/awslabs/git-secrets), [detect-secrets](https://github.com/Yelp/detect-secrets) veya [gitleaks](https://github.com/gitleaks/gitleaks) gibi araçlar, her commit öncesinde çalışacak şekilde yapılandırılmalıdır. Bu araçlar yaygın gizli bilgi kalıplarını otomatik olarak tespit eder.

- [ ] **Her commit öncesinde `git diff --staged` çıktısını manuel incele**  
  Araç tabanlı taramanın yanı sıra, özellikle yapılandırma dosyaları veya bağlantı dizesi içeren dosyalar commit'e dahilse, değişiklikler push öncesinde gözden geçirilmelidir.

- [ ] **CI/CD pipeline'ına gizli tarama adımı ekle**  
  GitHub Actions veya benzeri CI/CD sistemlerinde her push ve pull request için otomatik gizli tarama adımı tanımlanmalıdır. [GitHub'un yerleşik Secret Scanning özelliği](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning) etkinleştirilerek platform düzeyinde koruma sağlanmalıdır.

---

### 🗂️ Depo ve Erişim Yönetimi

- [ ] **Depo görünürlüğünü dikkatli belirle; şüphede kal, private ile başla**  
  Yeni oluşturulan depolar önce `private` olarak açılmalı, herkese açık hale getirmeden önce geçmiş commit'ler gizli bilgi açısından gözden geçirilmelidir.

- [ ] **Servis hesapları için minimum yetki prensibini uygula**  
  Depoya erişen botlar, deployment hesapları ve entegrasyonlar yalnızca işlevleri için zorunlu olan izinlere sahip olmalı; tam yetkili kişisel hesap token'ları kullanılmamalıdır.

- [ ] **Token ve API anahtarlarını düzenli olarak yenile (rotate)**  
  Kullanılan kimlik bilgileri belirli aralıklarla yenilenmeli; uzun süredir değiştirilmemiş anahtarlar geçersiz kılınarak yenileriyle değiştirilmelidir.

- [ ] **Geçmiş commit'leri periyodik olarak tara**  
  `git log` ile birlikte `gitleaks` veya benzeri araçlar kullanılarak depo geçmişi taranmalı; eski commit'lerde sızmış bilgi olup olmadığı kontrol edilmelidir. Sızıntı tespit edilirse yalnızca dosyayı silmek yeterli değildir; geçmiş yeniden yazılmalıdır.

- [ ] **Sızıntı sonrası müdahale planı hazır tut**  
  Gizli bir bilginin sızdığı anlaşıldığında: ilgili anahtar veya token **derhal iptal edilmeli**, yenisi oluşturulmalı ve olaya ilişkin bir erişim denetimi kaydı tutulmalıdır. "Commit'i sildim, tamam" yaklaşımı yeterli değildir.

---

## Why This Matters

### Anlık ve Otomatik Tehdit

Herkese açık bir depoya gizli bilgi içeren bir commit push edildiği anda, otomatik tarama botları bu bilgiyi saniyeler ile dakikalar arasında tespit edebilecek kapasitededir. Bu nedenle "hızlıca silerim" yaklaşımı gerçekçi bir savunma değildir; saldırgan, silme işlemi tamamlanmadan önce ilgili kimlik bilgisini kopyalamış olabilir.

### Depo Geçmişi Kalıcıdır

Git, değişiklik geçmişini tasarım gereği korur. Bir dosyadan gizli bilgiyi silip yeni bir commit atmak, o bilgiyi geçmişten kaldırmaz. Geçmişin yeniden yazılması (rebase, filter-branch veya BFG Repo Cleaner gibi araçlar) ve ardından tüm branch'lerin force-push edilmesi gerekir. Bu işlem karmaşık, zaman alıcı ve ekip koordinasyonu gerektiren bir süreçtir.

### Bulut Maliyetleri ve Hizmet Kötüye Kullanımı

Sızdırılan bir bulut sağlayıcı kimlik bilgisi; yetkisiz kaynak tüketimine, beklenmedik yüksek faturalara ve hizmet kotasının aşılmasına yol açabilir.

### Yasal ve Uyumluluk Yükümlülükleri

Müşteri verilerine veya kişisel verilere erişim sağlayan kimlik bilgilerinin sızması; KVKK, GDPR veya sektöre özgü düzenlemeler kapsamında bildirim ve belgeleme yükümlülüğü doğurabilir.

### Tedarik Zinciri Riski

Küçük ekiplerin açık kaynak projeleri bile bağımlılık zinciri aracılığıyla daha büyük sistemlere entegre olabilir. Bir geliştirici deposundaki gizli bilgi sızıntısı, yalnızca o kişiyi değil, projeyi kullanan tüm sistemleri etkileyebilir.

---

## Sources

Aşağıdaki kaynaklar, bu kontrol listesinin hazırlanmasında başvurulan bağımsız ve güvenilir referanslardır:

1. **GitHub Docs – Secret Scanning Hakkında**  
   GitHub'un yerleşik gizli tarama özelliğinin nasıl çalıştığını, hangi kalıpları tespit ettiğini ve uyarı mekanizmalarını açıklar.  
   🔗 [https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning)

2. **OWASP – Secrets Management Cheat Sheet**  
   Gizli bilgilerin uygulama yaşam döngüsü boyunca nasıl yönetileceğine dair kapsamlı en iyi uygulama rehberi.  
   🔗 [https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html)

3. **NIST SP 800-57 – Anahtar Yönetimi Önerisi**  
   Kriptografik anahtar ve kimlik bilgisi yaşam döngüsü yönetimine ilişkin NIST standart belgesi.  
   🔗 [https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final](https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final)

4. **Gitleaks – Açık Kaynak Gizli Tarama Aracı**  
   Git geçmişi ve anlık değişiklikler için kullanılan, CI/CD entegrasyonuna uygun gizli bilgi tarama aracının resmi deposu ve belgeleri.  
   🔗 [https://github.com/gitleaks/gitleaks](https://github.com/gitleaks/gitleaks)

---

*Bu yazı siber güvenlik farkındalığını artırmak için hazırlanmıştır.*  
*Siber Savunma Atlası — TAMGA*
