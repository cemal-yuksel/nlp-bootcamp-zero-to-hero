# 01. Metin Ön İşleme (Text Preprocessing)

<!-- SİSTEM MİMARİSİ & YOLCULUK -->
## 🚦 Metin Ön İşleme Yolculuğu

<p align="center">
  <b>Ham veriden temiz, anlamlı ve modellemeye hazır metne giden profesyonel yolculuk!</b>
</p>

<!-- Daha kare ve dengeli bir mermaid diyagramı -->
```mermaid
flowchart TD
    style A1 fill:#D6EAF8,stroke:#2980B9,stroke-width:2px
    style B1 fill:#F9E79F,stroke:#B7950B,stroke-width:2px
    style B2 fill:#D5F5E3,stroke:#229954,stroke-width:2px
    style B3 fill:#FADBD8,stroke:#C0392B,stroke-width:2px
    style B4 fill:#E8DAEF,stroke:#8E44AD,stroke-width:2px
    style B5 fill:#D4E6F1,stroke:#2471A3,stroke-width:2px
    style B6 fill:#FDEBD0,stroke:#CA6F1E,stroke-width:2px
    style B7 fill:#F6DDCC,stroke:#CA6F1E,stroke-width:2px
    style B8 fill:#D1F2EB,stroke:#148F77,stroke-width:2px
    style B9 fill:#F9E79F,stroke:#B7950B,stroke-width:2px
    style Z1 fill:#D5DBDB,stroke:#34495E,stroke-width:2px

    %% Satır 1
    A1([Ham Veri])
    B1([Veri Yükleme<br><i>Toplama & Okuma</i>])
    B2([Temizleme<br><i>Karakter, Boşluk, HTML</i>])

    %% Satır 2
    B3([Dil Tespiti<br><i>Language Detection</i>])
    B4([Normalizasyon<br><i>Küçük Harf, Yazım Düzeltme</i>])
    B5([Tokenizasyon<br><i>Cümle/Kelime Bölme</i>])

    %% Satır 3
    B6([Stopword Kaldırma<br><i>Gereksiz Kelimeler</i>])
    B7([Kök/Gövdeleme<br><i>Stemming/Lemmatization</i>])
    B8([NER için Hazırlık<br><i>Varlık Temizliği</i>])

    %% Son
    B9([Kalite Kontrol<br><i>Doğrulama & Son Kontrol</i>])
    Z1([Modellemeye Hazır Metin])

    %% Bağlantılar
    A1 --> B1
    B1 --> B2
    B2 --> B3
    B3 --> B4
    B4 --> B5
    B5 --> B6
    B6 --> B7
    B7 --> B8
    B8 --> B9
    B9 --> Z1

    %% Yatay bağlantılar (kare görünüm için)
    B1 -.-> B4
    B4 -.-> B7
    B2 -.-> B5
    B5 -.-> B8
    B3 -.-> B6
    B6 -.-> B9
```

---

## 🌟 Metin Ön İşleme Aşamaları & Flashcardlar

### 1. **Veri Yükleme (Toplama & Okuma)**
- **Amaç:** Ham metin verisini elde etmek ve uygun formata getirmek.
- <div style="border:1px solid #2980B9; border-radius:8px; padding:12px; background:#F4F8FB; margin:10px 0;">
  <b>Soru:</b> Veri yükleme neden kritik bir adımdır ve sürecin başarısına nasıl etki eder?<br>
  <b>Cevap:</b> Veri yükleme, doğal dil işleme projelerinin temelini oluşturur. Ham verinin doğru ve eksiksiz bir şekilde toplanması, sonraki tüm işlemlerin sağlıklı ilerlemesi için gereklidir. Eksik, hatalı veya yanlış formatta yüklenen veriler, modelin öğrenme sürecini olumsuz etkiler ve yanlış sonuçlara yol açabilir. Bu nedenle, veri yükleme aşamasında verinin kalitesi, bütünlüğü ve uygun formatta olması, projenin genel başarısı için kritik öneme sahiptir.
  </div>

