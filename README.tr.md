# kavra

Üniversite dersleri için bir yapay zekâ ajanı skill'i. İki hedefi var: **sınavdan alınabilecek en
yüksek not** ve **sınavdan sonra da kalan gerçek kavrayış**. Claude Code, Codex ve Antigravity ile
çalışır. Ders kitabı olarak Obsidian kasanı kullanır.

> English: [README.md](README.md)

## Ne yapar?

- **Önce hedefi sorar, sonra yoklar.** Ne istediğini netleştirir (tüm konu mu, yarınki quiz mi?),
  sonra puanlı sorularla bilginin tam nerede bittiğini bulur.
- **Plan çıkarır, onayını bekler.** Konuyu küçük bir bağımlılık haritasına döker: en üstte
  tartışmasız temel doğrular, en altta hedefin. Sen onaylamadan anlatmaya başlamaz.
- **Adım adım öğretir.** Her adımda: neden gerekli → kur → önceki adıma bağla → tek soruyla
  kontrol et. Önce sen denersin. Cevabı hazır vermez, ipucu merdiveniyle ilerler.
- **Takılınca anlatım biçimini değiştirir.** İki denemede oturmayan bir şeyi aynı cümlelerle
  tekrar etmez. Benzetmeye, kutu tablosuna, çizime ya da görselleştirme aracına geçer.
- **Kaynakları sen seçersin.** Slayt, kitap, ders videosu, kendi notların, çıkmış sorular. Hangisinden
  sınav çıktığını ve çelişkide hangisinin kazanacağını sen belirlersin. Kaynağın yerini gösterir:
  slayt no, sayfa, video dakikası.
- **Sınav modu.** Konuları ağırlık × zayıflık sırasına koyar ve öneri olarak sunar, karar senin.
  Hocanın tarzında yeni sorular yazar, açık uçlu cevabını hoca gibi sıkı puanlar.
- **Aralıklı tekrar.** Her konu tarihli tekrar soruları bırakır (1-3-7-14-30 gün). Her oturum
  vadesi gelen tekrarla başlar.
- **Her şey kasana yazılır.** Konu başına bir markdown dosyası; harita, sorular, cevapların,
  nerede kaldığın. Claude Code'da başlayıp Codex'te devam edebilirsin, devir bu dosyalarla olur.

## Kurulum

