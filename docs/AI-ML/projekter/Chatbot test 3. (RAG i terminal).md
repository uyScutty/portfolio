Målet:  
 At tage de dokument-matches vi finder via FAISS  
 jeg sender dem ind som kontekst til Llama 3 (via Ollama)  
 Modellen genererer et svar baseret på egen videnbase

jeg kobler:

- embeddings
    
- similarity search
    
- RAG prompt
    
- en rigtig LLM
    
- og returnerer et AI-svar

# **Hvad vi bygger nu

1️ Jeg skriver et spørgsmål i terminalen  
2️ Python embedder spørgsmålet  
3️ Python spørger FAISS → finder top-matches  
4️ Vi bygger en _RAG-prompt_: 
5️ Python kalder **Llama 3** via Ollama  
6️ Terminalen viser et _rigtigt AI-svar baseret på dine data_


Til dette projekt har jeg oprettet et nyt script.
![[Pasted image 20251124235219.png]]
# Hvad sker der her?

- jeg loader det gemte FAISS-index
    
- jeg loader metadata (dokumenter)
    
- jeg loader embedding-modellen
    
- jeg opretter en Ollama-client (for at tale med Llama 3)
    

![[Pasted image 20251124235316.png]]# 

|Trin|Hvad sker der?|
|---|---|
Jeg skriver et spørgsmål i terminalen|
Query embeddes til en vektor|
FAISS laver similarity search|
Systemet slår tekster op i metadata og viser dem



![[Pasted image 20251124235427.png]]


### Vi bygger en robust RAG-prompt

Prompten fortæller modellen:

- _brug kun konteksten_
    
- _vær ærlig hvis konteksten ikke har svaret_
    
- _her er dokumenterne_
    
- _her er spørgsmålet_
    


![[Pasted image 20251124235545.png]]# **Hvad sker der her? (kort og teknisk)**

### ✔ **client.generate(...)**

Dette kalder Ollama-serveren på:

`http://localhost:11434`

Og sender RAG-prompt ind i modellen:

- Prompten indeholder de _retrieved documents_
    
- og spørgsmålet
    

### Modellen genererer et svar

Llama 3 bruger:

kontekst (dokumenter)
    
og selve spørgsmålet til at lave et nyt, kontekstbaseret svar.

###  Vi udtrækker svaret

`ai_answer = response['response']`

###  Og printer det

Og vi får et RAG-svar

![[Pasted image 20251125001729.png]]
Her ses tydeligt at der tages udgangspunkt i vores dokumenter fra [[Chatbot i python test 2. (Persitens)]]
Modellen kan nemt besvare spørgsmålet via teksterne, da det er præcis samme kontekst og vidensområde det omhandler.


Jeg testede også modellen med et spørgsmål der ikke helt giver mening i forhold til de tekster den henter via RAG. og her blev svaret tydeligt påvirket af modellens egen viden. Her bliver dokumenterne taget med som kontekst, men her er der en langt større påvirkning fra anden viden, da det træder lidt ud over de simple teksters kontekst.
![[Pasted image 20251125124725.png]]
Denne model fungerer via RAG stadigvæk med egen fantasi



## 1) Dokumenterne omdannes til embeddings

- jeg har nogle små tekststykker (dine dokumenter).
    
- De sendes gennem en embedding-model (MiniLM).
    
- Resultatet er vektorer (fx længde 384), som placeres i en FAISS-database.
    

Dette gør det muligt at sammenligne betydning, ikke ord.

##2) FAISS bruges til at finde de mest relevante dokumenter

Når man stiller et spørgsmål:

→ Spørgsmålet embeddes til en vektor  
→ FAISS laver vektor-sammenligning (L2 distance)  
→ De nærmeste dokumenter findes (Top-K resultater)

Det er dine "fundne relevante dokumenter".



## **3) Disse dokumenter sendes som kontekst til Llama3**

Dine dokumenter kommer ind før spørgsmålet:

> “Her er nogle dokumenter. Brug dem til at svare så godt som muligt.”

Det betyder at modellen forstår, hvad dit projekt handler om, før den svarer.


## 4) Modellen bruger både:

- Mine dokumenter (RAG-kontekst)
    
- Sin egen træningsviden**
    

RAG påvirker svaret kraftigt, men modellen supplerer med sin almindelige viden.

Derfor får jeg:

- Relevante pointer fra dokumenter
    
- Ekstra detaljer fra modellens generelle viden
    



## **5) Output er et AI-svar, der er forankret i mine dokumenter, men ikke begrænset til dem

Derfor gav spørgsmåler “kan maskinlæring hjælpe på sundhed?” et langt, rigtigt sundhedssvar:

- Dokumenterne gjorde svaret relevant
    
- Modellen fyldte selv på med detaljer
