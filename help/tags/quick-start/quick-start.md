---
title: Quickstart Guide
description: Lär dig hur du snabbt kommer igång med taggar i Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 3%

---

# Snabbstartguide

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad referens av terminologiändringarna.

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

Taggar är helt integrerade med din Adobe ID. Användarbehörigheter hanteras via Admin Console med andra Adobe-produkter och -lösningar från [!DNL Creative Cloud], [!DNL Document Cloud] och Experience Cloud.

Taggar har ett rättighetsbaserat användarhanteringssystem. Detta innebär att individuella rättigheter måste beviljas uttryckligen. Dessa rättigheter tilldelas grupper och sedan läggs användarna till i rätt grupper för att få åtkomst. Även om din organisation har tillgång till datainsamling kan enskilda användare inte göra något förrän en administratör uttryckligen ger dem vissa rättigheter.

Detaljerade instruktioner om hur du skapar grupper och lägger till användare för taggar finns i [behörighetsguiden för datainsamling](../../collection/permissions.md).

## 2. Logga in

När taggrättigheter har lagts till i din Adobe ID måste du logga in i Experience Platform användargränssnitt eller användargränssnittet för datainsamling. Du kan göra detta genom att navigera direkt till inloggningsskärmen för [Experience Cloud](https://experience.adobe.com/) och välja antingen **[!UICONTROL Data Collection]** eller **[!UICONTROL Experience Platform]**.

>[!NOTE]
>
>Om du har ett enda konto med behörighet för flera organisationer kan du ändra organisationen genom att välja organisationens namn i kontrollfältet högst upp på skärmen och välja en annan organisation i listrutan.

## 3. Skapa en egenskap

När du har loggat in i användargränssnittet är det första du behöver göra att skapa en egenskap. En egenskap är i princip en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen. Många människor skapar en egenskap för varje webbplats (eller grupp med närbesläktade webbplatser) där de vill distribuera samma uppsättning taggar.

Mer information om hur du skapar egenskaper finns i [Skapa en egenskap](../ui/administration/companies-and-properties.md).

## 4. Installera tillägg

Ett tillägg är en integrering som byggts av Adobe eller en Adobe-partner och som lägger till nya och oändliga alternativ för de taggar som du kan distribuera på dina webbplatser. Om du tänker på en tagg som ett operativsystem är tillägg de program som du installerar för att göra det du behöver.

Alla nya egenskaper levereras med [Core-tillägget](../extensions/client/core/overview.md) installerat. Mobila egenskaper har ytterligare tillägg. Tillägget Core byggs av Adobe för att tillhandahålla en robust standarduppsättning med dataelementtyper för datalagret och händelsetyperna för era regler. De flesta åtgärder som du vill utföra (hämta ett ECID, skicka [!DNL Adobe Analytics] beacons, läsa in den globala mbox-filen [!DNL Target] osv) kommer från tillägg som du installerar från katalogen.

Det som gör taggar i Experience Platform verkligt unika är att dessa tillägg kan byggas av alla. Behöver du släppa en Facebook-pixel för återmarknadsföring på din webbplats? Ta en titt på det tillägg som Facebook har byggt. Vill du ha samma sak för Twitter eller Linked In? Använd dessa tillägg. Behöver du göra en undersökning? Titta på Query Pro eller Foresee. Behöver du hantera sekretess och samtycke från dina slutanvändare för att få hjälp med [!DNL GDPR]? Titta på Evidon och Trust Arc. Vill du se detaljerad information om hur enskilda användare på din webbplats beter sig? Ta en titt på Clicktale. Mer information finns i avsnittet om att [lägga till ett nytt tillägg](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Skapa dataelement och regler

**Dataelement** är pekare till den information som du vill samla in och skicka till olika platser på sidan:

* Ett definierat datalager i JSON
* DOM-element
* Cookies
* Session och lokal lagring
* Nästan allt annat

När dataelementet har definierats kan du använda elementet var som helst i användargränssnittet för alla tillägg. Mer information finns i dokumentationen om [dataelement](../ui/managing-resources/data-elements.md).

**Regler** är den logiska kärnan i implementeringen och styr vad, när, var och hur för alla taggar på din webbplats. Definiera en händelse, ange villkor och undantag och definiera sedan åtgärderna och ordningen. Publicera ändringarna för att se resultatet. Mer information finns i [Regler](../ui/managing-resources/rules.md).

## 6. Testa i utvecklingsmiljön.

### Bibliotek och byggen

Taggbyggen publiceras aldrig automatiskt. Varje uppsättning ändringar du gör är inkapslad i ett [bibliotek](../ui/publishing/libraries.md). Varje bibliotek du skapar ärver automatiskt allt som är uppströms (publicerat, godkänt eller skickat) som en baslinje, så allt du behöver göra är att definiera de ändringar du vill göra. Det här biblioteket fungerar som en plan för en [build](../ui/publishing/builds.md). Ett bygge är den faktiska uppsättningen JavaScript-filer som distribueras och används.

Det är viktigt att förstå relationen mellan din webbsida, din värdplats och taggar.

1. Värdservern tillhandahåller en plats där du kan publicera bygget. Bygget innehåller de JavaScript-filer som krävs för biblioteket.

   Varje miljö har en relation med en värd, och värden tillhandahåller en slutpunkt som anger var bygget ska levereras. Värden kan bara tillhöra en egenskap, men en egenskap kan ha många värdar.

2. En inbäddningskod anges i taggen `<script>` som finns i `<head>`-avsnitten på din webbplats HTML.

   När du skapar en miljö och bifogar en värd genererar miljön automatiskt en unik inbäddningskod som gör att du kan integrera dess tilldelade bygge på din plats. Koden `<script>` används för att distribuera biblioteksbygget vid körning.

3. När en användare surfar på din plats hämtar taggen `<script>` koden för inbäddning bygget från värdservern och utför dina definierade åtgärder i webbläsaren.

### Värdar

En värd är en anslutning mellan en taggegenskap och din värdplats. Taggar har för närvarande stöd för antingen Adobe-hanterad värdtjänst via en [!DNL Akamai]-värd eller självvärd via en SFTP-värd. När du skapar ett bygge ansluter taggar till servern som definieras av värden och levererar bygget.

Om du är självvärd kan en tagg genereras direkt till dina servrar via SFTP, eller så kan du överföra den till [!DNL Akamai] och hämta den med hjälp av arkivalternativet i din miljö.

Mer information finns i [Värdar](../ui/publishing/hosts/hosts-overview.md).

### Miljöer

Varje bibliotek skapas i en miljö. En miljö definierar hur du vill att ditt bygge ska se ut när det publiceras. Du kan ange:

* **Värd:** Varje miljö behöver en värd som bestämmer slutpunkten där byggen som skapas i den här miljön ska skickas.
* **Arkiv:** Standardinställningen är att distribuera bygget som en minifierad .js-fil. Om du använder anpassad kod kan det finnas flera filer som refererar till varandra. Dessa kan kombineras till en zip-fil och krypteras.

När du har sparat miljön genereras den inbäddade koden som du kan kopiera och klistra in på webbplatsen. Observera att inbäddningskoden inte fungerar förrän du har skapat ett bibliotek och skapat ett bygge. Mer information finns i [Miljö](../ui/publishing/environments.md).

### Publicera en version till Dev

Publiceringsprocessen beskrivs i stegen nedan.

1. Skapa en värd.
1. Skapa en dev-miljö med den värddator du skapade.
1. Distribuera inbäddningskoden från utvecklingsmiljön till din dev-testwebbplats.
1. Skapa ett bibliotek och tilldela det till den utvecklingsmiljö du skapade.
1. Bygg upp ditt bibliotek.

## 7. Främja produktionen

När du har testat ditt bygge i utvecklingsmiljön måste du skapa din scen- och produktionsmiljö och placera de inbäddade koderna på de platser som behövs. Du kan återanvända befintliga värdar för detta ändamål.

Att främja ett bibliotek hela vägen fram till produktionen kräver vanligtvis samordning mellan olika personer med lämpliga rättigheter.

* En utvecklare (någon med rättigheten Framkalla) skickar biblioteket, vilket flyttar biblioteket till skickat läge.
* En godkännare (någon med behörigheten Godkänn) kan skapa biblioteket till scenmiljön och godkänna det efter testning. Detta flyttar biblioteket till godkänt läge. Endast ett bibliotek kan skickas och godkännas åt gången.
* En utgivare (någon med behörigheten Publicera) kan skapa biblioteket i produktionsmiljön.

Du kan tilldela alla dessa rättigheter till en person.

Mer information om olika lägen och alternativ som är tillgängliga under publiceringsprocessen finns i [Arbetsflöde för godkännande](../ui/publishing/publishing-flow.md).

## Ytterligare resurser

Mer information om taggar finns i följande resurser:

* **[Samhälle för datainsamling](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community)**: Ställ frågor och svar, skicka idéer, rösta på andras idéer. Logga in med din Adobe ID.
* **[Utvecklardokumentation](../api/overview.md)**: Bygg tillägg eller använd tagg-API:er genom att engagera utvecklarcommunityn för taggar
* **[Översikt över självstudiekurser](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html)**: I de här dokumenten introduceras taggar som händelsevidarebefordran och Mobile SDK i Android-appar.
