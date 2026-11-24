# ZAINAB.org — Tasarım dili (DESIGN.md)

Bu dosya, `index.html` içinde `:root` değişkenleri ve ilgili CSS kuralları olarak
**zaten canlıda uygulanmış** olan tasarım dilini belgeler. Yeni bir yön önerisi
değildir — mevcut kararların referans kaydıdır, böylece sonraki her değişiklik
bu değerlerden grep ile yeniden türetmek yerine buradan okunabilir.

Konsept adı: **Purple Hope**. Kaynak: `docs/MASTER-BLUEPRINT` ve ZAINAB.ORG
Purple Hope paketi (bkz. proje geçmişi); kullanıcı tarafından onaylanıp canlıya
alındı.

## Renk paleti

| Token | Hex | Rol |
|---|---|---|
| `--plum` | `#452568` | Ana marka rengi (Deep Purple) |
| `--plum-2` | `#7851A9` | Butonlar, bağlantılar, odak çerçevesi (Royal Purple) |
| `--rose` | `#AA8BC8` | İkincil marka rengi (Soft Lavender) |
| `--peach` | `#E2D6EF` | Kart/ikon yüzeyleri (Light Lavender) |
| `--mist` | `#F5F0FA` | Bölüm arka planları (Lavender Mist) |
| `--cream` | `#FCFAFD` | Neredeyse beyaz zemin (Pearl White) |
| `--gold` | `#C6A16E` | Seyrek kullanılan özel vurgu (Soft Gold) — örn. konsept bloğunun üst kenarlığı |
| `--ink` | `#28212D` | Birincil metin rengi (Deep Charcoal) |
| `--muted` | `#685f78` | İkincil/açıklama metni |
| `--edge` | `#ddd0e8` | Kart ve bölüm kenarlıkları |
| `--footer` | `#2D1946` | Footer zemini |
| `--white` | `#fff` | Saf beyaz |

Kullanım oranı yönü (konsept belgesinden): kırık beyaz ~%40, koyu mor ~%25,
lavanta ~%20, kraliyet moru ~%10, altın ~%5. Altın renk bilerek seyrek
tutulur — ana vurgu değil, tek bir detay rengidir.

**Kural:** Yeni bir hex değeri eklemeden önce yukarıdaki tokenlardan birinin
yeterli olup olmadığını kontrol et. Bu oturumda birkaç kez eski bordo/şarap
paletinden kalma donuk hex değerleri (`#251922`, `#b75b89`, `#f4e7eb` vb.)
bulundu ve token'lara bağlandı; yeni kod bu hataya düşmemeli.

## Tipografi

- Başlıklar: **Playfair Display** → `Georgia, 'Times New Roman', serif`
- Gövde metni: **Manrope** → `system-ui, -apple-system, 'Segoe UI', sans-serif`
- Google Fonts üzerinden yüklenir (`<link>` `<style>` etiketinden hemen önce,
  `<head>` içinde).

| Rol | font-size |
|---|---|
| h1 | `clamp(2.8rem, 6vw, 5.45rem)` |
| h2 | `clamp(2rem, 4.1vw, 3.35rem)` |
| h3 | `1.27rem` |
| gövde | `16px` taban, `1.72` satır yüksekliği |

## Yerleşim ve bileşenler

- Konteyner: `width:min(1150px, calc(100% - 44px))`
- Kart yarıçapı: `--radius:22px` — yumuşak, yaklaşılabilir bir his için bilerek
  geniş; keskin köşeler bu projede kullanılmıyor.
- Kart gölgesi: `--shadow:0 14px 34px rgba(69,37,104,.09)` (ink renginden türetilir)
- Kart etkileşimi: `.card:hover` → `translateY(-3px)` + güçlenen gölge.
  **İstisna:** `.card.plan` (henüz gerçek içeriği olmayan "planlanan alan"
  kartları) hover'da **kalkmaz** — tıklanabilir olmayan bir şeye tıklanabilir
  görünüm vermemek için (Norman'ın afordans ilkesi).
- Kart giriş animasyonu: sadece `.card:not(.topic)` (yani rehber filtresiyle
  gösterilip gizlenmeyen, salt ana sayfa kartları) sayfa yüklendiğinde kısa bir
  gecikmeyle belirir. `.topic` kartlarına bilerek uygulanmaz — filtre
  tıklamasında yeniden tetiklenip can sıkıcı olurdu.
- Kırılma noktası: `850px` (mobil düzen, menü hamburger'e döner).
- Hareket: `prefers-reduced-motion: reduce` için sitede küresel bir kural var;
  tüm animasyon/geçiş süreleri `.01ms`'e iner. Yeni eklenen her animasyon bunu
  otomatik miras alır — ayrıca sarmalamaya gerek yok.

## Ses tonu ilkeleri (tasarımın bir parçası)

- Henüz gerçek olmayan hiçbir şey aktifmiş gibi gösterilmez: "Henüz aktif
  değil" / "Planlanan alan" etiketleri bilinçli bir marka sesi kararıdır,
  eksiklik değil.
- Gerçek kişilerin fotoğrafları veya kimlik bilgileri açık izin olmadan
  kullanılmaz (bkz. `docs/EDITORIAL_POLICY.md`).
- İlham alınan kuruluşlar (Kreftforeningen, Macmillan, Maggie's, vb.) açıkça
  adlandırılır ama hiçbir ortaklık/onay iddiası taşınmaz.

## Bu dosyayı ne zaman güncelle

Palet, tipografi veya yerleşimde canlıya alınan her kalıcı değişiklikten sonra
bu dosyayı güncelle — böylece bir sonraki oturum `index.html`'i grep'lemek
yerine buradan başlayabilir.
