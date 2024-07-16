---
title: Användarbehörigheter för taggar
description: Lär dig mer om de olika typerna av behörigheter som är tillgängliga för taggar och några grundläggande implementeringsstrategier för olika affärsanvändningsfall.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Användarbehörigheter för taggar

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Användarbehörigheter för taggar i Adobe Experience Platform tilldelas användare via Adobe Admin Console. I stället för att tilldelas enskilda användare, konfigureras olika behörighetsgrupper separat som produktprofiler. Användarna tilldelas sedan till dessa produktprofiler för att få de behörigheter de har konfigurerats för.

Den här guiden ger en översikt över de olika typerna av behörigheter som är tillgängliga för taggar, de funktioner de ger åtkomst till och vissa grundläggande implementeringsstrategier för olika affärsanvändningsfall.

>[!NOTE]
>
>Anvisningar om hur du konfigurerar behörigheter för användare som använder Admin Console finns i självstudiekursen [Hantera behörigheter för datainsamling](../../../collection/permissions.md).

## Behörighetstyper

Inom en produktprofil är behörigheter för taggar indelade i fyra kategorier:

1. Plattformar
1. Egenskaper
1. Egendomsrättigheter
1. Företagsrättigheter

### Plattformar

Varje taggegenskap har en plattform. Det finns för närvarande två plattformar som du kan använda för taggar: Webb och Mobil. Du kan använda den här behörighetstypen för att begränsa eller bevilja åtkomst till en viss typ av egenskap. Detta kan vara användbart när det team som hanterar dina mobilappar skiljer sig från det som hanterar dina webbplatser.

### Egenskaper

Som standard ger produktprofiler åtkomst till alla egenskaper som finns på företaget, både nu och i framtiden. Med den här behörighetstypen kan du begränsa eller bevilja åtkomst till specifika befintliga egenskaper efter namn.

### Egendomsrättigheter {#property-rights}

Alla taggegenskaper som du skapar i användargränssnittet blir tillgängliga i Admin Console, vilket gör att du kan gruppera egenskapen med specifika egenskapsbehörigheter i samma produktprofil.

Om till exempel en viss produktprofil inte har tillgång till egenskap A1 kan användare som tillhör den profilen inte se eller ändra några inställningar i egenskap A1.

Om en användare tillhör en profil som har åtkomst till egenskap A1, bestäms de åtgärder de kan utföra i egenskap A1 av de rättigheter de har beviljats från den här profilen. Om en användare har behörighet för egenskap A1 men saknar tilldelad behörighet, har de skrivskyddad åtkomst för den egenskapen.

I följande tabell visas de tillgängliga egenskapsrättigheterna och de funktioner som de ger åtkomst till:

| Egendomsrättighet | Beskrivning |
| --- | --- |
| **Framkalla** | Detta gör att du kan utföra följande åtgärder:<ul><li>Skapa regler och dataelement</li><li>Skapa bibliotek och bygg dem i befintliga utvecklingsmiljöer</li><li>Skicka ett bibliotek för godkännande</li></ul>De flesta rutinuppgifter i gränssnittet kräver det här. |
| **Godkänn** | På så sätt kan du ta ett skickat bibliotek och bygga vidare till testmiljön. Du kan också godkänna ett bibliotek för publicering när testningen är klar. |
| **Publish** | På så sätt kan du publicera godkända bibliotek i produktionsmiljön. |
| **Hantera tillägg** | Detta gör att du kan utföra följande åtgärder: <ul><li>Installera nya tillägg för en egenskap</li><li>Ändra konfigurationen för ett redan installerat tillägg</li><li>Ta bort ett tillägg</li></ul>I översiktsdokumentationen för tillägg finns [mer information om tillägg](../managing-resources/extensions/overview.md). Den här rollen tillhör vanligen IT eller marknadsföring, beroende på din organisation. |
| **Hantera miljöer** | På så sätt kan du skapa och ändra miljöer. Mer information finns i [miljödokumentationen](../publishing/environments.md). Den här rollen tillhör vanligtvis IT-gruppen. |

{style="table-layout:auto"}

### Företagsrättigheter

Företagsrättigheter gäller för behörigheter som sträcker sig över flera egenskaper.  Dessa beskrivs i tabellen nedan:

| Företagsrätt | Beskrivning |
| --- | --- |
| **Hantera egenskaper** | Detta gör att du kan utföra följande åtgärder:<ul><li>Skapa nya egenskaper</li><li>Ändra metadata och inställningar på egenskapsnivå</li><li>Ta bort egenskaper</li></ul>Administratörer utför vanligtvis den här rollen. Mer information finns i [egenskapsdokumentationen](companies-and-properties.md). |
| **Utveckla tillägg** | Ger möjlighet att skapa och ändra tilläggspaket som ägs av företaget, inklusive privata releaser och förfrågningar om allmän spridning. |
| **Hantera appkonfigurationer** | Detta gäller endast om du har en licens för Adobe Journey Optimizer eller en annan lösning som ger åtkomst till mobilmeddelanden i appen och push-meddelanden.  På så sätt kan du hantera de appar som Experience Cloud känner till tillsammans med de push-autentiseringsuppgifter som krävs för att kommunicera med meddelandetjänsten i Firebase Cloud och Apple push-meddelandetjänst. |

