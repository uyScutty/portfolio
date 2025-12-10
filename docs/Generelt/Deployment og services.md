
*** Deployment og services.

1. .NET-delen er én samlet deploybar enhed (modulær monolit)

Vi deployer hele .NET-applikationen som én container, fordi:

Domænet hænger tæt sammen (blog, reviews, membership, profiler).

Clean Architecture sikrer rene afhængigheder.

Vertical Slices gør features isolerede uden at splitte systemet fysisk.

Én deployment holder kompleksiteten nede.

→ Det giver en robust og enkel kerneapplikation, der er let at vedligeholde og teste.

2. Python AI-delen køres som en separat service

AI-logik lever i sin egen container og sin egen tekniske stak, fordi:

Python har langt bedre bibliotekstøtte til embeddings, LLM'er og vektor-databaser.

AI må ikke påvirke eller ændre domænelogik i .NET.

Den kan skaleres, opdateres eller udskiftes uafhængigt af resten af systemet.

Den fungerer som en ren ekstern integration: .NET → API → AI-service.

→ AI holdes teknisk isoleret, men integreres kontrolleret.

3. Fælles database (Postgres) i egen container

Databasen køres separat, fordi:

Det giver tydelig isolation mellem app og data.

Det gør det muligt at migrere, tage backups og opgradere uden at påvirke koden direkte.

Postgres passer perfekt til Clean Architecture, hvor domain og data er adskilt.

→ Det giver stabilitet og fleksibilitet i drift.

4. Infrastruktur er altid udskiftelig

Alle tekniske afhængigheder (email, repositories, AI, API’er, logging) ligger i Infrastructure-laget, hvilket betyder:

Man kan skifte database

Skifte email-udbyder

Udskifte AI-service

Tilføje nye API-gateways

…uden ændringer i Domain eller Application.

→ Det er netop formålet med Clean Architecture: teknologien må aldrig eje forretningen.

5. Arkitekturen gør fremtidig opsplitning muligt

Selvom vi deployer som én modulær monolit i dag, er systemet bygget sådan, at:

Hver feature er isoleret (Vertical Slice)

Domænet er rent og klart afgrænset

Infrastruktur er pluggable

Python-AI’en er allerede en ekstern service

→ Hvis systemet vokser, kan man bryde enkelte moduler ud som microservices senere, uden at lave alt om.

Kort konklusion – den stærke sætning

Vi deployer .NET-applikationen som én modulær monolit for at holde domænet samlet, simpelt og testbart, mens AI-delen kører som en isoleret Python-service for fleksibilitet og teknisk specialisering. Clean Architecture gør infrastrukturen udskiftelig og forbereder systemet naturligt til microservices, hvis behovet opstår
