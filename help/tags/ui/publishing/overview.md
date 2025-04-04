---
title: Översikt över publicering
description: Lär dig hur du publicerar ändringar i kodbibliotek för tagghantering i Adobe Experience Platform.
exl-id: 32eaad87-d7dc-4812-b546-a136511512fe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 7%

---

# Översikt över publicering

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Med Adobe Experience Platform kan du kapsla in ändringar i tagghanteringskoden i enskilda bibliotek. Eftersom flera bibliotek nu kan utvecklas parallellt av olika team måste dessa bibliotek följa en avsiktlig, tillåten process för att sammanfoga ändringar innan de överförs till produktionsmiljön.

På en grundläggande nivå genomgår varje bibliotek följande publiceringsprocess:

1. Skapa ett nytt bibliotek (eller redigera ett befintligt bibliotek) i en utvecklingsmiljö.
1. Testa bibliotekets funktion i en testmiljö där det behövs.
1. Distribuera biblioteket till produktionsmiljön.

Tänk dig en situation där du skapar en ny utcheckningshändelse, skapar ett intäktselement som är relaterat till den händelsen och ändrar Adobe Analytics-tilläggskonfigurationen så att den stöder den nya händelsen och dataelementet. Du kan inkludera alla dessa ändringar i ett nytt bibliotek och använda publiceringsprocessen för att testa, godkänna och publicera dem som en enda enhet.

En översikt på hög nivå över arbetsflödet för bibliotekspublicering, inklusive information om hur bibliotek ärver resurser från uppströmsbyggen beroende på deras publiceringstillstånd, finns i [publiceringsflödesguiden](./publishing-flow.md).

Förutom publiceringsflödet finns det flera komponenter och relationer som är viktiga att förstå för att effektivt kunna utveckla och publicera dina bibliotek. I följande tabell beskrivs dessa nyckelbegrepp och du får länkar till dokumentation som hjälper dig att lära dig mer om dem:

| Komponent | Beskrivning |
| --- | --- |
| Bibliotek | Ett bibliotek är en uppsättning instruktioner för hur tillägg, dataelement och regler ska samverka med varandra och med din webbplats. När ett bibliotek kompileras för att distribueras till en miljö blir det biblioteket ett bygge.<br><br>Mer information om hur du skapar, hanterar och aktiverar bibliotek i användargränssnittet finns i översikten för [bibliotek](./libraries.md). |
| Bygger | Ett bygge är ett kompilerat bibliotek. När det distribueras i en miljö innehåller ett bygge den faktiska uppsättningen filer som innehåller koden som skickas till varje användares webbläsare när de visar din plats.<br><br>Mer information om byggens innehåll och format finns i översikten för [byggen](./builds.md). |
| Miljöer | En taggmiljö är en uppsättning driftsättningsanvisningar som talar om för Experience Platform vilket format du vill att ditt bygge ska ha och var du vill att det ska levereras.<br><br>Mer information om olika typer av miljöer, hur du installerar och konfigurerar befintliga miljöer och hur du skapar nya miljöer finns i översikten för [miljöer](./environments.md). |
| Värdar | En värd representerar anslutningsinformationen för en miljö som ska leverera en bygge till din webbplats. Du kan välja att låta Adobe hantera värdtjänsten för ditt bygge eller så kan du ange information för dina egna värdservrar i stället.<br><br>Se översikten på [värdar](./hosts/hosts-overview.md) för mer information om alla värdalternativ. |
| Kod på klientsidan | Koden på klientsidan är den uppsättning skript som du placerar i källkoden för platsen eller programmet och som anger för varje klientenhet var bygget ska hämtas. Koden är kopplad till en miljö och kan ändras när du ändrar din miljökonfiguration.<br><br>Mer information finns i avsnittet [Bädda in koder](./environments.md#embed-code) i miljööversikten. |

## Nästa steg

Det här dokumentet innehåller en översikt över de olika komponenter som ingår i publiceringen av taggbibliotek i Adobe Experience Platform. Mer information om publiceringsprocessen finns i dokumentationen som är länkad till i den här guiden.
