---
title: Begäranden om radering av post (UI-arbetsflöde)
description: Lär dig hur du tar bort poster i användargränssnittet i Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 9ee5225c7494c28023c26181dfe626780133bb5d
workflow-type: tm+mt
source-wordcount: '1781'
ht-degree: 0%

---

# Registrera borttagningsbegäranden (UI-arbetsflöde) {#record-delete}

Använd arbetsytan [[!UICONTROL Data Lifecycle] ](./overview.md) för att ta bort poster i Adobe Experience Platform utifrån deras primära identiteter. Dessa poster kan knytas till enskilda konsumenter eller andra enheter som ingår i identitetsdiagrammet.

>[!IMPORTANT]
>
>Postborttagningar är avsedda att användas för datarensning, borttagning av anonyma data eller datamängning. De **får inte** användas för förfrågningar om rättigheter för registrerade (efterlevnad) som gäller sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). Använd [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället för alla kompatibilitetsfall.

## Förhandskrav {#prerequisites}

Att ta bort poster kräver en fungerande förståelse för hur identitetsfält fungerar i Experience Platform. Du måste känna till identitets namnutrymmesvärden för de entiteter vars poster du vill ta bort, beroende på vilken datamängd (eller vilka datamängder) du tar bort dem från.

Mer information om identiteter i Experience Platform finns i följande dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Förena identiteter mellan enheter och system genom att länka samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [Identitetsnamnutrymmen](../../identity-service/features/namespaces.md): Identitetsnamnutrymmen definierar de olika typerna av identitetsinformation som kan relatera till en enskild person och är en obligatorisk komponent för varje identitetsfält.
* [Kundprofil i realtid](../../profile/home.md): Använder identitetsdiagram för att tillhandahålla enhetliga konsumentprofiler baserade på aggregerade data från flera källor, som uppdateras i nära realtid.
* [Experience Data Model (XDM)](../../xdm/home.md): Tillhandahåller standarddefinitioner och strukturer för Experience Platform-data genom användning av scheman. Alla Experience Platform-datauppsättningar följer ett specifikt XDM-schema, och schemat definierar vilka fält som är identiteter.
* [Identitetsfält](../../xdm/ui/fields/identity.md): Lär dig hur ett identitetsfält definieras i ett XDM-schema.

## Skapa en förfrågan {#create-request}

Om du vill starta processen väljer du **[!UICONTROL Data Lifecycle]** i den vänstra navigeringen i användargränssnittet i Experience Platform. Arbetsytan [!UICONTROL Data lifecycle requests] visas. Välj sedan **[!UICONTROL Create request]** på huvudsidan på arbetsytan.

![Arbetsytan [!UICONTROL Data lifecycle requests] med [!UICONTROL Create request] markerad.](../images/ui/record-delete/create-request-button.png)

Arbetsflödet för att skapa en begäran visas. Som standard är alternativet **[!UICONTROL Delete record]** markerat under avsnittet **[!UICONTROL Requested Action]**. Låt alternativet vara markerat.

>[!IMPORTANT]
> 
>För att förbättra effektiviteten och göra datauppsättningsåtgärderna mindre dyra kan organisationer som har flyttats till Delta-formatet ta bort data från identitetstjänsten, kundprofilen i realtid och datasjön. Den här typen av användare kallas deltmigrerad. Användare från organisationer som har deltmigrerats kan välja att ta bort poster från en enda eller alla datauppsättningar. Användare från organisationer som inte har genomgått deltamigrering kan inte selektivt ta bort poster från en enskild datauppsättning eller alla datauppsättningar, vilket visas i bilden nedan. I det här fallet fortsätter du till avsnittet [Ange identiteter](#provide-identities) i handboken.

![Arbetsflödet för att skapa en begäran med alternativet [!UICONTROL Delete record] markerat och markerat.](../images/ui/record-delete/delete-record.png)

## Välj datauppsättningar {#select-dataset}

Nästa steg är att avgöra om du vill ta bort poster från en enskild datauppsättning eller alla datauppsättningar. Beroende på din organisations konfiguration kanske inte datauppsättningsalternativet är tillgängligt. Om du inte ser det här alternativet fortsätter du till avsnittet [Ange identiteter](#provide-identities) i handboken.

I avsnittet **[!UICONTROL Record Details]** väljer du en alternativknapp för att välja en specifik datamängd eller alla datamängder.

Om du vill ta bort från en viss datauppsättning väljer du **[!UICONTROL Select dataset]** och sedan databasikonen (![Databasikonen](/help/images/icons/database.png)). I dialogrutan som visas väljer du en datauppsättning och sedan **[!UICONTROL Done]** för att bekräfta.

![Dialogrutan [!UICONTROL Select dataset] med en datamängd markerad och [!UICONTROL Done] markerad.](../images/ui/record-delete/select-dataset.png)

Om du vill ta bort från alla datauppsättningar väljer du **[!UICONTROL All datasets]**. Det här alternativet ökar åtgärdens omfattning och kräver att du anger alla relevanta identitetstyper.

![Dialogrutan [!UICONTROL Select dataset] med alternativet [!UICONTROL All datasets] markerat.](../images/ui/record-delete/all-datasets.png)

>[!WARNING]
>
>Om du väljer **[!UICONTROL All datasets]** utökas åtgärden till alla datauppsättningar i organisationen. Varje datauppsättning kan ha en annan primär identitetstyp. Du måste ange **alla identitetstyper** som krävs för att säkerställa korrekt matchning.
>
>Om någon identitetstyp saknas kan vissa poster hoppas över under borttagningen. Detta kan göra bearbetningen långsam och leda till **partiella resultat**.

Varje datauppsättning i Experience Platform har bara stöd för en primär identitetstyp.

* När du tar bort från en **enskild datamängd** måste alla identiteter i din begäran använda **samma typ**.
* När du tar bort från **alla datauppsättningar** kan du ta med **flera identitetstyper**, eftersom olika datauppsättningar kan vara beroende av olika primära identiteter.&quot;

## Ange identiteter {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Namnutrymme för identitet"
>abstract="Ett identitetsnamnutrymme är ett attribut som kopplar en post till en konsumentprofil i Experience Platform. Identitetsnamnområdesfältet för en datauppsättning definieras av det schema som datauppsättningen baseras på. I den här kolumnen måste du ange typen (eller namnutrymmet) för postens ID-namnområde, till exempel `email` för e-postadresser och `ecid` för Experience Cloud ID. Mer information finns i användargränssnittshandboken för datalängd."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Primärt identitetsvärde"
>abstract="I den här kolumnen måste du ange värdet för postens ID-namnutrymme, som måste motsvara identitetstypen som anges i den vänstra kolumnen. Om identitetsnamnområdestypen är `email` ska värdet vara postens e-postadress. Mer information finns i användargränssnittshandboken för datalängd."

När du tar bort poster måste du ange identitetsinformation så att systemet kan avgöra vilka poster som ska tas bort. För datauppsättningar i Experience Platform tas poster bort baserat på fältet **identity namespace** som definieras av datasetens schema.

Precis som alla identitetsfält i Experience Platform består ett identitetsnamnutrymme av två saker: **type** (kallas ibland för ett identitetsnamnutrymme) och **value**. Identitetstypen ger kontext om hur fältet identifierar en post (till exempel en e-postadress). Värdet representerar en posts specifika identitet för den typen (till exempel `jdoe@example.com` för identitetstypen `email`). Vanliga fält som används som identiteter är kontoinformation, enhets-ID och cookie-ID:n.

>[!TIP]
>
>Om du inte känner till identitetsnamnutrymmet för en viss datauppsättning kan du hitta det i Experience Platform-gränssnittet. Välj datauppsättningen i listan på arbetsytan **[!UICONTROL Datasets]**. På informationssidan för datauppsättningen håller du pekaren över namnet på datasetens schema i den högra listen. Identitetsnamnområdet visas tillsammans med schemanamnet och beskrivningen.
>
>![Kontrollpanelen för datauppsättningar med en datauppsättning markerad och en schemadialogruta öppnas från informationspanelen för datauppsättningar. Datauppsättningens primära ID är markerat.](../images/ui/record-delete/dataset-primary-identity.png)

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

Om du vill lägga till fler identiteter väljer du plusikonen (![En plusikon).](/help/images/icons/tree-expand-all.png)) bredvid en av raderna eller välj **[!UICONTROL Add identity]**.

![Arbetsflödet för att skapa en begäran med plusikonen och ikonen för att lägga till identitet markerad.](../images/ui/record-delete/more-identities.png)

## Kvoter och bearbetningstidslinjer {#quotas}

Begäran om att radera poster omfattas av dagliga och månadsvisa gränser för hur många identifierare som får skickas in, beroende på organisationens licensberättigande. Dessa begränsningar gäller för både UI- och API-baserade borttagningsbegäranden.

>[!NOTE]
>
>Du kan skicka upp till **1 000 000 identifierare per dag**, men bara om den återstående månadskvoten tillåter det. Om din månadskvot är mindre än 1 miljon, kan din dagliga inskickning inte överstiga denna gräns.

### Möjlighet att skicka in per produkt varje månad {#quota-limits}

Tabellen nedan visar inlämningsgränser för identifierare per produkt och berättigandenivå. För varje produkt är den månatliga övre gränsen det lägsta av två värden: ett fast identifierartak eller ett procentbaserat tröskelvärde som är knutet till den licensierade datavolymen.

| Produkt | Tillståndsbeskrivning | Månatligt tak (den som är mindre) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP eller Adobe Journey Optimizer | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 5 % av den adresserbara publiken |
| Real-Time CDP eller Adobe Journey Optimizer | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 10 % av den adresserbara publiken |
| Customer Journey Analytics | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 100 identifierare per miljon CJA-rader |
| Customer Journey Analytics | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 200 identifierare per miljon CJA-rader |

>[!NOTE]
>
> De flesta organisationer har lägre månadsgränser baserat på den faktiska adresserbara målgruppen eller CJA-radrättigheterna.

Kvoterna återställs den första dagen i varje kalendermånad. Oanvänd kvot för överföring av **inte**.

>[!NOTE]
>
>Kvoterna baseras på din organisations licensierade månadsberättigande för **skickade identifierare**. Dessa används inte av systemskyddsräcken, men kan övervakas och granskas.
>
>Borttagning av post är en **delad tjänst**. Det högsta antalet licenser som gäller för Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics och eventuella tillägg till Shield.

### Bearbetar tidslinjer för identifieraröverföringar {#sla-processing-timelines}

När du har skickat in en post köas och bearbetas förfrågningar om radering baserat på din berättigandenivå.

| Produkt- och berättigandebeskrivning | Kövaraktighet | Maximal bearbetningstid (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | Upp till 15 dagar | 30 dagar |
| Med tillägget Privacy and Security Shield eller Healthcare Shield | Normalt 24 timmar | 15 dagar |

Om din organisation kräver högre gränser kontaktar du Adobe för att få en tillståndsgranskning.

>[!TIP]
>
>Information om hur du kontrollerar din aktuella kvotanvändning eller tillståndsnivå finns i [referensguiden för kvoter](../api/quota.md).

## Skicka begäran {#submit}

När du har lagt till identiteter i begäran anger du ett namn och en valfri beskrivning för begäran under **[!UICONTROL Request settings]** innan du väljer **[!UICONTROL Submit]**.

>[!TIP]
>
>Du kan skicka upp till 10 000 identiteter per begäran via gränssnittet. Om du vill skicka större volymer (upp till 100 000 ID:n per begäran) använder du [API-metoden](../api/workorder.md#create).

![Begärandeinställningens [!UICONTROL Name]- och [!UICONTROL Description]-fält med [!UICONTROL Submit] markerat.](../images/ui/record-delete/submit.png)

En [!UICONTROL Confirm request]-dialogruta visas som anger att identiteterna inte kan återställas när de har tagits bort. Markera **[!UICONTROL Submit]** för att bekräfta listan med identiteter vars data du vill ta bort.

![Dialogrutan [!UICONTROL Confirm request].](../images/ui/record-delete/confirm-request.png)

När begäran har skickats skapas en arbetsordning och visas på fliken [!UICONTROL Record] på arbetsytan i [!UICONTROL Data Lifecycle]. Härifrån kan du övervaka arbetsorderns status medan den bearbetar begäran.

>[!NOTE]
>
>Se översiktsavsnittet på [tidslinjer och genomskinlighet](../home.md#record-delete-transparency) för mer information om hur postborttagningar bearbetas när de har körts.

![Fliken [!UICONTROL Record] på arbetsytan [!UICONTROL Data Lifecycle] med den nya begäran markerad.](../images/ui/record-delete/request-log.png)

## Nästa steg

I det här dokumentet beskrivs hur du tar bort poster i användargränssnittet i Experience Platform. Mer information om hur du utför andra hanteringsuppgifter för datalängd i användargränssnittet finns i [Översikt över användargränssnittet för datalängd](./overview.md).

Mer information om hur du tar bort poster med hjälp av API:t för datahygien finns i [slutpunktshandboken för arbetsorder](../api/workorder.md).
