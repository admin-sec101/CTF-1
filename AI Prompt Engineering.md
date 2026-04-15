<img width="1800" height="1800" alt="image" src="https://github.com/user-attachments/assets/2a735714-b14c-4205-b47a-3995550d1d96" />

***Prompt Engineering***

Learn how LLMs process text and craft effective prompts for security and adversarial testing

**Task 1: Introdiction**

 I understand the learning objectives and am ready to learn about prompt engineering!

```no answer needed```

**1. Dasar-Dasar LLM**

Mempelajari bagaimana model seperti GPT memproses input teks menggunakan token dan memprediksi kata berikutnya dalam suatu rangkaian. Bagian ini memberikan dasar teknis tentang keterbatasan dan kemampuan model bahasa.
  
  What is the term for the smallest units that an LLM breaks text into in order to process it?
  
  ```Tokens```

  What parameter would you set to 0.0 to make an LLM behave as close to deterministic as possible?

  ```Temperature```

  What parameter restricts which tokens the model considers by limiting selection to a cumulative probability mass?

  ```Top-p```

  What term describes the maximum working memory of an LLM, measured in tokens?

  ```Context window```

  **2. Anatomi Prompt**

  Menjelaskan komponen utama yang membuat sebuah prompt berhasil, termasuk:
    Instruksi: Tugas yang ingin diselesaikan.
    Konteks: Informasi latar belakang untuk memandu respons.
    Input Data: Data spesifik yang perlu diproses.
    Indikator Output: Format hasil yang diinginkan (seperti JSON, tabel, atau poin-poin).
  
  Which pillar instructs the model on how the answer should be structured, such as bullet points or a JSON object?

  ```Output Format```

  Which pillar specifies rules or limits imposed on the model's response, such as enforcing a tone or forbidding certain topics?

  ```Constraints```

  Which pillar provides the AI with relevant background information or scenario so it understands the situation?

  ```Context```

  Which pillar of prompt engineering defines the core command or action you want the AI to perform?

  ``Instruction```

**3. System vs User Prompts**

  Membahas perbedaan antara:

  System Prompt: Instruksi tingkat tinggi yang menentukan kepribadian, batasan, dan aturan main AI (biasanya tidak terlihat oleh pengguna    akhir).
  User Prompt: Input langsung yang diberikan pengguna saat berinteraksi dengan AI.
    

  What type of prompt is developer-defined, persistent, and remains constant across all sessions?

  ```System prompt```

  What is the term for the intended order of priority between system and user instructions in an LLM application?

  ```Instruction hierarchy```

**4. Teknik Prompting Lanjutan**

   Memperkenalkan metode yang lebih canggih untuk mendapatkan hasil yang akurat:

    Zero-shot: Memberikan instruksi langsung tanpa contoh.
    One-shot / Few-shot: Memberikan satu atau beberapa contoh input-output agar AI memahami pola yang diinginkan.
    Chain-of-Thought (CoT): Meminta AI untuk "berpikir langkah demi langkah" guna memecahkan masalah logika atau keamanan yang kompleks.
    Prompt Templates: Menggunakan placeholder (seperti [LOG_ENTRY]) agar prompt dapat digunakan kembali secara konsisten.

   What is the term for the prompting technique introduced by Google researchers in 2022 that asks models to break tasks into intermediate reasoning steps?

   ```Chain-of-Thought```

   What prompting technique involves providing no examples and relying entirely on the model's pre-trained knowledge?

   ```Zero-shot```

   What prompting technique involves saving and reusing a standardised prompt structure for recurring tasks?

   ```Prompt templates```

   What simple phrase can be added to a prompt to trigger Zero-shot Chain-of-Thought reasoning?

   ```Let's think step by step```

**5. Tantangan Praktis (Challenge)**

Tugas akhir di mana Anda harus menerapkan teknik-teknik di atas untuk menyelesaikan tugas keamanan nyata, seperti:

    Mengklasifikasikan log keamanan.
    Menganalisis kode (seperti Python) untuk menemukan kerentanan seperti SQL Injection.
    Mendeteksi upaya login yang mencurigakan (brute-force atau impossible travel).

  What's the flag?

  ```THM{Pr0mpt_3ng1neer}```

```  text
  Act as a security log analyzer. Review the following authentication logs for any anomalous patterns or potential security threats.

Authentication Log Entry:
[LOG_ENTRY]

Detection Context:
- Time Window for Analysis: [TIME_WINDOW]
- Maximum Allowed Failed Attempts (Threshold): [THRESHOLD]

Instructions:
1. Scan the [LOG_ENTRY] for repeated failure patterns.
2. Flag any user accounts exceeding the [THRESHOLD] within the [TIME_WINDOW].
3. Report any 'impossible travel' anomalies where logins occur from different locations too quickly.

Anomalies Detected:
[Output]
```
  
  <img width="682" height="572" alt="image" src="https://github.com/user-attachments/assets/311d4e1e-c65f-46ec-9f9e-331c7360e21b" />

**Conclusion**

```no answer needed```

