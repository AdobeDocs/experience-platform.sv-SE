---
title: Fältbaserade arbetsflöden i Schemaredigeraren
description: Lär dig hur du lägger till fält från befintliga fältgrupper individuellt i XDM-scheman (Experience Data Model).
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: 19e0a26958ec57ccbc614be53b5aaacce7ce9450
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---

# Fältbaserade arbetsflöden i Schemaredigeraren

Adobe Experience Platform har en robust uppsättning standardiserade [fältgrupper](../schema/composition.md#field-group) för användning i XDM-scheman (Experience Data Model). Strukturen och semantiken bakom dessa fältgrupper är noga anpassade för att uppfylla ett stort antal användningsfall för segmentering och andra applikationer längre fram i kedjan av plattformar. Du kan också definiera egna fältgrupper för att tillgodose unika affärsbehov.

När du lägger till en fältgrupp i ett schema, ärver schemat alla fält i gruppen. Du kan nu lägga till enskilda fält i schemat utan att behöva ta med andra fält från den associerade fältgruppen som du kanske inte använder.

Den här guiden beskriver olika metoder för att lägga till enskilda fält i ett schema i plattformsgränssnittet.

## Förutsättningar

I den här självstudiekursen förutsätts det att du känner till [XDM-schemats sammansättning](../schema/composition.md) och hur du använder schemaredigeraren i plattformsgränssnittet. För att följa med i utvecklingen bör du påbörja [skapa ett nytt schema](./resources/schemas.md) och tilldela den till en standardklass innan du fortsätter med den här guiden.

## Ta bort fält som lagts till från standardfältgrupper {#remove-field-group}

När du har lagt till en standardfältgrupp i ett schema kan du ta bort alla standardfält som du inte behöver.

>[!NOTE]
>
>Om du tar bort fält från en standardfältgrupp påverkas endast schemat som du arbetar med och inte själva fältgruppen. Om du tar bort standardfält i ett schema är dessa fält fortfarande tillgängliga i alla andra scheman som använder samma fältgrupp.

I följande exempel är standardfältgruppen **[!UICONTROL Demographic Details]** har lagts till i ett schema. Ta bort ett enskilt fält som `maritalStatus`markerar du fältet på arbetsytan och väljer **[!UICONTROL Remove]** i rätt spår.

![Schemaredigeraren med fältgruppen, fältet Marital status och Ta bort markerat.](../images/ui/field-based-workflows/remove-single-field.png)

Om det finns flera fält som du vill ta bort kan du hantera fältgruppen som helhet. Markera ett fält som tillhör gruppen på arbetsytan och välj sedan **[!UICONTROL Manage related fields]** i rätt spår.

![Schemaredigeraren med ett fält och Hantera relaterade fält markerade.](../images/ui/field-based-workflows/manage-related-fields.png)

En dialogruta visas med strukturen för fältgruppen i fråga. Härifrån kan du använda de angivna kryssrutorna för att markera eller avmarkera de fält som du behöver. När du är nöjd väljer du **[!UICONTROL Confirm]**.

![Dialogrutan Hantera relaterade fält med fältgruppsdiagrammet och Bekräfta markerat.](../images/ui/field-based-workflows/select-fields.png)

Arbetsytan visas igen med endast de markerade fälten i schemastrukturen.

![Schemaredigeraren med den nyligen redigerade fältgruppen markerad.](../images/ui/field-based-workflows/fields-added.png)

## Lägga till standardfält direkt i ett schema

Du kan lägga till fält från standardfältgrupper direkt i ett schema utan att först behöva känna till deras motsvarande fältgrupp. Om du vill lägga till ett standardfält i ett schema väljer du plustecknet (**+**) bredvid schemats namn på arbetsytan. An **[!UICONTROL Untitled Field]** platshållaren visas i schemastrukturen och uppdaterar den högra listen för att visa kontroller för att konfigurera fältet.

![Schemaredigeraren med en platshållare för rotfält markerad.](../images/ui/field-based-workflows/root-custom-field.png)

Under **[!UICONTROL Field name]** börjar du skriva namnet på det fält som du vill lägga till. Systemet söker automatiskt efter standardfält som matchar frågan och listar dem under **[!UICONTROL Recommended Standard Fields]**, inklusive de fältgrupper som de tillhör.

![Fältnamnet är markerat och en lista över rekommenderade standardfält visas i fältegenskaperna i Schemaredigeraren.](../images/ui/field-based-workflows/standard-field-search.png)

Vissa standardfält har samma namn, men strukturen kan variera beroende på vilken fältgrupp de kommer ifrån. Om ett standardfält är kapslat i ett överordnat objekt i fältgruppsstrukturen, kommer det överordnade fältet också att inkluderas i schemat om det underordnade fältet läggs till.

Välj förhandsvisningsikonen (![Ikonen Förhandsgranska](../images/ui/field-based-workflows/preview-icon.png)) bredvid ett standardfält för att visa strukturen för dess fältgrupp och bättre förstå hur den kan kapslas. Om du vill lägga till standardfältet i schemat väljer du plusikonen (![Plustecken](../images/ui/field-based-workflows/add-icon.png)).

![Ikonen Lägg till är markerad för ett objekt i de föreslagna standardfälten.](../images/ui/field-based-workflows/add-standard-field.png)

Arbetsytan uppdateras för att visa det standardfält som lagts till i schemat, inklusive alla överordnade fält som är kapslade i fältgruppsstrukturen. Namnet på fältgruppen visas också under **[!UICONTROL Field groups]** till vänster. Om du vill lägga till fler fält från samma fältgrupp väljer du **[!UICONTROL Manage related fields]** i rätt spår.

![Schemaredigeraren med fältgruppen, standardfältet och Hantera relaterade fält markerade.](../images/ui/field-based-workflows/standard-field-added.png)

## Lägga till anpassade fält direkt i ett schema

På samma sätt som arbetsflödet för standardfält kan du även lägga till egna anpassade fält direkt i ett schema.

Om du vill lägga till fält på rotnivån för ett schema väljer du plustecknet (**+**) bredvid schemats namn på arbetsytan. An **[!UICONTROL Untitled Field]** platshållaren visas i schemastrukturen och uppdaterar den högra listen för att visa kontroller för att konfigurera fältet.

![Schemaredigeraren med ikonen Lägg till och ett namnlöst rotnivåfält markerat.](../images/ui/field-based-workflows/root-custom-field.png)

Börja skriva in namnet på det fält som du vill lägga till så börjar systemet automatiskt att söka efter matchande standardfält. Om du vill skapa ett nytt anpassat fält i stället väljer du det översta alternativet som bifogas med **([!UICONTROL New Field])**.

![Fältnamnet och förslaget till nytt fält är markerade i fältegenskaperna i schemaredigeraren.](../images/ui/field-based-workflows/custom-field-search.png)

Här anger du ett visningsnamn och en datatyp för fältet. Under **[!UICONTROL Assign field group]** måste du välja en fältgrupp för det nya fältet som ska kopplas. Börja skriva in namnet på fältgruppen och om du tidigare har [skapade anpassade fältgrupper](./resources/field-groups.md#create) visas i listrutan. Du kan också skriva ett unikt namn i fältet för att skapa en ny fältgrupp i stället.

![Fältegenskapsinställningarna Visningsnamn, Typ och Tilldela till är markerade i Schemaredigeraren.](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Om du väljer en befintlig anpassad fältgrupp kommer alla andra scheman som använder den fältgruppen också att ärva det nya fältet när du har sparat ändringarna. Därför bör du bara markera en befintlig fältgrupp om du vill använda den här typen av spridning. Annars bör du välja att skapa en ny anpassad fältgrupp i stället.

När du är klar väljer du **[!UICONTROL Apply]**.

![Använd är markerat i fältegenskaperna i Schemaredigeraren.](../images/ui/field-based-workflows/apply-field.png)

Det nya fältet läggs till på arbetsytan och får ett namn under [klient-ID](../api/getting-started.md#know-your-tenant_id) för att undvika konflikter med XDM-standardfält. Fältgruppen som du har associerat det nya fältet med visas också under **[!UICONTROL Field groups]** till vänster.

![Schemaredigeraren med det nya fältet tillagt på arbetsytan och namngivet under ditt klient-ID. Fältgruppen och fältet markeras.](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Resten av fälten i den valda anpassade fältgruppen tas som standard bort från schemat. Om du vill lägga till några av dessa fält i schemat markerar du ett fält som tillhör gruppen och väljer sedan **[!UICONTROL Manage related fields]** i rätt spår.

### Lägga till anpassade fält i strukturen för standardfältgrupper

Om schemat du arbetar med har ett objekttypsfält från en standardfältgrupp, kan du lägga till egna anpassade fält till det standardobjektet. Markera plustecknet (**+**) bredvid objektets rot.

>[!IMPORTANT]
>
>Alla fält som läggs till i en fältgrupp i ett schema visas också i alla andra scheman som använder samma fältgrupp.

![Schemaredigeraren med plusikonen bredvid ett standardobjekt markerat.](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Se [Skapa och redigera scheman i gränssnittsguiden](./resources/schemas.md#custom-fields-for-standard-groups) om du vill ha mer information om hur du lägger till anpassade fält.

## Nästa steg

I den här guiden beskrivs de nya fältbaserade arbetsflödena för Schemaredigeraren i plattformsgränssnittet. Mer information om hur du hanterar scheman i användargränssnittet finns i [Översikt över användargränssnittet](./overview.md).
