# CS5760 Natural Language Processing — Homework 1  
University of Central Missouri  
**Department of Computer Science & Cybersecurity**  
**Student:** Santhosh Reddy Kistipati  
**Student ID:** 700776947  

---

## Assignment Overview
This repository contains my solutions for **Homework 1 of CS5760 — NLP**.  
The assignment covered **theoretical problems, manual calculations, regular expressions, tokenization, subword models (BPE), and edit distance**.  
This README provides explanations for each question and instructions to run the code.  

---

## Question Explanations  

### Q1 — Regular Expressions  
- **Task:** Write regex for different language/text processing cases.  
- **Solutions:**  
  1. Match U.S. ZIP codes (`12345`, `12345-6789`, `12345 6789`):  
     `\b\d{5}(?:[ -]\d{4})?\b`  
  2. Words that do **not** start with capital letters:  
     `\b(?![A-Z])[a-z]+(?:['’-][a-z]+)*\b`  
  3. Numbers with signs, commas, decimals, scientific notation:  
     `\b[+-]?(?:(?:\d{1,3}(?:,\d{3})+|\d+)(?:\.\d+)?|\.\d+)(?:[eE][+-]?\d+)?\b`  
  4. Variants of “email”:  
     `(?i)\bE(?:\s|[-\u2013])?mail\b`  
  5. Interjection **go/goo/gooo…**:  
     `\bgo+\b[!.,?]?`  
  6. Lines ending with `?`:  
     `(?m)^[^\n]*\?[)"\]\u201D\u2019\s]*$`  

---

### Q2 — Tokenization  
- **Task:** Tokenize a paragraph manually and compare with NLTK tool.  
- **Steps:**  
  1. Manual: Space-based split + regex cleanup for clitics and punctuation.  
  2. Tool: `nltk.word_tokenize`.  
- **Findings:**  
  - Both methods tokenize punctuation correctly.  
  - Small differences occur (e.g., contractions with apostrophes).  
- **Answer:** Tool-based tokenization is more robust, while manual rules highlight mismatches.  

---

### Q3 — Byte Pair Encoding (BPE)  

**3.1 Manual BPE on Toy Corpus**  
- Corpus: `low low low low low lowest lowest newer newer newer newer newer newer wider wider wider new new`  
- Added end-of-word `_`.  
- Performed **3 merges**:  
  1. `e+r → er`  
  2. `er+_ → er_`  
  3. `n+e → ne`  

**3.2 Mini-BPE Learner (Code)**  
- Implemented BPE learner in Python.  
- Printed **top pairs per step** and segmented words like:  
  - `new → ['new', '_']`  
  - `newestest → ['new', 'e', 's', 't', 'e', 's', 't', '_']`  
- Reflection: Subwords solve OOV; `er_` aligns with a real morpheme.  

**3.3 Train BPE on Paragraph**  
- Paragraph: 6 sentences on AI/NLP.  
- Learned **30 merges**.  
- Frequent merges: `s+_`, `i+n`, `t+i`, `e+n`, `a+n`.  
- Longest tokens: `ation`, `ing_`, `tion`, `and_`, `ter`.  
- Example segmentations:  
  - `developers → ['dev', 'el', 'op', 'er', 's_']`  
  - `processing → ['pro', 'c', 'es', 's', 'ing_']`  
- Reflection: Subwords capture **stems, prefixes, suffixes**.  
  - **Pros:** Handles morphology, reduces OOV.  
  - **Cons:** Frequency-driven merges may ignore true morpheme boundaries, domain-sensitive.  

---

### Q4 — Minimum Edit Distance  
- Word pair: **Sunday → Saturday**  
- **Model A (Sub=1, Ins=1, Del=1):** Distance = 3  
  - Insert `a`, Insert `t`, Substitute `n → r`.  
- **Model B (Sub=2, Ins=1, Del=1):** Distance = 4  
  - Insert `a`, Insert `t`, Delete `n`, Insert `r`.  
- **Reflection:**  
  - Distances differ because substitution is costlier in Model B.  
  - Insertions were most useful due to length mismatch.  
  - Spell-check: substitutions cheap (typos). DNA alignment: substitutions costlier to reflect mutations.  

---

## How to Run the Code  

1. Clone the repo:  
   ```bash
   https://github.com/santhoshK12/Homework1NLP/tree/main
   cd Homework1NLP
   ```  
2. Install dependencies:  
   ```bash
   pip install nltk
   ```  
3. Run the script:  
   ```bash
   python homework1nlp.py
   ```  
4. Or open `Homework1nlp.ipynb` in **Google Colab**.  
