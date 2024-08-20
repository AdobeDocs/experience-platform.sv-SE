---
keywords: Experience Platform;hem;populära ämnen;identitetstjänst;Identitetstjänst;delade enheter;Delade enheter
title: Översikt över delade enheter (Beta)
description: Delad enhetsidentifiering identifierar olika autentiserade användare av samma enhet, vilket ger en mer korrekt återgivning av kunddata i identitetsdiagram
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---

# Översikt över identifiering av delad enhet (Beta)

>[!IMPORTANT]
>
>Funktionen [!DNL Shared Device Detection] är i betaversion. Dess funktioner och dokumentation kan komma att ändras.

Adobe Experience Platform [!DNL Identity Service] hjälper dig att få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

[!DNL Shared Device] refererar till enheter som används av mer än en individ. Exempel på delade enheter är surfplattor, biblioteksdatorer och kioskdatorer. Genom funktionen [!DNL Shared Device Detection] kan olika användare av samma enhet förhindras från att sammanfogas till en enda identitet, vilket ger en mer korrekt representation av en individ.

Med [!DNL Shared Device Detection] kan du:

* Skapa separata identitetsdiagram för olika användare av samma enhet,
* förhindra att data från olika personer blandas med samma enhet,
* Generera en renare och exaktare bild av era kunder.

>[!TIP]
>
>Konfigurationer för [!DNL Shared Device Detection] måste slutföras innan du aktiverar profil för datauppsättning eftersom du inte längre kan ändra inställningar när diagram har genererats i [!DNL Identity Service].

## Kom igång med [!DNL Shared Device Detection]

Att arbeta med [!DNL Shared Device Detection] kräver förståelse för de olika plattformstjänsterna. Innan du börjar arbeta med [!DNL Shared Device Detection] bör du läsa dokumentationen för följande tjänster:

* [[!DNL Identity Service]](./home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
   * [Identitetsdiagramvisningsprogram](./features/identity-graph-viewer.md): Visa och interagera med identitetsdiagramvisningsprogrammet för att bättre förstå hur kundidentiteter sammanfogas, och på vilka sätt.
   * [Identitetsnamnutrymmen](./features/namespaces.md): Se komponenterna för en fullständigt kvalificerad identitet och hur identitetsnamnutrymmen gör att du kan särskilja kontext och typ för en identitet.

## Förstå [!DNL Shared Device Detection]

Det är viktigt att förstå följande terminologi när du arbetar med
[!DNL Shared Device Detection]. I tabellen nedan finns en lista med termer som är viktiga för att förstå [!DNL Shared Device Detection].

### Terminologi

| Villkor | Definition |
| --- | --- |
| Delad enhet | En delad enhet är en enhet som används av flera personer. Exempel på delade enheter är surfplattor, biblioteksdatorer och kioskdatorer. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] refererar till en konfigurationsinställning som tillåter att data från olika användare av samma enhet separeras från varandra. |
| Namnområde för delad identitet | Namnutrymmet för delad identitet representerar den enhet som kan användas av flera användare. Namnutrymmet för delad identitet är vanligtvis ECID, men kan anges till andra enhets-ID:n. |
| Namnområde för användaridentitet | Namnområdet för användaridentitet representerar den autentiserade (inloggade) användaren av en delad enhet. |
| Senaste autentiserade användare | Den senast autentiserade användaren representerar den användare som senast loggade in på en enhet, om en enhet loggas in med flera konton. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] fungerar genom att etablera två namnutrymmen: namnutrymmet **Shared Identity** och namnområdet **User Identity**.

* Namnutrymmet för delad identitet representerar den enhet som kan användas av flera användare. Adobe rekommenderar att kunderna använder ECID som delad enhetsidentifierare.
* Namnområdet för användaridentitet mappas till det identitetsnamnområde som motsvarar användarens inloggnings-ID, det kan vara användarens CRMID, e-postadress, hashad e-post eller telefonnummer.

En delad enhet, som en surfplatta, har ett **namnområde för delad identitet**. Å andra sidan har varje användare av en delad enhet ett eget angivet **Namnområde för användaridentitet** som motsvarar deras respektive inloggnings-ID. En surfplatta som Kevin och Nora delar för e-handel har till exempel ett eget ECID `1234`, medan Kevin har ett eget namnområde för användaridentitet som mappas till hans `kevin@email.com`-konto och Nora har ett eget namnområde för användaridentitet mappat till sitt `nora@email.com`-konto.

[!DNL Shared Device Detection] kan göra distinktioner mellan flera användare av samma enhet genom att länka det delade ID-namnutrymmet (t.ex. ECID) med den senast autentiserade användarens namnområde för användaridentitet (inloggnings-ID).

### Hur identitetsdata skickas till ett identitetsdiagram

Titta på följande exempel för att få en bättre förståelse för hur [!DNL Shared Device Detection] fungerar:

>[!NOTE]
>
>I det här diagrammet är namnområdet för delad identitet konfigurerat till ECID och namnområdet för användaridentitet är konfigurerat till CRMID.

![diagram](./images/shared-device/diagram.png)

