# **Samfundsmæssige aspekter af softwarearkitektur og AI-integration**

Softwarearkitektur handler ikke kun om teknik; den har også tydelige samfundsmæssige konsekvenser. I vores projekt bliver dette især tydeligt, fordi vi arbejder med både **AI**, **persondata**, **sundhedsindhold** og **brugergenereret content**. Valget af arkitektur påvirker derfor både **brugernes sikkerhed**, **systemets kvalitet** og **fremtidens mulighed for vedligehold og udvikling**.

## **1. Sikkerhed og ansvarlig datahåndtering (samfundsperspektiv)**

En ren og velstruktureret arkitektur (Clean Architecture + modulær monolith) har stor betydning for datasikkerhed.  
Når:

- domænelaget er isoleret
- AI ikke har direkte adgang til databasen
- UI ikke kender forretningslogik
- infrastrukturen er tydeligt adskilt

…så reduceres risikoen for datalæk, misbrug og uautoriseret adgang.

I et samfund hvor data (især helbredsdata) er ekstremt følsomme, er dette en essentiel del af ansvarlig softwareudvikling.

---

## **2. Bæredygtighed og langsigtet digital infrastruktur**

Dårligt designede systemer forældes hurtigt og kræver:

- dyr vedligeholdelse
- store omskrivninger
- ressourcetunge driftsmiljøer
- risiko for fejl og ustabilitet

Ved at bygge en modulær monolith:

- kan systemet vokse gradvist
- moduler kan udskiftes uden at genopbygge alt
- AI-delen kan skaleres uafhængigt
- driftsomkostninger holdes nede (økonomisk bæredygtighed)

God arkitektur har derfor en **samfundsøkonomisk dimension**, fordi robuste systemer sparer tid, penge og energi — både for virksomheder, det offentlige og brugerne.

---

## **3. Samfundsmæssig tillid til AI-baserede systemer**

Når AI integreres forkert, risikerer man:

- mangel på gennemsigtighed
- bias i beslutningsprocesser
- fejlfortolkning af data
- manglende kontrol over forretningskritiske flows

Ved at placere AI som _eksternt modul_ i vores arkitektur (ikke i Domain, ikke i Application), får vi:

- kontrol over hvilke data AI får adgang til
- mulighed for at udskifte eller forbedre AI uden risiko
- transparens i hvordan AI bruges
- bedre mulighed for revision og dokumentation

Dette bidrager til digital ansvarlighed — en central samfundspraksis i dag.

