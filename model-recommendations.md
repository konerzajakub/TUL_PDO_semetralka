# 🚀 Příručka k výběru jazykového modelu

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

## 📊 Doporučení modelů (GGUF) dle HW

| Model                                  | Velikost (Parametry) | Odhadované nároky na paměť (Q4_K_M) |
|----------------------------------------|----------------------|--------------------------|
| **Malé a efektivní modely**            |                      |                          |
| `Phi-3-mini-4k-instruct`               | 3.8 Miliard          | ~2.4 GB                  |
| `Ministral-8B-2410`                    | 8 Miliard            | ~4.9 GB                  |
| `Meta-Llama-3.1-8B-Instruct`           | 8 Miliard            | ~4.9 GB                  |
| **Středně velké modely**               |                      |                          |
| `Qwen1.5-14B-Chat`                     | 14 Miliard           | ~8.0 GB                  |
| `Phi-3-medium-4k-instruct`             | 14 Miliard           | ~7.0 GB           |
| **Větší a výkonnější modely**         |                      |                          |
| `Mixtral-8x7B-Instruct-v0.1` (MoE)   | 46.7 Miliard  | ~25-30 GB                |
| `Llama-3-70B-Instruct`                 | 70 Miliard           | ~40-43 GB                |
| `Qwen2-72B-Instruct`                   | 72 Miliard           | ~40-45 GB     |
| `Command R+` (Cohere)                  | 104 Miliard          | ~60-63 GB                |     
