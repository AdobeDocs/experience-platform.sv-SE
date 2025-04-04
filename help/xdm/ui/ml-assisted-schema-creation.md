---
title: Skapa inlärningsassisterat schema
description: Lär dig hur du skapar scheman i Experience Platform användargränssnitt.
badgeBeta: label="Beta" type="Informative"
exl-id: 6b14caed-a3ad-4834-8fa8-8d67dce6290e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---

# Skapa scheman med hjälp av maskininlärning

>[!AVAILABILITY]
>
>* Maskinininlärningsassisterade scheman är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

Använd ML-algoritmer för att generera ett schema från exempeldata. Den här processen sparar tid och ökar noggrannheten när struktur, fält och datatyper definieras för stora komplexa datauppsättningar.

Med generering av ML-schema kan du snabbt integrera nya datakällor och minska antalet misstag från manuell generering. Icke-tekniska användare kan använda den för att generera scheman eller hantera stora och komplexa datauppsättningar utan extra ansträngning. Den här hjälpen snabbar upp processen från att hämta data till att få insikter, vilket gör det enklare att kombinera nya datakällor och utföra dataanalys.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av kraven för att skapa scheman. Innan du fortsätter med den här guiden bör du läsa [gränssnittsguiden för att skapa och redigera scheman](./resources/schemas.md).

