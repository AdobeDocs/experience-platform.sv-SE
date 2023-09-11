---
title: Sandlådor
description: Exportera och importera sömlöst sandlådekonfigurationer mellan sandlådor.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 1%

---


# [!BADGE Beta] Verktyg i sandlådan

>[!IMPORTANT]
>
>The **Verktyg i sandlådan** funktionen som beskrivs nedan är endast tillgänglig för utvalda betakunder.

>[!NOTE]
>
>Verktyg i sandlådan är en grundläggande funktion som har stöd för båda [!DNL Real-Time Customer Data Platform] och [!DNL Journey Optimizer] för att förbättra utvecklingscykelns effektivitet och konfigurationsnoggrannheten.<br><br>Du måste ha följande två rollbaserade behörigheter för åtkomstkontroll för att kunna använda sandlådeverktygen:<br>- `manage-sandbox` eller `view-sandbox`<br>- `manage-package`

Förbättra konfigurationsnoggrannheten över sandlådor och exportera och importera smidigt sandlådekonfigurationer mellan sandlådor med sandlådeverktygen. Använd sandlådeverktyg för att minska tidsåtgången för implementeringsprocessen och flytta framgångsrika konfigurationer mellan sandlådor.

Du kan använda sandlådeverktygen för att markera olika objekt och exportera dem till ett paket. Ett paket kan bestå av ett enda objekt, flera objekt eller en hel sandlåda. Alla objekt som ingår i ett paket måste komma från samma sandlåda.

## Objekt som stöds för sandlådeverktyg {#supported-objects}

I tabellen nedan visas objekt som för närvarande stöds för sandlådeverktyg:

| Plattform | Objekt |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | Resor |
| Kunddataplattform | Källor |
| Kunddata Plattform | Segment |
| Kunddataplattform | Identiteter |
| Kunddataplattform | Policyer |
| Kunddataplattform | Scheman |
| Kunddataplattform | Datauppsättningar |

Följande objekt importeras men har utkaststatus eller inaktiverad status:

| Funktion | Objekt | Status |
| --- | --- | --- |
| Importstatus | Källdataflöde | Utkast |
| Importstatus | Resa | Utkast |
| Enhetlig profil | Schema | Handikappade |
| Enhetlig profil | Datauppsättning | Handikappade |
| Policyer | Samtyckesprinciper | Handikappade |
| Policyer | Datastyrningspolicyer | Handikappade |

De kantfall som anges nedan ingår inte i paketet:

* Schemarelationer

## Exportera objekt till ett paket {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="Spara och avsluta paket"
>abstract="Om du vill avsluta paketet och spara kan du helt enkelt använda alternativet Bakåt."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Ta bort ett objekt"
>abstract="Användaren måste markera raden och sedan använda borttagningsalternativet (som är tillgängligt när den markeras) för att ta bort raden."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Förfallotid för paket"
>abstract="Datumet anges till 90 dagar från idag. Datumet ändras inte förrän paketet publiceras. Om en användare besöker paketet med utkaststatus i morgon flyttas datumet med +1 dag (om inte användaren anger det)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Paketstatus"
>abstract="Som standard är statusen Utkast. När paketet har publicerats ändras statusen till publicerad. Inga ändringar kan göras efter att paketet har publicerats."

>[!NOTE]
>
>Du kan bara importera ett paket om du har behörighet att komma åt objekten.

I det här exemplet dokumenteras processen att exportera ett schema och lägga till det i ett paket. Du kan använda samma process för att exportera andra objekt, till exempel datauppsättningar, resor och många andra.

### Lägga till objekt i ett nytt paket {#add-object-to-new-package}

Välj **[!UICONTROL Schemas]** från vänster navigering och sedan väljer du **[!UICONTROL Browse]** som listar tillgängliga scheman. Välj sedan ellipsen (`...`) bredvid det valda schemat och en listruta visar kontroller. Välj **[!UICONTROL Add to package]** i listrutan.

![Lista med scheman som visar listrutemenyn med markering av [!UICONTROL Add to package] kontroll.](../images/ui/sandbox-tooling/add-to-package.png)

Från **[!UICONTROL Add to package]** väljer du **[!UICONTROL Create new package]** alternativ. Ange en [!UICONTROL Name] för ditt paket och [!UICONTROL Description]väljer **[!UICONTROL Add]**.

![The [!UICONTROL Add to package] dialogruta med [!UICONTROL Create new package] markerat och markerat [!UICONTROL Add].](../images/ui/sandbox-tooling/create-new-package.png)

Du kommer tillbaka till **[!UICONTROL Schemas]** miljö. Nu kan du lägga till fler objekt i det paket du skapade genom att följa stegen nedan.

