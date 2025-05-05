---
title: Översikt över källan RainFocus
description: Lär dig hur du överför händelsehantering och analysdata från ditt RainFocus-konto till Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# [!DNL RainFocus]

>[!NOTE]
>
>Källan [!DNL RainFocus] är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

[!DNL RainFocus] är en plattform som du kan använda för att marknadsföra dina händelser och bygga målgrupper. Du kan använda [!DNL RainFocus] för att skapa snygga kampanjsidor, spåra kampanjresultat och optimera registreringskonverteringar.

Använd [!DNL RainFocus]-källan i Adobe Experience Platform och Real-time Customer Data Platform för att automatiskt berika dina kunddataprofiler med händelser för deltagarupplevelser i realtid. När upplevelsehändelser är aktiverade strömmas de automatiskt in i Real-Time CDP, vilket möjliggör kraftfull målgruppssegmentering, dataanalys och aktivering av deltagarresan med efterföljande destinationer och applikationer som Customer Journey Analytics och Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Den här källkopplingen och dokumentationssidan skapas och underhålls av [!DNL RainFocus]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på <span>@rainfocus.com eller går till [[!DNL RainFocus] Help Center](https://help.rainfocus.com/hc/en-us)

## Förhandskrav

Du måste uppfylla följande krav innan du kan aktivera integreringen av [!DNL RainFocus] på Experience Platform:

[Skapa ett Adobe-tjänstkonto (JWT) i Adobe Developer-portalen](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe har nyligen meddelat att JWT-tokens till förmån för OAuth har ersatts. [!DNL RainFocus]-källan migreras till OAuth inom den närmaste framtiden för att kunna hantera den här ändringen.

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL RainFocus] till Experience Platform måste du ange värden för följande anslutningsegenskaper i [!DNL RainFocus]:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Klient-ID | Klient-ID kan hämtas från Adobe Service Account i Adobe Developer Portal. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Klienthemlighet | Klienthemligheten kan hämtas från Adobes tjänstkonto i Adobe Developer Portal. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| Tekniskt konto-ID | Det tekniska konto-ID:t kan hämtas från Adobe Service Account i Adobe Developer Portal. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| Organisations-ID | Organisations-ID kan hämtas från Adobe Service Account i Adobe Developer Portal | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Skapa ett XDM-schema och definiera identitetsfältet {#create-an-xdm-schema-and-define-the-identity-field}

För att kunna lagra Experience Events från [!DNL RainFocus] i Experience Platform måste du skapa ett XDM-schema (Experience Data Model) som beskriver en datauppsättning som kan lagra möjliga fält och datatyper som ska skickas från [!DNL RainFocus].

[!DNL RainFocus] rekommenderar följande fält, som omfattar alla möjliga data som skickas som standard.

Följande fältgrupper rekommenderas också (anges med prefix):

* Deltagare
* Exhibitor
* Lead
* Session
* SessionTime

**Schemat ska innehålla följande fält:**

| Fält | Typ | Exempel | Beskrivning |
| --- | --- | --- | --- |
| `attendee.registered` | Sträng | Ja | En flagga som avgör om deltagaren anses vara registrerad. |
| `attendee.attendeeId` | Sträng | 1619119968857001fvLB | Deltagar-ID i [!DNL RainFocus]. |
| `attendee.externalId` | Sträng | 1666809456617001wyPj | Det externa ID som anges av en organisation. |
| `attendee.clientId` | Sträng | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | Deltagarens SSO-klient-ID. |
| `attendee.email` | Sträng | användare<span>@company.com | Deltagarens e-postadress. |
| `transmissionId` | Sträng | 168030955713001YHhz | En unik identifierare som används för datapush. |
| `eventType` | Sträng | SessionScheduled | Namnet på Attendee Experience Event. |
| `timestamp` | DateTime | 2023-04-01T00:41:57.000Z | Tidsstämpeln för datapush. |
| `event.name` | Sträng | Adobe Summit 2023 | Namnet på händelsen där överföringen ägde rum. |
| `exhibitor.exhibitorId` | Sträng | 168030955713001YHhz | Identifieraren [!DNL RainFocus] för utställaren. |
| `exhibitor.externalId` | Sträng | 1666809514105001lSJN | Identifieraren för utställaren i klientsystemet. |
| `exhibitor.name` | Sträng | IBM | Utställarens namn. |
| `lead.leadId` | Sträng | 1666809456617001wyPj | ID [!DNL RainFocus] för leadet. |
| `lead.note` | Sträng | | |
| `session.sessionId` | Sträng | 1666809373585001t4aV | Identifieraren [!DNL RainFocus] för sessionen. |
| `session.externalId` | Sträng | 1666809456617001wyPj | Identifieraren för sessionen i klientsystemet. |
| `session.code` | Sträng | GS3 | Koden för sessionen. |
| `session.title` | Sträng | Inspiration Keynote | Sessionens titel. |
| `session.length` | Heltal | 90 | Sessionens längd. |
| `sessiontime.sessiontimeId` | Sträng | 1673033149739001OJLZ | Identifieraren [!DNL RainFocus] för sessionstiden. |
| `sessiontime.startTime` | Sträng | 2023-03-22 10:00:00 | Sessionens starttid. |
| `sessiontime.endTime` | Sträng | 2023-03-22 10:00:00 | Sessionens sluttid. |
| `sessiontime.room` | Sträng | B32 | Rummet som används för sessionen. |

{style="table-layout:auto"}

Om du vill skapa ett schema för [!DNL RainFocus]-data läser du följande dokumentation för steg om hur du skapar ett schema med API:er eller gränssnittet.

* [Skapa schemat med användargränssnittet](../../../xdm/tutorials/create-schema-ui.md)
* [Skapa schemat med API:t](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Schemat måste utöka klassen **XDM ExperienceEvent.**
>* Du måste se till att schemat innehåller en **primär identitet** och är **aktiverat för profilen**. Mer information finns i handboken [Definiera identitetsfält i användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=sv-SE)
>* Du kan ersätta exempelidentiteten (E-post) med en annan lämplig identifierare, som sha256-e-post eller ECID.

### Skapa en integreringsprofil i RainFocus {#create-an-integration-profile-in-rainfocus}

När tjänstkontot och XDM-schemat är klara kan du nu aktivera [!DNL Integration Profile] via [!DNL RainFocus]-plattformen. [!DNL Integration Profile] ansvarar för att strömma data till Experience Platform.

Logga in på [[!DNL RainFocus] plattformen](https://app.rainfocus.com). I den primära navigeringen väljer du **[!DNL Libraries]** och sedan **[!DNL Integration Profiles]**

![Gränssnittet RainFocus med bibliotek och integreringsprofiler har valts.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Om du vill skapa en ny profil väljer du ikonen **(`+`)** . Välj sedan **Adobe Real-time Customer Data Platform** och sedan **OK**.

![Fönstret Skapa integreringsprofil i RainFocus-gränssnittet.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Ange sedan de autentiseringsuppgifter som du har hämtat i Adobe Developer Portal Project:

* **Klient-ID**
* **Klienthemlighet**
* **ID för tekniskt konto**
* **Organisations-ID**

När autentiseringsuppgifterna har angetts väljer du **[!DNL Save]**. Nu bör du se den nya [!DNL Integration Profile] som visas på kontrollpanelen [!DNL RainFocus].

Markera [!DNL Integration Profile] som du just har skapat för att visa en lista över fördefinierade **push-typer** som redan har konfigurerats. Det här är de [Experience Events](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=sv-SE) som skickas till Experience Platform när de inträffar.

![En lista med fördefinierade push-typer i RainFocus-kontrollpanelen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Om du vill hämta en kopia av JSON-exempelnyttolasten väljer du **[!DNL Sample JSON Payload]**. Därefter markerar och kopierar du JSON-exempelnyttolasten och **sparar den i en ny fil med filnamnstillägget .json**. Detta kommer att användas senare i Experience Platform för [mappningskonfigurationer](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Ett exempel på JSON-nyttolast i kontrollpanelen RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**Installationen är inte klar än**: När dataflödet har skapats måste du gå tillbaka till [!DNL RainFocus]-instrumentpanelen för att slutföra [!DNL Integration Profile] genom att ange **URL:en för direktuppspelningsslutpunkten** och **dataflödes-ID**.

## Nästa steg

Genom att läsa det här dokumentet har du slutfört nödvändiga inställningar för att kunna strömma data från ditt [!DNL RainFocus]-konto till Experience Platform. Du kan nu fortsätta med guiden för [att ansluta [!DNL RainFocus] till Experience Platform via användargränssnittet](../../tutorials/ui/create/analytics/rainfocus.md).
