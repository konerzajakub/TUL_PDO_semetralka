# 🚀 Stručný návod pro výběr jazykového modelu

## 🧠 Důležité termíny

* **GGUF:** Populární formát souborů pro LLM, optimalizovaný pro běh na CPU i GPU.
* **Kvantizace:** Technika zmenšení modelu useknutím přenosti vah. Výsledkem je zmenšení velikosti za cenu přesnosti.
    * **Typy:** Od `Q2_K` (nejmenší, nejrychlejší, nejnižší kvalita) po `Q8_0` (větší, pomalejší, vyšší kvalita)
    * **Nejvyšší kvalita (`F16`, `F32` - nekvantizované):** Tyto modely nabízejí původní přesnost po trénování, ale jsou velmi náročné.
        * **Požadovaný HW:** Nejlepší GPU na trhu s velkou kapacitou VRAM (např. herní NVIDIA RTX 4090 s 24GB VRAM, profesionální karty jako NVIDIA A100/H100 s 80GB+ VRAM).
        * **Pro běžné uživatele:** Řešením může být pronájem cloudových serverů (AWS, GCP, Azure)

---

## 🛠️ Co zvážit před výběrem modelu?

1. **Výpočetní zdroje:** Modely mohou běžet buď na procesoru (CPU) a operační paměti (RAM), nebo na grafické kartě (GPU) a její vlastní paměti (vRAM).

   - **CPU + RAM:** Tato kombinace je vhodná, pokud máte silný procesor a dostatek operační paměti, a nemáte výkonnou grafickou kartu. Model běží přímo na procesoru a může to být použitelné.
   - **GPU + vRAM:** Pokud máte výkonnou dedikovanou grafickou kartu s dostatečnou vRAM, tohle je ta nejlepší volba. 

2. **RAM:** Máte k dispozici dostatek operační paměti pro uložení vah modelu do paměti RAM?
3. **VRAM (GPU):** Máte k dispozici dostatek operační paměti pro uložení vah modelu do paměti vRAM?

---

## 📊 Doporučení modelů (GGUF) dle HW (květen 2025)

| HW Konfigurace                     | Doporučená kvantizace         | Velikost* | Příklady modelů (GGUF)                    |
|------------------------------------|-------------------------------|-----------|-------------------------------------------|
| ≤ 8GB RAM / integrovaná GPU        | `Q3_K_S`, `Q4_0`              | ~2-4 GB   | `Phi-3-mini-4k-instruct.Q4_0.gguf`        |
| 8-16GB RAM / 8GB VRAM (GPU)      | `Q4_K_M`, `Q5_0`              | ~4-7 GB   | `Llama-3-8B-Instruct.Q4_K_M.gguf`         |
| 16-32GB RAM / 12GB VRAM (GPU)    | `Q5_K_M`, `Q6_K`              | ~6-10 GB  | `Llama-3-8B-Instruct.Q5_K_M.gguf`         |
| ≥ 32GB RAM / 16GB+ VRAM (GPU)      | `Q6_K`, `Q8_0`                | 10GB+     | `Llama-3-8B-Instruct.Q8_0.gguf`, nebo větší modely jako `Llama-3-70B` s agresivní kvantizací (např. `Q4_K_M`) |


| Model                                  | Velikost (Parametry) | Chatbot Arena Elo (Přibližně) | Odhadovaná VRAM (Q4_K_M) | Poznámka k hostování / Kvalitě                                  |
|----------------------------------------|----------------------|-------------------------------|--------------------------|-----------------------------------------------------------------|
| **Malé a efektivní modely**            |                      |                               |                          |                                                                 |
| `Phi-3-mini-4k-instruct`               | 3.8 Miliard          | ~1120-1150                     | ~2.4 GB                  | Velmi schopný na svou velikost, skvělý pro omezené zdroje. |
| `Mistral-7B-Instruct-v0.2`             | 7 Miliard            | ~1100-1130                     | ~4.4 GB                  | Stále velmi populární, dobrý kompromis.           |
| `Llama-3-8B-Instruct`                  | 8 Miliard            | ~1150-1180                     | ~4.9 GB                  | Výborný výkon ve své třídě, top volba pro mnoho uživatelů.  |
| **Středně velké modely**               |                      |                               |                          |                                                                 |
| `Qwen1.5-14B-Chat`                     | 14 Miliard           | ~1100-1140                     | ~8.0 GB                  | Silný model od Alibaba, dobré vícejazyčné schopnosti. |
| `Phi-3-medium-4k-instruct`             | 14 Miliard           | ~1120-1150                     | ~7.0 GB (odhad)          | Výkonnější verze Phi-3. [1]                                     |
| **Větší a výkonnější modely**         |                      |                               |                          |                                                                 |
| `Mixtral-8x7B-Instruct-v0.1` (MoE)   | 46.7 Miliard (efektivně ~13B aktivních) | ~1110-1140 | ~25-30 GB                | Skvělá kvalita, ale náročnější na VRAM.        |
| `Llama-3-70B-Instruct`                 | 70 Miliard           | ~1200-1230                     | ~40-43 GB                | Špičkový open-source model, vyžaduje výkonný HW.  |
| `Qwen1.5-72B-Chat`                     | 72 Miliard           | ~1180-1210                     | ~40-45 GB (odhad)        | Velmi výkonný, konkurent Llama 3 70B.             |
| `Command R+` (Cohere)                  | 104 Miliard          | ~1190-1220                     | ~60-63 GB                | Extrémně schopný, ale velmi náročný na zdroje.   |
