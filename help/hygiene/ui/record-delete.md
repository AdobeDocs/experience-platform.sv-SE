---
title: Ta bort poster
description: Lär dig hur du tar bort poster i användargränssnittet i Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 6e97b3a6b3830cf88802a8dd89944b6ce8791f02
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 0%

---

# [!BADGE Beta]{type=Informative} Ta bort poster {#record-delete}

Använd [[!UICONTROL Data Lifecycle] arbetsyta](./overview.md) om du vill ta bort poster i Adobe Experience Platform utifrån deras primära identiteter. Dessa poster kan knytas till enskilda konsumenter eller andra enheter som ingår i identitetsdiagrammet.

>[!IMPORTANT]
> 
Funktionen Ta bort post är för närvarande i betaversionen och endast tillgänglig i en **begränsad release**. Det är inte tillgängligt för alla kunder. Begäranden om postborttagning är bara tillgängliga för organisationer i den begränsade versionen.
> 
> 
Postborttagningar är avsedda att användas för datarensning, borttagning av anonyma data eller datamängning. De är **not** som ska användas för förfrågningar om registrerade rättigheter (överensstämmelse) som rör sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). För all användning av regelefterlevnad [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället.

## Förutsättningar {#prerequisites}

Att ta bort poster kräver en fungerande förståelse för hur identitetsfält fungerar i Experience Platform. Du måste känna till de primära identitetsvärdena för de entiteter vars poster du vill ta bort, beroende på vilken datamängd (eller vilka datamängder) du tar bort dem från.

Mer information om identiteter i Platform finns i följande dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Överbryggar identiteter mellan enheter och system, länkar samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [Identitetsnamnutrymmen](../../identity-service/namespaces.md): Identitetsnamnutrymmen definierar olika typer of identitetsinformation som kan relatera till en person och som är en obligatorisk komponent för varje identitetsfält.
* [Kundprofil i realtid](../../profile/home.md): Använder identitetsdiagram för att tillhandahålla enhetliga konsumentprofiler baserade på aggregerade data från flera källor, som uppdateras i nära realtid.
* [Experience Data Model (XDM)](../../xdm/home.md): Tillhandahåller standarddefinitioner och -strukturer för plattformsdata genom användning av scheman. Alla plattformsdatauppsättningar följer ett specifikt XDM-schema, och schemat definierar vilka fält som är identiteter.
* [Identitetsfält](../../xdm/ui/fields/identity.md): Lär dig hur ett identitetsfält definieras i ett XDM-schema.

## Skapa en förfrågan {#create-request}

För att starta processen väljer du **[!UICONTROL Data Lifecycle]** i den vänstra navigeringen i plattformsgränssnittet. The [!UICONTROL Data lifecycle requests] visas. Nästa, välj **[!UICONTROL Create request]** från huvudsidan på arbetsytan.

![The [!UICONTROL Data lifecycle requests] arbetsyta med [!UICONTROL Create request] markerat.](../images/ui/record-delete/create-request-button.png)

Arbetsflödet för att skapa en begäran visas. Som standard är **[!UICONTROL Delete record]** alternativet är markerat under **[!UICONTROL Requested Action]** -avsnitt. Låt alternativet vara markerat.

>[!IMPORTANT]
> 
Som en del av de pågående förändringarna för att förbättra effektiviteten och göra datauppsättningarna billigare kan organisationer som har flyttats till Delta-formatet ta bort data från identitetstjänsten, kundprofilen i realtid och datasjön. Den här typen of -användaren kallas deltmigrerad. Användare från organisationer som har deltmigrerats kan välja att ta bort poster från en enda eller alla datauppsättningar. Användare från organisationer som inte har deltmigrerats kan inte välja att ta bort poster från en enda eller alla datauppsättningar enligt bilden nedan. I det här fallet fortsätter du till [ange identiteter](#provide-identities) i guiden.

![Arbetsflödet för att skapa begäran med [!UICONTROL Delete record] markerat och markerat alternativ.](../images/ui/record-delete/delete-record.png)

## Välj datauppsättningar {#select-dataset}

Nästa steg är att avgöra om du vill ta bort poster från en enskild datauppsättning eller alla datauppsättningar. Om det här alternativet inte är tillgängligt för dig fortsätter du till [ange identiteter](#provide-identities) i guiden.

Under **[!UICONTROL Record Details]** använder du alternativknappen för att välja mellan en viss datauppsättning och alla datauppsättningar. Om du väljer **[!UICONTROL Select dataset]** fortsätter du med att välja databasikonen (![Databasikonen](../images/ui/record-delete/database-icon.png)) för att öppna en dialogruta med en lista över tillgängliga datauppsättningar. Välj önskad datauppsättning i listan följt av **[!UICONTROL Done]**.

![The [!UICONTROL Select dataset] dialogruta med en datauppsättning vald och [!UICONTROL Done] markerad.](../images/ui/record-delete/select-dataset.png)

Om du vill ta bort poster från alla datauppsättningar väljer du **[!UICONTROL All datasets]**.

![The [!UICONTROL Select dataset] med [!UICONTROL All datasets] markerat alternativ.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
Markera **[!UICONTROL All datasets]** kan göra att borttagningsåtgärden tar längre tid och kanske inte resulterar i korrekt borttagning av poster.

## Ange identiteter {#provide-identities}

[!CONTEXTUALHELP]
id="platform_hygiene_primaryidentity"
title="Primär identitet"
abstract="En primär identitet är ett attribut som kopplar en post till en konsumentprofil i Experience Platform. Det primära identitetsfältet för en datauppsättning definieras av det schema som datauppsättningen baseras på. I den här kolumnen måste du ange typ (or namnutrymme) för postens primära identitet, till exempel `email` för mejladresser och `ecid` för Experience Cloud ID. Mer information finns i användargränssnittshandboken för datalängd."

[!CONTEXTUALHELP]
id="platform_hygiene_identityvalue"
title="Identitetsvärde"
abstract="I den här kolumnen måste du ange värdet för postens primära identitet, som måste motsvara identitetstypen provided i den vänstra kolumnen. Om den primära identitetstypen is `email`ska värdet vara postens e-postadress. Mer information finns i användargränssnittshandboken för datalängd."

När du tar bort poster måste du ange identitetsinformation så att systemet kan avgöra vilka poster som ska tas bort. För alla datauppsättningar i plattformen tas poster bort baserat på **primär identitet** fält som definieras av datauppsättningens schema.

Precis som alla identitetsfält i Platform består en primär identitet av två saker: en **type** (kallas ibland för ett id-namnutrymme) och en **value**. Identitetstypen provides kontext för hur fältet identifierar en post (t.ex. en e-postadress) och värdet representerar en posts specifika identitet för den typen (for exempel, `jdoe@example.com` för `email` identitetstyp). Common fält som används som identiteter innehåller kontoinformation, enhets-ID och cookie-ID:n.

>[!TIP]
>
Om du inte känner till den primära identiteten för en viss datauppsättning kan du hitta den i användargränssnittet för plattformen. I **[!UICONTROL Datasets]** väljer du den aktuella datauppsättningen i listan. På informationssidan för datauppsättningen håller du pekaren över namnet på datasetens schema i den högra listen. Den primära identiteten visas tillsammans med schemanamnet och beskrivningen.
>
![Kontrollpanelen för datauppsättningar med en datauppsättning markerad och en schemadialogruta öppnas från panelen med datauppsättningsinformation. Datauppsättningens primära ID är markerat.](../images/ui/record-delete/dataset-primary-identity.png)

Om du tar bort poster från en enskild datauppsättning måste alla identiteter som du anger ha samma typ, since en datauppsättning kan bara ha en primär identitet. Om du tar bort från alla datauppsättningar kan du inkludera flera identitetstyper since olika datauppsättningar kan ha olika primära identiteter.

Det finns två alternativ för att ange identiteter när du tar bort poster:

* [Överföra en JSON-fil](#upload-json)
* [Ange identitetsvärden manuellt](#manual-identity)

### Överföra en JSON-fil {#upload-json}

Om du vill överföra en JSON-fil kan du dra och släppa filen till det angivna området, eller välja **[!UICONTROL Choose files]** för att bläddra och välja från din lokala katalog.

![Arbetsflödet för att skapa en begäran med de valda filerna och dra och släpp-gränssnittet för att överföra JSON-filer markerade.](../images/ui/record-delete/upload-json.png)

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
| `value` | Identitetsvärdet som anges av typen. |

När filen har överförts kan du fortsätta [skicka förfrågan](#submit).

### Ange identiteter manuellt {#manual-identity}

Om du vill ange identiteter manuellt väljer du **[!UICONTROL Add identity]**.

![Arbetsflödet för att skapa begäran med [!UICONTROL Add identity] markerat alternativ.](../images/ui/record-delete/add-identity.png)

Det visas kontroller som gör att du kan ange identiteter en åt gången. Under **[!UICONTROL Primary Identity]** använder du listrutan för att välja identitetstyp. Under **[!UICONTROL Identity Value]**, anger det primära identitetsvärdet för posten.

![Arbetsflödet för att skapa en begäran med ett identitetsfält har lagts till manuellt.](../images/ui/record-delete/identity-added.png)

Om du vill lägga till fler identiteter väljer du plusikonen (![En plusikon.](../images/ui/record-delete/plus-icon.png)) bredvid en av raderna eller markera **[!UICONTROL Add identity]**.

![Arbetsflödet för att skapa en begäran med plusikonen och ikonen för att lägga till identitet markerad.](../images/ui/record-delete/more-identities.png)

## Skicka begäran {#submit}

När du är klar med att lägga till identiteter i begäran, under **[!UICONTROL Request settings]**, ange ett namn och en valfri beskrivning för begäran innan du väljer **[!UICONTROL Submit]**.

>[!IMPORTANT]
> 
Det finns olika gränser för det totala antalet unika ID-postborttagningar som kan skickas varje månad. Dessa begränsningar baseras på ditt licensavtal. Organisationer som har köpt alla utgåvor av Adobe Real-time Customer Data Platform och Adobe Journey Optimizer kan skicka in upp till 100 000 identitetspostborttagningar varje månad. Organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield** kan skicka in upp till 600 000 identitetsposter som tas bort varje månad.<br>En enda begäran om radering av en post via användargränssnittet gör att du kan skicka 10 000 ID:n åt gången. The [API-metod för att ta bort poster](../api/workorder.md#create) gör att 100 000 ID kan skickas samtidigt.<br>Det är en god vana att skicka så många ID:n som möjligt per begäran, upp till din ID-gräns. Om du tänker ta bort en stor mängd ID:n bör du inte skicka in en låg volym eller ett enda ID per postborttagningsbegäran.

![Inställningarna för begäran [!UICONTROL Name] och [!UICONTROL Description] fält med [!UICONTROL Submit] markerad.](../images/ui/record-delete/submit.png)

A [!UICONTROL Confirm request] visas för att ange att identiteterna inte kan återställas när de har tagits bort. Välj **[!UICONTROL Submit]** för att bekräfta listan med identiteter vars data du vill ta bort.

![The [!UICONTROL Confirm request] -dialogrutan.](../images/ui/record-delete/confirm-request.png)

När begäran har skickats skapas en arbetsorder och visas på [!UICONTROL Record] -fliken i [!UICONTROL Data Lifecycle] arbetsyta. Härifrån kan du övervaka arbetsorderns status medan den bearbetar begäran.

>[!NOTE]
>
Se översiktsavsnittet i [tidslinjer och genomskinlighet](../home.md#record-delete-transparency) om du vill ha information om hur postborttagningar bearbetas när de har körts.

![The [!UICONTROL Record] -fliken i [!UICONTROL Data Lifecycle] arbetsyta med den nya begäran markerad.](../images/ui/record-delete/request-log.png)

## Nästa steg

I det här dokumentet beskrivs hur du tar bort poster i användargränssnittet för Experience Platform. Mer information om hur du utför andra uppgifter för livscykelhantering i användargränssnittet finns i [Översikt över användargränssnittet för datalängd](./overview.md).

Mer information om hur du tar bort poster med API:t för datahygien finns i [slutpunktsguide för arbetsorder](../api/workorder.md).
