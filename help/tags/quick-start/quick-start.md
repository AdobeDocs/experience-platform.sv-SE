---
title: Quickstart Guide
description: Lär dig hur du snabbt kommer igång med taggar i Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---

# Snabbstartguide

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Taggar är Adobe Experience Platform nästa generation av tagghanteringsteknik. Den är uppbyggd från grunden för att stödja ett öppet och hållbart ekosystem där alla kan bygga egna integreringar som Adobe-kunder kan driftsätta på sina webbplatser. Det är ett API-program först, så allt du kan göra via användargränssnittet kan du också göra programmatiskt via ett API.

Grundläggande arbetsflöde för taggar:

1. Konfigurera grupper och användare.
2. Logga in.
3. Skapa en egenskap.
4. Installera tillägg.
5. Skapa dataelement och regler.
6. Testa i utvecklingsmiljön.
7. Marknadsför till produktion.

## 1. Konfigurera grupper och användare

Taggar är helt integrerade med din Adobe ID. Användarbehörigheter hanteras via Admin Console med andra Adobe-produkter och lösningar från [!DNL Creative Cloud], [!DNL Document Cloud]och Experience Cloud.

Taggar har ett rättighetsbaserat användarhanteringssystem. Detta innebär att individuella rättigheter måste beviljas uttryckligen. Dessa rättigheter tilldelas grupper och sedan läggs användarna till i rätt grupper för att få åtkomst. Även om din organisation har tillgång till datainsamling kan enskilda användare inte göra något förrän en administratör uttryckligen ger dem vissa rättigheter.

Detaljerade instruktioner om hur du skapar grupper och lägger till användare för taggar finns i [behörighetsguide för datainsamling](../../collection/permissions.md).

## 2. Logga in

