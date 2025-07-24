---
title: Arkitekturuppgraderingar till Real-Time CDP B2B edition
description: Läs det här dokumentet om du vill veta mer om de omfattande uppgraderingarna av arkitekturen till Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
hide: true
hidefromtoc: true
source-git-commit: 78444555178773a8305ba27aaaf7998fe279a71d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Arkitekturuppgraderingar till Real-Time CDP B2B edition

>[!IMPORTANT]
>
>I det här dokumentet beskrivs uppgraderingar av arkitekturen till Real-Time CDP B2B- och B2P-utgåvor. **Du behöver inte utföra någon åtgärd** just nu. I det här dokumentet finns information om hur uppgraderingarna kommer att påverka Adobe Experience Platform befintliga funktioner. Kontakta Adobe Account Team om du har några frågor.

Adobe har omdesignat Real-Time CDP B2B- och B2P-utgåvorna för att förbättra skalbarhet, prestanda och tillförlitlighet, samtidigt som de har stöd för mer avancerade B2B-användningsfall. För att alla kunder ska kunna dra nytta av dessa förbättringar kommer Adobe att uppgradera alla befintliga B2B- och B2P-kunder till den nya arkitekturen.

Använd den förbättrade arkitekturen för följande fördelar:

* **Skalbarhet för datainmatning**: Förbättrat stöd för B2B-relationer med hög kardinalitet, till exempel konton som är anslutna till tusentals personer.
* **Prestanda och tillförlitlig publikutvärdering**: Snabbare och mer flexibel segmentering för komplexa B2B-målgrupper.
* **entitetsupplösning**: Förbättrad identitetsupplösning för B2B-enheter, förbättrad datakvalitet och reducerad duplicering för att möjliggöra mer korrekt segmentering och aggregering.

## Nya funktioner

Här följer några viktiga förbättringar som ingår i uppgraderingen av arkitekturen.

### Ögonblicksbilder av konton för målgruppsmedlemskap

Med den nya B2B-arkitekturen inkluderas nu information om målgruppsmedlemskap för kontoenheter vid export av ögonblicksbilder. Med den här funktionen kan du få åtkomst till målgruppsstatus, tidsstämplar och medlemsindikatorer på kontonivå.

Med den här uppgraderingen kan du nu:

* Gör det möjligt för marknadsförings- och verksamhetsteam att direkt validera medlemskap för målgrupper.
* Uppnå en enhetlig funktion mellan er profil (person) och era kontosegmenteringsmodeller, vilket ger en enhetlig upplevelse på alla enheter.

Mer information finns i dokumentationen för [kontomålgrupper](../segmentation/types/account-audiences.md).

### Målgrupper som omfattar B2B-enheter

Beräkningar av målgruppsstorlek för målgrupper med B2B-enheter beräknas nu med exakt precision. Dessa uppskattningar är tillgängliga under förhandsgranskningen och ger mer korrekta och tillförlitliga insikter för målgrupper som involverar komplexa B2B-relationer.

Med den här uppgraderingen kan du nu:

* Använd insikter från exakta uppskattningar av målgruppsstorlek för att förbättra planering och beslutsfattande under målgruppsprocessen.
* Designa tryggt komplexa B2B-målgrupper med kunskap om exaktare målgruppsuppskattningar.
* Få smartare kampanjplanering, mer exakt målinriktning och bättre resurstilldelning.

Mer information finns i dokumentationen för [kontomålgrupper](../segmentation/types/account-audiences.md).

### Fullständig sökning efter händelser på personnivå i kontomålgrupper

Kontogrupper kan nu utnyttja hela historiken med händelser på personnivå, vilket sträcker sig bortom det föregående 30-dagars uppslagsfönstret.

Med den här uppgraderingen kan du nu:

* Skapa mer omfattande målgrupper baserat på hela historiken med tillhörande händelser på personnivå.
* Få djupare och exaktare målgruppsdefinitioner genom att utnyttja långsiktiga beteendedata.
* Identifiera värdefulla konton baserat på djupare engagemangsmönster över tid.
* Stöd för användningsfall som kräver insikter från historiska händelser, t.ex. om långa försäljningscykler eller fördröjda köpsignaler.

Mer information finns i dokumentationen för [kontomålgrupper](../segmentation/types/account-audiences.md).

## Uppgradera till befintliga funktioner

Följande funktioner har uppdaterats som en del av uppgraderingarna av B2B-arkitekturen.

### Uppdateringar till målgrupper med flera enheter med B2B-attribut och Experience Events

Som en del av den nya uppgraderingen av arkitekturen kan Experience Event-filter inte längre användas inom en enda målgrupp med flera enheter som innehåller B2B-attribut.

Om du vill uppnå samma målgruppslogik använder du segmentmetoden:

1. Skapa en Experience Event-målgrupp: Definiera beteendeförhållandena separat. Exempel:&quot;Personer som besökt prissidan de senaste tre dagarna.&quot;
2. Skapa en målgrupp med flera enheter med B2B-attribut: Se Experience Event-målgruppen som en del av målgruppens kriterier. Exempel:&quot;Personer som är en **&#39;beslutsfattare&#39;** för en möjlighet där kontot finns i **&#39;Finanssektorn&#39;** och som är medlem i den målgrupp som besökt prissidan de senaste tre dagarna.

När uppgraderingen är klar måste alla nya målgrupper med flera enheter med B2B-attribut och Experience Events skapas enligt segmentsegmentmetoden. Dessutom måste ni validera målgruppsmedlemskapet för att säkerställa förväntat beteende.

### Enhetsupplösning och sammanslagning med tidsprioritet inom B2B-målgrupper

Som en del av uppgraderingen av arkitekturen har Adobe infört en lösning för konton och affärsmöjligheter som körs dagligen. Denna förbättring gör att Experience Platform kan identifiera och sammanställa flera poster som representerar samma verkliga enhet, vilket ger enhetligare data och möjliggör mer korrekt målgruppssegmentering.

Med den här uppgraderingen kan du nu:

* Använd [!DNL Profile Access] API:er för att visa de senaste sammanfogningsprofilerna när de dagliga entitetsupplösningsjobben är klara.
* Utnyttja den förbättrade exaktheten och enhetligheten i era kontouppgifter och affärsmöjlighetsdata för segmentering, aktivering och analys.

Läs [[!DNL Profile Access] API](../profile/api/entities.md) om du vill ha mer information.

### Stöd för sammanslagningsprinciper i B2B-målgrupper med flera enheter

Flera målgrupper med B2B-attribut har nu stöd för en enda sammanfogningsprincip - standardprincipen för sammanfogning som du konfigurerar - i stället för flera sammanfogningsprinciper.

Målgrupper som tidigare förlitat sig på en sammanfogningsprincip som inte är standard kan få olika resultat. Om du vill förstå de potentiella förändringarna i målgruppens sammansättning kan du granska och testa alla målgrupper som använder en sammanfogningspolicy som inte är standard. Övervaka dessutom aktiveringsresultaten för att upptäcka eventuella förändringar i målgruppssammansättning på grund av ändringen av sammanfogningspolicyn.

Läs fallguiden [för segmenteringsanvändning för Real-Time CDP B2B edition](./segmentation/b2b.md) om du vill ha mer information.

### Borttagning av B2B-entitetssökning och borttagning i API:t [!DNL Profile Access]

Följande sökfunktioner för B2B-entiteter som använder API:t [!DNL Profile Access] har tagits bort:

* Konto-personrelation
* Relation mellan möjlighet och person
* Campaign
* Kampanjmedlem
* Marknadsföringslista
* Medlemmar i marknadsföringslista

Ta bort begäranden för följande B2B-entiteter som använder API:t [!DNL Profile Access] har tagits bort:

* Konto
* Konto-personrelation
* Möjligheter
* Relation mellan möjlighet och person
* Campaign
* Kampanjmedlem
* Marknadsföringslista
* Medlemmar i marknadsföringslista

Läs [[!DNL Profile Access] API](../profile/api/entities.md) om du vill ha mer information.

### Profilsökningar för konto och affärsmöjlighet

Du kan nu hämta konto- och affärsmöjlighetsscheman som sökdimensionsenheter först efter att de har slutfört den dagliga enhetsupplösningsprocessen. Nya inmatade poster är inte tillgängliga för profilberikning eller segmentdefinitioner förrän nästa entitetsupplösningscykel har slutförts (vanligtvis var 24:e timme).

Du rekommenderas att granska alla användningsfall som kräver åtkomst i realtid till konto- och affärsmöjlighetsdata. Du rekommenderas även att planera för upp till en 24-timmars svarstid när du utformar eller uppdaterar arbetsflöden som är beroende av uppslagsbaserad segmentering eller personalisering med konto- och säljprojektsenheter.

### Föråldrat målgruppsskapande via API för B2B-enheter

Skapande av målgrupper med B2B-enheter via API är föråldrat. Listan över berörda B2B-enheter omfattar:

* Konto
* Möjligheter
* Konto-personrelation
* Relation mellan möjlighet och person
* Campaign
* Kampanjmedlem
* Marknadsföringslista
* Marknadsföringslistans medlem

Mer information finns i [API-handboken för segmentdefinitioner](../segmentation/api/segment-definitions.md).

### Ändringar av målgruppsimporter för flera enheter i sandlådeverktyg

Tack vare uppgraderingarna kan ni inte längre importera målgrupper med flera enheter med B2B-attribut och Experience Events om de exporterades före uppgraderingen. Dessa målgrupper kommer inte att kunna importera och kan inte automatiskt konverteras till den nya arkitekturen. Om du vill kringgå den här begränsningen måste du återexportera dessa målgrupper och sedan importera dem till deras respektive målsandlådor med hjälp av sandlådeverktyg.

Läs [Verktygshandboken för sandlådan](../sandboxes/ui/sandbox-tooling.md) om du vill ha mer information.