---

### 2. **Temizleme (Cleaning)**
- **Aşamalar:**  
  - Özel karakter, sayı, HTML etiketi, gereksiz boşluk temizliği
- **Kod:**
  ```python
  import re
  metin = "<p>Merhaba NLP! 2024 yılında, Python ile çalışıyoruz...</p>"
  temiz = re.sub(r'<.*?>', '', metin)  # HTML etiketlerini kaldır
  temiz = re.sub(r'[^a-zA-ZçğıöşüÇĞİÖŞÜ\s]', '', metin)  # özel karakterleri kaldır
  temiz = temiz.strip()
  print(temiz)
  # çıktı: Merhaba NLP yılında Python ile çalışıyoruz
  ```
- <div style="border:1px solid #229954; border-radius:8px; padding:12px; background:#F4FBF4; margin:10px 0;">
  <b>Soru:</b> Temizleme adımı neden gereklidir ve model performansına nasıl katkı sağlar?<br>
  <b>Cevap:</b> Temizleme işlemi, metindeki gereksiz karakterleri, sayıları, HTML etiketlerini ve fazla boşlukları ortadan kaldırarak verinin daha anlamlı ve işlenebilir hale gelmesini sağlar. Gürültülü veriler, modelin yanlış öğrenmesine ve düşük doğrulukta sonuçlar üretmesine sebep olur. Temiz bir veri seti, modelin gerçek anlamı yakalamasına ve daha güvenilir sonuçlar üretmesine yardımcı olur. Bu nedenle, temizleme adımı model başarısı için vazgeçilmezdir.
  </div>

---

### 3. **Dil Tespiti (Language Detection)**
- **Amaç:** Çok dilli veri setlerinde doğru dilde işlem yapmak.
- <div style="border:1px solid #C0392B; border-radius:8px; padding:12px; background:#FDF2F0; margin:10px 0;">
  <b>Soru:</b> Dil tespiti neden kritik bir adımdır ve yanlış dilde işlem yapılırsa ne gibi sorunlar ortaya çıkar?<br>
  <b>Cevap:</b> Dil tespiti, özellikle çok dilli veri setlerinde, her metnin hangi dilde olduğunu belirleyerek uygun ön işleme ve analiz adımlarının seçilmesini sağlar. Yanlış dilde yapılan işlemler, örneğin İngilizce stopword listesinin Türkçe bir metne uygulanması, anlam kaybına ve model başarısının ciddi şekilde düşmesine yol açar. Doğru dil tespiti, modelin her metni kendi diline uygun şekilde işlemesini ve daha doğru sonuçlar üretmesini sağlar.
  </div>

---

### 4. **Normalizasyon (Küçük Harf, Yazım Düzeltme)**
- **Aşamalar:**  
  - Tüm metni küçük harfe çevirme
  - Yazım hatalarını düzeltme, kısaltmaları açma
- **Kod:**
  ```python
  temiz = temiz.lower()
  # örnek yazım düzeltme için: pip install autocorrect
  from autocorrect import Speller
  spell = Speller(lang='tr')
  duzeltilmis = spell(temiz)
  print(duzeltilmis)
  # çıktı: merhaba nlp yılında python ile çalışıyoruz
  ```
- <div style="border:1px solid #8E44AD; border-radius:8px; padding:12px; background:#F7F1FA; margin:10px 0;">
  <b>Soru:</b> Normalizasyonun metin işleme sürecindeki rolü nedir ve neden gereklidir?<br>
  <b>Cevap:</b> Normalizasyon, metindeki tüm harfleri küçük harfe çevirerek ve yazım hatalarını düzelterek, aynı anlama gelen fakat farklı yazılmış kelimelerin tek bir biçimde temsil edilmesini sağlar. Bu, modelin kelimeleri daha tutarlı şekilde işlemesine ve gereksiz çeşitliliğin önüne geçmesine yardımcı olur. Ayrıca, yazım hatalarının düzeltilmesi, modelin yanlış kelimelerden etkilenmesini engeller ve genel doğruluğu artırır.
  </div>

