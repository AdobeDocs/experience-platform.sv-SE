---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Anslut till Aqua Data Studio
topic: connect
description: Det här dokumentet går igenom stegen för att ansluta Aqua Data Studio med Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---


# Anslut med [!DNL Aqua Data Studio]

Det här dokumentet går igenom stegen för att ansluta [!DNL Aqua Data Studio] med Adobe Experience Platform [!DNL Query Service].

När du har installerat [!DNL Aqua Data Studio] måste du först registrera servern. På huvudmenyn klickar du på **[!UICONTROL Server]** och sedan på **[!UICONTROL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Dialogrutan **[!UICONTROL Register Server]** visas. Under fliken **[!UICONTROL General]** väljer du **[!UICONTROL PostgreSQL]** i listan till vänster. Ange följande information för serverinställningarna i dialogrutan som visas.

- **[!UICONTROL Name]**: Namnet på anslutningen.
- **[!UICONTROL Login Name and Password]**: De inloggningsuppgifter som ska användas. Användarnamnet har formatet `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host and Port]**: Värdslutpunkten och dess port för  [!DNL Query Service]. Du måste använda port 80 för att ansluta med [!DNL Query Service].
- **[!UICONTROL Database]:** Databasen som ska användas.

>[!NOTE]
>
>Mer information om hur du hittar inloggningsuppgifter, värd, port och databasnamn finns på sidan [inloggningsuppgifter på Platform](https://platform.adobe.com/query/configuration). Om du vill hitta dina autentiseringsuppgifter loggar du in på [!DNL Platform], klickar på **[!UICONTROL Queries]** och sedan på **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Klicka på fliken **[!UICONTROL Driver]**.  Under **[!UICONTROL Parameters]** anger du `?sslmode=require` som värde

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

När du har angett anslutningsinformationen klickar du på **[!UICONTROL Test Connection]** för att kontrollera att inloggningsuppgifterna fungerar som de ska. Om anslutningen lyckas klickar du på **[!UICONTROL Save]** för att registrera servern. Anslutningen visas på **instrumentpanelen** när registreringen är klar, vilket bekräftar att du nu kan ansluta till servern och visa dess schemaobjekt.

## Nästa steg

Nu när du har anslutit till [!DNL Query Service] kan du använda **[!UICONTROL Query Analyzer]** i [!DNL Aqua Data Studio] för att köra och redigera SQL-satser. Mer information om hur du skriver och kör frågor finns i [frågeguiden](../best-practices/writing-queries.md) som körs.