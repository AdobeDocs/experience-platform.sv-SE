---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d2f1255be48c1df04757f7e071221e0552a0b921
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

För att kunna leverera bättre kundupplevelser måste ni samla in och lagra kundernas personuppgifter. När du använder dessa data är det viktigt att förstå och respektera dina kunders integritet. Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran.

Adobe Experience Platform [!DNL Privacy Service] utvecklades som svar på en grundläggande förändring i hur företag måste hantera sina kunders personuppgifter. Det centrala syftet med [!DNL Privacy Service] är att automatisera efterlevnaden av datasekretessregler som, när de överträds, kan leda till allvarliga böter och störa datahanteringen för ert företag.

[!DNL Privacy Service] innehåller ett RESTful-API och användargränssnitt som hjälper dig att hantera kunddataförfrågningar. Med [!DNL Privacy Service]kan ni skicka in förfrågningar om åtkomst till och radering av personuppgifter från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

## Getting started with [!DNL Privacy Service] {#getting-started}

För att kunna använda [!DNL Privacy Service]måste flera viktiga beslut fattas i fråga om organisationens sekretessbestämmelser, vilken typ av identitetsdata du samlar in från dina kunder och det bästa sättet att interagera CRM-systemet med tjänsten.

Dessa beslut kan sammanfattas i följande frågor:

