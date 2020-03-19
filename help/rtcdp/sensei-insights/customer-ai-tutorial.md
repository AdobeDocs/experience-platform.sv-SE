---
title: Förutse kundernas benägenhetspoäng med hjälp av kundens AI (alfa)
seo-title: Förutse kundernas benägenhetspoäng med hjälp av kundens AI (alfa)
description: I den här självstudiekursen finns anvisningar om hur du använder AI för kunder (alfa)
seo-description: I den här självstudiekursen finns anvisningar om hur du använder AI för kunder (alfa)
index: false
translation-type: tm+mt
source-git-commit: 1118983ce8f5704ef3a347c8c316a9cc5cc62815

---


# Förutse kundernas benägenhetspoäng med hjälp av kundens AI (alfa)

>[!NOTE]
>Kundens AI-funktionalitet som beskrivs i det här dokumentet är alfavärden. Dokumentationen och funktionaliteten kan komma att ändras.

Med kundens AI i Adobe Experience Platform, som har skapats och drivs av Adobe Sensei, kan ni generera anpassade benägenhetspoäng utan att behöva bekymra er om maskininlärningsaspekterna.

I den här självstudiekursen beskrivs stegen för hur du arbetar med AI för kunder med användargränssnittet i Experience Platform. Steg finns för följande ämnen:

* [Konfigurera en instans](#configure-an-instance)
* [Skapa kundsegment med förutbestämda poäng](#create-customer-segments-with-predicted-scores)

## Komma igång

Den här guiden kräver en fungerande förståelse av de olika plattformstjänster som används för att använda kundens AI. Läs följande dokument innan du börjar den här självstudiekursen:

* [Översikt över kundprofiler i realtid](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)
* [Översikt över segmenteringstjänsten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)
* [Användarhandbok för Segment Builder](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segment-builder-guide.md)

## Konfigurera en instans

Experience Platform ger kunden AI som en enkel att använda Adobe Sensei-tjänst som kan konfigureras för olika användningsfall. I följande avsnitt beskrivs hur du konfigurerar en instans av Kundens AI.

### Konfigurera din instans

Klicka på **Tjänster** i den vänstra navigeringen i plattformsgränssnittet. Webbläsaren **Services** visas och visar alla tillgängliga tjänster. Klicka på **Öppna** i behållaren för kundens AI.

![](./images/service.png)

På *kundens AI* -skärm visas alla befintliga AI-instanser för kunder. Klicka på **Skapa instans**.

![](./images/customer_ai.png)

Arbetsflödet för att skapa instanser visas med början i *steget Konfigurera* .

Nedan finns viktig information om värden som du måste ge instansen:

* Instansens namn kommer att användas på alla platser där kundens AI-poäng visas. Namnen bör därför beskriva vad förutsägelsepoängen representerar, till exempel&quot;Sannolikhet för att avbryta tidskriftsprenumeration&quot;.

* Propensitetstypen bestämmer poängsättets och den metriska polaritetens avsikt. Du kan antingen välja **Churn** eller **Conversion**.

* Datakällan refererar till den indatamängd som kommer att användas för att förutsäga bakgrundsmusik. Kunds-AI använder per design data om kundupplevelsehändelser för att beräkna benägenhetspoängen. När du väljer en datauppsättning i listruteväljaren visas bara de som är kompatibla med kundens AI.

* Som standard genereras benägenhetspoäng för alla profiler såvida inte en stödberättigad population anges. Du kan ange en berättigad population genom att definiera villkor för att inkludera eller exkludera profiler baserat på händelser.

Ange önskade värden och klicka sedan på **Nästa**.

![](./images/setup.png)

### Definiera ett mål

Steget *Definiera mål* visas och innehåller en interaktiv miljö där du kan definiera ett mål visuellt. Ett mål består av en eller flera händelser, där varje händelses förekomst baseras på det villkor den innehåller. Målet för en kundens AI-instans är att fastställa sannolikheten för att uppnå dess mål inom en viss tidsram.

Klicka på **Ange fältnamn** och välj ett fält i listrutan. Klicka på den andra inmatningen och välj en sats för händelsens villkor och ange sedan ett målvärde för att slutföra händelsen. Ytterligare händelser kan konfigureras genom att klicka på **Lägg till händelse**. Slutför målet genom att tillämpa en tidsram för förutsägelse i antal dagar och klicka sedan på **Nästa**.

![](./images/goal.png)

### Konfigurera ett schema *(valfritt)*

Det *avancerade* steget visas. Med det här valfria steget kan du konfigurera ett schema för att automatisera prediktionskörningar, definiera undantag för förutsägelser för att filtrera vissa händelser eller klicka på **Slutför** om inget behövs.

Konfigurera ett poängschema genom att konfigurera *poängfrekvensen*. Automatiserade prognoskörningar kan schemaläggas att köras antingen varje vecka eller varje månad.

![](./images/schedule.png)

Under schemakonfigurationen kan du definiera undantag för förutsägelse för att förhindra händelser som uppfyller vissa villkor från att utvärderas när du genererar poäng. Den här funktionen kan användas för att filtrera bort irrelevanta dataindata.

Om du vill utesluta vissa händelser klickar du på **Lägg till undantag** och definierar händelsen på samma sätt som målet definieras. Om du vill ta bort ett undantag klickar du på ellipserna (**..**) längst upp till höger i händelsebehållaren och sedan på **Ta bort behållare**.

![](./images/exclusion.png)

Uteslut händelser efter behov och klicka sedan på **Slutför** för att skapa instansen.

![](./images/advanced.png)

Om instansen skapas utan fel kommer en förutsägelsekörning att omedelbart aktiveras och efterföljande körs enligt ditt definierade schema.

>   **Obs!** Beroende på storleken på indata kan det ta upp till 24 timmar att slutföra förutsägelser.

Genom att följa det här avsnittet har du konfigurerat en instans av Kundens AI och en förutsägelsekörning utfördes. När körningen är klar kommer poängsatta insikter automatiskt att utrusta profiler med förutbestämda poäng. Vänta 24 timmar innan du fortsätter till nästa avsnitt i den här självstudiekursen.

## Skapa kundsegment med förutbestämda poäng

När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment som bygger på benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget. En mer robust självstudiekurs om hur du skapar segment finns i användarhandboken för [Segment Builder](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segment-builder-guide.md).

Klicka på **Segment** i den vänstra navigeringen i plattformsgränssnittet och klicka sedan på **Skapa segment**.

![](./images/segments.png)

Segmentbyggaren ** visas. Klicka på mappen *XDM Individual Profile* i den vänstra kolumnen *Fält* och under fliken **Attribut** och klicka sedan på mappen med organisationens namnområde. Mappen med namnet **Customer AI** innehåller resultatet av prediktionskörningar och namnges efter den instans poängen tillhör. Klicka och öppna resultatet av den önskade instansen.

![](./images/results.png)

Placerad i mitten av Segment Builder, dra och släpp attributet **Score** på *regelbyggarens arbetsyta* för att definiera en regel.

Under den högra kolumnen *Segmentegenskaper* väljer du en *sammanfogningsprincip* och anger ett namn för segmentet. Skapa sedan segmentet genom att klicka på **Spara** .

![](./images/properties.png)

## Nästa steg

Genom att följa den här självstudiekursen har du konfigurerat en instans av kundens AI, genererat benägenhetspoäng och skapat ett segment som genomdrivits av benägenhetspoängen med hjälp av Segment Builder. Ditt kundsegment kan nu användas av aktiverade destinationer för att nå era målgrupper. Mer information finns i Översikt över [](../destinations/destinations-overview.md) Destinationer.
