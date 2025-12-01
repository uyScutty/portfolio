
---

## **MVC i praksis 

I undervisningen lærte vi MVC gennem ASP.NET MVC, hvor:

- **Controlleren** håndterer HTTP-requests
- **Modellen** repræsenterer de data, som viewet skal vise
- **Viewet** er en Razor Page (.cshtml), der renderes af serveren

Det er en klassisk server-renderet webmodel, hvor hvert klik fører til et nyt HTTP-request og en ny server-side rendering.

### **Refleksion:**

MVC giver en klar separation i UI'et og fungerer godt til traditionelle webapplikationer, hvor hvert request er selvstændigt.  
Men i vores projekt havde vi brug for:

- **real-time UI-opdateringer**
- **fulde komponenter med state**
- **kompleks interaktion (chat, medlemsskabshåndtering, AI-integration)**
- **data binding i UI'et**

Dette passer ikke godt til MVC’s stateless request-model.

MVC er altså stærkt til struktureret server-baseret UI,  
men **det passer ikke altid til et moderne, interaktivt Blazor-baseret system**.


#  **MVC i forhold til vores systemarkitektur**

Når vi sætter MVC i forhold til **Clean Architecture + Vertical Slice + DDD**, bliver forskellen tydelig:

## **MVC’s rolle i systemet (hvis det var brugt):**

- ville ligge 100% i **UI-laget**
- ville IKKE påvirke Domain/Application/Infrastructure
- ville være en teknik til at strukturere UI views

#  **Hvornår bruger man hvad i et professionelt projekt?**

##  Man bruger MVC når:

- applikationen er primært stateless
- man laver klassisk request/response UI
- SEO-optimering er vigtigt
- man har simple UI’er (fx formularer og tabeller)
- man bygger et REST-API via controllers

MVC passer også til microservices-API’er, fordi controllers er gode entry-points.



#  **Perspektivering: 

---

## **1. UI-udvikling (MVC & Blazor) → Forståelse af præsentationsmønstre**

Tidligere har vi arbejdet med:

- **MVC** → server-renderet arkitektur, controller-flow
- **Blazor (MVVM-inspireret)** → komponenter, state management, binding

Denne viden er essentiel for at forstå:

- hvorfor MVC _ikke_ fungerede til dit projekt
- hvorfor Blazor’s MVVM-lignende model understøtter real-time UI
- hvordan UI passer ind som “yderste lag” i Clean Architecture
- hvordan vertical slices giver en naturlig mappe- og feature-struktur

**Perspektiv:**  
UI-fagene gav os evnen til at forstå præsentationsniveauet, så systemarkitekturen kan afgrænse det fra forretningskodens domæne.



