---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 3%

---


# Översikt över Adobe Experience Platform Privacy Servicen

För att kunna leverera bättre kundupplevelser måste ni samla in och lagra kundernas personuppgifter. När du använder dessa data är det viktigt att förstå och respektera dina kunders integritet. Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran.

Adobe Experience Platform Privacy Servicen utvecklades som svar på en grundläggande förändring i hur företag måste hantera sina kunders personuppgifter. Det centrala syftet med Privacy Servicen är att automatisera efterlevnaden av datasekretessregler som, när de överträds, kan leda till allvarliga böter och störa datahanteringen för ert företag.

Privacy Service tillhandahåller ett RESTful-API och användargränssnitt som hjälper dig att hantera kunddataförfrågningar. Med Privacy Service kan ni skicka in förfrågningar om åtkomst till och radering av personuppgifter från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

## Komma igång med Privacy Service {#getting-started}

För att kunna utnyttja Privacy Servicen måste flera viktiga beslut fattas i fråga om organisationens sekretessbestämmelser, vilken typ av identitetsdata du samlar in från dina kunder och det bästa sättet att interagera CRM-systemet med tjänsten.

Dessa beslut kan sammanfattas i följande frågor:

1. **Vilken information samlar jag in från mina kunder?**
   * För att kunna utnyttja Privacy Servicen på bästa sätt måste ni ha en detaljerad förståelse för vilka typer av data ni samlar in från era kunder och vilka av dessa som omfattas av sekretessbestämmelser. Mer information finns i avsnittet [om sekretesskrav](#requirements) .
1. **Har jag märkt mina data korrekt?**
   * Data måste vara korrekt märkta för att tjänsten ska kunna avgöra vilka fält som ska användas eller tas bort under sekretessjobb. Mer information finns i avsnittet om [etikettdata](#label) .
1. **Vet jag vilka ID:n som ska skickas till Privacy Servicen?**
   * När du skickar sekretessförfrågningar måste du ange individuella kund-ID:n som är specifika för vissa Adobe-program. Mer information finns i avsnitten om [att tillhandahålla identitetsdata](#identity) och [göra sekretessförfrågningar](#requests) .
1. **Hur spårar jag mina sekretessjobb?**
   * När du har gjort sekretessförfrågningar finns det flera alternativ för att spåra deras status och resultat. Mer information finns i avsnittet [Övervaka sekretessjobb](#monitor) .

Avsnitten nedan innehåller allmän vägledning om dessa viktiga nödvändiga steg och länkar till ytterligare Privacy Service för mer information.

### Ange organisationens sekretesskrav {#requirements}

Beroende på vilken typ av verksamhet ni bedriver och vilka jurisdiktioner ni bedriver under, kan det bero på att era uppgifter omfattas av lagenliga sekretessbestämmelser. Dessa bestämmelser ger ofta kunderna rätt att begära åtkomst till de uppgifter ni samlar in från dem och rätt att begära att lagrade uppgifter tas bort. Dessa kundförfrågningar om deras personuppgifter kallas för&quot;sekretessförfrågningar&quot; i hela dokumentationen.

I följande tabell beskrivs de juridiska sekretessbestämmelser som Privacy Servicen hanterar förfrågningar om, inklusive länkar till dokumentation för mer information:

| Förordning | Beskrivning |
| --- | --- |
| CCPA (Kalifornien) | California Consumer Privacy Act (CCPA) förbättrar sekretessen och konsumentskyddet för personer bosatta i Kalifornien. CCPA ger personer bosatta i Kalifornien nya integritetsrättigheter, inklusive rätten att få tillgång till och radera sina personuppgifter, att få veta om deras personuppgifter säljs eller offentliggörs (och till vem) samt rätten att avanmäla sig från att få sina uppgifter sålda till tredje part.<br/><br/>Länkar till ytterligare dokumentation: <ul><li>[Juridisk översikt](https://oag.ca.gov/privacy/ccpa)</li><li>[Vanliga frågor om CCPA](ccpa/faq.md)</li></ul> |
| GDPR (Europeiska unionen) | I den allmänna dataskyddsförordningen (GDPR) infördes flera nya rättigheter för EU-medlemmar, bland annat **rätten till åtkomst** och **rätten att raderas**. Detta innebär att alla EU-medborgare vars personuppgifter har samlats in av ert företag när som helst kan begära att få tillgång till eller radera sina uppgifter. <br/><br/>Länkar till ytterligare dokumentation: <ul><li>[Juridisk översikt](https://gdpr-info.eu/)</li><li>[Vanliga frågor om GDPR](gdpr/faq.md)</li><li>[GDPR-terminologi](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thailand) | Den thailändska lagen om skydd av personuppgifter (PDPA) infördes för att skydda thailändska dataägare från olaglig insamling, användning eller utlämnande av deras personuppgifter. Förordningen inspireras av EU:s allmänna dataskyddsförordningen och ger de thailändska medborgarna rätt att begära tillgång till eller radering av lagrade personuppgifter.<br/><br/>Länkar till ytterligare dokumentation: <ul><li>[Juridisk översikt](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[PDPA_THA FAQ](pdpa-tha/faq.md)</li><li>[PDPA_THA-terminologi](pdpa-tha/terminology.md)</li></ul> |

Om dina dataåtgärder omfattas av någon av ovanstående regler, bör du läsa deras dokumentation för att få viktig information, som vilka specifika sekretessrättigheter de har för dina kunder, samt för att få koll på efterlevnadsförfrågningar. Denna information bör beaktas vid fastställandet av hur Privacy Service ska integreras i CRM-systemet och hur kunderna ska interagera med er webbplats för att kunna göra sekretessförfrågningar.

Förutom lagar och andra författningar bör alla branschstandarder som är tillämpliga för din organisation också beaktas när du fattar dessa beslut.

### Etikettdata för sekretessförfrågningar {#label}

Beroende på vilka Experience Cloud-program du använder måste du märka de specifika datafält som ska vara tillgängliga eller tas bort som svar på sekretessförfrågningar. Processen för att märka data varierar mellan olika program. Om du vill lära dig att märka data för alla Adobe-program som stöds läser du dokumentet om [Experience Cloud-program](./experience-cloud-apps.md).

### Bestäm vilka typer av identitetsdata som ska skickas till Privacy Servicen {#identity}

För att Privacy Servicen ska kunna behandla en sekretessförfrågan från en kund måste minst ett unikt identitetsvärde för den kunden anges i själva begäran. Ett unikt identitetsvärde är all information som kan användas för att identifiera en enskild person och deras lagrade personuppgifter i dataarkiven i Experience Cloud. Privacy Servicen använder den här identitetsinformationen för att hitta och bearbeta kundens personuppgifter beroende på typ av begäran (åtkomst, borttagning eller avanmälan).

Beroende på vilka Experience Cloud-program ditt CRM-system använder varierar typen och antalet identitetsvärden som du måste ange för varje kund. Vissa program använder sina egna interna ID-värden (t.ex. Adobe Target ID), medan andra lösningar använder globala ID:n från Adobe Experience Cloud Identity Service (ECID) som spårar kundaktivitet i alla Experience Cloud-program. Dessutom kan allmän personlig information som en e-postadress eller ett telefonnummer också fungera som giltiga identitetsdata.

Dokumentet om [identitetsdata för sekretessförfrågningar](./identity-data.md) innehåller mer detaljerad information om vilka typer av identitetsinformation som accepteras för Privacy Service. Dokumentet innehåller också riktlinjer för hur man kan utnyttja Adobes tekniker för att effektivt hämta lämplig identitetsinformation från kunderna när de interagerar med webbplatsen och skicka dessa data till Privacy Service i API-förfrågningar.

### Börja göra sekretessförfrågningar {#requests}

När du har fastställt ditt företags sekretessbehov och bestämt vilka identitetsvärden som ska skickas till Privacy Servicen kan du börja göra sekretessförfrågningar. Med Privacy Service kan du skicka sekretessförfrågningar via antingen API:t eller gränssnittet.

>[!IMPORTANT]
>
>Avsnitten nedan innehåller länkar till dokumentation som beskriver hur du gör allmänna sekretessförfrågningar i API:t eller användargränssnittet. Beroende på vilka Experience Cloud-program du använder kan de fält du måste skicka i nyttolasten vara annorlunda än de exempel som visas i dessa handböcker.
>
>I dokumentet om [Privacy Service- och Experience Cloud-program](./experience-cloud-apps.md) finns mer information om hur du formaterar sekretessförfrågningar för dina Experience Cloud-program.

#### Använda API

API:t [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service ger flera slutpunkter för att skapa och hantera sekretessjobb med RESTful API-anrop, vilket gör att du kan programmässigt hantera kompatibilitetsregler för dina Experience Cloud-program. Detaljerade anvisningar om hur du använder API:t finns i utvecklarhandboken [för](api/getting-started.md)Privacy Service API.

#### Använda gränssnittet

>[!NOTE]
>
>Privacy Servicens gränssnitt har för närvarande bara stöd för begäranden om åtkomst och borttagning. Alla avanmälningsbegäranden måste göras via API i stället.

Med Privacy Servicens användargränssnitt kan du skapa och övervaka sekretessjobb med ett grafiskt gränssnitt. Användargränssnittet innehåller en **statusrapportwidget** som ger en visuell representation av statusen för alla aktiva begäranden, och som gör att du kan skapa nya begäranden med hjälp av den inbyggda **Request Builder** eller genom att överföra JSON-filer. Mer information om hur du använder användargränssnittet finns i användarhandboken för [Privacy Service](ui/overview.md).

### Övervaka sekretessjobb {#monitor}

När du har gjort sekretessjobb har du flera alternativ för att övervaka status och resultat:

| Övervakningsmetod | Beskrivning |
| --- | --- |
| Privacy Servicens användargränssnitt | Privacy Servicens gränssnitt innehåller en kontrollpanel som gör att du kan visa en visuell representation av statusen för alla aktiva begäranden. Mer information finns i användarhandboken [för](ui/overview.md) Privacy Service. |
| Privacy Services-API | Du kan programmässigt övervaka sekretessjobbens status med hjälp av sökslutpunkterna från Privacy Service-API:t. Mer information om hur du använder API finns i [utvecklarhandboken](./api/getting-started.md) för Privacy Service. |
| Sekretesshändelser | Integritetshändelser utnyttjar Adobe I/O-händelser som skickas till en konfigurerad webkrok för att underlätta automatisering av jobbförfrågningar. De minskar eller eliminerar behovet av att avfråga Privacy Service-API för att kontrollera om ett jobb är färdigt eller om en viss milstolpe i ett arbetsflöde har nåtts. Mer information finns i självstudiekursen om hur du [prenumererar på sekretesshändelser](./privacy-events.md) . |

## Nästa steg

Det här dokumentet innehåller en översikt över Privacy Servicen och de viktigaste stegen som krävs för att börja använda tjänstens funktioner. Se dokumentationen som är länkad till i hela översikten för mer ingående information om de olika aspekterna av att arbeta med Privacy Service.
