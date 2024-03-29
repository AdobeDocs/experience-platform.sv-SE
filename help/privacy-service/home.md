---
keywords: Experience Platform;hem;populära ämnen;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Översikt över Privacy Service
description: Upptäck hur Privacy Service kan underlätta automatiserad efterlevnad av juridiska sekretessregler i dataåtgärder från Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 19b33ddf2fc3f8d889d370eedfc732ac54178dcd
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 0%

---

# Översikt över Privacy Servicen

För att kunna leverera bättre kundupplevelser måste ni samla in och lagra kundernas personuppgifter. När du använder dessa data är det viktigt att förstå och respektera dina kunders integritet. Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran.

Adobe Experience Platform Privacy Service utvecklades som svar på en grundläggande förändring i hur företag måste hantera sina kunders personuppgifter. Det centrala syftet med Privacy Servicen är att automatisera efterlevnaden av datasekretessregler som, när de överträds, kan leda till allvarliga böter och störa datahanteringen för ert företag.

Privacy Service tillhandahåller ett RESTful-API och användargränssnitt som hjälper dig att hantera kunddataförfrågningar. Ni kan använda Privacy Service för att skicka in förfrågningar om åtkomst till och radering av personuppgifter från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

>[!IMPORTANT]
>
>Privacy Service är endast avsedd för den registrerade och för förfrågningar om konsumenträttigheter. All annan användning av Privacy Service för datarensning eller underhåll stöds inte eller tillåts inte. Adobe har en rättslig skyldighet att uppfylla dem i tid. Därför är lasttestning inte tillåtet på Privacy Service eftersom det är en produktionsmiljö och skapar en onödig eftersläpning av giltiga sekretessbegäranden.
>
>Det finns nu en hög överföringsgräns per dag för att förhindra missbruk av tjänsten. Användare som råkar missbruka systemet kommer att ha åtkomst till tjänsten inaktiverad. Därefter kommer ett möte att hållas med dem för att diskutera deras åtgärder och hur Privacy Servicen kan användas.

## Komma igång med Privacy Service {#getting-started}

För att Privacy Servicen ska kunna användas på bästa sätt måste flera viktiga beslut fattas utifrån organisationens sekretessbestämmelser, vilken typ av identitetsdata du samlar in från dina kunder och det bästa sättet att interagera CRM-systemet med tjänsten.

Dessa beslut kan sammanfattas i följande frågor:

