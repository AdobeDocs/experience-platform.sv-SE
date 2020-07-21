---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anslut till Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# Anslut med [!DNL Aqua Data Studio]

Det här dokumentet går igenom stegen för att ansluta [!DNL Aqua Data Studio] till Adobe Experience Platform [!DNL Query Service].

Efter installationen [!DNL Aqua Data Studio]måste du först registrera servern. Klicka på huvudmenyn **[!UICONTROL Server]** och sedan på **[!UICONTROL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Dialogrutan *[!UICONTROL Register Server]* visas. Under *[!UICONTROL General]* fliken väljer du **[!UICONTROL PostgreSQL]** i listan till vänster. Ange följande information för serverinställningarna i dialogrutan som visas.

- **[!UICONTROL Name]**: Namnet på anslutningen.
- **[!UICONTROL Login Name and Password]**: De inloggningsuppgifter som ska användas. Användarnamnet har formen av `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host and Port]**: Värdslutpunkten och dess port för [!DNL Query Service].
- **[!UICONTROL Database]:**Databasen som ska användas.

>[!NOTE]
>
>Mer information om hur du hittar inloggningsuppgifter, värd, port och databasnamn finns på [inloggningssidan på Platform](https://platform.adobe.com/query/configuration). Logga in på, [!DNL Platform]klicka **[!UICONTROL Queries]** och klicka sedan på **[!UICONTROL Credentials]** för att hitta dina inloggningsuppgifter.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Klicka på **[!UICONTROL Driver]** fliken. Under *[!UICONTROL Parameters]* anger du värdet som `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

När du har angett anslutningsinformationen klickar du på **[!UICONTROL Test Connection]** för att kontrollera att inloggningsuppgifterna fungerar som de ska. Om anslutningen lyckas klickar du på **[!UICONTROL Save]** för att registrera servern. Anslutningen visas på *Dashboard* när registreringen är klar, vilket bekräftar att du nu kan ansluta till servern och visa dess schemaobjekt.

## Nästa steg

Nu när du har anslutit till [!DNL Query Service]kan du använda *[!UICONTROL Query Analyzer]* i [!DNL Aqua Data Studio] för att köra och redigera SQL-satser. Mer information om hur du skriver och kör frågor finns i [frågeguiden](../creating-queries/creating-queries.md).