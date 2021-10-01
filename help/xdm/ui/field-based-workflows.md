---
title: Fältbaserade arbetsflöden i Schemaredigeraren
description: Lär dig hur du lägger till standardfält från Adobe-definierade fältgrupper i XDM-scheman (Experience Data Model) separat.
hide: true
hidefromtoc: true
source-git-commit: 8947fbb815f3eda97fb218be6791cb67e6e66719
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Fältbaserade arbetsflöden i Schemaredigeraren

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

## Lägga till anpassade fält direkt i ett schema

Om du tidigare har [skapat anpassade fältgrupper](./resources/field-groups.md#create) kan du lägga till anpassade fält direkt i schemat utan att behöva lägga till dem separat i en anpassad fältgrupp i förväg.

>[!WARNING]
>
>När du lägger till ett anpassat fält i ett schema måste du fortfarande markera en befintlig anpassad fältgrupp som det ska kopplas till. Det innebär att om du vill lägga till anpassade fält direkt i ett schema måste du ha minst en anpassad fältgrupp som har definierats tidigare i sandlådan som du arbetar i. Alla andra scheman som använder den anpassade fältgruppen ärver dessutom det nya fältet när du har sparat ändringarna.

Om du vill lägga till fält på rotnivån för ett schema, markerar du plusikonen (**+**) bredvid schemats namn på arbetsytan. En **[!UICONTROL Untitled Field]**-platshållare visas i schemastrukturen och den högra uppdateringen av rälen för att visa kontroller för att konfigurera fältet.

![Anpassat rotfält](../images/ui/field-based-workflows/root-custom-field.png)

Använd kontrollerna i den högra listen för att ange namn, visningsnamn och datatyp för fältet. Under **[!UICONTROL Assign field group]** väljer du den anpassade fältgrupp som du vill att det nya fältet ska associeras med.

![Välj fältgrupp](../images/ui/field-based-workflows/select-field-group.png)

När du är klar väljer du **[!UICONTROL Apply]**.

![Använd fält](../images/ui/field-based-workflows/apply-field.png)

Det nya fältet läggs till på arbetsytan och namnges under ditt [klient-ID](../api/getting-started.md#know-your-tenant_id) för att undvika konflikter med standardfält för XDM. Fältgruppen som du kopplade det nya fältet till visas också under **[!UICONTROL Field groups]** i den vänstra listen.

![Klient-ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Resten av fälten i den valda anpassade fältgruppen tas som standard bort från schemat. Om du vill lägga till några av dessa fält i schemat markerar du ett fält som tillhör gruppen och väljer sedan **[!UICONTROL Manage related fields]** i den högra listen.

### Lägga till fält i strukturen för standardfältgrupper

Om schemat du arbetar med har ett objekttypsfält från en standardfältgrupp, kan du lägga till egna anpassade fält till det standardobjektet. Markera plusikonen (**+**) bredvid roten för objektet och ange information om det anpassade fältet i den högra listen.

![Lägg till fält i standardobjekt](../images/ui/field-based-workflows/add-field-to-standard-object.png)

När du har gjort ändringarna visas det nya fältet under ditt innehavar-ID-namnutrymme i standardobjektet. Det här kapslade namnutrymmet förhindrar konflikter mellan fält och namn inom själva fältgruppen för att undvika att bryta ändringar i andra scheman som använder samma fältgrupp.

## Nästa steg

I den här guiden beskrivs de nya fältbaserade arbetsflödena för Schemaredigeraren i plattformsgränssnittet. Mer information om att hantera scheman i användargränssnittet finns i [användargränssnittsöversikt](./overview.md).
