# İçerik Politikası — siber-savunma-atlas

## Kabul Edilen İçerik

- Kamuya açık siber olayların savunma odaklı analizi
- Sektör/kurum bazlı risk profilleri ve uygulanabilir kontroller
- Dönemsel tehdit eğilimi özetleri
- Tekil olaylardan çıkarılan genel savunma prensipleri

## Kesin Yasaklar

- Çalışan exploit, PoC kodu veya istismar zinciri
- Çalıştırılabilir malware örneği
- C2 (komuta-kontrol) altyapısı kurulum talimatı
- Gerçek hedef, kurban veya kurum adının yetkisiz ifşası
- Parola, token, API key, sızıntı veri veya herhangi bir PII
- Aktif istismar edilen veya disclosure süresi dolmamış zafiyetlerin teknik detayı
- Teknik kaynak desteği olmayan politik attribution iddiası ("X devleti bunu yaptı" formunda kesin ifade)
- Gerçek şirket/proje adı geçirerek savunma sanayii tedarik zinciri tartışması (bkz. aşağıdaki özel kural)

## Attribution Kuralı

Hiçbir içerikte bir devlet veya aktör kesin fail olarak yazılamaz. Yalnızca "açık kaynak raporları X ile ilişkilendirdi" veya "public reporting has associated..." formundaki temkinli dil kullanılabilir. Detaylar için `.github/methodology/facts-vs-assessment.md` ve `.github/methodology/source-reliability.md`.

## Savunma Sanayii / Tedarik Zinciri İçeriği — Özel Kural

`sector-risk-notes/defense-industry-suppliers/` altındaki içerik, genel risk kategorisi düzeyinde kalır. Hiçbir gerçek Türk savunma şirketi veya proje adı anılmaz. Bu içerik türü her zaman Tier 3 ve maintainer onayı zorunludur.

## Metodoloji Ağırlığı

İçerik türüne göre hangi metodoloji katmanının (hafif/orta/ağır) uygulandığı `.github/methodology/facts-vs-assessment.md`'de tanımlıdır. Bu repodaki her template, ilgili katmanı belirtir.

## Dil

İçerik Türkçe veya İngilizce yazılabilir; YAML frontmatter'daki `language` alanı doğru ayarlanmalıdır. KOBİ/bireysel okuyucuya yönelik içerik (örn. checklist) Türkçe önceliklidir.
