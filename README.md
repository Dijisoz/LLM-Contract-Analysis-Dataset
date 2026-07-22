# LLM Contract Analysis Dataset

Bu veri kümesi, **UBMK 2026** kapsamında sunulan *"Çoklu Yapay Zekâ Modellerinin Sözleşme Yönetim Platformuna Entegrasyonu İçin Modüler Bir Mimari Yaklaşımı"* başlıklı çalışmanın deneysel verilerini içermektedir. Çalışma, DijiSöz platformunun yapay zekâ analiz modülünde kullanılan **Çoklu Etmen (Multi-Agent - MA)** mimarisi ile **Tekil İstem (Single Prompt - SP)** yapısını karşılaştırmalı olarak analiz etmektedir.

## İçerik ve Amaç

Sistemin başarımını ve ayırt ediciliğini ölçmek amacıyla 4 adet Gizlilik Sözleşmesi (NDA) ve 4 adet Yatırım Sözleşmesi olmak üzere toplam 8 adet sentetik test sözleşmesi üretilmiş; bu sözleşmelere modellerin risk tespit kapasitesini, çıkarım yeteneğini ve perspektif uyumluluğunu ölçmek amacıyla sistematik olarak hukuki hatalar, eksiklikler ve muğlaklıklar enjekte edilmiştir. Bu test veri kümesi üzerinden toplam 16 bağımsız analiz sonucu elde edilmiştir.

Analiz çıktılarının kalitesi, çift kör (double-blind) bir değerlendirme süreciyle bağımsız hakem modeller (Gemini ve Claude) tarafından 1-10 arası puanlanmıştır.

## Klasör Yapısı
LLM-Contract-Analysis-Dataset/
├── contracts/       8 adet analiz edilmiş sözleşme (PDF) — 4 NDA + 4 Yatırım Sözleşmesi
├── prompts/         Değerlendirme (hakem) promptları (TXT)
├── results/         CSV (ham puanlama verisi) + PDF (tablolaştırılmış sonuçlar/sunum)
├── LICENSE
└── README.md


## Metodoloji Özeti

İki aşamalı bir test prosedürü uygulanmıştır:

1. **Baseline Testi** — OpenAI'nin GPT-4o-Mini modeli ile Single Prompt (SP) ve Multi-Agent (MA) mimarileri karşılaştırılmıştır.
2. **İleri Seviye Model Testi** — Aynı testler, agentic yapılara yönelik optimizasyonlar içeren GPT-5.4-Mini modeli ile tekrarlanmıştır.

Her iki aşamada da istem şablonları, sıcaklık (temperature) parametresi ve diğer sistem girdileri sabit tutulmuştur.

## Değerlendirme Kriterleri

Her analiz çıktısı 5 temel metrik üzerinden 1-10 arası puanlanmıştır:

| Kriter | Açıklama |
|---|---|
| Veri Çıkarma Doğruluğu | Somut, sayısal ve hukuki verilerin metinden doğru çekilme düzeyi |
| Perspektif Uyumu | Temsil edilen tarafın çıkarlarını koruma başarısı |
| Çelişki ve Mantık Yürütme | İçsel tutarlılık ve hukuki terminolojinin doğru kullanımı |
| Eksiklik Tespiti | Sözleşmede bulunması gereken ama yer almayan mekanizmaların fark edilme oranı |
| Karar Tutarlılığı | Nihai "imzalanabilirlik" kararı ile tespit edilen riskler arasındaki tutarlılık |

Detaylı puanlama bantları (9-10 Mükemmel, 7-8 İyi, 5-6 Orta, 3-4 Zayıf, 1-2 Çok Zayıf/İhlal) ve her kriter için özel değerlendirme kuralları `prompts/` klasöründeki dosyalarda tam olarak yer almaktadır.

## Temel Bulgular

- **Mimarinin Belirleyici Rolü:** Multi-Agent (MA) tasarımı, özellikle sınırlı kapasiteli modellerde (GPT-4o-Mini) çıktı kalitesini ve risk yakalama hassasiyetini belirgin şekilde iyileştirmektedir.
- **Model Gelişimi ve Entegrasyon Sinerjisi:** Akıl yürütme seviyesi yüksek modellerde (GPT-5.4-Mini) mimariler arası fark daralsa da, karmaşık senaryolarda MA yapısı en yüksek kararlılığı sunmaktadır.
- **Maliyet ve Süre:** MA mimarisi analiz sürelerini yaklaşık iki katına çıkarmaktadır (ortalama 35-45 saniyeden 75-85 saniyeye), ancak kritik risklerin kaçırılmaması göz önüne alındığında bu maliyet kabul edilebilir düzeydedir.
- **Bağlam Penceresi Yönetimi:** Doküman hacmi arttığında Single Prompt yapısında dikkat dağılımı (loss in the middle) performansı olumsuz etkilerken, MA mimarisi dokümanı mantıksal parçalara ayırıp (chunking) alt etmenlere dağıtarak sürdürülebilirliği sağlar.
- **Heterojen Model Entegrasyonu:** MA mimarisi, farklı alt görevlerde farklı LLM'lerin (kritik analizler için yüksek kapasiteli, basit işlemler için ekonomik modeller) bir arada kullanılmasına imkân tanıyarak maliyet-performans dengesini optimize eder.

## Kullanılan Modeller

- OpenAI GPT-4o-Mini
- OpenAI GPT-5.4-Mini
- Değerlendirici (hakem) modeller: Google Gemini, Anthropic Claude

## Atıf (Citation)

Bu veri kümesini kullanırken lütfen ilgili UBMK 2026 bildirisine atıf yapınız. *(Bildiri yayınlandığında burada tam atıf bilgisi ve DOI güncellenecektir.)*

## Lisans

Bu veri kümesi [Creative Commons Attribution 4.0 International License (CC-BY 4.0)](https://creativecommons.org/licenses/by/4.0/) ile lisanslanmıştır.

## İletişim

Sorularınız için: **Dijisoz** — [GitHub](https://github.com/Dijisoz)
