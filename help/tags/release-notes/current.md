---
title: Versionsinformation
description: Den senaste versionsinformationen för taggar i Adobe Experience Platform.
source-git-commit: f1e6741de9aa00652e9af290a89f73788e0f1d83
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Versionsinformation

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

## 19 juli 2021

**Justeringar av rättigheten**  Hantera egenskaper - rättigheten Hantera egenskaper stötte på ett problem där en användare hade behörighet att skapa en ny egenskap, men inte kunde se den efter att den skapades (vilket beskrivs i communitytråden  [här](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176)). En korrigering är nu aktiv med behörigheter som framtvingas enligt beskrivningen i artikeln.

>[!NOTE]
>
>Om du tilldelar den nya behörigheten Redigera egenskap till en användargrupp uppdateras inte gränssnittet för att aktivera fälten på egenskapskonfigurationsskärmen. En korrigering av problemet kommer att implementeras i en kommande version.

## 17 maj 2021

**Bättre hantering av osparade ändringar**  - Det brukade vara så att du tillfrågades om du ville ignorera ändringarna när du navigerade bort från en inställningsvy (tillägg, dataelement och regelkomponenter). Men logiken för att fastställa det var inte särskilt bra, så större delen av tiden du fick en uppmaning att spara ändringar trots att det inte fanns några.  Det har rättats till.  Från och med nu bör du bara se den uppmaningen när du har gjort ändringar.

## 10 maj 2021

**Förenklad publicering**  - Det behövs inte längre någon byggnad i testmiljön.  Om du har rätt behörighet kan du hoppa över tillståndet Skickat helt och publicera direkt från Development så länge som du har skapat något och det inte finns några andra bibliotek i uppströmmen.

## 22 april 2021

**Datainsamling i Adobe Experience Platform**  - Att skicka data till Adobe handlar inte bara om att distribuera taggar till din webbplats eller konfiguration till din app.  Användning av Experience Platform SDK och Edge Network kräver åtkomst till andra plattformsfunktioner.  Tidigare krävdes det att man loggade in i några olika verktyg, men nu är de tillsammans på ett ställe.

Datainsamling i Platform består av sex funktioner, och din nya smidiga navigering innehåller bara de objekt som ditt företag och ditt användarkonto har tillgång till.  Vissa funktionsnamn har också uppdaterats för att matcha Experience Platform namngivningsmönster.

* Klient (som tidigare användes som klientsida)
* Datastreams (tidigare Edge Configurations)
* Server (tidigare använd som serversida)
* Appkonfigurationer
* Scheman
* Identiteter

Se fram emot fler uppdateringar i takt med att Experience Platform och datainsamlingen utvecklas.

## 18 februari 2021

* Användargränssnittet för datainsamling har uppdaterats för att reagera-spektrum v3
* Uppdaterade tilläggskort till de senaste spektrummönstren
* Ökade storleken på namnfält i hela programmet

## 13 januari 2021

**Allmän tillgänglighet: HändelsevidarebefordringSkicka data på händelsenivå till Adobe Experience Platform Edge Network använder sedan händelsevidarebefordran för att omvandla, förbättra och skicka data till en slutpunkt som inte är Adobe med hjälp av Adobe, inte klienten, med låg latens.** 

Mer information finns i [översikten över vidarebefordran av händelser](../ui/event-forwarding/overview.md) och [guiden](../ui/event-forwarding/getting-started.md) Komma igång.
