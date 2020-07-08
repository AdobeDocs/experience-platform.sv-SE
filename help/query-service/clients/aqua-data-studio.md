---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anslut till Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Anslut till Aqua Data Studio

Det här dokumentet går igenom stegen för att ansluta Aqua Data Studio med Adobe Experience Platform Query Service.

När du har installerat Aqua Data Studio måste du först registrera servern. På huvudmenyn klickar du på **Server** och sedan på **Register Server**.

![](../images/clients/aqua-data-studio/register-server.png)

Dialogrutan *Registrera server* visas. Under fliken *Allmänt* väljer du **PostgreSQL** i listan till vänster. Ange följande information för serverinställningarna i dialogrutan som visas.

- **Namn**: Namnet på anslutningen.
- **Inloggningsnamn och lösenord**: De inloggningsuppgifter som ska användas. Användarnamnet har formen av `ORG_ID@AdobeOrg`.
- **Värd och port**: Värdslutpunkten och dess port för Query Service.
- **Databas:** Databasen som ska användas.

>[!NOTE]
>
>Mer information om hur du hittar inloggningsuppgifter, värd, port och databasnamn finns på [inloggningssidan på Platform](https://platform.adobe.com/query/configuration). Logga in på Platform, klicka på **Frågor** och klicka sedan på **Autentiseringsuppgifter** för att hitta dina inloggningsuppgifter.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Välj fliken **Drivrutin** . Ange värdet som under *Parametrar*`?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

När du har angett anslutningsinformationen klickar du på **Testa anslutning** för att kontrollera att inloggningsuppgifterna fungerar som de ska. Om anslutningen lyckas klickar du på **Spara** för att registrera servern. Anslutningen visas på *Dashboard* när registreringen är klar, vilket bekräftar att du nu kan ansluta till servern och visa dess schemaobjekt.

## Nästa steg

Nu när du har anslutit till Query Service kan du använda *Query Analyzer* i Aqua Data Studio för att köra och redigera SQL-satser. Mer information om hur du skriver och kör frågor finns i [frågeguiden](../creating-queries/creating-queries.md).