---

### 5. **Tokenizasyon (Cümle/Kelime Bölme)**
- **Aşamalar:**  
  - Cümle ve kelime bazında bölme
- **Kod:**
  ```python
  from nltk.tokenize import word_tokenize
  tokenler = word_tokenize(duzeltilmis, language="turkish")
  print(tokenler)
  # çıktı: ['merhaba', 'nlp', 'yılında', 'python', 'ile', 'çalışıyoruz']
  ```
- <div style="border:1px solid #2471A3; border-radius:8px; padding:12px; background:#F4F8FB; margin:10px 0;">
  <b>Soru:</b> Tokenizasyon nedir ve metin madenciliğinde neden önemli bir adımdır?<br>
  <b>Cevap:</b> Tokenizasyon, metni cümle veya kelime gibi daha küçük ve anlamlı parçalara ayırma işlemidir. Bu adım, metnin bilgisayar tarafından işlenebilir hale gelmesini sağlar. Tokenler sayesinde, model her bir kelimeyi veya cümleyi ayrı birer analiz birimi olarak ele alabilir. Bu, metindeki anlamın daha iyi yakalanmasına ve daha hassas analizlerin yapılmasına olanak tanır.
  </div>

---

### 6. **Stopword Kaldırma**
- **Aşamalar:**  
  - "ve", "ile", "bu" gibi anlamsız kelimelerin çıkarılması
- **Kod:**
  ```python
  from nltk.corpus import stopwords
  stop_words = set(stopwords.words('turkish'))
  filtreli = [w for w in tokenler if w not in stop_words]
  print(filtreli)
  # çıktı: ['merhaba', 'nlp', 'yılında', 'python', 'çalışıyoruz']
  ```
- <div style="border:1px solid #CA6F1E; border-radius:8px; padding:12px; background:#FDF6ED; margin:10px 0;">
  <b>Soru:</b> Metin ön işleme sürecinde stopword (gereksiz kelime) kaldırmanın model başarısına etkisi nedir ve neden gereklidir?<br>
  <b>Cevap:</b> Stopword kaldırma işlemi, metin içerisindeki "ve", "ile", "bu" gibi anlam taşımayan, cümle yapısı için gerekli fakat modelin öğrenmesi açısından katkı sağlamayan kelimeleri temizler. Bu sayede model, asıl anlamı taşıyan kelimelere odaklanır ve gereksiz bilgiyle uğraşmaz. Özellikle Türkçe gibi eklemeli dillerde, stopword'lerin çıkarılması modelin daha hızlı ve doğru öğrenmesini sağlar, eğitim süresini kısaltır ve sonuçların doğruluğunu artırır. Ayrıca, gereksiz kelimelerin çıkarılması modelin karmaşıklığını azaltır ve daha verimli çalışmasını sağlar.
  </div>

---

### 7. **Kök Bulma & Gövdeleme (Stemming & Lemmatization)**
- **Aşamalar:**  
  - Kelimeleri kök/gövde haline indirgeme
- **Kod:**
  ```python
  from nltk.stem.snowball import SnowballStemmer
  stemmer = SnowballStemmer("turkish")
  kokler = [stemmer.stem(k) for k in filtreli]
  print(kokler)
  # çıktı: ['merhab', 'nlp', 'yıl', 'python', 'çalış']
  ```