När taggrättigheter har lagts till i Adobe ID måste du logga in i användargränssnittet för Experience Platform eller datainsamlingen. Du kan göra detta genom att navigera direkt till [Experience Cloud inloggningsskärm](https://experience.adobe.com/)och välja antingen **[!UICONTROL Data Collection]** eller **[!UICONTROL Experience Platform]**.

>[!NOTE]
>
>Om du har ett enda konto med behörighet för flera organisationer kan du ändra organisationen genom att välja organisationens namn i kontrollfältet högst upp på skärmen och välja en annan organisation i listrutan.

## 3. Skapa en egenskap

När du har loggat in i användargränssnittet är det första du behöver göra att skapa en egenskap. En egenskap är i princip en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen. Många människor skapar en egenskap för varje webbplats (eller grupp med närbesläktade webbplatser) där de vill distribuera samma uppsättning taggar.

Mer information om hur du skapar egenskaper finns i [Skapa en egenskap](../ui/administration/companies-and-properties.md).

## 4. Installera tillägg

Ett tillägg är en integrering som byggts av Adobe eller en Adobe-partner som lägger till nya och oändliga alternativ för taggarna som du kan distribuera till dina webbplatser. Om du tänker på en tagg som ett operativsystem är tillägg de program som du installerar för att göra det du behöver.

Alla nya egenskaper levereras med [Kärntillägg](../extensions/web/core/overview.md) installerade. Mobila egenskaper har ytterligare tillägg. Core-tillägget har byggts av Adobe för att ge en robust standarduppsättning med dataelementtyper för datalagret och händelsetyperna för dina regler. De flesta åtgärder du vill utföra (skaffa ett ECID, skicka [!DNL Adobe Analytics] beacons, ladda [!DNL Target] global mbox osv) kommer från tillägg som du installerar från katalogen.

Det som gör taggar i Platform verkligt unika är att dessa tillägg kan byggas av vem som helst. Behöver ni släppa en Facebook-pixel för återmarknadsföring på er webbplats? Ta en titt på det tillägg som Facebook har byggt. Vill du ha samma sak för Twitter eller Linked In? Använd dessa tillägg. Behöver du göra en undersökning? Titta på Query Pro eller Foresee. Behöver ni hantera sekretess och samtycke från era slutanvändare för att få hjälp med [!DNL GDPR]? Ta en titt på Evidon och Trust Arc. Vill du se detaljerad information om hur enskilda användare på din webbplats beter sig? Ta en titt på Clicktale. Mer information finns i avsnittet om [lägga till ett nytt tillägg](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Skapa dataelement och regler

**Dataelement** är pekare till den information som du vill samla in och skicka till olika platser på sidan:

* Ett definierat datalager i JSON
* DOM-element
* Cookies
* Session och lokal lagring
* Nästan allt annat

När dataelementet har definierats kan du använda elementet var som helst i användargränssnittet för alla tillägg. Läs dokumentationen om [Dataelement](../ui/managing-resources/data-elements.md) för mer detaljerad information.

**Regler** är den logiska kärnan i implementeringen och styr vad, när, var och hur av alla taggar på din webbplats ska vara. Definiera en händelse, ange villkor och undantag och definiera sedan åtgärderna och ordningen. Publicera ändringarna för att se resultatet. Mer information finns i [Regler](../ui/managing-resources/rules.md).

## 6. Testa i utvecklingsmiljön

### Bibliotek och byggen

Taggbyggen publiceras aldrig automatiskt. Varje uppsättning ändringar du gör är inkapslad i en [bibliotek](../ui/publishing/libraries.md). Varje bibliotek du skapar ärver automatiskt allt som är uppströms (publicerat, godkänt eller skickat) som en baslinje, så allt du behöver göra är att definiera de ändringar du vill göra. Det här biblioteket fungerar som en plan för en [bygga](../ui/publishing/builds.md). Ett bygge är den faktiska uppsättningen JavaScript-filer som distribueras och används.

Det är viktigt att förstå relationen mellan din webbsida, din värdplats och taggar.

1. Värdservern tillhandahåller en plats där du kan publicera bygget. Själva bygget innehåller de JavaScript-filer som krävs för biblioteket.

   Varje miljö har en relation med en värd, och värden tillhandahåller en slutpunkt som anger var bygget ska levereras. Värden kan bara tillhöra en egenskap, men en egenskap kan ha många värdar.

2. En inbäddningskod anges i formuläret  `<script>` -taggen som `<head>` -avsnitt på din webbplats HTML.

   När du skapar en miljö och bifogar en värd genererar miljön automatiskt en unik inbäddningskod som gör att du kan integrera dess tilldelade bygge på din plats. The `<script>` koden används för att distribuera biblioteksbygget vid körning.

3. När en användare bläddrar på webbplatsen är det inbäddningskoden `<script>` taggen hämtar bygget från värdservern och utför de definierade åtgärderna i webbläsaren.

### Värdar

En värd är en anslutning mellan en taggegenskap och din värdplats. Taggar har för närvarande stöd för antingen Adobe-hanterad värdtjänst via en [!DNL Akamai] värddator eller värdtjänst via en SFTP-värd. När du skapar ett bygge ansluter taggar till servern som definieras av värden och levererar bygget.

Om du är värd för en tagg kan den skickas direkt till dina servrar via SFTP eller så kan du skicka den till [!DNL Akamai] och ladda ned den med hjälp av systemens arkivalternativ.

Mer information finns i [Värdar](../ui/publishing/hosts/hosts-overview.md).

### Miljöer

Varje bibliotek skapas i en miljö. En miljö definierar hur du vill att ditt bygge ska se ut när det publiceras. Du kan ange:

* **Värd:** Varje miljö behöver en värd som bestämmer vilken slutpunkt som eventuella byggen som skapas i den här miljön ska skickas till.
* **Arkiv:** Standardinställningen är att distribuera bygget som en minifierad .js-fil. Om du använder anpassad kod kan det finnas flera filer som refererar till varandra. Dessa kan kombineras till en zip-fil och krypteras.

När du har sparat miljön genereras den inbäddade koden som du kan kopiera och klistra in på webbplatsen. Observera att inbäddningskoden inte fungerar förrän du har skapat ett bibliotek och skapat ett bygge. Mer information finns i [Miljö](../ui/publishing/environments.md).

### Publicera en version till Dev

Publiceringsprocessen beskrivs i stegen nedan.

1. Skapa en värd.
1. Skapa en dev-miljö med den värddator du skapade.
1. Distribuera inbäddningskoden från utvecklingsmiljön till din dev-testwebbplats.
1. Skapa ett bibliotek och tilldela det till den utvecklingsmiljö du skapade.
1. Bygg upp ditt bibliotek.

## 7. Befordra till produktion

När du har testat ditt bygge i utvecklingsmiljön måste du skapa din scen- och produktionsmiljö och placera de inbäddade koderna på de platser som behövs. Du kan återanvända befintliga värdar för detta ändamål.

Att främja ett bibliotek hela vägen fram till produktionen kräver vanligtvis samordning mellan olika personer med lämpliga rättigheter.

* En utvecklare (någon med rättigheten Framkalla) skickar biblioteket, vilket flyttar biblioteket till skickat läge.
* En godkännare (någon med behörigheten Godkänn) kan skapa biblioteket till scenmiljön och godkänna det efter testning. Detta flyttar biblioteket till godkänt läge. Endast ett bibliotek kan skickas och godkännas åt gången.
* En utgivare (någon med behörigheten Publicera) kan skapa biblioteket i produktionsmiljön.

Du kan tilldela alla dessa rättigheter till en person.

Mer information om olika lägen och alternativ som är tillgängliga under publiceringsprocessen finns i [Arbetsflöde för godkännande](../ui/publishing/publishing-flow.md).

## Ytterligare resurser

Mer information om taggar finns i följande resurser:

* **[Samlingsforum för datainsamling](https://forums.adobe.com/community/experience-cloud/platform/launch)**: Ställ och besvara frågor, lämna idéer, rösta på andras idéer. Logga in med din Adobe ID.
* **[Utvecklardokument](https://developer.adobelaunch.com/)**: Delta i tagghanterarens community för att bygga tillägg eller använda tagg-API:er
* **[Översikt över Tutorials](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html)**: I dessa dokument introduceras taggar som vidarebefordran av händelser och Mobile SDK i Android-appar.
