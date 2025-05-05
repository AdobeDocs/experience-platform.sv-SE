---
title: Säkerhetskopiera objektkonfigurationer med sandlådeverktyg
description: Om du vill återställa sandlådor säkert och lägga till versionshanteringsstöd säkerhetskopierar du objektkonfigurationer (eller metadata) med verktygspaket för sandlådor. Säkerhetskopieringspaket förhindrar förlust av kritiska konfigurationer som scheman, datauppsättningar och målgrupper, särskilt under utvecklingsiterationer.
exl-id: cccbaaf1-ee68-4a00-9a44-aa5db4a83a14
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 2%

---

# Säkerhetskopiera objektkonfigurationer med sandlådeverktyg

Om du vill återställa sandlådor säkert och lägga till versionshanteringsstöd säkerhetskopierar du objektkonfigurationer (eller metadata) med verktygspaket för sandlådor. Säkerhetskopieringspaket förhindrar förlust av kritiska konfigurationer som scheman, datauppsättningar och målgrupper, särskilt under utvecklingsiterationer.

![Översikt som visar fördelarna med sandlådeverktyg](../images/use-cases/tooling-overview.png){zoomable="yes"}

## Varför ska man tänka på det här användningsexemplet? {#why-this-use-case}

Genom att skapa ett säkerhetskopieringspaket med hjälp av sandlådeverktyg kan du vara säker på att dina objektkonfigurationer lagras och skyddas. Utvecklingssandlådor kan snabbt fylla i allt eftersom du experimenterar och bygger, medan det kan vara tidsödande att bygga en sandlåda från grunden efter att du har återställt den och lämna plats för fel. Med hjälp av sandlådeverktyg kan du importera ett säkerhetskopieringspaket till en sandlåda som återställs nyligen för att omedelbart returnera dina idealiska konfigurationer så att du kan fortsätta utveckla.

Med säkerhetskopieringspaket kan du också använda versionshantering under hela utvecklingsprocessen. När sandlådan ändras kan du skapa ytterligare säkerhetskopieringspaket tillsammans med dina tidigare paket så att du enkelt kan återställa sandlådan till någon av dina konfigurationer.

## Förutsättningar och planering {#prerequisites-and-planning}

När du planerar att skapa ett eget säkerhetskopieringspaket i din organisation bör du tänka på följande under planeringsprocessen:

