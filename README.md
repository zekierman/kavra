# tutor

Üniversite dersleri için bir yapay zekâ ajanı skill'i. İki hedefi var: **sınavdan alınabilecek en
yüksek not** ve **sınavdan sonra da kalan gerçek kavrayış**. Claude Code, Codex ve Antigravity ile
çalışır. Ders kitabı olarak Obsidian kasanı kullanır.

> *English: an agent skill that tutors university courses for the top grade and real understanding.
> Instructions are in English; this README is in Turkish.*

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

Skill, `skills/tutor/` klasörüdür. Ajanının skill aradığı yere kopyala. En iyisi Obsidian kasanın
içine koymak: böylece yalnız ders çalışırken devreye girer.

| Ajan | Kasa içinde (önerilen) | Global |
| --- | --- | --- |
| Claude Code | `.claude/skills/tutor/` | `~/.claude/skills/tutor/` |
| Codex | `.agents/skills/tutor/` | `~/.agents/skills/tutor/` |
| Antigravity | `.agents/skills/tutor/` | — (kasa içi kullan) |

```bash
git clone https://github.com/zekierman/tutor
cd <obsidian-kasan>
mkdir -p .claude/skills .agents/skills
cp -r <klon>/skills/tutor .claude/skills/
cp -r <klon>/skills/tutor .agents/skills/     # Codex + Antigravity ortak
```

Sonra ajanını kasanın içinde aç ve "Veri Yapıları'ndan bağlı listeyi çalışalım" de. İlk seferde
derslerin nerede duracağını sorar ve `learner.md` profilini oluşturur: nasıl öğrendiğin, neyi
sevmediğin, hangi dilde çalıştığın. Bu dosya senin; istediğin gibi düzenle, skill her oturumda onu
okur ve varsayılanlarının önüne koyar.

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

Öğretme ilkeleri ("önce koşulsuz doğrular", "bunu ben nasıl keşfederdim?", yokla → planla → öğret)
[amosblomqvist/learn](https://github.com/amosblomqvist/learn) projesinden uyarlandı. O proje `pi`
ajanı için yazılmış; bu, Claude Code, Codex ve Antigravity için sınav odaklı, bağımsız bir yeniden
yazım.

## Lisans

MIT