I den här guiden beskrivs hur du skapar scheman med hjälp av HTML-algoritmer (maskininlärning) för att generera ett schema från exempeldata. Mer information om hur du skapar scheman finns i den [manuella arbetsflödesguiden](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas#add-field-groups) för att skapa scheman, eller i dokumentet om [fältbaserade arbetsflöden i Schemaredigeraren](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/field-based-workflows).

>[!NOTE]
>
>Du kan också skapa ett schema med API:t [!DNL Schema Registry]. Om du vill skapa ett schema manuellt med API:t läser du först [[!DNL Schema Registry] utvecklarhandboken](../api/getting-started.md) innan du provar självstudiekursen om hur du [skapar ett schema med API:t](../tutorials/create-schema-api.md).

## Navigera till arbetsflödet Skapa schema {#navigate-to-schema-creation-workflow}

Välj arbetsytan **[!UICONTROL Schemas]** i den vänstra navigeringen i Experience Platform-gränssnittet. Arbetsytan **[!UICONTROL Schemas]** visas. Välj **[!UICONTROL Create schema]** om du vill lägga till ett nytt schema för att starta ett arbetsflöde för att skapa schema.

![Arbetsytan Scheman med schemat i den vänstra navigeringen och Skapa schema är markerade.](../images/ui/ml-schema-creation/schemas-workspace-create-schema.png)

## Skapa ett schema {#create-a-schema}

Dialogrutan [!UICONTROL Create a schema] visas. Välj alternativet **[ML-assisterad]** för att skapa schema följt av **[!UICONTROL Select]** för att bekräfta ditt val.

![Dialogrutan [!UICONTROL Create a schema] med [!UICONTROL ML- Assisted] markerad.](../images/ui/ml-schema-creation/use-sample-csv.png)

### Välj en basklass {#select-base-class}

Arbetsflödet [!UICONTROL Create schema] visas. Välj en basklass för ditt schema följt av **[!UICONTROL Next]**.

![Arbetsytan Schemainformation med en klass och nästa markerad.](../images/ui/ml-schema-creation/select-base-class.png)

### Överföra en CSV-fil {#upload-csv}

**[!UICONTROL Select data]**-steget i arbetsflödet för att skapa visas. I avsnittet **[!UICONTROL Upload files]** väljer du **[!UICONTROL Choose files]** eller avsnittet **[!UICONTROL Drag and Drop files]**. Välj en CSV-fil på datorn för att generera ett schema.

![Dataseriet Välj i arbetsflödet Skapa schema med avsnittet Överför filer markerat.](../images/ui/ml-schema-creation/upload-files.png)

### Förhandsgranska data {#preview-data}

I avsnittet [!UICONTROL Upload file] visas namnet på CSV-filen som du importerade och i avsnittet **[!UICONTROL Preview]** visas rader med exempeldata från filen som du överförde. Välj **[!UICONTROL Next]** om du vill fortsätta med arbetsflödet.

![Rader med exempeldata markerade i förhandsvisningsavsnittet och Nästa markerade.](../images/ui/ml-schema-creation/preview-data.png)

### Granska och redigera schema {#review-schema}

**[!UICONTROL Review and edit]**-steget i arbetsflödet för att skapa visas och maskininlärningsassistenten **[!UICONTROL Schema recommendation]** visas i en tabellägd vy. I det här skedet kan du redigera, lägga till eller ta bort fält från det rekommenderade schema som genererats av maskininlärningsmodellen. Tabellen innehåller följande fält:

| Fältnamn | Beskrivning |
|------------------|---------------------------------------------------------|
| [!UICONTROL Data table] | Den datauppsättning eller databas som fältet kommer från. |
| [!UICONTROL Source Field] | Det ursprungliga fältnamnet från källsystemet. |
| [!UICONTROL Target Field] | Fältnamnet i målsystemet där data ska mappas. |
| [!UICONTROL Display Name] | Namnet som används för att visa fältet i användargränssnittet. Namnet ska vara mer användarvänligt eller beskrivande. |
| [!UICONTROL Data Type] | Den typ av data som lagras i fältet (till exempel `String`, `Date`). |
| [!UICONTROL Field Group] | En kategorisering av fältet baserat på dess användning eller kontext (till exempel [!UICONTROL Demographic Details], [!UICONTROL Commerce Details]). |

![Gransknings- och redigeringsfasen i arbetsflödet för att skapa schema.](../images/ui/ml-schema-creation/schema-recommendation.png)

#### Lägg till ett fält {#add-field}

Om du vill lägga till ett fält i schemat väljer du **[!UICONTROL Add new field]**.

![Gransknings- och redigeringsfasen i arbetsflödet för schemaskapande med Lägg till nytt fält markerat.](../images/ui/ml-schema-creation/add-new-field.png)

Dialogrutan [!UICONTROL Select field] visas. Dialogrutan innehåller ett diagram över schemat så som det finns. Markera det önskade fältet och välj **[Välj]** för att lägga till ett nytt fält i schemat. Välj **[Avbryt]** om du vill stänga dialogrutan vid behov.

![Dialogrutan Välj fält med ett fält markerat och Markera markerat.](../images/ui/ml-schema-creation/select-field-dialog.png)

En ny rad visas i det rekommenderade schemat. Nu kan du redigera fältet.

#### Redigera ett fält {#edit-field}

Om du vill redigera ett fält väljer du pennikonen för raden som du vill redigera. En informationspanel visas till höger där du kan redigera den anpassade fältmappningen. Informationspanelen innehåller [!UICONTROL Target field], [!UICONTROL Display Name], [!UICONTROL Data Type] och [!UICONTROL Field Group]. Gör nödvändiga ändringar och bekräfta genom att välja **[!UICONTROL Apply]**. Välj pennikonen igen för att stänga informationspanelen.

![Gransknings- och redigeringsfasen i arbetsflödet för att skapa scheman med pennikonen och informationspanelen markerad.](../images/ui/ml-schema-creation/edit-field.png)

#### Ta bort ett fält {#remove-field}

Om du vill ta bort ett fält markerar du minusikonen på en rad som du vill ta bort.

>[!CAUTION]
>
>Ingen bekräftelsedialogruta visas när det här objektet tas bort.

![Gransknings- och redigeringsfasen i arbetsflödet där schemat skapas med minusikonen markerad.](../images/ui/ml-schema-creation/remove-field.png)

#### Godkänn det rekommenderade schemat {#approve}

Om du vill godkänna det rekommenderade schemat och fortsätta med arbetsflödet **[!UICONTROL Create schema]** väljer du **[Nästa]**.

![Gransknings- och redigeringsfasen i arbetsflödet där schemat skapas med Nästa markerat.](../images/ui/ml-schema-creation/next.png)

### Namnge och spara schema {#name-and-save}

**[!UICONTROL Name and save]**-steget i arbetsflödet för att skapa visas. Ange ett **[visningsnamn för schema]** och en valfri beskrivning. Avsnittet **[Schema genererat]** innehåller ett diagram över det ML-genererade schemat. Välj **[Slutför]** om du vill slutföra arbetsflödet för att skapa schema.

![Namn- och sparschemasteget i arbetsflödet för schemaskapande med Finish markerat.](../images/ui/ml-schema-creation/name-and-save.png)

### Visa i schemaredigeraren {#view-in-editor}

Schemaredigeraren visas med det schema du nyss skapade på arbetsytan. Välj **[!UICONTROL Save]** om du vill återgå till arbetsytan för [!UICONTROL Schemas].

![Schemaredigeraren visar ditt namngivna ML-genererade schema.](../images/ui/ml-schema-creation/schema-editor.png)

## Nästa steg

När du har skapat schemat kan du använda Schemaredigeraren för att göra ytterligare ändringar, om det behövs. Ditt nya schema är nu klart att integreras med dina datakällor och användas för dataanalys.

Se [Redigera en befintlig schemahandbok](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas#edit) för mer information om hur du använder schemaredigeraren.