- Utvärdera den aktuella användningen av sandlådorna i organisationen. Finns det sandlådor som inte är produktionssandlådor som närmar sig eller överskrider licensrättigheterna?
- Vilken omfattning har de metadata du vill säkerhetskopiera? Du kan överväga att säkerhetskopiera antingen en fullständig eller partiell sandlåda, beroende på ditt användningssätt.
- Beroende på vilka scopemetadata du vill säkerhetskopiera, kontrollerar du att du förstår hur du manuellt [lägger till objekt i ett paket](../ui/sandbox-tooling.md#add-object-to-a-new-package) eller hur du [exporterar en hel sandlåda](../ui/sandbox-tooling.md#export-an-entire-sandbox).
- Se till att du har tillgång till sandlådeverktyg i din organisation med rätt behörigheter.

### Gränssnittsfunktioner, Experience Platform-komponenter och Experience Cloud-produkter som du kommer att använda {#ui-functionality-and-elements}

För att implementera det här användningsexemplet måste du använda flera områden i Adobe Experience Platform. Kontrollera att du har de [attributbaserade åtkomstkontrollsbehörigheterna](../../access-control/abac/overview.md) som krävs för alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

- [Verktyg i sandlådan](../ui/sandbox-tooling.md)
- [Sandlådehantering](../ui/user-guide.md)
- [Kontrollpanel för licensanvändning](../../landing/license-usage-and-guardrails/license-usage-dashboard.md)
- [Datauppsättningar](../../catalog/datasets/overview.md)
- [Scheman](../../xdm//home.md)
- [Målgrupper](../../segmentation/home.md)
- [Resor från Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

1. Definiera omfattningen för de metadata som du vill säkerhetskopiera.
2. Använd sandlådeverktygets användargränssnitt för att exportera önskade objekt till ett säkerhetskopieringspaket.
3. Skapa regelbundet nya versioner av säkerhetskopieringspaketet för att se till att sandlådorna förblir justerade med dina nuvarande konfigurationer.
4. Kontrollera din nuvarande användning i kontrollpanelen för licensanvändning mot dina berättiganden för icke-produktionssandlådor.
5. Återställ icke-produktionssandlådor så att de uppfyller kraven eller frigör onödiga resurser och datalagring.
6. Importera säkerhetskopiepaketet till sandlådan när du har återställt det för att återställa objektkonfigurationer.

## Så här uppnår du användningsfallet: stegvisa instruktioner {#step-by-step-instructions}

Läs igenom avsnitten nedan, som innehåller länkar till ytterligare dokumentation, för att slutföra varje steg i översikten ovan.

### Definiera metadataomfånget

Innan du börjar skapa ett säkerhetskopieringspaket bör du överväga paketets användningsfall. Beroende på dina behov kan du behöva säkerhetskopiera en fullständig sandlåda eller välja specifika objekt att lägga till i ditt paket, vilket anges i [förinställningarna](#prerequisites-and-planning).

>[!NOTE]
>
> Om du funderar på att säkerhetskopiera din sandlåda för att återställa den bör du vara medveten om de [begränsningar](../ui/user-guide.md#reset-a-sandbox) som omger återställningen av sandlådor.

### Exportera valda metadata till ett paket

Nu är du redo att säkerhetskopiera din sandlåda med användargränssnittet för sandlådeverktyg. I det här steget beskrivs både säkerhetskopiering av en hel sandlåda och säkerhetskopiering av specifika objekt.

>[!NOTE]
>
> Alla objekt stöds inte för sandlådeverktyg. I handboken [Objekt som stöds för sandlådeverktyg](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) finns en omfattande lista över tillåtna objekt.

#### Exportera en fullständig sandlåda

Om du vill säkerhetskopiera hela sandlådan följer du [verktygsguiden för sandlådan](../ui/sandbox-tooling.md#export-an-entire-sandbox) för att skapa och publicera ett nytt paket som innehåller konfigurationerna för hela sandlådan.

#### Exportera enskilda objekt

Du kan säkerhetskopiera enskilda objekt till ett paket på något av följande sätt. Dessa stödlinjer fokuserar på att lägga till ett schema i paketet, men samma steg gäller för andra objekt, som datauppsättningar, målgrupper eller resor.

- Lägg till ett enskilt objekt i ett nytt paket, efter [stödlinjen för att lägga till objekt](../ui/sandbox-tooling.md#add-object-to-a-new-package) för sandlådeverktyget.
- Lägg till ett enskilt objekt i ett befintligt säkerhetskopieringspaket, som följer [sandlådeverktygshandboken](../ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish), och se till att du publicerar ändringarna.
- Skapa ett tomt paket med flera objekt som du vill lägga till objekt i, enligt anvisningarna nedan.

##### Skapa ett paket med flera objekt

I Experience Platform väljer du **[!UICONTROL Sandboxes]** i den vänstra navigeringen och sedan **[!UICONTROL Packages]**. Om du vill börja skapa ett nytt paket väljer du **[!UICONTROL Create package]** i det övre högra hörnet.

![Fliken Paket i kontrollpanelen för sandlådor med Skapa-paketet markerat.](../images/use-cases/create-package.png)

Dialogrutan **[!UICONTROL Create package]** visas. Välj **[!UICONTROL Select objects]** och sedan **[!UICONTROL Select]**.

![Dialogrutan Skapa paket med Markera objekt och alternativet Välj markerat.](../images/use-cases/create-package-select-objects.png)

Välj alternativet **[!UICONTROL Multi-object]**. Nu måste du ange ett namn för det nya paketet. Skriv ditt namn i textfältet **[!UICONTROL Package name]**. När du är klar väljer du **[!UICONTROL Create]**.

![Dialogrutan Skapa paket med flera objekt markerade och paketnamnet &quot;Säkerhetskopiera&quot; ifyllt.](../images/use-cases/name-multi-object.png)

Ditt nya paket med flera objekt skapas och är tillgängligt på kontrollpanelen [!UICONTROL Packages]. Välj paketet i listan.

![Kontrollpanelen för paket med paketet Säkerhetskopiering är markerad.](../images/use-cases/package-created.png)

Paketets information och innehåll visas. För närvarande finns det inga objekt i vårt nya paket. Om du vill börja lägga till objekt följer du vägledningen när du [lägger till objekt i ett befintligt paket](../ui/sandbox-tooling.md#add-object-to-a-new-package).

### Skapa nya versioner av säkerhetskopieringspaketet efter behov

Nu när du har skapat det första säkerhetskopieringspaketet för din sandlåda, vill du skapa nya versioner av ditt säkerhetskopieringspaket när dina sandlådekonfigurationer ändras.

Det går att lägga till nya objekt i ditt befintliga säkerhetskopieringspaket, men du uppmanas att skapa nya paket som stöder versionshantering i din sandlåda. Detta gör att du enkelt kan återställa och importera tidigare versioner av dina sandlådor när du fortsätter att utveckla dem.

### Kontrollera din nuvarande användning mot dina licensrättigheter

Nu när säkerhetskopieringspaketet är klart kan du återställa sandlådan för att återställa din användning. Du bör regelbundet övervaka din användning så att du kan justera dina licensrättigheter eller återställa din sandlåda efter behov. Du kan läsa mer om kontrollpanelen för licensanvändning i [användarhandboken](../../dashboards/guides/license-usage.md).

### Återställ sandlådan

Nu kan du återställa sandlådan på ett säkert sätt, förutsatt att sandlådan uppfyller de nödvändiga parametrarna. Följ [återställningen av en sandlådestödlinje](../ui/user-guide.md#reset-a-sandbox) för att börja återställa din sandlåda, och se till att läsa de varningslistningsfall som kan hindra dig från att återställa din sandlåda.

### Importera det nyligen skapade säkerhetskopiepaketet till återställningssandlådan

Nu när du har återställt sandlådan kan du använda det säkerhetskopieringspaket du skapade. Följ verktygshandboken för [sandlådan](../ui/sandbox-tooling.md#import-a-package-to-a-target-sandbox) om du vill se en steg-för-steg-process för att importera ett paket till målsandlådan.

## Andra användningsområden som nås via sandlådeverktyg: {#other-use-cases}

Utforska fler användningsexempel som kan användas via sandlådeverktyg:

- [Aktivera ett kompetenscentrum med hjälp av sandlådeverktyg](./center-of-excellence.md)
