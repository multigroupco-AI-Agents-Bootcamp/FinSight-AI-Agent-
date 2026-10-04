# FinSight AI Agent — Adım Adım Proje & Takvim Planı

Bu plan, **AI Agents Bootcamp** takvimine ve **6 Kasım 2026** son teslim tarihine uygun olarak, aşamalı araştırma, teknik geliştirme ve değerlendirme süreçlerini içerir.

> [!IMPORTANT]
> **Son Teslim Tarihi**: **6 Kasım 2026, 23:59**
> **Proje Kapsamı**: FinSight — Halka Açık Şirketler & KAP/Bilanço Analiz AI Agent Sistemi (Multi-Agent, MCP, RAG, Critic Döngüsü, Değerlendirme & Web UI).

---

## 🗓️ Kilometre Taşları & Zaman Çizelgesi (Milestones)

| Aşama | Tarih Aralığı | Odak & Çıktılar | Puan/Kriter |
| :--- | :--- | :--- | :--- |
| **M0: Başlangıç & Araştırma** | 2 – 5 Ekim | Veri kaynakları (SEC/KAP/Borsa), problem tanımı, 10 örnek soru, baseline (tek LLM) ölçümü | Problem Tanımı (%10) |
| **M1: Çekirdek Agent & Tool'lar** | 5 – 11 Ekim | ≥4 Özel Tool (hesaplayıcı, veri çekici, RAG retriever), ReAct döngüsü, ilk golden set | Tool & Agent (%20) |
| **M2: Multi-Agent, MCP & UI** | 12 – 18 Ekim | Multi-agent orkestrasyonu (Analyst, Data, Critic), MCP Server/Client, İnteraktif Dashboard | Multi-Agent & MCP (%10) |
| **M3: Eval, Güvenlik & Deploy** | 19 Ekim – 6 Kasım | 25+ Golden Set Eval, Prompt-injection testleri, Deploy (Web UI/Public Demo), Teknik Yazı | Eval & Güvenlik (%25), Deploy & Doküman (%20) |

---

## 🚀 Adım Adım Uygulama & Araştırma Planı

### Aşama 0: Detaylı Araştırma & Veri Altyapısı (M0: 2 - 5 Ekim)
1. **Finansal Veri Setleri ve API Araştırması**:
   - Yahoo Finance (`yfinance`), CoinGecko API ve KAP/Bilanço verilerinin entegrasyon yapısının incelenmesi.
   - Şirket finansal tablolarının (Bilanço, Gelir Tablosu, Nakit Akım) veri yapısının modellenmesi.
2. **Problem Tanımı & 10 Örnek Soru**:
   - Finansal analistlerin 1-2 günde yaptığı bilanço ve KAP bildirim analizlerini AI Agent ile otomatikleştirme senaryolarının yazılması.
3. **Baseline (Tek LLM) Ölçümü**:
   - Tek bir LLM çağrısının finansal hesaplamalarda uydurma (hallucination) yapabildiğini ve kaynak gösteremediğini kanıtlayan baseline testinin yapılması.

### Aşama 1: Çekirdek Tool'lar & ReAct Döngüsü (M1: 5 - 11 Ekim)
1. **Deterministik Finansal Tool Katmanı (`tools/`)**:
   - `financial_calculator.py`: F/K, PD/DD, Borç/Özkaynak, ROE, CAGR ve Oran analizleri (Python kod katmanında %100 kesin hesaplama).
   - `market_data.py`: Hisse fiyatları ve geçmiş finansal verileri getirme.
   - `kap_retriever.py`: KAP bildirimleri ve bilanço dipnotları üzerinde kaynaklı RAG/vektör araması.
   - `report_generator.py`: Yapılandırılmış finansal rapor şablonu oluşturucu.
2. **Agent Döngüsü (`agents/base_agent.py`)**:
   - ReAct (Thought -> Action -> Observation) döngüsü, adım sınırı (`max_steps=10`) ve sonsuz döngü koruması.

### Aşama 2: Multi-Agent Mimarisi, MCP & Görsel UI (M2: 12 - 18 Ekim)
1. **Multi-Agent Orkestrasyonu (`agents/`)**:
   - **Data Agent**: Ham bilanço ve KAP verilerini toplayan uzman.
   - **Analyst Agent**: Finansal oranları ve büyüme trendlerini hesaplayan analist.
   - **Critic / Validator Agent**: Üretilen rapordaki tüm rakamları kaynak verilerle karşılaştırıp doğrulayan denetçi.
   - **Orchestrator**: Soruyu analiz edip uzmanlara dağıtan ve yanıtı birleştiren lider agent.
2. **Model Context Protocol (MCP)**:
   - FinSight tool'larını standart MCP Server protokolu üzerinden dışarıya açma ve client entegrasyonu.
3. **Görsel Web Arayüzü (`web/`)**:
   - Modern, koyu temalı (dark mode), ReAct canlı düşünce izleyici (trace), finansal grafikler ve metrik kartları içeren interaktif web dashboard.

### Aşama 3: Değerlendirme (Eval), Güvenlik & Yayına Alma (M3: 19 Ekim - 6 Kasım)
1. **Golden Set Değerlendirmesi (`evals/`)**:
   - 25+ adet finansal test sorusu üzerinde Baseline vs. FinSight Agent doğruluk, kaynak oran ve sayısal hassasiyet karşılaştırması.
2. **Güvenlik & Sorumlu AI**:
   - Yetkisiz işlem engelleme, prompt-injection testleri ve "Yatırım tavsiyesi değildir" uyarı politikası.
3. **Teknik Yayın & Dokümantasyon**:
   - Proje mimari şeması, README.md ve TVT / Medium teknik yazısının tamamlanması.
4. **Final Teslim (6 Kasım 23:59)**:
   - Sistem testi, demo kaydı ve teslimat.

---

## 🛠️ Proje Klasör Yapısı

```
Projects/01_FinSight_Finans/
├── config.py                 # API anahtarları & ortam değişkenleri
├── main.py                   # CLI & Ana Başlatıcı
├── server.py                 # FastAPI / Python Web Server
├── tools/                    # Özel Deterministik Tool'lar
│   ├── financial_calculator.py
│   ├── market_data.py
│   ├── kap_retriever.py
│   └── report_generator.py
├── agents/                   # Agent Mimarisi & Döngüsü
│   ├── base_agent.py
│   ├── analyst_agent.py
│   ├── critic_agent.py
│   └── orchestrator.py
├── evals/                    # Değerlendirme & Benchmark
│   ├── golden_dataset.json   # 25+ Finansal test sorusu
│   └── eval_runner.py        # Baseline vs Agent Eval scripti
├── web/                      # Web Dashboard Arayüzü
│   ├── index.html
│   ├── styles.css
│   └── app.js
└── tests/                    # Birim testler
```

---

## 🔍 Doğrulama & Kontrol Listesi

- [ ] **M0**: Veri kaynakları indirildi, baseline sorunu tanımlandı.
- [ ] **M1**: 4 adet tipli tool yazıldı ve ReAct döngüsüne bağlandı.
- [ ] **M2**: Multi-agent + Critic döngüsü ve Web Dashboard tamamlandı.
- [ ] **M3**: 25 soruluk Golden Set Eval çalıştırıldı, %85+ doğruluk sağlandı, doküman ve demo teslim edildi.