1. **Vilken information samlar jag in från mina kunder?**
   * För att kunna använda [!DNL Privacy Service]på bästa sätt måste ni ha en detaljerad förståelse för vilka typer av data ni samlar in från era kunder, och vilka av dem som omfattas av sekretesslagstiftningen. Mer information finns i avsnittet [om sekretesskrav](#requirements) .
1. **Har jag märkt mina data korrekt?**
   * Data måste vara korrekt märkta för att tjänsten ska kunna avgöra vilka fält som ska användas eller tas bort under sekretessjobb. Mer information finns i avsnittet om [etikettdata](#label) .
1. **Vet jag vilka ID:n jag ska skicka till [!DNL Privacy Service]?**
   * När sekretessförfrågningar skickas måste enskilda kund-ID:n som är specifika för vissa Adobe-program tillhandahållas. Mer information finns i avsnitten om [att tillhandahålla identitetsdata](#identity) och [göra sekretessförfrågningar](#requests) .
1. **Hur spårar jag mina sekretessjobb?**
   * När du har gjort sekretessförfrågningar finns det flera alternativ för att spåra deras status och resultat. Mer information finns i avsnittet [Övervaka sekretessjobb](#monitor) .

Avsnitten nedan innehåller allmän vägledning om dessa viktiga nödvändiga steg och länkar till ytterligare [!DNL Privacy Service] dokumentation för mer information.

### Ange organisationens sekretesskrav {#requirements}

Beroende på vilken typ av verksamhet ni bedriver och vilka jurisdiktioner ni bedriver under, kan det bero på att era uppgifter omfattas av lagenliga sekretessbestämmelser. Dessa bestämmelser ger ofta kunderna rätt att begära åtkomst till de uppgifter ni samlar in från dem och rätt att begära att lagrade uppgifter tas bort. Dessa kundförfrågningar om deras personuppgifter kallas för&quot;sekretessförfrågningar&quot; i hela dokumentationen.

Mer information om de olika juridiska sekretessreglerna som hanterar förfrågningar, inklusive nyckeltermer och svar på vanliga frågor och svar, finns i dokumentationen [!DNL Privacy Service] till [](./regulations/overview.md)sekretesslagstiftningen.

Om dina dataåtgärder omfattas av någon av de regler som stöds kan du läsa deras dokumentation för att få viktig information, t.ex. vilka specifika sekretessrättigheter de har för dina kunder, samt för att kontrollera att efterlevnadskrav uppfylls. Denna information bör beaktas när ni avgör hur ni ska integrera dem [!DNL Privacy Service] i ert CRM-system och hur kunderna ska interagera med er webbplats för att kunna göra sekretessförfrågningar.

Förutom lagar och andra författningar bör alla branschstandarder som är tillämpliga för din organisation också beaktas när du fattar dessa beslut.

### Etikettdata för sekretessförfrågningar {#label}

Beroende på vilka program du använder måste du märka de specifika datafält som ska vara tillgängliga eller tas bort som svar på sekretessförfrågningar. [!DNL Experience Cloud] Processen för att märka data varierar mellan olika program. Om du vill lära dig hur du etiketterar data för alla Adobe-program som stöds läser du dokumentet om [Experience Cloud-program](./experience-cloud-apps.md).

### Bestäm vilka typer av identitetsdata som ska skickas till [!DNL Privacy Service] {#identity}

För [!DNL Privacy Service] att kunna behandla en sekretessförfrågan från en kund måste minst ett unikt identitetsvärde för kunden anges i själva begäran. Ett unikt identitetsvärde är all information som kan användas för att identifiera en enskild person och deras lagrade personuppgifter i era [!DNL Experience Cloud] datalager. [!DNL Privacy Service] använder den här identitetsinformationen för att hitta och bearbeta kundens personuppgifter beroende på typ av begäran (åtkomst, borttagning eller avanmälan).

Beroende på vilka program ditt CRM-system använder varierar typen och antalet identitetsvärden som du måste ange för varje kund. [!DNL Experience Cloud] Vissa program använder sina egna interna ID-värden (t.ex. Adobe Target ID), medan andra lösningar använder globala ID:n från Adobe [!DNL Experience Cloud Identity Service] (ECID) som spårar kundaktivitet i alla [!DNL Experience Cloud] program. Dessutom kan allmän personlig information som en e-postadress eller ett telefonnummer också fungera som giltiga identitetsdata.

Dokumentet om [identitetsdata för sekretessförfrågningar](./identity-data.md) innehåller mer detaljerad information om vilka typer av identitetsinformation som accepteras för [!DNL Privacy Service]. Dokumentet innehåller också riktlinjer för hur man kan utnyttja Adobe-tekniker för att effektivt hämta lämplig identitetsinformation från era kunder när de interagerar med er webbplats och skicka dessa data till [!DNL Privacy Service] API-förfrågningar.

### Börja göra sekretessförfrågningar {#requests}

När du har fastställt ditt företags sekretessbehov och bestämt vilka identitetsvärden du vill skicka till [!DNL Privacy Service]kan du börja göra sekretessförfrågningar. [!DNL Privacy Service] gör att du kan skicka sekretessförfrågningar via antingen API:t eller gränssnittet.

>[!IMPORTANT]
>
>Avsnitten nedan innehåller länkar till dokumentation som beskriver hur du gör allmänna sekretessförfrågningar i API:t eller användargränssnittet. Beroende på vilka program du använder kan dock de fält som du måste skicka i nyttolasten för begäran skilja sig från de exempel som visas i dessa handböcker. [!DNL Experience Cloud]
>
>I dokumentet om [Privacy Service- och Experience Cloud-program](./experience-cloud-apps.md) finns mer information om hur du formaterar sekretessförfrågningar för just dina [!DNL Experience Cloud] program.
>
>Det är också viktigt att notera att sekretessförfrågningar behandlas asynkront mellan olika Experience Cloud-program. När en begäran har tagits emot av Privacy Servicen kan det ta en stund mellan minuter och veckor innan den kan slutföras. Den tid det tar att slutföra varje begäran är specifik för programmet du arbetar med och den mängd data som behöver behandlas.

#### Använda API

Den [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) innehåller flera slutpunkter för att skapa och hantera sekretessjobb med RESTful API-anrop, vilket gör att du kan programmässigt hantera kompatibiliteten för sekretesslagstiftning för dina [!DNL Experience Cloud] program. Detaljerade anvisningar om hur du använder API:t finns i utvecklarhandboken [för](api/getting-started.md)Privacy Service API.

#### Använda gränssnittet

>[!NOTE]
>
>Gränssnittet [!DNL Privacy Service] har för närvarande bara stöd för begäranden om åtkomst och borttagning. Alla avanmälningsbegäranden måste göras via API i stället.

Med [!DNL Privacy Service] användargränssnittet kan du skapa och övervaka sekretessjobb med ett grafiskt gränssnitt. Gränssnittet innehåller en **[!UICONTROL Status Report]** widget som ger en visuell representation av statusen för alla aktiva begäranden, och som gör att du kan skapa nya begäranden med hjälp av det inbyggda **[!UICONTROL Request Builder]** programmet eller genom att överföra JSON-filer. Mer information om hur du använder användargränssnittet finns i användarhandboken för [Privacy Service](ui/overview.md).

### Övervaka sekretessjobb {#monitor}

När du har gjort sekretessjobb har du flera alternativ för att övervaka status och resultat:

| Övervakningsmetod | Beskrivning |
| --- | --- |
| [!DNL Privacy Service] UI | Användargränssnittet [!DNL Privacy Service] innehåller en kontrollpanel som gör att du kan visa en visuell representation av statusen för alla aktiva begäranden. Mer information finns i användarhandboken [för](ui/overview.md) Privacy Service. |
| [!DNL Privacy Service] API | Du kan övervaka sekretessjobbens status programmatiskt med hjälp av sökslutpunkterna från [!DNL Privacy Service] API:t. Mer information om hur du använder API finns i [utvecklarhandboken](./api/getting-started.md) för Privacy Service. |
| [!DNL Privacy Events] | [!DNL Privacy Events] utnyttja Adobe I/O-händelser som skickas till en konfigurerad webkrok för att underlätta en effektiv automatisering av jobbförfrågningar. De minskar eller eliminerar behovet av att avfråga [!DNL Privacy Service] API för att kontrollera om ett jobb är färdigt eller om en viss milstolpe i ett arbetsflöde har nåtts. Mer information finns i självstudiekursen om hur du [prenumererar på sekretesshändelser](./privacy-events.md) . |

## Nästa steg

Det här dokumentet innehåller en översikt på hög nivå över [!DNL Privacy Service] och de viktigaste steg som krävs för att börja använda tjänstens funktioner. Se dokumentationen som är länkad till i hela översikten för mer ingående information om de olika aspekterna av att arbeta med [!DNL Privacy Service].
