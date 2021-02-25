---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Introduktion till beräknade attribut
topic: guide
type: Dokumentation
description: Beräknade attribut är funktioner för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# (Alfa) Översikt över beräknade attribut

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering.

Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Dessa beräknade attributvärden kan sedan visas i en profil, användas för att skapa ett segment eller nås via ett antal olika åtkomstmönster.

Den här guiden hjälper dig att bättre förstå vilken roll beräknade attribut har i Adobe Experience Platform.

## Förstå beräknade attribut

Med Adobe Experience Platform kan du enkelt importera och sammanfoga data från flera källor för att generera [!DNL Real-time Customer Profiles]. Varje profil innehåller viktig information om en individ, t.ex. kontaktinformation, inställningar och inköpshistorik, vilket ger en helhetsbild av kunden.

En del av den information som samlas in i profilen är lätt att förstå när datafälten läses direkt (t.ex.&quot;förnamn&quot;) medan andra data kräver att man utför flera beräkningar eller använder andra fält och värden för att kunna generera informationen (t.ex.&quot;köpsumma för livstid&quot;). Om du vill göra dessa data lättare att förstå snabbt kan du med [!DNL Platform] skapa beräknade attribut som automatiskt utför dessa referenser och beräkningar och returnera värdet i rätt fält.

Beräknade attribut inkluderar att skapa ett uttryck, eller &quot;rule&quot;, som fungerar på inkommande data och lagrar resultatvärdet i ett profilattribut. Uttryck kan definieras på flera olika sätt, så att du kan ange att en regel endast utvärderar inkommande händelser, inkommande händelse- och profildata eller inkommande händelse, profildata och historiska händelser.

### Användningsfall

Användningsexempel för beräknade attribut kan omfatta allt från enkla beräkningar till mycket komplexa referenser. Här följer några exempel på hur du kan använda beräknade attribut:

1. **[!UICONTROL Percentages]:** Ett enkelt beräknat attribut kan inkludera att ta två numeriska fält på en post och dela dem för att skapa en procentsats. Du kan t.ex. ta det totala antalet e-postmeddelanden som skickas till en individ och dividera det med antalet e-postmeddelanden personen öppnar. Om du tittar på det resulterande attributfältet visar det snabbt hur många procent av det totala antalet e-postmeddelanden som öppnats av den enskilda personen.
1. **[!UICONTROL Application use]:** Ett annat exempel inkluderar möjligheten att samla det antal gånger en användare öppnar ditt program. Genom att spåra det totala antalet öppna applikationer, baserat på enskilda öppna händelser, kan ni leverera specialerbjudanden eller meddelanden till användarna på deras 100:e öppna sida, vilket främjar ett djupare engagemang i ert varumärke.
1. **[!UICONTROL Lifetime values]:** Det kan vara svårt att samla in löpande summor, t.ex. ett livstidsvärde för en kund. Detta kräver att historiksumman uppdateras varje gång en ny köphändelse inträffar. Med ett beräknat attribut kan ni göra detta mycket enklare genom att behålla livstidsvärdet i ett enda fält som uppdateras automatiskt efter varje lyckad köphändelse som gäller kunden.

## Kända begränsningar

### Försenad tillgänglighet för nya beräknade attribut

Tillgängligheten för nya beräknade attribut kan fördröjas upp till 2 timmar efter att motsvarande schemaattribut har lagts till i unionsschemat.

Fördröjningen beror på den aktuella cachelagringskonfigurationen. Efter alfa kan cachens uppdateringsfrekvens ökas.

### Beroendespårning i segment

Schemaattribut som redan har använts i ett segmentdefinitionsuttryck men senare konverterats till ett beräknat attribut spåras inte som ett beroende för det segmentet.

Eftersom inget beroende har identifierats utvärderas inte det associerade beräknade attributet automatiskt av Experience Platform varje gång segmentdefinitionen utvärderas.

Alternativt kan du skapa beräknade attribut med hjälp av en specifik blandning som lägger till nya beräknade attribut som inte står i konflikt med befintliga attribut. Ett annat alternativ är att återskapa segmentet med rätt beroendespårning för de nya beräknade attributen.