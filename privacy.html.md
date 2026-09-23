# Maya — Gizlilik Politikası / Privacy Policy

> Son güncelleme / Last updated: 24 Eylül 2026 · Uygulama sürümü 3.0
> https://necatidogrul.github.io/maya-site/privacy.html

## Kısaca (TR)

- Hesap açılmıyor. Ad, e-posta, telefon numarası istenmiyor ve bilinmiyor.
- Menü, market listesi, favoriler ve tercihler **cihazda** durur.
- Tarif üretilirken yazılan malzeme, tercihler ve — kullanılırsa — fotoğraf yapay zekâ modeline
  gider. **Fotoğraflar saklanmaz.**
- **İzleme yapılmıyor.** Reklam SDK'sı, izleme SDK'sı ve IDFA yok; veriler reklam ya da ölçüm
  için üçüncü taraf verisiyle eşleştirilmiyor.
- Veri satılmıyor, veri simsarlarına aktarılmıyor.

## 1. Veri sorumlusu
Maya'yı bağımsız iOS geliştiricisi **Necati Doğrul** yayımlıyor (KVKK'da veri sorumlusu, GDPR'da
controller). İletişim: necatidogrul7@gmail.com

## 2. Cihazda kalanlar
Haftalık menü, market listesi, favori tarifler, damak tercihleri, alerji ve sevilmeyenler
listesi, porsiyon ayarları, uygulama ayarları ve indirilmiş tarif görsellerinin önbelleği
telefondan hiç çıkmaz. Sunucuda kullanıcıya ait hesap ya da profil yoktur.

## 3. Cihazdan çıkanlar

### 3.1 Yapay zekâ ile üretim
Bir menü, tarif, besin bilgisi ya da sohbet cevabı üretildiğinde sunucuya gidenler: yazılan veya
söylenen malzemeler, mutfak/diyet tercihleri, kaç kişi için pişirildiği, dil tercihi ve — o
özellik kullanılırsa — çekilen fotoğraf. İstek önce **Firebase Cloud Functions**'a gider (Google
Cloud, **europe-west3 / Frankfurt**), oradan **Google Gemini** modeline iletilir ve cevap döner.

### 3.2 Fotoğraflar
Buzdolabı ve tabak fotoğrafı isteğin gövdesinde gönderilir, modele iletilir ve cevap üretildikten
sonra **bırakılır**. Hiçbir dosya depolamaya yazılmaz, hiçbir veritabanı satırına kaydedilmez,
kopyası tutulmaz. Dayanağı yapılandırma: bulut depolamada istemciye açık tek yazma yolu yoktur ve
fotoğrafı işleyen iki fonksiyon da sonucu döndürdükten sonra görüntüyü hiçbir yere yazmaz.
Depolamada yalnızca uygulamanın kendi yemek kataloğu ve tarif fotoğrafları bulunur.

### 3.3 Kullanım ölçümü
Hangi ekranların açıldığı ve hangi adımda vazgeçildiği **Firebase Analytics** ile ölçülür. Bu
olaylar ekran adları ve buton dokunuşlarıdır; yazılan malzeme, tarif metni ya da fotoğraf içermez.

## 4. Kullanılan servisler

| Servis | Ne için | Ne alıyor |
|---|---|---|
| Firebase Analytics (Google) | Kullanım ölçümü, huni analizi | Kullanım olayları, cihaz tanımlayıcı (Firebase kurulum kimliği), cihaz modeli, dil, ülke |
| Firebase App Check (Google) | İsteğin gerçek bir kurulumdan geldiğini doğrulama | Apple App Attest jetonu; kişisel veri taşımaz |
| Firebase Cloud Functions + Gemini (Google) | Tarif, menü, besin ve sohbet üretimi | Malzemeler, tercihler, dil ve varsa fotoğraf |
| RevenueCat | Abonelik durumu ve Pro erişimi | Anonim app user ID, satın alma ve yenileme geçmişi, ülke, platform |
| Kingfisher | Tarif görsellerini indirip cihazda önbelleğe alma | Hiçbir şey göndermez (açık kaynak görsel önbelleği) |
| Apple | Satın alma ve abonelik | Ödemeyi Apple alır; kart bilgisi hiçbir zaman görülmez |

**Listede olmayanlar:** reklam ağı, atıf/attribution SDK'sı, sosyal medya SDK'sı, ayrı üçüncü
taraf çökme kaydı ve IDFA yok. Uygulama `AdSupport` çerçevesini bağlamaz, bu yüzden izleme izni
(ATT) penceresi hiç açılmaz.

## 5. Tanımlayıcılar
- **Kurulum kimliği** — uygulamanın ürettiği rastgele UUID, cihazın anahtarlığında saklanır,
  ücretsiz üretim hakkını sayar. Kimliğe bağlı değildir.
