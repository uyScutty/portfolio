# **Læringsside – Uddybning til Etape 3 (Tokenisering & Modeltræning)**



## 🧩 **Hvad er tokenisering – og hvorfor er det vigtigt?**

Tokenisering er processen hvor tekst bliver opdelt i mindre enheder, der kaldes _tokens_.  
Modellerne arbejder ikke med ord som vi kender dem, men med talrækker som repræsenterer tokens.

Eksempel:  
Ordet _”sunhedstilstand”_ kan blive delt i flere tokens:

- sund
    
- hed
    
- stil
    
- stand
    

Dette afhænger af den algoritme modellen bruger.

Tokenisering er vigtig fordi:

- den bestemmer **hvordan modellen forstår tekst**
    
- den påvirker **pris** (flere tokens = dyrere)
    
- den påvirker **kvalitet** (fagtermer → bedre eller dårligere delt)
    
- den påvirker **præcision**, især i sundhedsdata
    

---

## 🔧 **Byte Pair Encoding (BPE)**

En af de mest brugte algoritmer.

Princip:  
Start med helt små enheder (bogstaver), og slå de kombinationer sammen der forekommer oftest.

Fordele:

- effektiv til mange sprog
    
- håndterer nye ord godt
    
- bruges i GPT, Claude, DeepSeek, Llama
    

Ulemper:

- faglige ord kan blive delt meget, hvilket gør dem sværere for modellen
    

---

## 🔧 **WordPiece**

Anvendes bl.a. af BERT.

Princip:  
Finder subwords baseret på sandsynlighed i træningsdata.

Fordele:

- godt til generelle domæner
    
- stabil struktur
    

Ulemper:

- medicinske eller sjældne ord splittes ofte ekstremt meget
    

---

## 🔧 **SentencePiece**

En anden tokeniseringsmetode, ofte brugt i open-source modeller.

Fordele:

- kan arbejde uden mellemrum (“whitespace-agnostic”)
    
- god til ikke-engelske sprog
    

---

## 🧠 **Hvorfor bruger LLM’er subwords?**

Modellerne kan ikke lære alle ord i alle sprog.  
Subwords er en løsning:

- modellen lærer stykker af ord
    
- kan kombinere dem til nye ord
    
- bedre generalisering
    
- færre tokens end bogstav-for-bogstav modeller
    

For sundhedsdomænet betyder det:

- nogle modeller forstår medicinske ord bedre end andre
    
- ord som “betahistine” eller “labyrintitis” kan være ét token eller fem
    
- dette påvirker forståelsen i en chatbot
    

---

## 🔬 **Hvordan påvirker tokenisering modeltræning?**

Når en model trænes, lærer den mønstre baseret på tokens, ikke ord.

Hvis et vigtigt ord bliver delt op i mange subwords, så skal modellen:

- lære mønstre mellem flere tokens
    
- bruge mere kontekst
    
- bruge flere ressourcer
    
- har større risiko for at misforstå sammenhænge
    

→ Derfor er nogle modeller bedre til sundhedsdata end andre.

---

## 💸 **Tokenisering og pris**

Hvis du bruger API-modeller (OpenAI, Claude osv.):

- pris beregnes per token
    
- flere subwords = dyrere
    
- lange ord → dyre forkerte modeller
    

OpenAI og Claude kan være dyrere, fordi deres tokenizers splitter dansk + medicinsk tekst mere aggressivt.

---

## 🆚 **Hvorfor forskellige modeller giver forskellige resultater**


Tokenisering spiller en rolle fordi:

- modeller er trænet på forskellige typer data
    
- deres tokenizere er optimeret til forskellige sprog
    
- subword-logikken påvirker hvordan de “forstår” fagtermer
    
- encoder-modeller og decoder-modeller bruger nogle gange forskellige tokenizers
    

Dette forklarer hvorfor:

- nogle modeller er bedre til dansk
    
- nogle er bedre til medicinske termer
    
- nogle er bedre til komplekse brugerbeskeder
    
- prisen ændrer sig fra model til model
    