Claude Code kullanıyorsan en kısası eklenti. Codex ve Antigravity için iki yol var: ikinci beyin kullanmıyorsan **A**, [Avenox Beyin](https://github.com/avenoxai/avenoxbeyin)
kullanıyorsan ya da kurmak istiyorsan **B**.

### Claude Code eklentisi

```
/plugin marketplace add zekierman/kavra
/plugin install kavra@kavra
```

### A) Yalnız kavra

Obsidian kasanın içine kopyala. Böylece sadece o kasada çalışırken devreye girer.

```bash
git clone https://github.com/zekierman/kavra
cd <obsidian-kasan>
mkdir -p .claude/skills .agents/skills
cp -r <klon>/skills/kavra .claude/skills/     # Claude Code
cp -r <klon>/skills/kavra .agents/skills/     # Codex + Antigravity ortak
```

Windows PowerShell'de `cp -r` yerine `Copy-Item -Recurse`, `mkdir -p` yerine `mkdir` kullan.
Bütün projelerinde açık olsun istersen global yollar: Claude Code `~/.claude/skills/`,
Codex `~/.agents/skills/`.

### B) Avenox Beyin ile: ikinci beyin + kavra

Avenox Beyin kalıcı hafıza sağlar: oturumlar arası süreklilik, günlük loglar, bilgi tabanı.
kavra bunun üstünde ders çalışır. Birlikte kullanınca herhangi bir ajanda "dün nerede kalmıştık?"
sorusunun cevabı hazır olur.

1. Avenox Beyin'i **resmî kurulumuyla** kur: [avenox.lol/beyin.md](https://avenox.lol/beyin.md).
   Ajanına bu adresi verip "oku ve kur" demen yeterli. Avenox yalnız resmî sürümün kullanılmasını
   istiyor; bu repo onun kodunu içermez.
2. kavra'yı beynin resmî skill içe aktarma komutuyla ekle (vault kökünde):

   ```bash
   git clone https://github.com/zekierman/kavra
   python3 beyin.py skill-import --source <klon>/skills/kavra     # Windows: py -3 beyin.py ...
   python3 beyin.py doctor
   ```

   Bu komut skill'i `.agents/skills/` ve `.claude/skills/` altına eşler ve takip eder. Önerilen yol
   budur. Elle kopyaladıysan iki taraf birebir aynı olsun, ardından `beyin.py skill-sync` çalıştır.
3. Ajanını kasada aç, "ders çalışalım" de. kavra beyni tanır: dersleri projeler klasörüne koyar,
   beynin kimlik ve kurallar dosyalarını tercihlerin olarak okur, oturum sonunda aktif konular
   dosyasına tek satırlık bir ders durumu yazar (konu, sıradaki adım, bekleyen tekrar sayısı).
   Beyin bu dosyayı oturum başında ajana verdiği için, hangi ajanda açarsan aç nerede kaldığın
   görünür.

> Eski (v2) Avenox kurulumlarında `beyin.py` yoktur. Onlarda A yolundaki gibi elle kopyala.

### İlk çalıştırma

"Veri Yapıları'ndan bağlı listeyi çalışalım" de. İlk seferde derslerin nerede duracağını ve
neyden çalıştığını (slayt, kitap, video, not, çıkmış soru) sorar, `learner.md` profilini oluşturur.
Profil senin: nasıl öğrendiğini, neyi sevmediğini yaz, kavra her oturumda onu okur.
Kurulumu kontrol etmek için: "kavra kontrol".

## Kasanda nasıl görünür

```
Dersler/
├── learner.md            # profilin
└── Veri Yapıları/
    ├── _course.md        # kaynaklar, sınavlar, konu haritası, hata günlüğü, tekrar kuyruğu
    └── bagli-liste.md    # harita, neredeyim, oturumlar
```

Terminal sınıf, Obsidian ders kitabı. Ders dosyasını terminalin yanında aç; harita, LaTeX ve
ilerleme orada canlı dolar. Kasan senkronluysa tablette de okursun. Çalışma kağıdı istersen
cevaplar katlanır kutularda gizli gelir, kalemle çözüp kendini kontrol edersin.

## Sınırlar

- Ajanlar video izleyemez. Video kaynağı için altyazı ya da kendi notların gerekir.
- Ders dosyaları kilitli değildir. İki ajanı aynı anda aynı derste çalıştırma.
- Beyin entegrasyonu, beynin ayarlarına uyar: hafıza kapalıysa ya da manuel moddaysa kavra oraya
  yazmaz.
- Erken sürüm. Hedef ajanlar Claude Code, Codex ve Antigravity; gerçek ders oturumlarıyla
  deneniyor. Hata görürsen issue aç.

## Neden böyle?

Her kural bir araştırma bulgusuna dayanır:

- **Kendini test etmek ve tekrarı zamana yaymak**, incelenen on çalışma tekniği arasında en etkili
  iki teknik çıktı. Skill bu yüzden kendi çalışma yönteminin yerine geçmez, üstüne test ve
  tekrar ekler.
  ([Dunlosky vd., 2013](https://journals.sagepub.com/doi/abs/10.1177/1529100612453266))
- **Cevabı veren yapay zekâ öğrenmeyi bozar.** Yaklaşık 1000 lise öğrencisiyle yapılan deneyde düz
  GPT-4 alıştırma puanlarını yükseltti ama yapay zekâ kaldırılınca öğrenciler daha kötü yaptı. Cevap
  yerine ipucu veren sürüm bu zararı hafifletti. Bu yüzden skill cevap değil ipucu verir.
  ([Bastani vd., PNAS 2025](https://www.pnas.org/doi/10.1073/pnas.2422633122))
- **İyi tasarlanmış yapay zekâ öğretmeni sınıfı geçebilir.** Harvard'daki deneyde kısa cevaplar
  veren, her seferinde tek adım açan, önce öğrenciye denettiren ve doğru çözümleri önceden verilmiş
  bir öğretmen, aktif öğrenme dersinin iki katından fazla kazanım sağladı. Bu skill aynı ilkeleri
  izler: kısa mesaj, tek adım, önce sen dene, sorudan önce doğru cevabı kaynaktan doğrula.
  ([Kestin vd., Scientific Reports 2025](https://www.nature.com/articles/s41598-025-97652-6))
- **Önce denemek, yanılsan bile işe yarar.** Bilmediğin bir şeyi tahmin etmeye çalışıp ardından
  düzeltme almak, sadece okumaktan daha iyi öğretir. Emin olduğun bir yanlışın düzeltilmesi ise
  özellikle akılda kalır.
  ([hata yoluyla öğrenme üzerine derleme](https://link.springer.com/article/10.3758/s13423-021-02022-8),
  [hiperdüzeltme etkisi](https://www.researchgate.net/publication/11641193_Errors_Committed_with_High_Confidence_Are_Hypercorrected))
- **Çözümlü örnek, sonra kademeli geri çekme.** Yeni başlayan biri çözümlü örnekten daha hızlı
  öğrenir. Ustalaştıkça bu etki tersine döner, bu yüzden adımlar yavaş yavaş boş bırakılır.
  ([çözümlü örnek etkisi](https://en.wikipedia.org/wiki/Worked-example_effect),
  [uzmanlığın ters etkisi](https://en.wikipedia.org/wiki/Expertise_reversal_effect))
- **Aktif öğrenme, bilişsel yük, öğrenciye uyum, merak, üstbiliş.** Google'ın eğitim modeli LearnLM
  de aynı beş ilkeyi izliyor.
  ([Google](https://blog.google/products-and-platforms/products/education/google-learnlm-gemini-generative-ai/))

## Teşekkür

- İkinci beyin: [Avenox Beyin](https://github.com/avenoxai/avenoxbeyin) (MIT). kavra onun kodunu
  içermez, resmî içe aktarma yoluyla üstüne eklenir.

Öğretme ilkeleri ("önce koşulsuz doğrular", "bunu ben nasıl keşfederdim?", yokla → planla → öğret)
[amosblomqvist/learn](https://github.com/amosblomqvist/learn) projesinden uyarlandı. O proje `pi`
ajanı için yazılmış; bu, Claude Code, Codex ve Antigravity için sınav odaklı, bağımsız bir yeniden
yazım.

## Lisans

MIT