- <div style="border:1px solid #CA6F1E; border-radius:8px; padding:12px; background:#FDF6ED; margin:10px 0;">
  <b>Soru:</b> Lemmatizasyon ile stemming arasındaki temel farklar nelerdir ve model başarısına etkileri nasıldır?<br>
  <b>Cevap:</b> Stemming, kelimeleri basit kurallarla kök/gövde haline indirgerken, lemmatizasyon ise kelimenin sözlükteki gerçek kökünü bulmaya çalışır. Stemming hızlıdır ancak bazen anlamsız kökler üretebilir. Lemmatizasyon ise daha doğru ve anlamlı kökler sunar fakat daha fazla işlem gücü gerektirir. Doğru köklerin bulunması, modelin kelimeler arasındaki ilişkileri daha iyi anlamasını sağlar ve genel doğruluğu artırır. Özellikle Türkçe gibi zengin eklemeli dillerde lemmatizasyonun önemi büyüktür.
  </div>

---

### 8. **NER için Hazırlık (Varlık Temizliği)**
- **Amaç:** Kişi, yer, organizasyon gibi varlıkların doğru tespiti için metni sadeleştirmek.
- <div style="border:1px solid #148F77; border-radius:8px; padding:12px; background:#F0FBF7; margin:10px 0;">
  <b>Soru:</b> NER (Adlandırılmış Varlık Tanıma) öncesi ön işleme neden önemlidir ve hangi hataları önler?<br>
  <b>Cevap:</b> NER öncesi yapılan ön işleme, metindeki gürültüyü ve gereksiz bilgileri temizleyerek kişi, yer, organizasyon gibi varlıkların daha doğru tespit edilmesini sağlar. Gürültülü veya hatalı veriler, NER algoritmalarının yanlış varlıkları tanımasına veya önemli varlıkları atlamasına neden olabilir. Temiz ve sadeleştirilmiş bir metin, NER doğruluğunu artırır ve modelin gerçek dünyadaki varlıkları daha iyi tanımasını sağlar.
  </div>

---

### 9. **Kalite Kontrol & Doğrulama**
- **Amaç:** Tüm adımlar sonrası verinin tutarlılığını kontrol etmek.
- <div style="border:1px solid #34495E; border-radius:8px; padding:12px; background:#F4F6F7; margin:10px 0;">
  <b>Soru:</b> Kalite kontrol ve doğrulama adımı neden kritik öneme sahiptir ve hangi riskleri azaltır?<br>
  <b>Cevap:</b> Kalite kontrol, ön işleme adımlarının doğru ve eksiksiz uygulandığından emin olmak için gereklidir. Hatalı veya eksik ön işleme, modelin yanlış öğrenmesine, düşük doğrulukta sonuçlar üretmesine ve güvenilirliğin azalmasına yol açar. Kalite kontrol ile veri kaybı, yanlış dönüşümler ve tutarsızlıklar tespit edilip düzeltilir. Bu sayede modelin eğitimi ve test aşamalarında beklenmedik hataların önüne geçilmiş olur.
  </div>

---

## 🎯 En İyi Uygulamalar & İpuçları

- **Pipeline oluşturun:** Tüm adımları otomatikleştirin.
- **Dil bağımlılıklarını unutmayın:** Türkçe için özel karakter ve ekler kritik.
- **Veri kaybına dikkat:** Gereksiz bilgi silmeyin.
- **Her adımda kalite kontrolü yapın.**

---

## 📂 Klasör İçeriği

- `01.metin-on-isleme/temizleme.py` : Temel metin temizleme fonksiyonları
- `01.metin-on-isleme/tokenizasyon.py` : Tokenizasyon örnekleri
- `01.metin-on-isleme/stopword.py` : Stopword kaldırma uygulamaları
- `01.metin-on-isleme/kok_bulma.py` : Stemming ve lemmatization örnekleri
- `01.metin-on-isleme/ornek_veri/` : Örnek metin dosyaları

---

## 💡 Kaynaklar

- [NLTK Documentation](https://www.nltk.org/)
- [spaCy Documentation](https://spacy.io/)
- [Türkçe Doğal Dil İşleme Kaynakları](https://github.com/ahmetax/tr-nlp-tools)

---

> **Metin ön işleme, NLP projelerinin temelidir. Temiz veri, güçlü modellerin anahtarıdır!**