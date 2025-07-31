---
title: Arkitekturuppgraderingar till Real-Time CDP B2B edition
description: Läs det här dokumentet om du vill veta mer om de omfattande uppgraderingarna av arkitekturen till Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: 1a3be99ca3c270dda6e8dc559359cbe21bb8f4fb
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Arkitekturuppgraderingar till Real-Time CDP B2B edition

>[!IMPORTANT]
>
>I det här dokumentet beskrivs uppgraderingar av arkitekturen till Real-Time CDP B2B- och B2P-utgåvor. Uppgraderingarna kräver inga åtgärder från de flesta kunder. Det finns dock målgrupper som inte kan uppgraderas automatiskt. Adobe kommer att arbeta direkt med dig för att ta itu med dessa scenarier. I det här dokumentet finns information om hur uppgraderingarna kommer att påverka Adobe Experience Platform befintliga funktioner. Kontakta Adobe Account Team om du har några frågor.

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

## Uppgradera till befintliga funktioner

Följande funktioner har uppdaterats som en del av uppgraderingarna av B2B-arkitekturen.

### Uppdateringar till målgrupper med flera enheter med B2B-attribut och Experience Events

Som en del av den nya uppgraderingen av arkitekturen kan Experience Event-filter inte längre användas inom en enda målgrupp med flera enheter som innehåller B2B-attribut.

För att uppnå samma målgruppslogik kan du använda segmentbyggaren för att [lägga till målgrupper och referera till målgrupper](../segmentation/ui/segment-builder.md#adding-audiences)

Exempel:

* Skapa en Experience Event-målgrupp
   * Definiera beteendeförhållandena separat. Exempel:&quot;Personer som besökt prissidan de senaste tre dagarna.&quot;
* Skapa en målgrupp med flera enheter med B2B-attribut.
   * Härifrån kan ni referera till Experience Event-målgruppen som en del av målgruppens kriterier. Exempel:&quot;Personer som är en **&#39;beslutsfattare&#39;** för en möjlighet där kontot finns i **&#39;Finanssektorn&#39;** och som är medlem i den målgrupp som besökt prissidan de senaste tre dagarna.

När uppgraderingen är klar måste alla nya målgrupper med flera enheter med B2B-attribut och Experience Events skapas med metoden [segment-of-segment](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types) .

>[!TIP]
>
>Ett **segment i segment** är en segmentdefinition som innehåller en eller flera grupper eller kantsegment. **Obs!**: Om du använder ett segment av segment kommer profilinaktiveringen att ske **var 24:e timme**.

### Enhetsupplösning och sammanslagning med tidsprioritet inom B2B-målgrupper

Som en del av uppgraderingen av arkitekturen introducerar Adobe en lösning för konton och säljprojekt. Enhetsupplösningen baseras på deterministisk ID-matchning och baseras på de senaste data. Enhetsupplösningsjobbet körs dagligen under gruppsegmentering, innan man utvärderar flerenhetsmålgrupper med B2B-attribut.

>[!BEGINSHADEBOX]

#### Hur fungerar enhetsupplösning?

* **Före**: Om ett DUNS-nummer (Data Universal Numbering System) användes som en ytterligare identitet och kontots DUNS-nummer uppdaterades i ett källsystem som CRM, länkas konto-ID till både gamla och nya DUNS-nummer.
* **Efter**: Om DUNS-numret användes som en extra identitet och kontots DUNS-nummer uppdaterades i ett källsystem som CRM, länkas konto-ID bara till det nya DUNS-numret, vilket ger en mer korrekt bild av det aktuella kontotillståndet.

>[!ENDSHADEBOX]

Med den här uppgraderingen kan du nu:

* Använd [!DNL Profile Access] API:er för att visa de senaste sammanfogningsprofilerna när de dagliga entitetsupplösningsjobben är klara.
* Utnyttja den förbättrade exaktheten och enhetligheten i era kontouppgifter och affärsmöjlighetsdata för segmentering, aktivering och analys.

Läs [[!DNL Profile Access] API](../profile/api/entities.md) om du vill ha mer information.

### Stöd för sammanslagningsprinciper i B2B-målgrupper med flera enheter

Flera målgrupper med B2B-attribut har nu stöd för en enda sammanfogningsprincip - standardprincipen för sammanfogning som du konfigurerar - i stället för flera sammanfogningsprinciper.

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

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### Ändringar av målgruppsimporter för flera enheter i sandlådeverktyg

Med uppgraderingarna av arkitekturen kan ni inte längre importera målgrupper med flera enheter med B2B-attribut och Experience Events om ett paket som innehöll dessa målgrupper publicerades före uppgraderingen. Dessa målgrupper kommer inte att kunna importera och kan inte automatiskt konverteras till den nya arkitekturen. För att kringgå den här begränsningen måste du skapa ett nytt paket med de uppdaterade målgrupperna och sedan importera dem till deras respektive målsandlådor med hjälp av sandlådeverktyg.

Utvecklingssandlådor uppgraderas till den nya arkitekturen. Publiker som kan uppdateras automatiskt kommer att uppgraderas; de som inte kan inaktiveras. Inaktiverade målgrupper måste återskapas efter uppgraderingen.

Läs [Verktygshandboken för sandlådan](../sandboxes/ui/sandbox-tooling.md) om du vill ha mer information.
