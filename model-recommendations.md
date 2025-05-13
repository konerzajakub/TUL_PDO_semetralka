# 🚀 Stručný návod pro výběr jazykového modelu

## 🧠 Důležité termíny

* **GGUF:** Populární formát souborů pro LLM, optimalizovaný pro běh na CPU i GPU.
* **Kvantizace:** Technika zmenšení modelu. Výsledkem je kompromis mezi velikostí/rychlostí a přesností.
    * **Typy:** Od `Q2_K` (nejmenší, nejrychlejší, nejnižší kvalita) po `Q8_0` (větší, pomalejší, vyšší kvalita)
    * **Nejvyšší kvalita (`F16`, `F32` - nekvantizované/méně kvantizované):** Tyto modely nabízejí maximální přesnost, ale jsou extrémně náročné.
        * **Požadovaný HW:** Vysoce výkonné GPU s velkou VRAM (např. NVIDIA RTX 4090 s 24GB VRAM, profesionální karty jako NVIDIA A100/H100 s 80GB+ VRAM).
        * **Pro běžné uživatele:** Řešením může být **pronájem cloudových serverů** (AWS, GCP, Azure)

---

## 🛠️ Co zvážit před výběrem modelu?

1.  **RAM:** Kolik máte k dispozici operační paměti? (např. 8GB, 16GB, 32GB+)
2.  **VRAM (GPU):** Máte dedikovanou grafickou kartu a kolik má paměti (vRAM)? (např. 4GB, 8GB, 16GB+)

---

## 📊 Doporučení modelů (GGUF) dle HW (květen 2025)

| HW Konfigurace                     | Doporučená kvantizace         | Velikost* | Příklady modelů (GGUF)                    |
|------------------------------------|-------------------------------|-----------|-------------------------------------------|
| ≤ 8GB RAM / integrovaná GPU        | `Q3_K_S`, `Q4_0`              | ~2-4 GB   | `Phi-3-mini-4k-instruct.Q4_0.gguf`        |
| 8-16GB RAM / 8GB VRAM (GPU)      | `Q4_K_M`, `Q5_0`              | ~4-7 GB   | `Llama-3-8B-Instruct.Q4_K_M.gguf`         |
| 16-32GB RAM / 12GB VRAM (GPU)    | `Q5_K_M`, `Q6_K`              | ~6-10 GB  | `Llama-3-8B-Instruct.Q5_K_M.gguf`         |
| ≥ 32GB RAM / 16GB+ VRAM (GPU)      | `Q6_K`, `Q8_0` | 10GB+     | `Llama-3-8B-Instruct.Q8_0.gguf`, nebo větší modely jako `Llama-3-70B` s agresivní kvantizací (např. `Q4_K_M`) |

> **Důležité:** Větší základní modely (např. 70B) budou i po silné kvantizaci stále vyžadovat výrazně více zdrojů než menší modely (např. 8B) se stejnou kvantizací.