{style="table-layout:auto"}

## Totalt antal användarbehörigheter

En enskild användares totala behörigheter bestäms av det totala medlemskapet i olika produktprofiler. Om en användare tillhör flera produktprofiler läggs behörigheterna för varje profil ihop i stället för att multipliceras.

Produktprofil A ger dig till exempel rätten att utveckla för egenskap 1. Produktprofil B ger dig Publish rätt att använda Property 2. I det här fallet kan du Utveckla i Egenskap 1 och Publish i Egenskap 2, men du kan inte publicera i Egenskap 1 eller Utveckla i Egenskap 2 eftersom du inte har fått behörighet att göra det explicit.

## Rättigheter och scenarier

Olika företag har olika behov när de skapar nya produktprofiler. Dessa behov varierar beroende på företagets storlek, organisationsstruktur, antalet webbplatser, antalet personer som deltar i hanteringen av taggar osv.

Nedan beskrivs några vanliga scenarier och en rekommenderad utgångspunkt när du tänker på att skapa produktprofiler och lägga till användare till dem.

### Enpersonsprogram

Om du kör ett litet företag som har en person som ansvarar för allt, ger du den här användaren behörighet för alla egenskaper och tilldelar dem alla rättigheter som anges ovan.

### Avgränsning av tullar

Tänk på en situation där många personer i organisationen är inblandade i taggning. Du har en uppsättning personer (till exempel en extern konsult) som skapar regler och dataelement, men du vill inte att de ska ha tillgång till produktionsmiljön. I det här fallet vill du se till att ingen driftsätter till Production förutom IT-teamet.

Så här gör du:

1. Skapa ett konto för dina konsulter och ge dem endast rättighet att utveckla.
1. Konsulten bygger och testar inom de gränser ni anger.
1. Om konsulten vill ha en ny förlängning eller är redo att publicera, utför en representant från organisationen (med rätt behörighet) dessa åtgärder.

### Enterprise

Ett företagsföretag kan ha flera platser uppdelade geografiskt, med olika team som ansvarar för varje region. Inom dessa team utvecklar och publicerar olika individer.

Detta liknar&quot;åtskillnad av tullar&quot; ovan, men är organiserat i geografiska områden. Du kan till exempel skapa en&quot;Framkalla&quot;-profil och en&quot;Publish&quot;-profil för Nordamerika och skapa separata&quot;Framkalla&quot;- och&quot;Publish&quot;-grupper för Europa.

## Exempel på roller

Följande tabell innehåller några exempel på vilka typer av roller du kan ha i organisationen och vilka behörigheter du bör tilldela dem:

| Roll | Beskrivning | Egenskaper | Egendomsrättigheter | Företagsrättigheter |
| --- | --- | --- | --- | --- |
| Hanteraren | vill se vad som händer i systemet, men ska inte kunna göra några ändringar. | Ta med automatiskt | (Ingen) | (Ingen) |
| Marknadsföraren | Kan installera tillägg och ställa in nya taggar för befintliga egenskaper, men kan inte publicera till staging- eller produktionsmiljöerna. | Ta med automatiskt | <ul><li>Utveckla</li><li>Hantera tillägg</li></ul> | <ul><li>Hantera egenskaper</li></ul> |
| Mobilappsutvecklaren | Ansvarar för implementering av Adobe och tredjepartslösningar inuti en inbyggd mobilapp. | Ta med automatiskt | <ul><li>Utveckla</li><li>Hantera tillägg</li></ul> | <li>Hantera egenskaper</li><li>Hantera appkonfigurationer</li> |
| IT-teamet | Ändrar inga taggar, men de har full kontroll över miljöer för staging och produktion och vad som finns i dem. | Ta med automatiskt | (Ingen) | <ul><li>Godkänn</li><li>Publish</li><li>Hantera miljöer</li></ul> |
| Extension Developer | Utvecklar tillägg och kan skicka för godkännande, men kan inte publicera eller lägga till dem i befintliga egenskaper. | Ta med automatiskt | <ul><li>Utveckla</li></ul> | <ul><li>Hantera egenskaper</li><li>Utveckla tillägg</li></ul> |
| Den superanvändare | Gör allt. | Ta med automatiskt | <ul><li>Utveckla</li><li>Godkänn</li><li>Publish</li><li>Hantera tillägg</li><li>Hantera miljöer</li></ul> | <ul><li>Hantera egenskaper</li></ul> |

{style="table-layout:auto"}

## Nästa steg

Det här dokumentet innehåller en översikt över de tillgängliga behörigheterna för taggar i Experience Platform. Anvisningar om hur du konfigurerar produktprofiler för taggar i Adobe Admin Console finns i guiden [Hantera användarbehörigheter för datainsamling](../../../collection/permissions.md).
