---
keywords: Experience Platform;hem;populära ämnen;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Anslut PSQL till frågetjänst
description: PSQL är ett kommandoradsgränssnitt som medföljer när du installerar PostgreSQL på datorn. Du kan installera det genom att följa dessa anvisningar.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Anslut PSQL till frågetjänst

PSQL är ett kommandoradsgränssnitt som installeras när du installerar [!DNL PostgreSQL] på din dator. Det här dokumentet innehåller stegen för att ansluta PSQL med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL PSQL] och känner till hur den används. Mer information om [!DNL PSQL] finns i [officiell [!DNL PSQL] dokumentation](https://www.postgresql.org/docs/current/app-psql.html).

När du har installerat PSQL på datorn kan du ansluta PSQL med frågetjänsten. Återgå till [!DNL Platform] Gränssnitt, välj sedan **[!UICONTROL Queries]**, följt av **[!UICONTROL Credentials]**.

Under **[!UICONTROL PSQL Command]** väljer du **[!UICONTROL Copy to clipboard]** ikon (![Kopiera ikon](../images/clients/psql/copy-icon.png)) för att kopiera kommandosträngen.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med kopieringsikonen markerad.](../images/clients/psql/connect-bi.png)

Klistra in kommandosträngen i ett terminal- eller kommandoradsfönster och tryck på **Retur** på tangentbordet.

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
