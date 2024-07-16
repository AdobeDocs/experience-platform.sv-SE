---
title: Ta bort poster
description: Lär dig hur du tar bort poster i användargränssnittet i Adobe Experience Platform.
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 9981f35732b041a92c5a371e727a8facb6636cf5
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 0%

---

# Ta bort poster {#record-delete}

Använd arbetsytan [[!UICONTROL Data Lifecycle] ](./overview.md) för att ta bort poster i Adobe Experience Platform utifrån deras primära identiteter. Dessa poster kan knytas till enskilda konsumenter eller andra enheter som ingår i identitetsdiagrammet.

>[!IMPORTANT]
> 
>Funktionen Ta bort post finns för närvarande i Beta och är endast tillgänglig i en **begränsad version**. Det är inte tillgängligt för alla kunder. Begäranden om postborttagning är bara tillgängliga för organisationer i den begränsade versionen.
> 
> 
>Postborttagningar är avsedda att användas för datarensning, borttagning av anonyma data eller datamängning. De **får inte** användas för förfrågningar om rättigheter för registrerade (efterlevnad) som gäller sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). Använd [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället för alla kompatibilitetsfall.

## Förhandskrav {#prerequisites}

Att ta bort poster kräver en fungerande förståelse för hur identitetsfält fungerar i Experience Platform. Du måste känna till identitets namnutrymmesvärden för de entiteter vars poster du vill ta bort, beroende på vilken datamängd (eller vilka datamängder) du tar bort dem från.

Mer information om identiteter i Platform finns i följande dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Förena identiteter mellan enheter och system genom att länka samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [Identitetsnamnutrymmen](../../identity-service/features/namespaces.md): Identitetsnamnutrymmen definierar de olika typerna av identitetsinformation som kan relatera till en enskild person och är en obligatorisk komponent för varje identitetsfält.
* [Kundprofil i realtid](../../profile/home.md): Använder identitetsdiagram för att tillhandahålla enhetliga konsumentprofiler baserade på aggregerade data från flera källor, som uppdateras i nära realtid.
* [Experience Data Model (XDM)](../../xdm/home.md): Tillhandahåller standarddefinitioner och strukturer för plattformsdata genom användning av scheman. Alla plattformsdatauppsättningar följer ett specifikt XDM-schema, och schemat definierar vilka fält som är identiteter.
* [Identitetsfält](../../xdm/ui/fields/identity.md): Lär dig hur ett identitetsfält definieras i ett XDM-schema.

## Skapa en förfrågan {#create-request}

Om du vill starta processen väljer du **[!UICONTROL Data Lifecycle]** i den vänstra navigeringen i plattformsgränssnittet. Arbetsytan [!UICONTROL Data lifecycle requests] visas. Välj sedan **[!UICONTROL Create request]** på huvudsidan på arbetsytan.

![Arbetsytan [!UICONTROL Data lifecycle requests] med [!UICONTROL Create request] markerad.](../images/ui/record-delete/create-request-button.png)

Arbetsflödet för att skapa en begäran visas. Som standard är alternativet **[!UICONTROL Delete record]** markerat under avsnittet **[!UICONTROL Requested Action]**. Låt alternativet vara markerat.

>[!IMPORTANT]
> 
>För att förbättra effektiviteten och göra datauppsättningsåtgärderna mindre dyra kan organisationer som har flyttats till Delta-formatet ta bort data från identitetstjänsten, kundprofilen i realtid och datasjön. Den här typen av användare kallas deltmigrerad. Användare från organisationer som har deltmigrerats kan välja att ta bort poster från en enda eller alla datauppsättningar. Användare från organisationer som inte har genomgått deltamigrering kan inte selektivt ta bort poster från en enskild datauppsättning eller alla datauppsättningar, vilket visas i bilden nedan. I det här fallet fortsätter du till avsnittet [Ange identiteter](#provide-identities) i handboken.

![Arbetsflödet för att skapa en begäran med alternativet [!UICONTROL Delete record] markerat och markerat.](../images/ui/record-delete/delete-record.png)

## Välj datauppsättningar {#select-dataset}

Nästa steg är att avgöra om du vill ta bort poster från en enskild datauppsättning eller alla datauppsättningar. Om det här alternativet inte är tillgängligt för dig fortsätter du till avsnittet [Ange identiteter](#provide-identities) i handboken.

Under avsnittet **[!UICONTROL Record Details]** använder du alternativknappen för att välja mellan en viss datauppsättning och alla datauppsättningar. Om du väljer **[!UICONTROL Select dataset]** fortsätter du med att välja databasikonen (![Databasikonen](../images/ui/record-delete/database-icon.png)) för att öppna en dialogruta med en lista över tillgängliga datauppsättningar. Välj önskad datauppsättning i listan följt av **[!UICONTROL Done]**.

![Dialogrutan [!UICONTROL Select dataset] med en datamängd markerad och [!UICONTROL Done] markerad.](../images/ui/record-delete/select-dataset.png)

Om du vill ta bort poster från alla datauppsättningar väljer du **[!UICONTROL All datasets]**.

![Dialogrutan [!UICONTROL Select dataset] med alternativet [!UICONTROL All datasets] markerat.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Om du väljer alternativet **[!UICONTROL All datasets]** kan det ta längre tid att ta bort borttagningen och det kan leda till att posten inte tas bort korrekt.

## Ange identiteter {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Namnutrymme för identitet"
>abstract="Ett identitetsnamnutrymme är ett attribut som kopplar en post till en konsumentprofil i Experience Platform. Identitetsnamnområdesfältet för en datauppsättning definieras av det schema som datauppsättningen baseras på. I den här kolumnen måste du ange typen (eller namnutrymmet) för postens ID-namnområde, till exempel `email` för e-postadresser och `ecid` för Experience Cloud ID. Mer information finns i användargränssnittshandboken för datalängd."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Primärt identitetsvärde"
>abstract="I den här kolumnen måste du ange värdet för postens ID-namnutrymme, som måste motsvara identitetstypen som anges i den vänstra kolumnen. Om identitetsnamnområdestypen är `email` ska värdet vara postens e-postadress. Mer information finns i användargränssnittshandboken för datalängd."

När du tar bort poster måste du ange identitetsinformation så att systemet kan avgöra vilka poster som ska tas bort. För alla datauppsättningar i plattformen tas poster bort baserat på fältet **identity namespace** som definieras av datasetens schema.

Precis som alla identitetsfält i Platform består ett identitetsnamnutrymme av två saker: **type** (kallas ibland för ett identitetsnamnutrymme) och **value**. Identitetstypen ger kontext om hur fältet identifierar en post (till exempel en e-postadress). Värdet representerar en posts specifika identitet för den typen (till exempel `jdoe@example.com` för identitetstypen `email`). Vanliga fält som används som identiteter är kontoinformation, enhets-ID och cookie-ID:n.

>[!TIP]
>
>Om du inte känner till identitetsnamnutrymmet för en viss datauppsättning kan du hitta det i plattformsgränssnittet. Välj datauppsättningen i listan på arbetsytan **[!UICONTROL Datasets]**. På informationssidan för datauppsättningen håller du pekaren över namnet på datasetens schema i den högra listen. Identitetsnamnområdet visas tillsammans med schemanamnet och beskrivningen.
>
>![Kontrollpanelen för datauppsättningar med en datauppsättning markerad och en schemadialogruta öppnas från informationspanelen för datauppsättningar. Datauppsättningens primära ID är markerat.](../images/ui/record-delete/dataset-primary-identity.png)

Om du tar bort poster från en enskild datauppsättning måste alla identiteter som du anger ha samma typ, eftersom en datauppsättning bara kan ha ett identitetsnamnutrymme. Om du tar bort från alla datauppsättningar kan du inkludera flera identitetstyper eftersom olika datauppsättningar kan ha olika primära identiteter.

Det finns två alternativ för att ange identiteter när du tar bort poster:

* [Överföra en JSON-fil](#upload-json)
* [Ange primära identitetsvärden manuellt](#manual-identity)

### Överföra en JSON-fil {#upload-json}

Om du vill överföra en JSON-fil kan du dra och släppa filen till det angivna området eller välja **[!UICONTROL Choose files]** för att bläddra och välja från din lokala katalog.

![Arbetsflödet för att skapa en begäran med valda filer och dra och släpp-gränssnittet för överföring av JSON-filer är markerat.](../images/ui/record-delete/upload-json.png)

JSON-filen måste formateras som en array med objekt, där varje objekt representerar en identitet.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Egenskap | Beskrivning |
| --- | --- |
| `namespaceCode` | Identitetstypen. |
| `value` | Det primära identitetsvärdet som anges av typen. |

När filen har överförts kan du fortsätta att [skicka begäran](#submit).

### Ange identiteter manuellt {#manual-identity}

Om du vill ange identiteter manuellt väljer du **[!UICONTROL Add identity]**.

![Arbetsflödet för att skapa en begäran med alternativet [!UICONTROL Add identity] markerat.](../images/ui/record-delete/add-identity.png)

Det visas kontroller som gör att du kan ange identiteter en åt gången. Under **[!UICONTROL identity namespace]** använder du listrutan för att välja identitetstyp. Ange ID-namnutrymmesvärdet för posten under **[!UICONTROL Primary Identity Value]**.

![Arbetsflödet för att skapa en begäran med ett identitetsfält har lagts till manuellt.](../images/ui/record-delete/identity-added.png)

Om du vill lägga till fler identiteter väljer du plusikonen (![En plusikon).](../images/ui/record-delete/plus-icon.png)) bredvid en av raderna eller välj **[!UICONTROL Add identity]**.

![Arbetsflödet för att skapa en begäran med plusikonen och ikonen för att lägga till identitet markerad.](../images/ui/record-delete/more-identities.png)

## Skicka begäran {#submit}

När du har lagt till identiteter i begäran anger du ett namn och en valfri beskrivning för begäran under **[!UICONTROL Request settings]** innan du väljer **[!UICONTROL Submit]**.

>[!IMPORTANT]
> 
>Det finns olika gränser för det totala antalet unika ID-postborttagningar som kan skickas varje månad. Dessa begränsningar baseras på ditt licensavtal. Organisationer som har köpt alla utgåvor av Adobe Real-time Customer Data Platform eller Adobe Journey Optimizer kan skicka in upp till 100 000 identitetspostborttagningar varje månad. Organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield** kan skicka in upp till 600 000 identitetspostborttagningar varje månad.<br>Du kan skicka 10 000 ID:n åt gången med en enda begäran om radering av en post via gränssnittet. [API-metoden för att ta bort poster](../api/workorder.md#create) tillåter att 100 000 ID:n skickas samtidigt.<br>Det är bäst att skicka så många ID:n som möjligt per begäran, upp till din ID-gräns. Om du tänker ta bort en stor mängd ID:n bör du inte skicka in en låg volym eller ett enda ID per postborttagningsbegäran.

![Begärandeinställningens [!UICONTROL Name]- och [!UICONTROL Description]-fält med [!UICONTROL Submit] markerat.](../images/ui/record-delete/submit.png)

En [!UICONTROL Confirm request]-dialogruta visas som anger att identiteterna inte kan återställas när de har tagits bort. Markera **[!UICONTROL Submit]** för att bekräfta listan med identiteter vars data du vill ta bort.

![Dialogrutan [!UICONTROL Confirm request].](../images/ui/record-delete/confirm-request.png)

När begäran har skickats skapas en arbetsordning och visas på fliken [!UICONTROL Record] på arbetsytan i [!UICONTROL Data Lifecycle]. Härifrån kan du övervaka arbetsorderns status medan den bearbetar begäran.

>[!NOTE]
>
>Se översiktsavsnittet på [tidslinjer och genomskinlighet](../home.md#record-delete-transparency) för mer information om hur postborttagningar bearbetas när de har körts.

![Fliken [!UICONTROL Record] på arbetsytan [!UICONTROL Data Lifecycle] med den nya begäran markerad.](../images/ui/record-delete/request-log.png)

## Nästa steg

I det här dokumentet beskrivs hur du tar bort poster i användargränssnittet för Experience Platform. Mer information om hur du utför andra hanteringsuppgifter för datalängd i användargränssnittet finns i [Översikt över användargränssnittet för datalängd](./overview.md).

Mer information om hur du tar bort poster med hjälp av API:t för datahygien finns i [slutpunktshandboken för arbetsorder](../api/workorder.md).
