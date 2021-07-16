---
title: Översikt över publicering
description: Lär dig hur du publicerar ändringar i kodbibliotek för tagghantering i Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Översikt över publicering

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Med Adobe Experience Platform kan du kapsla in ändringar i tagghanteringskoden i enskilda bibliotek. Eftersom flera bibliotek nu kan utvecklas parallellt av olika team måste dessa bibliotek följa en avsiktlig, tillåten process för att sammanfoga ändringar innan de överförs till produktionsmiljön.

På en grundläggande nivå genomgår varje bibliotek följande publiceringsprocess:

1. Skapa ett nytt bibliotek (eller redigera ett befintligt bibliotek) i en utvecklingsmiljö.
1. Testa bibliotekets funktion i en testmiljö där det behövs.
1. Distribuera biblioteket till produktionsmiljön.

Tänk dig en situation där du skapar en ny utcheckningshändelse, skapar ett intäktselement som är relaterat till den händelsen och ändrar Adobe Analytics-tilläggskonfigurationen så att den stöder den nya händelsen och dataelementet. Du kan inkludera alla dessa ändringar i ett nytt bibliotek och använda publiceringsprocessen för att testa, godkänna och publicera dem som en enda enhet.

En översikt över arbetsflödet för bibliotekspublicering, inklusive information om hur bibliotek ärver resurser från uppströmsbyggen beroende på deras publiceringstillstånd, finns i [publiceringsflödesguiden](./publishing-flow.md).

Förutom publiceringsflödet finns det flera komponenter och relationer som är viktiga att förstå för att effektivt kunna utveckla och publicera dina bibliotek. I följande tabell beskrivs dessa nyckelbegrepp och du får länkar till dokumentation som hjälper dig att lära dig mer om dem:

| Komponent | Beskrivning |
| --- | --- |
| Bibliotek | Ett bibliotek är en uppsättning instruktioner för hur tillägg, dataelement och regler ska samverka med varandra och med din webbplats. När ett bibliotek kompileras för att distribueras till en miljö blir det biblioteket ett bygge.<br><br>Se översikten över  [](./libraries.md) bibliotek för mer information om hur du skapar, hanterar och aktiverar bibliotek i användargränssnittet. |
| Bygger | Ett bygge är ett kompilerat bibliotek. När det distribueras i en miljö innehåller ett bygge den faktiska uppsättningen filer som innehåller koden som skickas till varje användares webbläsare när de visar din plats.<br><br>Mer information om byggens innehåll och format finns i översikten  [](./builds.md) över byggen. |
| Miljöer | En taggmiljö är en uppsättning driftsättningsanvisningar som anger vilket format du vill att ditt bygge ska ha och var du vill att det ska levereras.<br><br>Mer information om olika typer av miljöer, hur du installerar och konfigurerar befintliga miljöer och hur du skapar nya miljöer finns i översikten över  [](./environments.md) miljöer. |
| Värdar | En värd representerar anslutningsinformationen för en miljö som ska leverera en bygge till din webbplats. Du kan välja att låta Adobe hantera värdtjänsten för ditt bygge eller så kan du ange information för dina egna värdservrar i stället.<br><br>Se översikten på  [](./hosts/hosts-overview.md) värdtjänster för mer information om varje värdalternativ. |
| Kod på klientsidan | Koden på klientsidan är den uppsättning skript som du placerar i källkoden för platsen eller programmet och som anger för varje klientenhet var bygget ska hämtas. Koden är kopplad till en miljö och kan ändras när du ändrar din miljökonfiguration.<br><br>Mer information finns i avsnittet om  [att bädda in ](./environments.md#embed-code) kod i miljööversikten. |

## Nästa steg

Det här dokumentet innehåller en översikt över de olika komponenter som ingår i publiceringen av taggbibliotek i Adobe Experience Platform. Mer information om publiceringsprocessen finns i dokumentationen som är länkad till i den här guiden.
