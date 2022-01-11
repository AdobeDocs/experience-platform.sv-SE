---
keywords: Experience Platform;hem;populära ämnen;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Anslut PSQL till frågetjänst
topic-legacy: connect
description: PSQL är ett kommandoradsgränssnitt som medföljer när du installerar PostgreSQL på datorn. Du kan installera det genom att följa dessa anvisningar.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 06d3a8aa6f2f73c2d5392a76fb5b36b18691cf0d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

---

# Anslut PSQL till frågetjänst

PSQL är ett kommandoradsgränssnitt som installeras när du installerar [!DNL PostgreSQL] på din dator. Det här dokumentet innehåller stegen för att ansluta PSQL med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL PSQL] och känner till hur den används. Mer information om [!DNL PSQL] finns i [officiell [!DNL PSQL] dokumentation](https://www.postgresql.org/docs/current/app-psql.html).

När du har installerat PSQL på datorn kan du ansluta PSQL med frågetjänsten. Återgå till [!DNL Platform] Gränssnitt, välj sedan **[!UICONTROL Queries]**, följt av **[!UICONTROL Credentials]**.

![Bild](../images/clients/psql/connect-bi.png)

Markera ikonen om du vill kopiera avsnittet med etiketten **[!UICONTROL PSQL Command]** klistrar du sedan in kommandosträngen i ett terminal- eller kommandoradsfönster innan du trycker på Retur.

>[!IMPORTANT]
>
>Om du är på en dator använder du en textredigerare för att ta bort radbrytningarna i kommandosträngen och kopierar sedan strängen. Om du använder version 12.0 eller senare måste du lägga till `PGGSSENCMODE=disable` till anslutningssträngen. Om du använder inloggningsuppgifter som inte förfaller måste du dessutom ersätta lösenordsfältet med det inloggningslösenord som inte förfaller. Om du vill veta mer om autentiseringsuppgifter som inte upphör att gälla läser du [inloggningsguide](../ui/credentials.md).

Du bör se följande resultat:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Om du inte ser minst version 10.5 måste du ladda ned den versionen eller senare.

## Nästa steg

Nu när du är ansluten till [!DNL Query Service]kan du använda PSQL för att skriva frågor. Mer information om hur du skriver och kör frågor finns i guiden [köra frågor](../best-practices/writing-queries.md).