### Lägga till ett objekt i ett befintligt paket och publicera {#add-object-to-existing-package}

Om du vill visa en lista med tillgängliga scheman väljer du **[!UICONTROL Schemas]** från vänster navigering och sedan väljer du **[!UICONTROL Browse]** -fliken. Välj sedan ellipsen (`...`) bredvid det valda schemat för att visa kontrollalternativ i en listruta. Välj **[!UICONTROL Add to package]** i listrutan.

![Lista med scheman som visar listrutemenyn med markering av [!UICONTROL Add to package] kontroll.](../images/ui/sandbox-tooling/add-to-package.png)

The **[!UICONTROL Add to package]** visas. Välj **[!UICONTROL Existing package]** väljer du **[!UICONTROL Package name]** och välj det paket som behövs. Äntligen väljer du **[!UICONTROL Add]** för att bekräfta dina val.

![[!UICONTROL Add to package] visas ett valt paket i listrutan.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Listan med objekt som läggs till i paketet visas. Om du vill publicera paketet och göra det tillgängligt för import till sandlådor väljer du **[!UICONTROL Publish]**.

![En lista med objekt i paketet som markerar [!UICONTROL Publish] alternativ.](../images/ui/sandbox-tooling/publish-package.png)

Välj **[!UICONTROL Publish]** för att bekräfta att paketet ska offentliggöras.

![Bekräftelsedialogrutan för publiceringspaket, markera [!UICONTROL Publish] alternativ.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>När det har publicerats kan paketets innehåll inte ändras. För att undvika kompatibilitetsproblem måste du se till att alla nödvändiga resurser har valts. Om ändringar måste göras måste du skapa ett nytt paket.

Du kommer tillbaka till **[!UICONTROL Packages]** i [!UICONTROL Sandboxes] -miljö, där du kan se det nya publicerade paketet.

![Lista över sandlådepaket som markerar det nya publicerade paketet.](../images/ui/sandbox-tooling/published-packages.png)

## Importera ett paket till en målsandlåda {#import-package-to-target-sandbox}

Om du vill importera paketet till en målsandlåda går du till sandlådorna **[!UICONTROL Browse]** och välj plustecknet (+) bredvid namnet på sandlådan.

![Sandlådorna **[!UICONTROL Browse]** som markerar valet av importpaket.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Välj menyn **[!UICONTROL Package name]** du vill importera till målsandlådan. Lägg till ett valfritt **[!UICONTROL Job name]**, som kommer att användas för framtida övervakning, väljer sedan **[!UICONTROL Next]**.

![Sidan med importinformation som visar [!UICONTROL Package name] listrutemarkering](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

The [!UICONTROL Package object and dependencies] sidan innehåller en lista med alla resurser som ingår i det här paketet. Systemet identifierar automatiskt beroende objekt som krävs för att importera markerade överordnade objekt.

![The [!UICONTROL Package object and dependencies] visas en lista med resurser som ingår i paketet.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>Beroende objekt kan ersättas med befintliga objekt i målsandlådan, vilket gör att du kan återanvända befintliga objekt i stället för att skapa en ny version. Om du till exempel importerar ett paket som innehåller scheman kan du återanvända befintliga anpassade fältgrupper och identitetsnamnutrymmen i målsandlådan. När du importerar ett paket som innehåller Journeys kan du också återanvända befintliga segment i målsandlådan.

Om du vill använda ett befintligt objekt väljer du pennikonen bredvid det beroende objektet. Alternativen för att skapa nya eller använda befintliga visas. Välj **[!UICONTROL Use existing]**.

![The [!UICONTROL Package object and dependencies] sida med alternativ för beroende objekt [!UICONTROL Create new] och [!UICONTROL Use existing].](../images/ui/sandbox-tooling/use-existing-object.png)

The **[!UICONTROL Field group]** visas en lista med fältgrupper som är tillgängliga för objektet. Markera de fältgrupper som krävs och välj sedan **[!UICONTROL Save]**.

![En lista med fält som visas på [!UICONTROL Field group] dialogruta, markera [!UICONTROL Save] markering. ](../images/ui/sandbox-tooling/field-group-list.png)

Du kommer tillbaka till [!UICONTROL Package object and dependencies] sida. Välj **[!UICONTROL Finish]** för att slutföra paketimporten.

![The [!UICONTROL Package object and dependencies] sidan visar en lista med resurser som ingår i paketet, med markering [!UICONTROL Finish].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportera och importera en hel sandlåda

### Exportera en hel sandlåda {#export-entire-sandbox}

Om du vill exportera en hel sandlåda går du till [!UICONTROL Sandboxes] **[!UICONTROL Packages]** och markera **[!UICONTROL Create package]**.

![The [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tabbmarkering [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Välj **[!UICONTROL Entire sandbox]** för pakettypen i [!UICONTROL Create package] -dialogrutan. Ange en [!UICONTROL Package name] för ditt paket och väljer **[!UICONTROL Sandbox]** i listrutan. Äntligen väljer du **[!UICONTROL Create]** för att bekräfta tävlingsbidragen.

![The [!UICONTROL Create package] dialogruta med ifyllda fält och markering [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

Paketet har skapats. Välj **[!UICONTROL Publish]** för att publicera paketet.

![Lista över sandlådepaket som markerar det nya publicerade paketet.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Du kommer tillbaka till **[!UICONTROL Packages]** i [!UICONTROL Sandboxes] -miljö, där du kan se det nya publicerade paketet.

### Importera hela sandlådepaketet {#import-entire-sandbox-package}

Om du vill importera paketet till en målsandlåda går du till [!UICONTROL Sandboxes] **[!UICONTROL Browse]** och välj plustecknet (+) bredvid namnet på sandlådan.

![Sandlådorna **[!UICONTROL Browse]** som markerar valet av importpaket.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Använd listrutemenyn och markera den fullständiga sandlådan med **[!UICONTROL Package name]** nedrullningsbar meny. Lägg till ett valfritt **[!UICONTROL Job name]**, som kommer att användas för framtida övervakning, väljer sedan **[!UICONTROL Next]**.

![Sidan med importinformation som visar [!UICONTROL Package name] listrutemarkering](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Alla objekt skapas som nya från paketet när du importerar en hel sandlåda. Objekten finns inte med i listan [!UICONTROL Package object and dependencies] sida, eftersom det kan finnas multipler. Ett textbundet meddelande visas med information om objekttyper som inte stöds.

Du kommer till [!UICONTROL Package object and dependencies] sida där du kan se antalet objekt och beroenden som är importerade och exkluderade objekt. Välj **[!UICONTROL Import]** för att slutföra paketimporten.

![The [!UICONTROL Package object and dependencies] sidan visar det textbundna meddelandet om objekttyper som inte stöds, markering [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

## Övervaka importjobb och visa information om importobjekt

Om du vill visa importerade objekt och importerad information går du till [!UICONTROL Sandboxes] **[!UICONTROL Imports]** och väljer paketet i listan. Du kan också använda sökfältet för att söka efter paketet.

![Sandlådorna [!UICONTROL Imports] -fliken markerar valet av importpaket.](../images/ui/sandbox-tooling/imports-tab.png)

### Visa importerade objekt {#view-imported-objects}

På **[!UICONTROL Imports]** i [!UICONTROL Sandboxes] miljö, välja **[!UICONTROL View imported objects]** från den högra informationsrutan.

Välj **[!UICONTROL View imported objects]** från höger informationsruta på sidan **[!UICONTROL Imports]** i [!UICONTROL Sandboxes] miljö.

![Sandlådorna [!UICONTROL Imports] tabbmarkeringar i [!UICONTROL View imported objects] i den högra rutan.](../images/ui/sandbox-tooling/view-imported-objects.png)

Använd pilarna för att expandera objekt och visa den fullständiga listan med fält som har importerats till paketet.

![Sandlådorna [!UICONTROL Imported objects] med en lista över objekt som importerats till paketet.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### Visa importinformation {#view-import-details}

Välj **[!UICONTROL View import details]** från den högra informationsrutan i **[!UICONTROL Imports]** i sandlådemiljön.

![Sandlådorna [!UICONTROL Imports] tabbmarkeringar i [!UICONTROL View import details] i den högra rutan.](../images/ui/sandbox-tooling/view-import-details.png)

The **[!UICONTROL Import details]** visas en detaljerad beskrivning av importen.

![The [!UICONTROL Import details] en detaljerad beskrivning av importen.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>När en import är klar får du meddelanden i plattformsgränssnittet. Du kommer åt dessa meddelanden via varningsikonen. Du kan navigera till felsökning härifrån om ett jobb misslyckas.

## Nästa steg

Det här dokumentet visar hur du använder sandlådeverktygen i användargränssnittet i Experience Platform. Mer information om sandlådor finns i [användarhandbok för sandlåda](../ui/user-guide.md).

Anvisningar om hur du utför olika åtgärder med sandbox-API:t finns i [utvecklarguide för sandlådor](../api/getting-started.md). En översikt över sandlådor i Experience Platform på hög nivå finns i [översiktlig dokumentation](../home.md).