1. **Vilken information samlar jag in från mina kunder?**
   * För att kunna utnyttja Privacy Servicen på bästa sätt måste ni ha en detaljerad förståelse för vilka typer av data ni samlar in från era kunder och vilka av dessa som omfattas av sekretessbestämmelser. Se avsnittet om [fastställa sekretesskrav](#requirements) för mer information.
1. **Har jag märkt mina data korrekt?**
   * Data måste ha rätt etikett för tjänsten för att kunna avgöra vilka fält som ska användas eller tas bort under sekretessjobb. Se avsnittet om [etikettdata](#label) för mer information.
1. **Vet jag vilka ID:n som ska skickas till Privacy Servicen?**
   * När sekretessförfrågningar skickas måste enskilda kund-ID:n som är specifika för vissa Adobe-program tillhandahållas. Se avsnitten om [tillhandahålla identitetsdata](#identity)  och [göra sekretessförfrågningar](#requests) för mer information.
1. **Hur spårar jag mina sekretessjobb?**
   * När du har gjort sekretessförfrågningar finns det flera alternativ för att spåra deras status och resultat. Se avsnittet om [övervaka sekretessjobb](#monitor) för mer information.

Avsnitten nedan innehåller allmän vägledning om dessa viktiga nödvändiga steg och länkar till ytterligare Privacy Service för mer information.

### Ange organisationens sekretesskrav {#requirements}

Beroende på vilken typ av verksamhet ni bedriver och vilka jurisdiktioner ni bedriver under, kan det bero på att era uppgifter omfattas av lagenliga sekretessbestämmelser. Dessa bestämmelser ger ofta kunderna rätt att begära åtkomst till de uppgifter ni samlar in från dem och rätt att begära att lagrade uppgifter tas bort. Dessa kundförfrågningar om deras personuppgifter kallas för&quot;sekretessförfrågningar&quot; i hela dokumentationen.

Mer information om olika juridiska sekretessregler som Privacy Servicen hanterar förfrågningar om, inklusive nyckeltermer och svar på vanliga frågor finns i [dokumentation om sekretesskrav](./regulations/overview.md).

Om dina dataåtgärder omfattas av någon av de regler som stöds kan du läsa deras dokumentation för att få viktig information, t.ex. vilka specifika sekretessrättigheter de har för dina kunder, samt för att kontrollera att efterlevnadskrav uppfylls. Denna information bör beaktas vid fastställandet av hur Privacy Service ska integreras i CRM-systemet och hur kunderna ska interagera med er webbplats för att kunna göra sekretessförfrågningar.

Förutom lagar och andra författningar bör alla branschstandarder som är tillämpliga för din organisation också beaktas när du fattar dessa beslut.

### Etikettdata för sekretessförfrågningar {#label}

Beroende på [!DNL Experience Cloud] program som du använder måste du märka de specifika datafält som ska vara tillgängliga eller tas bort som svar på sekretessförfrågningar. Processen för att märka data varierar mellan olika program. Om du vill lära dig hur du etiketterar data för alla Adobe-program som stöds läser du dokumentet på [Experience Cloud-program](./experience-cloud-apps.md).

### Bestäm vilka typer av identitetsdata som ska skickas till Privacy Servicen {#identity}

För att Privacy Servicen ska kunna behandla en sekretessförfrågan från en kund måste minst ett unikt identitetsvärde för den kunden anges i själva begäran. Ett unikt identitetsvärde är all information som kan användas för att identifiera en enskild person och deras lagrade personuppgifter i din [!DNL Experience Cloud] datalager. Privacy Servicen använder den här identitetsinformationen för att hitta och bearbeta kundens personuppgifter beroende på typ av begäran (åtkomst, borttagning eller avanmälan).

Beroende på [!DNL Experience Cloud] de program som CRM-systemet använder varierar den typ och det antal identitetsvärden som du måste ange för varje kund. Vissa program använder sina egna interna ID-värden (t.ex. Adobe Target ID), medan andra lösningar använder globala ID:n från Adobe [!DNL Experience Cloud Identity Service] (ECID) som spårar kundaktivitet i alla [!DNL Experience Cloud] program. Dessutom kan allmän personlig information som en e-postadress eller ett telefonnummer också fungera som giltiga identitetsdata.

Läs dokumentet på [identitetsdata för sekretessförfrågningar](./identity-data.md) om du vill ha mer detaljerad information om vilka typer av identitetsinformation som accepteras för Privacy Service. Dokumentet innehåller också riktlinjer för hur man använder Adobe-tekniker för att effektivt hämta lämplig identitetsinformation från kunderna när de interagerar med webbplatsen och skicka dessa data till Privacy Service i API-förfrågningar.

### Börja göra sekretessförfrågningar {#requests}

När du har fastställt ditt företags sekretessbehov och bestämt vilka identitetsvärden som ska skickas till Privacy Servicen kan du börja göra sekretessförfrågningar. Använd Privacy Service för att skicka sekretessförfrågningar via API:t eller användargränssnittet.

>[!IMPORTANT]
>
>Avsnitten nedan innehåller länkar till dokumentation som beskriver hur du gör allmänna sekretessförfrågningar i API:t eller användargränssnittet. Beroende på [!DNL Experience Cloud] de fält som du måste skicka i nyttolasten kan skilja sig från de exempel som visas i dessa handböcker.
>
>Läs dokumentet om [Privacy Service och Experience Cloud](./experience-cloud-apps.md) för mer dokumentation om hur du formaterar sekretessförfrågningar för din [!DNL Experience Cloud] program.
>
>Det är också viktigt att notera att sekretessförfrågningar behandlas asynkront mellan olika Experience Cloud-program. När en begäran har tagits emot av Privacy Servicen kan det ta en stund mellan minuter och veckor innan den kan slutföras. Den tid det tar att slutföra varje begäran är specifik för programmet du arbetar med och den mängd data som behöver behandlas.

#### Använda API:et {#api}

För att programmera regelefterlevnad för sekretess för [!DNL Experience Cloud] -program kan du använda RESTful API-anrop till [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) slutpunkter för att skapa och hantera sekretessjobb. Detaljerade anvisningar om hur du använder API:t finns i [API-guide för Privacy Service](api/overview.md).

#### Använda gränssnittet {#ui}

>[!NOTE]
>
>Privacy Servicens användargränssnitt har för närvarande bara stöd för begäranden om åtkomst och borttagning. Alla avanmälningsbegäranden måste göras via API i stället.

Du kan skapa och övervaka sekretessjobb med ett grafiskt gränssnitt med Privacy Servicens användargränssnitt. Användargränssnittet innehåller en **[!UICONTROL Status Report]** widgeten som ger en visuell representation av statusen för alla aktiva begäranden, och du kan skapa begäranden med den inbyggda **[!UICONTROL Request Builder]** eller genom att överföra JSON-filer. Mer information om hur du använder användargränssnittet finns i [Användarhandbok för Privacy Service](ui/overview.md).

### Övervaka sekretessjobb {#monitor}

När du har gjort sekretessjobb har du flera alternativ för att övervaka status och resultat:

| Övervakningsmetod | Beskrivning |
| --- | --- |
| Privacy Servicens användargränssnitt | Du kan visa en visuell representation av statusen för alla aktiva begäranden med kontrollpanelen för användargränssnittsövervakning för Privacy Service. Se [Användarhandbok för Privacy Service](ui/overview.md) för mer information. |
| Privacy Services-API | Du kan programmässigt övervaka sekretessjobbens status med hjälp av sökslutpunkterna från Privacy Service-API:t. Se [API-guide för Privacy Service](./api/overview.md) om du vill ha detaljerade anvisningar om hur du använder API:t. |
| [!DNL Privacy Events] | [!DNL Privacy Events] Använd Adobe I/O-händelser som skickas till en konfigurerad webkrok för att underlätta en effektiv automatisering av jobbförfrågningar. De minskar eller eliminerar behovet av att avfråga Privacy Service-API för att kontrollera om ett jobb är färdigt eller om en viss milstolpe i ett arbetsflöde har nåtts. Se självstudiekursen om [prenumerera på sekretesshändelser](./privacy-events.md) för mer information. |

## Nästa steg

Det här dokumentet innehåller en översikt över Privacy Servicen och de viktigaste stegen som krävs för att börja använda tjänstens funktioner. Mer information om olika aspekter av att arbeta med Privacy Service finns i dokumentationen som är länkad till i hela översikten.
