---
keywords: Experience Platform;hem;populära ämnen;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Anslut PSQL till frågetjänst
topic: connect
description: 'PSQL är ett kommandoradsgränssnitt som medföljer när du installerar PostgreSQL på datorn. Du kan installera det genom att följa dessa anvisningar. '
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---


# Anslut PSQL till frågetjänst

PSQL är ett kommandoradsgränssnitt som installeras när du installerar [!DNL PostgreSQL] på datorn. Det här dokumentet innehåller stegen för att ansluta PSQL med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL PSQL] och är bekant med hur du använder den. Mer information om [!DNL PSQL] finns i [officiell [!DNL PSQL]-dokumentation](https://www.postgresql.org/docs/current/app-psql.html.

När du har installerat PSQL på datorn kan du ansluta PSQL med frågetjänsten. Återgå till användargränssnittet för [!DNL Platform] och välj sedan **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]**.

![Bild](../images/clients/psql/connect-bi.png)

Markera ikonen om du vill kopiera avsnittet **[!UICONTROL PSQL Command]** och klistra sedan in kommandosträngen i ett terminal- eller kommandoradsfönster innan du trycker på Retur.

>[!IMPORTANT]
>
>Om du är på en dator använder du en textredigerare för att ta bort radbrytningarna i kommandosträngen och kopierar sedan strängen. Om du använder version 12.0 eller senare måste du lägga till `PGGSSENCMODE=disable` i anslutningssträngen.

Du bör se följande resultat:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Om du inte ser minst version 10.5 måste du ladda ned den versionen eller senare.

## Nästa steg

Nu när du är ansluten till [!DNL Query Service] kan du använda PSQL för att skriva frågor. Mer information om hur du skriver och kör frågor finns i guiden [kör frågor](../best-practices/writing-queries.md).