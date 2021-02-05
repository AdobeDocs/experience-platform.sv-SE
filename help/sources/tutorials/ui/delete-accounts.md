---
keywords: Experience Platform;hemmabruk;populära ämnen; ta bort konton
description: Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du tar bort konton från arbetsytan Källor.
solution: Experience Platform
title: Ta bort konton för källanslutning i användargränssnittet
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Ta bort källanslutningskonton

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs hur du tar bort konton från arbetsytan **[!UICONTROL Sources]**.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Ta bort konton med användargränssnittet

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa konton och dataflöden med. Varje källa visar antalet befintliga konton och dataflöden som är kopplade till dem.

Välj **[!UICONTROL Accounts]** för att komma åt sidan **[!UICONTROL Accounts]**.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

En lista över befintliga konton visas. På den här sidan finns en lista med sorterbar information för befintliga konton, t.ex. källa, användarnamn, associerade dataflöden och skapat datum. Välj **kanalikonen** i det övre vänstra hörnet om du vill sortera.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Sorteringspanelen visas till vänster på skärmen och innehåller en lista med tillgängliga källor. Du kan välja mer än en källa med sorteringsfunktionen.

Välj den källa som du vill komma åt och leta reda på kontot som du vill ta bort från listan med konton i huvudgränssnittet. I exemplet är den valda källan **[!DNL Azure Blob Storage]** och kontonamnet är **[!UICONTROL blobTestConnector]**. När du väljer flera källor från sorteringspanelen visas dina senast skapade konton först eftersom listan sorteras efter skapad den.

Välj det konto du vill ta bort.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Panelen **[!UICONTROL Properties]** visas till höger på skärmen och innehåller information om det valda kontot.

Markera ellipserna (`...`) bredvid namnet på kontot som du vill ta bort. En popup-panel visas med alternativ för **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** och **[!UICONTROL Delete]**. Välj **[!UICONTROL Delete]** om du vill ta bort kontot.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

En slutgiltig bekräftelsedialogruta visas. Välj **[!UICONTROL Delete]** för att slutföra processen.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Nästa steg

I den här självstudiekursen har du använt arbetsytan **[!UICONTROL Sources]** för att ta bort befintliga konton.

Anvisningar om hur du utför dessa åtgärder programmatiskt med API:t [!DNL Flow Service] finns i självstudiekursen om att [ta bort anslutningar med API:t för Flow Service](../../tutorials/api/delete.md)