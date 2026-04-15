# TryHackMe: AI/ML Security Threats - Writeup

Repository ini berisi ringkasan jawaban dan konsep kunci untuk modul **AI/ML Security Threats** di TryHackMe. Modul ini membahas berbagai ancaman keamanan yang menargetkan model kecerdasan buatan dan cara mitigasinya.

## 📝 Ringkasan Jawaban

### Task 2: Introduction to AI/ML Security
*   **What category of machine learning combines both labelled and unlabelled data?**
    *   `Semi-supervised Learning`
*   **What is the first layer in a neural network that handles incoming raw data?**
    *   `Input Layer`
*   **Which learning method does not require human-labelled data and can extract features from raw, unstructured input?**
    *   `Unsupervised Learning`
*   **What are the weighted connections between nodes in a neural network meant to simulate in the human brain?**
    *   `Synapses`
*   **What type of AI model enabled major advancements in ChatGPT and similar tools?**
    *   `Large Language Models`
*   **What is the first training stage where an LLM processes massive amounts of data?**
    *   `Pre-training`
*   **What type of neural network introduced by Google in 2017 powers modern LLMs?**
    *   `Transformer`

### Task 3: AI Model Security Threats
*   **What framework was developed by MITRE to guide the understanding of AI-specific cyber threats?**
    *   `MITRE ATLAS`
*   **What type of attack involves cloning an AI model by interacting with its API?**
    *   `Model Theft`
*   **What generative AI technique can replicate a person’s voice or appearance with high realism?**
    *   `Deepfake`
*   **What common social engineering attack has become harder to detect due to AI-generated fluent and convincing messages?**
    *   `Phishing`

### Task 4: Defensive AI
*   **According to IBM, how many days faster does AI help identify and contain breaches?**
    *   `108`
*   **What cybersecurity task benefits from AI helping to imagine attacker behavior we might not consider?**
    *   `Threat Hunting`
*   **Explainability tools such as SHAP and LIME help with what?**
    *   `Model Transparency`

### Task 6: Practical Lab (The Flag)
Berdasarkan nilai teknis yang ditemukan melalui AI Assistant:
*   DNS over HTTPS (DoH) Port: **443**
*   SYN flood timeout: **60**
*   Windows ephemeral port range size: **16384**

**Flag:** `thm{443/60/16384}`

---

## 🚀 Konsep Utama yang Dipelajari
1. **Adversarial Attacks:** Memahami bagaimana input yang dimanipulasi dapat mengecoh model AI.
2. **Data Poisoning:** Pentingnya integritas data pada tahap pelatihan model.
3. **Model Theft:** Risiko keamanan pada API yang terbuka untuk publik.
4. **Defensive AI:** Bagaimana AI digunakan oleh tim SOC untuk mempercepat deteksi ancaman.

## 🛡️ Referensi
*   [TryHackMe AI Security Path](https://tryhackme.com)
*   [MITRE ATLAS Framework](https://mitre.org)
