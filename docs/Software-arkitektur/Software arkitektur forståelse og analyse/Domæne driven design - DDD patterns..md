

#  Hvorfor vi havde brug for DDD i projektet



Projektet havde:

- content med regler og moderation
- medlemskaber (premium, owner, normal)
- reviews og opsummeringer
- domænehændelser
- forskellige brugertyper
- flere bounded contexts
- AI-genererede anbefalinger og analyser
- valideringsregler, workflows og tilstande

Dette er præcis den type system, hvor DDD giver værdi.


#  Hvordan DDD understøtter vores arkitektur

DDD passer perfekt ovenpå Clean Architecture.

##  Domain-laget får rene modeller

Entities og Value Objects uden EF Core eller AI-logik.

##  Application-laget bliver orkestrator

Use case handlers styrer workflows gennem Commands og Queries.

##  Infrastructure bliver teknologisk adapter

Database, AI, Identity, Email og Logging er plugins.

##  Vertical Slice forbinder UI til use cases

Hver slice aktiverer en handler, som interagerer med domænet.

DDD beskriver **hvad der foregår i domænet**, Clean Architecture beskriver **hvor det ligger**, og Vertical Slice beskriver **hvordan det bruges**.

---

#  ** Entities — ting med identitet**

Eksempler fra projektet:

- **Content** (post/artikel)
- **Review**
- **Membership**
- **User**

Karakteristika:

- har ID
- ændrer tilstand
- har regler
- kan trigge domain events

**I projektet:**  
Entities ligger i _Domain_ og indeholder AL logik der hører til objektets kerne.



#  
#  Domain Services — logik der ikke hører til en enkelt entity**

Eksempler:

- Beregning af medlemskab tilstand
- Moderationsstrategi for content
- Aggregation af data på tværs af entities

Domain services ligger i **Domain**, men de _orkestrerer_ regler mellem flere modeller.

---

#  Aggregates — grupper af entities der hænger sammen**

Eksempler:

- Content + Reviews kan være separate aggregates
- Membership kan være sin egen aggregate

Regel:

> “Kun aggregate root må eksponeres til omverdenen.”

Dette styrer dataintegritet og reducerer coupling.

---

#  Domain Events — hændelser udløst af domænet**

Brugt aktivt i projektet:

- **PostPublishedEvent**
- **MembershipActivatedEvent**
- **ReviewCreatedEvent**

Fordele:

- løs kobling mellem domæner
- Application-layer håndterer sideeffekter
- Infrastructure udfører tekniske ting (fx email, AI analyse)

Dette passer perfekt til Clean Architecture’s afhængighedsregler.

#  Bounded Contexts — de naturlige domæneopdelinger**

I vores projekt fandt vi disse bounded contexts:

- **Content**
- **Membership**
- **Review**
- **Notification**
- **Chat/AI**

Hver context har:

- egne modeller
- egne events
- egne regler
- egne use cases
- egne vertical slices
    

Dette er fundamentet for modulær monolith.
