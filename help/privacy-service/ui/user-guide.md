---
keywords: Experience Platform;hem;populära ämnen;export;Exportera
solution: Experience Platform
title: Hantera sekretessjobb i Privacy Servicens användargränssnitt
description: Lär dig hur du använder Privacy Servicens användargränssnitt för att samordna och övervaka sekretessförfrågningar i olika Experience Cloud-program.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 0a8d7c4414f6091025d36ed85dc09e057ee24df9
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---

# Hantera sekretessjobb i Privacy Servicens användargränssnitt {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Följa förfrågningar om integritetsskydd för registrerade"
>abstract="<h2>Beskrivning</h2><p>Med Adobe Experience Platform Privacy Service kan ni skapa och hantera sekretessförfrågningar för kunder som vill få tillgång till eller ta bort sina personuppgifter i enlighet med juridiska sekretessbestämmelser.</p>"

Det här dokumentet innehåller steg för att skapa och hantera sekretessbegäranden med användargränssnittet [!DNL Privacy Service].

>[!IMPORTANT]
>
>Privacy Service är endast avsedd för den registrerade och för förfrågningar om konsumenträttigheter. All annan användning av Privacy Service för datarensning eller underhåll stöds inte eller tillåts inte. Adobe har en rättslig skyldighet att uppfylla dem i tid. Därför är lasttestning inte tillåtet på Privacy Service eftersom det är en produktionsmiljö och skapar en onödig eftersläpning av giltiga sekretessbegäranden.
>
>Det finns nu en hög överföringsgräns per dag för att förhindra missbruk av tjänsten. Användare som råkar missbruka systemet kommer att ha åtkomst till tjänsten inaktiverad. Därefter kommer ett möte att hållas med dem för att diskutera deras åtgärder och hur Privacy Servicen kan användas.

## Bläddra i [!DNL Privacy Service]-gränssnittspanelen

Kontrollpanelen för användargränssnittet [!DNL Privacy Service] innehåller två widgetar som gör att du kan visa statusen för dina sekretessjobb: [!UICONTROL Status Report] och [!UICONTROL Job Requests]. Kontrollpanelen visar även den aktuella valda regeln för de visade jobben.

![Kontrollpanel för användargränssnitt](../images/user-guide/dashboard.png)

### Regeltyp

[!DNL Privacy Service] stöder jobbförfrågningar för flera sekretessregler. I följande tabell visas vilka regler som stöds och deras motsvarande etikett som representeras i användargränssnittet:

