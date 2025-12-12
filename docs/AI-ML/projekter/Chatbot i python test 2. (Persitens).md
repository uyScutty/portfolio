
# Persistent Vector Store

Formål:  
At gøre embeddings permanente, så de ikke forsvinder når programmet stopper — i modsætning til Projekt 2, som kørte “in-memory”.

her vil vi:
- FAISS index i RAM
- Gemmer index på disk (`faiss_index.idx`)
- Gemmer metadata (teksterne) i JSON (`metadata.json`)
- Loader index igen og kan søge i det

Her har jeg valgt efter valg af model.
opsat "faiss_index.idx" til at være stedet hvor vektor-indexet bliver gemt
og "metadata.json" til at indeholde tekst-dokumenter.

![[Pasted image 20251125001146.png]]
Bagefter bliver hvert dokument embedded  til en 384-dimensionel vektor. via modellens encoder.
Herefter  bliver filen oprettet eller indlæst og dokumenter gemmes permanent som i en DB.
Herefter er der en test query.

![[Pasted image 20251125001204.png]]
Efter kørsel af scriptet i mit python miljø, så svarer modellen tilbage på queryen i scriptet.

Her får vi et svar ved at modellen opretter en embedding af teksten og går igennem den for at kunne sammenligne dens vektorer fra teksten vi oprettede i scriptet. Den query der bliver embedded og gemt samt brugt i RAM så længe programmet kører.
![[Pasted image 20251125001348.png]]
I svaret får vi angivet en afstand, der viser hvor relevant tekst svaret er vurderet til at være.
0.425... som første svar gengiver er den korteste af de to tekster, men tekst nummer to er stadigvæk tæt nok på til at være vurderet af relevans i forhold til min query.


# En rigtig Vector Database Workflow**

### ** Embedding af dokumenter**

→ Ved hjælp af SentenceTransformer (MiniLM).

### ** Gemning af embeddings permanent på disk**

→ `faiss_index.idx`  
→ `metadata.json`

### ** Query-embedding (brugerens spørgsmål)**

→ Samme embedding-model → vektor i samme rum.

### ** Semantisk similarity search med FAISS**

→ Finder meningsmæssigt relaterede dokumenter.

### ** Returnering af top-matches med distance**

→ Afstand fortæller relevans.

Dette er **hele fundamentet for RAG (Retrieval-Augmented Generation)**.

Vi har bygget:

##  **En fuld funktionel persistent vector store med FAISS, inkl. opslag og similarity search.**

Og ikke kun in-memory — vi har:

- persistence
    
- metadata-mapping
    
- query-pipeline
    
- semantisk rangerede resultater
    
- genindlæsning mellem sessions
    
- en Python-kodebase der ligner en “rigtig” RAG back-end



