---
title: Fältbaserade arbetsflöden i Schemaredigeraren (beta)
description: Lär dig hur du lägger till fält från befintliga fältgrupper individuellt i XDM-scheman (Experience Data Model).
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: b7c6f37d3e6d824465713647b624473cff188378
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# Fältbaserade arbetsflöden i Schemaredigeraren (beta)

>[!IMPORTANT]
>
>De arbetsflöden som beskrivs i det här dokumentet är för närvarande betaversioner. Funktionen och dokumentationen kan komma att ändras.

Adobe Experience Platform tillhandahåller en robust uppsättning standardiserade [fältgrupper](../schema/composition.md#field-group) som kan användas i XDM-scheman (Experience Data Model). Strukturen och semantiken bakom dessa fältgrupper är noga anpassade för att uppfylla ett stort antal användningsfall för segmentering och andra applikationer längre fram i kedjan av plattformar. Du kan också definiera egna fältgrupper för att tillgodose unika affärsbehov.

När du lägger till en fältgrupp i ett schema, ärver schemat alla fält i gruppen. Du kan nu lägga till enskilda fält i schemat utan att behöva ta med andra fält från den associerade fältgruppen som du kanske inte använder.

Den här guiden beskriver olika metoder för att lägga till enskilda fält i ett schema i plattformsgränssnittet.

## Förutsättningar

I den här självstudien förutsätts att du är bekant med [kompositionen för XDM-scheman](../schema/composition.md) och hur du använder Schemaredigeraren i plattformsgränssnittet. Om du vill följa med i utvecklingen bör du påbörja processen med [att skapa ett nytt schema](./resources/schemas.md) och tilldela det till en standardklass innan du fortsätter med den här guiden.

## Ta bort fält som lagts till från standardfältgrupper

När du har lagt till en standardfältgrupp i ett schema kan du ta bort alla standardfält som du inte behöver.

>[!NOTE]
>
>Om du tar bort fält från en standardfältgrupp påverkas endast schemat som du arbetar med och inte själva fältgruppen. Om du tar bort standardfält i ett schema är dessa fält fortfarande tillgängliga i alla andra scheman som använder samma fältgrupp.

I följande exempel har standardfältgruppen **[!UICONTROL Demographic Details]** lagts till i ett schema. Om du vill ta bort ett enskilt fält, till exempel `taxId`, markerar du fältet på arbetsytan och väljer sedan **[!UICONTROL Remove]** i den högra listen.

![Ta bort ett fält](../images/ui/field-based-workflows/remove-single-field.png)

Om det finns flera fält som du vill ta bort kan du hantera fältgruppen som helhet. Markera ett fält som tillhör gruppen på arbetsytan och välj sedan **[!UICONTROL Manage related fields]** i den högra listen.

![Hantera relaterade fält](../images/ui/field-based-workflows/manage-related-fields.png)

En dialogruta visas med strukturen för fältgruppen i fråga. Härifrån kan du använda de angivna kryssrutorna för att markera eller avmarkera de fält som du behöver. När du är nöjd väljer du **[!UICONTROL Add fields]**.

![Välj fält från fältgrupp](../images/ui/field-based-workflows/select-fields.png)

Arbetsytan visas igen med endast de markerade fälten i schemastrukturen.

![Fält har lagts till](../images/ui/field-based-workflows/fields-added.png)

## Lägga till standardfält direkt i ett schema

Du kan lägga till fält från standardfältgrupper direkt i ett schema utan att först behöva känna till deras motsvarande fältgrupp. Om du vill lägga till ett standardfält i ett schema väljer du plusikonen (**+**) bredvid schemats namn på arbetsytan. En **[!UICONTROL Untitled Field]**-platshållare visas i schemastrukturen och den högra uppdateringen av rälen för att visa kontroller för att konfigurera fältet.

![Platshållare för fält](../images/ui/field-based-workflows/root-custom-field.png)

Under **[!UICONTROL Field name]** börjar du skriva namnet på fältet som du vill lägga till. Systemet söker automatiskt efter standardfält som matchar frågan och listar dem under **[!UICONTROL Recommended Standard Fields]**, inklusive de fältgrupper som de tillhör.

![Rekommenderade standardfält](../images/ui/field-based-workflows/standard-field-search.png)

Vissa standardfält har samma namn, men strukturen kan variera beroende på vilken fältgrupp de kommer ifrån. Om ett standardfält är kapslat i ett överordnat objekt i fältgruppsstrukturen, kommer det överordnade fältet också att inkluderas i schemat om det underordnade fältet läggs till.

Välj förhandsvisningsikonen (![Förhandsgranskningsikonen](../images/ui/field-based-workflows/preview-icon.png)) bredvid ett standardfält för att visa strukturen i fältgruppen och förstå hur den kan kapslas. Om du vill lägga till standardfältet i schemat väljer du plusikonen (![plusikonen](../images/ui/field-based-workflows/add-icon.png)).

![Lägg till standardfält](../images/ui/field-based-workflows/add-standard-field.png)

Arbetsytan uppdateras för att visa det standardfält som lagts till i schemat, inklusive alla överordnade fält som är kapslade i fältgruppsstrukturen. Namnet på fältgruppen visas också under **[!UICONTROL Field groups]** i den vänstra listen. Om du vill lägga till fler fält från samma fältgrupp väljer du **[!UICONTROL Manage related fields]** i den högra listen.

![Standardfältet har lagts till](../images/ui/field-based-workflows/standard-field-added.png)

## Lägga till anpassade fält direkt i ett schema

Om du tidigare har [skapat anpassade fältgrupper](./resources/field-groups.md#create) kan du lägga till anpassade fält direkt i schemat utan att behöva lägga till dem separat i en anpassad fältgrupp i förväg.

>[!WARNING]
>
>När du lägger till ett anpassat fält i ett schema måste du fortfarande markera en befintlig anpassad fältgrupp som det ska kopplas till. Det innebär att om du vill lägga till anpassade fält direkt i ett schema måste du ha minst en anpassad fältgrupp som har definierats tidigare i sandlådan som du arbetar i. Alla andra scheman som använder den anpassade fältgruppen ärver dessutom det nya fältet när du har sparat ändringarna.

Om du vill lägga till fält på rotnivån för ett schema, markerar du plusikonen (**+**) bredvid schemats namn på arbetsytan. En **[!UICONTROL Untitled Field]**-platshållare visas i schemastrukturen och den högra uppdateringen av rälen för att visa kontroller för att konfigurera fältet.

![Anpassat rotfält](../images/ui/field-based-workflows/root-custom-field.png)

Börja skriva in namnet på det anpassade fält som du vill lägga till så börjar systemet automatiskt att söka efter matchande standardfält. Om du vill skapa ett nytt anpassat fält i stället, markerar du det översta alternativet som lagts till med **([!UICONTROL New Field])**.

![Nytt fält](../images/ui/field-based-workflows/custom-field-search.png)

Här anger du ett visningsnamn och en datatyp för fältet. Under **[!UICONTROL Assign field group]** väljer du den anpassade fältgrupp som du vill att det nya fältet ska associeras med.

![Välj fältgrupp](../images/ui/field-based-workflows/select-field-group.png)

När du är klar väljer du **[!UICONTROL Apply]**.

![Använd fält](../images/ui/field-based-workflows/apply-field.png)

Det nya fältet läggs till på arbetsytan och namnges under ditt [klient-ID](../api/getting-started.md#know-your-tenant_id) för att undvika konflikter med standardfält för XDM. Fältgruppen som du kopplade det nya fältet till visas också under **[!UICONTROL Field groups]** i den vänstra listen.

![Klient-ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Resten av fälten i den valda anpassade fältgruppen tas som standard bort från schemat. Om du vill lägga till några av dessa fält i schemat markerar du ett fält som tillhör gruppen och väljer sedan **[!UICONTROL Manage related fields]** i den högra listen.

### Lägga till anpassade fält i strukturen för standardfältgrupper

Om schemat du arbetar med har ett objekttypsfält från en standardfältgrupp, kan du lägga till egna anpassade fält till det standardobjektet. Markera plusikonen (**+**) bredvid roten för objektet och ange information om det anpassade fältet i den högra listen.

![Lägg till fält i standardobjekt](../images/ui/field-based-workflows/add-field-to-standard-object.png)

När du har gjort ändringarna visas det nya fältet under ditt innehavar-ID-namnutrymme i standardobjektet. Det här kapslade namnutrymmet förhindrar konflikter mellan fält och namn inom själva fältgruppen för att undvika att bryta ändringar i andra scheman som använder samma fältgrupp.

## Nästa steg

I den här guiden beskrivs de nya fältbaserade arbetsflödena för Schemaredigeraren i plattformsgränssnittet. Mer information om att hantera scheman i användargränssnittet finns i [användargränssnittsöversikt](./overview.md).