* Kevin och Nora delar en surfplatta för att besöka en e-handelswebbplats. De har dock båda sina egna oberoende konton som de använder för att surfa och handla online.
   * Som en delad enhet har surfplattan ett motsvarande ECID, som representerar webbläsarens cookie-ID.
* Anta att Kevin använder surfplattan och **loggar in** på sitt e-handelskonto för att söka efter hörlurar, vilket innebär att Kevin&#39;s CRMID (**Namespace för användaridentitet**) nu är länkat till surfplattets ECID (**Namnområde för delad identitet**). Surfplattans surfdata är nu inbyggt i Kevins identitetsdiagram.
   * Om Kevin **loggar ut** och Nora använder surfplattan och **loggar in** på sitt eget konto och köper en kamera, är hennes CRMID nu länkat till surfplattans ECID. Därför är surfplattets surfdata nu inbyggt i Noras identitetsdiagram.
   * Om Nora **inte loggar ut** och Kevin använder surfplattan, men **inte loggar in**, är surfplattans surfdata fortfarande inbyggda i Nora, eftersom hon fortfarande är den autentiserade användaren och hennes CRMID fortfarande är länkat till surfplattans ECID.
   * Om Nora **loggar ut** och Kevin använder surfplattan, men **inte loggar in**, så är surfplattets surfdata fortfarande inbyggda i Noras identitetsdiagram, eftersom hennes CRMID-värde fortfarande är länkat till surfplattets ECID som den **senaste autentiserade användaren**.
   * Om Kevin **loggar in** igen länkas hans CRMID till surfplatsens ECID, eftersom han nu är den sista autentiserade användaren och surfplattets surfdata nu införlivas med identitetsdiagrammet.

### Så här sammanfogar [!DNL Profile Service] profilfragment med [!DNL Shared Device Detection] aktiverat

[!DNL Profile Service] noterar profilfragment och sammanfogade profiler. Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden.

När [!DNL Shared Device Detection] är aktiverat definierar [!DNL Profile] profilfragmentets primära identitet baserat på om upplevelsehändelsen är autentiserad eller oautentiserad

En **händelse för autentiserad upplevelse** är en åtgärd som slutfördes av en användare när han/hon var inloggad på en enhet. För händelser för autentiserade upplevelser är den primära identiteten **Namnområde för användaridentitet** (inloggnings-ID). En **oautentiserad upplevelsehändelse** är en åtgärd som har slutförts av en användare som inte är inloggad på en enhet. För oautentiserade upplevelsehändelser är den primära identiteten **Namnområde för delad identitet** (ECID).

Mer information finns i [[!DNL Real-Time Customer Profile] översikten](../profile/home.md).

## Gränssnitt för delade enheter

I plattformsgränssnittet väljer du **[!UICONTROL Identities]** i den vänstra navigeringen och sedan **[!UICONTROL Identity settings]**.

![ID-dashboard](./images/shared-device/identity-dashboard.png)

Sidan [!UICONTROL Shared device settings] visas med ett gränssnitt för att konfigurera inställningar för delade enheter för dina data. Delade enhetsinställningar är inaktiverade som standard.

När det här alternativet är aktiverat kan data från olika användare på samma enhet separeras från varandra. Den här konfigurationsinställningen ger en renare och exaktare representation av identitetsdiagram, där användaridentiteter för samma enhet inte kombineras.

Välj **[!UICONTROL Enable]** om du vill börja ändra inställningarna för den delade enheten.

![enable-shared-device](./images/shared-device/enable-shared-device.png)

Konfigurationsalternativen [!UICONTROL Shared Identity Namespace] och [!UICONTROL User Identity Namespace] visas så att du kan ändra de identitetsnamnutrymmen som du vill använda.

![set-namespaces](./images/shared-device/set-namespaces.png)

[!UICONTROL Shared Identity Namespace] representerar en enhet som används av flera olika användare. Det här namnområdet är alltid inställt på **[!UICONTROL ECID]** eftersom alla plattformsanvändare använder **[!UICONTROL ECID]** som webbläsaridentifierare.

![shared-identity-namespace](./images/shared-device/shared-identity-namespace.png)

Med [!UICONTROL User Identity Namespace] kan du identifiera olika användare av samma enhet och förhindra att data kombineras till samma identitetsdiagram.

![user-identity-namespace](./images/shared-device/user-identity-namespace.png)

Välj sökfältet **[!UICONTROL User Identity Namespace]** och ange antingen ett identitetsnamnområde eller välj ett identitetsnamnområde på den nedrullningsbara menyn.

>[!TIP]
>
>[!UICONTROL User Identity Namespace] ska mappas till det identitetsnamnutrymme som motsvarar slutanvändarens inloggnings-ID. Alternativen är kund-ID, e-post och hashad e-post.

![e-post](./images/shared-device/emails.png)

När du har konfigurerat din [!UICONTROL Shared Device Settings] väljer du **[!UICONTROL Save]**.

![spara](./images/shared-device/save.png)

Ett popup-fönster visas med en uppmaning om att bekräfta ditt val. Välj **[!UICONTROL Yes]** för att slutföra konfigurationsinställningen.

![bekräfta](./images/shared-device/confirm.png)
