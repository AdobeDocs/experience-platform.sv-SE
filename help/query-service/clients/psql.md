---
keywords: Experience Platform;home;populära topics;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Anslut PSQL till frågetjänst
description: Lär dig hur du ansluter PSQL-klienten till Adobe Experience Platform Query Service, inklusive PostgreSQL-versioner som stöds och installationsanvisningar.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 74f4ac5a3ca4c06e81111ef453ae0effd21b3f16
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Anslut PSQL till frågetjänst

PSQL är ett kommandoradsgränssnitt som installeras tillsammans med PostgreSQL på datorn. Det här dokumentet innehåller stegen för att ansluta PSQL med Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Frågetjänsten stöder endast anslutning med PSQL version 14.x. Versioner tidigare än 14.x (till exempel 10.x till 13.x) och senare (15.x och senare) stöds inte officiellt. Kontrollera att du har installerat en kompatibel klientversion. Se [PostgreSQL End-of-Life Dates](https://endoflife.date/postgresql) för mer information.

Innan du börjar bör du kontrollera att du har tillgång till PSQL och grundläggande kunskaper om hur du använder klienten. Mer information om PSQL finns i den [officiella PSQL-dokumentationen](https://www.postgresql.org/docs/current/app-psql.html).

>[!IMPORTANT]
>
>När du hämtar PostgreSQL måste du välja version 14.x. PostgreSQL-webbplatsen har som standard den senaste versionen, som kanske inte är kompatibel med Query Service.

När PSQL har installerats kan du ansluta den till frågetjänsten. Återgå till Experience Platform-gränssnittet och välj sedan **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]**.

Under avsnittet **[!UICONTROL PSQL Command]** väljer du ikonen **[!UICONTROL Copy to clipboard]** (![Kopiera ikon](/help/images/icons/copy.png)) för att kopiera kommandosträngen.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med kopieringsikonen markerad.](../images/clients/psql/connect-bi.png)

Klistra in kommandosträngen i terminalen och tryck på **Enter** på tangentbordet.

>[!IMPORTANT]
>
>Om du är på en dator använder du en textredigerare för att ta bort radbrytningarna i kommandosträngen och kopierar sedan strängen. Om du använder version 12.0 eller senare måste du lägga till `PGGSSENCMODE=disable` i anslutningssträngen. Den här inställningen inaktiverar GSSAPI-kryptering, som inte behövs för anslutningar till frågetjänsten och som kan orsaka anslutningsfel.<br>Om du använder inloggningsuppgifter som inte förfaller måste du dessutom ersätta lösenordsfältet med det inloggningslösenord som inte förfaller. Läs [handboken för inloggningsuppgifter](../ui/credentials.md) om du vill veta mer om autentiseringsuppgifter som inte upphör att gälla.

Du bör se följande resultat:

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Om du inte ser version 14.x hämtar och installerar du en 14.x-version av PSQL som stöds från [sidan för officiella PostSQL-hämtningar](https://www.postgresql.org/download/).

>[!NOTE]
>
>Följ installationsanvisningarna för ditt operativsystem och verifiera sedan den installerade PSQL-versionen genom att köra `psql --version` i terminalen.

## Nästa steg

Nu när du har anslutit till frågetjänsten kan du använda PSQL för att skriva frågor. Mer information finns i guiden om [att köra frågor](../best-practices/writing-queries.md).