- **Firebase kurulum kimliği** — analitik olaylarını bağlayan rastgele Google kimliği.
- **RevenueCat app user ID** — anonim abonelik kimliği; Maya'da giriş olmadığı için her zaman
  anonim kalır.

**Dürüstçe:** kurulum kimliği anahtarlıkta durduğu için silme-kurma sonrası **aynı kalabilir**
(aynı cihaz, aynı Apple Kimliği) ve iCloud yedeğinden geri gelebilir — ücretsiz hakkın silip
kurmayla sıfırlanmaması için. Cihaz değişirse ya da tüm içerik silinirse yeni kimlikle başlanır.
Bu kimlik yalnızca kota sayacıdır; reklam için kullanılmaz, kimseyle paylaşılmaz.

## 6. Saklama süreleri
- **Fotoğraflar:** saklanmaz.
- **Malzeme metni ve tarif istekleri:** cevap üretildikten sonra saklanmaz.
- **Günlük kota sayaçları:** otomatik silme (TTL) politikasıyla silinir.
- **Teknik ölçüm kayıtları** (hangi görsel katmanı cevap verdi, gecikme, model adı, dil):
  kullanıcı kimliği içermez, aynı otomatik silme politikasına tabidir.
- **Ömür boyu ücretsiz hak sayacı:** süresiz tutulur — içeriği bir sayıdır, kullanıcı girdisi değil.
- **Analitik olayları:** Google'ın Firebase Analytics saklama politikasına tabidir.
- **Abonelik kayıtları:** RevenueCat ve Apple tarafında tutulur.

## 7. İzleme (Apple'ın tanımıyla)
**Maya izleme yapmaz.** IDFA kullanılmaz, uygulamalar arası kimlik üretilmez, veriler reklam veya
ölçüm amacıyla üçüncü taraf verisiyle eşleştirilmez, veri simsarına aktarılmaz. App Store
gizlilik etiketinde hiçbir veri türü "İzleme için kullanılan veriler" altında beyan edilmemiştir.

## 8. Bildirimler
İzin verilirse günde bir hatırlatma (kendi menüden o günün yemeği) ve market gününde bir
hatırlatma daha. Cihazda zamanlanır; iOS Ayarlar → Bildirimler → Maya'dan kapatılır.

## 9. Verileri silmek
1. **Cihazdakiler:** uygulamayı silmek menüyü, listeyi, favorileri, tercihleri ve görsel
   önbelleğini siler.
2. **Anahtarlıktaki kurulum kimliği:** uygulama silinince kalabilir. Tamamen temizlemek için
   necatidogrul7@gmail.com adresine yazın; sunucudaki kota sayaçları silinir.
3. **Abonelik kaydı:** aynı adrese yazarak RevenueCat'teki anonim abone kaydının silinmesi talep
   edilebilir. Bu kayıt silinirse satın almayı geri yükleme zorlaşır; abonelik hâlâ Apple
   tarafında duruyorsa iptal Apple hesap ayarlarından yapılmalıdır.
4. **Analitik:** talep üzerine, cihazın Firebase kurulum kimliğine bağlı analitik kayıtlarının
   silinmesi Google'dan istenir.

Talepler 30 gün içinde yanıtlanır. Hesap olmadığı için kimlik doğrulaması yapılamaz; talebin
kullanılan cihazdan gönderilmesi yeterlidir.

## 10. Çocukların gizliliği
Maya çocuklara yönelik değildir ve App Store Kids kategorisinde yer almaz. 13 yaşından (AB'de
ilgili ülkenin belirlediği yaştan, genellikle 16) küçük çocuklardan bilerek veri toplanmaz.

## 11. Haklar (KVKK ve GDPR)
Erişim, düzeltme, silme, işlemenin kısıtlanması, veri taşınabilirliği, itiraz ve rızayı geri
çekme hakları. İşleme dayanakları: uygulamanın istenen işi yapması için sözleşmenin ifası;
kullanım ölçümü ve uygulama bütünlüğü için meşru menfaat; bildirimler ve fotoğraf/mikrofon
erişimi için açık rıza. Başvuru: necatidogrul7@gmail.com. Türkiye'de KVKK Kurumu'na, AB'de
bulunulan ülkenin veri koruma otoritesine şikâyet hakkı saklıdır.

## 12. Yurt dışına aktarım
Yapay zekâ istekleri Google Cloud **europe-west3 (Frankfurt, Almanya)** bölgesinde işlenir.
Google ve RevenueCat altyapılarının bir bölümünü ABD'de çalıştırır; aktarımlar sağlayıcıların
standart sözleşme hükümleri (SCC) ve veri işleme sözleşmeleri kapsamındadır.