| UI-etikett | Förordning |
|-------------------------------------|------------------------|
| [!UICONTROL APA_AUS  (Australia)] | [!DNL Australia Privacy Act] |
| [!UICONTROL CCPA (California)] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPA_USA (Colorado)] | [!DNL Colorado Privacy Act] |
| [!UICONTROL CPRA_USA (California)] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA_USA (Connecticut)] | [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL FDBR_USA (Florida)] | [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL GDPR (European Union)] | Europeiska unionens [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPPA_USA (United States)] | [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL ICDPA_USA] (Iowa) | [!DNL Iowa Consumer Data Protection Act] |
| [!UICONTROL LGPD_BRA (Brazil)] | Brasiliens [!DNL General Data Protection Law] [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA_USA (Washington)] | [!DNL Washington My Health My Data Act] |
| [!UICONTROL MCDPA_USA (Montana)] | [!DNL Montana Consumer Data Privacy Act] |
| [!UICONTROL NDPA_USA (Nebraska)] | [!DNL Nebraska Data Protection Act] |
| [!UICONTROL NZPA_NZL (New Zealand)] | Nya Zeelands [!DNL Privacy Act] |
| [!UICONTROL NHPA_USA (New Hampshire)] | [!DNL New Hampshire Privacy Act] |
| [!UICONTROL NJDPA_USA (New Jersey)] | [!DNL New Jersey Data Protection Act] |
| [!UICONTROL OCPA USA (Oregon)] | [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA (Thailand)] | Thailands [!DNL Personal Data Protection Act] |
| [!UICONTROL TDPSA USA (Texas)] | [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL UCPA_USA (Utah)] | [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA (Virginia)] | [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!-- 
Waiting:
| **[!UICONTROL PIPA_KOR]**  ?        | South Korea [!DNL Personal Information Privacy Act] |
 -->

>[!NOTE]
>
>Mer information om det juridiska sammanhanget för varje regel finns i översikten om [sekretessregler](../regulations/overview.md) som stöds.

Jobb för varje regeltyp spåras separat. Om du vill växla mellan olika regeltyper väljer du listrutan **[!UICONTROL Regulation Type]** och väljer önskad regel i listan.

![Privacy Service-konsolen med listrutan Regeltyp.](../images/user-guide/regulation.png)

När du ändrar regeltypen uppdateras instrumentpanelen så att alla åtgärder, filter, widgetar och dialogrutor för att skapa jobb som gäller för den valda förordningen visas.

![Uppdaterad instrumentpanel](../images/user-guide/dashboard-update.png)

### Statusrapport

I diagrammet till vänster i widgeten Statusrapport spåras skickade jobb mot jobb som kan ha rapporterats tillbaka med fel. I diagrammet till höger spåras jobb som närmar sig slutet av det 30 dagar långa kompatibilitetsfönstret.

Välj en av de två växlingsknapparna ovanför diagrammet för att visa eller dölja deras respektive mätvärden.

![](../images/user-guide/hide-errors.png)

Du kan visa det exakta antalet jobb som är kopplade till en datapunkt i diagrammen genom att hålla muspekaren över datapunkten i fråga.

![Datapunkter för muspekaren](../images/user-guide/mouse-over.png)

Om du vill visa mer information om en viss datapunkt markerar du datapunkten i fråga så att de associerade jobben visas i widgeten Jobbförfrågningar. Observera filtret som används precis ovanför jobblistan.

![Använt filter från widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>När ett filter har tillämpats på widgeten Jobbförfrågningar kan du ta bort filtret genom att välja **X** i filterpillet. Jobbförfrågningar återgår sedan till standardspårningslistan.

### Jobbförfrågningar {#job-requests}

Arbetsytan [!UICONTROL Job Requests] innehåller information om de senaste jobbförfrågningarna i din organisation. Informationen innehåller typ av begäran, aktuell status, förfallodatum, e-postadress till begärande och så vidare. Uppsättningar om 100 poster läses in samtidigt. Som standard visas de senast skapade jobben överst med fler uppsättningar poster inlästa när du bläddrar nedåt.

>[!NOTE]
>
>Data för tidigare skapade jobb är bara tillgängliga i 30 dagar efter slutförandedatumet.

Du kan filtrera listan genom att skriva nyckelord i sökfältet under rubriken [!UICONTROL Job Requests]. Listan filtreras automatiskt medan du skriver och visar begäranden som innehåller värden som matchar söktermerna. Sökfältet utför en snabbsökning som matchar sekretessposter-ID:n för de återgivna/inlästa jobben i användargränssnittet. Det är inte en omfattande sökning efter alla dina skickade jobb. Det är i stället ett filter som tillämpas på de inlästa resultaten. Använd Privacy Service-API:t för att [returnera jobb baserat på en viss regel, datumintervall eller ett enskilt jobb ](../api/privacy-jobs.md#list).

>[!TIP]
>
>Om du vill läsa in poster i användargränssnittet från de senaste 30 dagarna måste du rulla nedåt i tabellen och läsa in fler grupper med poster.

![Avsnittet Sekretesskonsolens jobbbegäran med sökfältet markerat.](../images/user-guide/job-search.png)

Du kan också använda sökknappen för att utföra en sekretessjobbfråga som sträcker sig över ett visst datumintervall. Den här åtgärden returnerar alla sekretessjobb som skickats in av organisationen under den angivna tidsramen. Välj listrutan **[!UICONTROL Requested on]** för att välja ett start- och avslutsdatum för frågan. De tillgängliga alternativen är [!UICONTROL Today], [!UICONTROL Last 7 Days], [!UICONTROL Last 2 Weeks], [!UICONTROL Last 30 Days] eller [!UICONTROL Custom]. När sökfunktionen används med alternativet [!UICONTROL Requested on] visas endast jobbbegäranden som har skickats mellan de valda datumintervallen.

![Avsnittet Jobbbegäran med sökfältet, listrutan Begärd och knappen Sök markerad.](../images/user-guide/requested-on-dropdown-menu.png)

Om du vill visa information om en viss jobbförfrågan väljer du begärans jobb-ID i listan för att öppna sidan **[!UICONTROL Job Details]**.

![GDPR-gränssnittsjobbinformation](../images/user-guide/job-details.png)

Den här dialogrutan innehåller statusinformation om varje [!DNL Experience Cloud]-lösning och dess aktuella tillstånd i relation till det övergripande jobbet. Eftersom alla sekretessjobb är asynkrona visar sidan det senaste datumet och den senaste tiden (GMT) för varje lösning, eftersom vissa kräver mer tid än andra för att behandla begäran.

Om en lösning har tillhandahållit ytterligare data kan den visas i den här dialogrutan. Du kan visa dessa data genom att markera enskilda produktrader.

Om du vill hämta alla jobbdata som en CSV-fil väljer du **[!UICONTROL Export to CSV]** längst upp till höger i dialogrutan.

## Skapa en ny begäran om sekretessjobb {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Instruktioner"
>abstract="<ul><li>Välj <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">Förfrågningar</a> i den vänstra navigeringen för att öppna sekretesspolicyn och välj sedan <b>Skapa förfrågan</b>.</li><li>Härifrån kan du antingen använda begärandeverktyget eller överföra en JSON-fil med registrerade.</li><li>Om du använder begärandebyggaren väljer du jobbtyp (åtkomst och/eller borttagning) och sedan den typ av identitet som du anger (e-post, ECID eller AAID) eller anger ett anpassat ID-namnutrymme. Ange lämpliga identitetsvärden för kunderna och välj <b>Skapa</b> när du är klar.</li><li>Om du överför en JSON-fil markerar du pilen bredvid Skapa begäran. I listan med alternativ väljer du <b>Överför JSON</b> och överför filen. Om du inte har någon JSON-fil att överföra väljer du <b>Hämta Adobe-GDPR-Request.json</b> för att hämta en mall som du kan fylla i. Ladda upp JSON och välj <b>Create</b> när du är klar.</li><li>Mer hjälp om den här funktionen finns i <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html">Privacy Servicens användarhandbok</a> på Experience League.</li></ul>"

>[!NOTE]
>
>För att kunna skapa en begäran om ett sekretessjobb måste du ange identitetsinformation för de specifika kunder vars data ska nås eller tas bort. Granska dokumentet om [identitetsdata för sekretessförfrågningar](../identity-data.md) innan du fortsätter med det här avsnittet.

Gränssnittet [!DNL Privacy Service] innehåller två metoder för att skapa nya jobbbegäranden:

* [Använda Request Builder](#request-builder)
* [Överföra en JSON-fil](#json)

Steg för att använda dessa metoder finns i följande avsnitt.

### Använda Request Builder {#request-builder}

Med hjälp av Request Builder kan du manuellt skapa en ny begäran om sekretessjobb i användargränssnittet. Request Builder är bäst att använda för enklare och mindre uppsättningar av begäranden eftersom Request Builder begränsar antalet begäranden som bara har ID-typ per användare. För mer komplicerade begäranden är det bättre att [överföra en JSON-fil](#json) i stället.

Om du vill börja använda Request Builder väljer du **[!UICONTROL Create Request]** under widgeten Statusrapport till höger på skärmen.

![Välj Skapa begäran](../images/user-guide/create-request.png)

Dialogrutan **[!UICONTROL Create Request]** öppnas och visar tillgängliga alternativ för att skicka en begäran om sekretessjobb för den valda regeltypen.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Välj **[!UICONTROL Job Type]** för begäran (&quot;Ta bort&quot; eller&quot;Åtkomst&quot;) och en eller flera tillgängliga produkter i listan.

Privacy Servicen stöder två typer av jobbförfrågningar för personliga data: [!UICONTROL Access] (läs) och/eller [!UICONTROL Delete]. Du kan antingen skicka in en begäran om att få alla uppgifter som finns i produkten och som rör ämnet för förfrågan, eller begära att få ta bort alla uppgifter som rör ämnet för förfrågan.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Under **[!UICONTROL Namespace type]** väljer du lämplig namnområdestyp för de kund-ID som skickas till [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

När du använder standardnamnområdestypen väljer du ett namnutrymme på den nedrullningsbara menyn (e-post, ECID eller AAID), skriver sedan ID-värdena i textrutan till höger och trycker på **\&lt;enter>** för varje ID för att lägga till det i listan.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

När du använder den anpassade namnområdestypen måste du skriva in namnutrymmet manuellt innan du anger ID-värdena nedan.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

När du är klar väljer du **[!UICONTROL Create]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Dialogrutan försvinner och det nya jobbet (eller de nya jobben) visas i widgeten Jobbförfrågningar tillsammans med deras aktuella bearbetningsstatus.

### Överföra en JSON-fil {#json}

När du skapar mer komplicerade begäranden, till exempel sådana som använder flera ID-typer för varje registrerade som behandlas, kan du skapa en begäran genom att överföra en JSON-fil.

Välj pilen bredvid **[!UICONTROL Create Request]**, under widgeten Statusrapport till höger på skärmen. Välj **[!UICONTROL Upload JSON]** i listan med alternativ som visas.

![Alternativ för att skapa begäranden](../images/user-guide/create-options.png)

Dialogrutan **[!UICONTROL Upload JSON]** visas med ett fönster där du kan dra och släppa JSON-filen i.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Om du inte har någon JSON-fil att överföra väljer du **[!UICONTROL Download Adobe-GDPR-Request.json]** för att hämta en mall som du kan fylla i enligt de värden som du har samlat in från dina registrerade.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Leta reda på JSON-filen på datorn och dra den till dialogfönstret. Om överföringen lyckas visas filnamnet i dialogrutan. Du kan fortsätta lägga till fler JSON-filer om det behövs genom att dra och släppa dem i dialogrutan.

När du är klar väljer du **[!UICONTROL Create]**. Dialogrutan försvinner och det nya jobbet (eller de nya jobben) visas i widgeten Jobbförfrågningar tillsammans med deras aktuella bearbetningsstatus.

### Nästa steg

Genom att läsa det här dokumentet har du lärt dig att använda användargränssnittet i [!DNL Privacy Service] för att skapa ett sekretessjobb, visa information om ett jobb och övervaka dess bearbetningsstatus, och hämta resultaten när det är klart.

Anvisningar om hur du utför dessa åtgärder programmatiskt med API:t [!DNL Privacy Service] finns i [API-handboken](../api/overview.md).
