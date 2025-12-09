# **Læringsside – Uddybning til Etape “RAG vs. Fine-tuning”**


Forklaring af forskellen mellem RAG og Fine-tuning

RAG (Retrieval-Augmented Generation) og fine-tuning er to meget forskellige tilgange til at udvide en LLMs evne til at besvare domænespecifikke spørgsmål. De løser forskellige problemer og har forskellige styrker.

1. RAG – Retrieval-baseret viden

RAG tilføjer ekstern viden til en generativ model uden at ændre på selve modellen.
Modellen forbliver uændret, og alt domænespecifikt indhold leveres som kontekst ved hver forespørgsel.

Sådan fungerer RAG

Brugeren stiller et spørgsmål.

Systemet henter relevante dokumenter ved hjælp af embeddings og en vektor-database.

De relevante tekststykker bliver tilføjet som kontekst i prompten.

Modellen svarer ud fra både prompt og dokumenter.

Hvad RAG bruges til

Når viden ændrer sig ofte

Når der er mange dokumenter

Når svaret skal være faktisk forankret i specifikke tekster

Når man vil undgå at træne en model

Når man vil have fuld kontrol over hvilke dokumenter der bruges

Fordele

Fleksibel: dokumenter kan opdateres når som helst.

Billig: ingen træning nødvendig.

Transparent: man kan altid se hvilke kilder modellen brugte.

2. Fine-tuning – modelbaseret læring

Fine-tuning ændrer selve modellen ved at træne den videre på nye data.
Det betyder, at modellen indbygger mønstre, stil og viden direkte i sine parametre.

Hvad fine-tuning bruges til

Faste svarformater

Konsistent skrivestil

Smalle og gentagne opgaver

Klassifikation og strukturerede outputs

Når modellen skal opføre sig på en bestemt måde hver gang

Hvornår fine-tuning ikke er ideelt

Når indhold ændrer sig ofte (kræver løbende retræning)

Når der er mange dokumenter med detaljeret viden

Når man har brug for faktuelle referencer og opdaterbar viden

Når man arbejder med bredt domæneindhold der skifter over tid

3. Sammenligning
Dimension	RAG	Fine-tuning
Hvad ændres?	Ingen modelændring. Kun dokumenter.	Selve modellen ændres.
Opdatering af viden	Meget let – tilføj eller erstat dokumenter.	Kræver ny træning.
Bedst til	Faktuelt indhold, der ændrer sig.	Fast form/skrivestil.
Krav	Embeddings + vector store.	Træningsdata + GPU.
Output	Svar baseret på dokumenter + prompt.	Svar baseret på modelens indlærte parametre.
4. Hvorfor man ofte vælger RAG

RAG fungerer godt når:

systemet skal trække direkte på tekstkilder, artikler eller opslagsværk

viden opdateres ofte

man vil have fuld kontrol over hvad modellen må bruge

forskellige agenter skal deles om samme videns-base

finetuning ville være unødigt tunge processer

RAG giver desuden mulighed for at styre både tone og adfærd via few-shot prompting, uden behov for træning.

5. Kort opsummering

RAG tilføjer kontekst – modellen læser dokumenterne ved hver forespørgsel.

Fine-tuning tilføjer færdigheder eller stil – modellen ændrer sin adfærd permanent.

RAG er bedst, når viden ændrer sig og skal være faktuelt korrekt.

Fine-tuning er bedst, når form og output skal være fuldstændig ens hver gang.