## 13. Değişiklikler ve iletişim
Sayfa değişirse yukarıdaki tarih güncellenir; toplanan veri türü genişlerse uygulama içinde de
duyurulur. İletişim: necatidogrul7@gmail.com (genellikle 48 saat içinde yanıt).

---

# Privacy Policy (English)

**In short:** no account (no name, email or phone number); your plan, shopping list, favourites
and preferences stay on the device; when a recipe is generated the ingredients you type, your
preferences and — if you use it — your photo go to the AI model, and **photos are not stored**;
**we do not track you** (no ad SDK, no tracking SDK, no IDFA, no linking with third-party data
for advertising or measurement); we do not sell data or share it with data brokers.

**Controller.** Necati Dogrul, independent iOS developer. necatidogrul7@gmail.com

**On the device.** Weekly plan, shopping list, saved recipes, taste preferences, allergies and
dislikes, portion settings, app settings and the cache of downloaded recipe photographs. There is
no account or profile for you on any server.

**What leaves the device.** For AI generation: ingredients you type or say, cuisine and dietary
preferences, how many people you cook for, language, and — if used — your photo. The request goes
to our **Firebase Cloud Functions** (Google Cloud, **europe-west3 / Frankfurt**) and from there to
the **Google Gemini** model.

**Photos are not stored.** A fridge or plate photo is sent inside the request, passed to the
model and dropped once the answer is produced. No file is written to storage, no database row, no
copy. This rests on configuration: storage rules reject every client write, and neither function
that handles a photo writes the image anywhere after returning its result. Our storage holds only
our own dish catalogue and recipe photographs.

**Usage measurement.** Firebase Analytics records screen names and button taps to fix onboarding
and the purchase screen. It never includes typed ingredients, recipe text or photos.

**Services.** Firebase Analytics (usage events, Firebase installation ID, device model, language,
country) · Firebase App Check (Apple App Attest token, no personal data) · Firebase Cloud
Functions + Gemini (ingredients, preferences, language, optional photo) · RevenueCat (anonymous
app user ID, purchase and renewal history, country, platform) · Kingfisher (local image cache,
sends nothing) · Apple (payment; we never see card details). **Not on the list:** no ad network,
no attribution SDK, no social SDK, no separate third-party crash reporter, no IDFA. The app does
not link `AdSupport`, so the App Tracking Transparency prompt never appears.

**Identifiers.** A random install UUID in the device keychain (counts free generations), the
Firebase installation ID, and an anonymous RevenueCat app user ID. Honestly: the keychain install
identifier **can survive deleting and reinstalling** the app on the same device and Apple ID and
can return from an iCloud backup — that is deliberate, so the free allowance cannot be reset by
reinstalling. It is only a usage counter, never used for advertising, never shared.

**Retention.** Photos: not stored. Ingredient text and recipe requests: not stored after the
answer. Daily usage counters: deleted by an automatic time-to-live policy. Technical telemetry
(cache tier, latency, model name, language): no user identifier, same automatic deletion. The
lifetime free-allowance counter is kept indefinitely — it is a number, not your input. Analytics:
Google's Firebase Analytics retention. Subscription records: RevenueCat and Apple.

**Tracking.** Maya does not track as Apple defines it: no IDFA, no cross-app identifier, no
linking with third-party data for advertising or measurement, no data brokers. Nothing is
declared under "Data Used to Track You" in the App Store privacy label.

**Notifications.** With permission, one reminder a day plus one shopping-day reminder, scheduled
on the device. Revoke in iOS Settings → Notifications → Maya.

**Deleting your data.** Deleting the app removes everything on the device. For the keychain
install identifier and server-side usage counters, and for the anonymous RevenueCat record, write
to necatidogrul7@gmail.com; we answer within 30 days. On request we also ask Google to delete
analytics records tied to your Firebase installation ID. Because there is no account we cannot
verify identity, so writing from the device in question is enough.

**Children.** Maya is not directed at children and is not in the Kids category. We do not
knowingly collect data from children under 13 (or the age set by your country in the EU).

**Your rights (GDPR / KVKK).** Access, rectification, erasure, restriction, portability,
objection, withdrawal of consent. Legal bases: performance of a contract, legitimate interest
(usage measurement, app integrity) and consent (notifications, photo/microphone access). Write to
necatidogrul7@gmail.com; you may also complain to your national data protection authority.

**International transfers.** AI requests are processed in Google Cloud's europe-west3 (Frankfurt,
Germany) region. Google and RevenueCat run parts of their infrastructure in the United States
under standard contractual clauses and data processing agreements.

**Contact.** necatidogrul7@gmail.com — we usually reply within 48 hours.
