---
title: Hantera behörigheter för Privacy Service
description: Lär dig hur du hanterar användarbehörigheter för Adobe Experience Platform Privacy Service med Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 1%

---

# Hantera behörigheter för Privacy Service

>[!IMPORTANT]
>
>Behörigheterna för Adobe Experience Platform Privacy Service har förbättrats för att öka deras granularitet. Med dessa ändringar kan organisationsadministratörer ge fler användare åtkomst med önskad roll och behörighetsnivå. Användare av tekniska konton måste uppdatera sina behörigheter för Privacy Service eftersom den här kommande uppdateringen utgör en viktig förändring för dem. Den här behörighetsändringen verkställs på **13 april 2023**. Läs dokumentationen om [migrera äldre API-autentiseringsuppgifter](#migrate-tech-accounts) för vägledning om hur du löser detta problem.
>
>Tekniska konton är tillgängliga för företagskunder och skapas via Adobe Developers Console. En teknisk kontoinnehavares Adobe ID avslutas med `@techacct.adobe.com`. Om du är osäker på om du har ett tekniskt konto kontaktar du din organisations administratör.

Åtkomst till [Adobe Experience Platform Privacy Service](./home.md) styrs av rollbaserade behörigheter i Adobe Admin Console. Genom att skapa produktprofiler som tilldelar behörigheter till användargrupper kan du bestämma vem som har åtkomst till vilka funktioner i Privacy Servicen [UI](./ui/overview.md) och [API](./api/overview.md).

>[!NOTE]
>
>När du skapar en integrering för Privacy Service-API måste du välja en befintlig produktprofil för att kunna avgöra vilka funktioner eller åtgärder som integreringen har behörighet för. Se guiden [komma igång med Privacy Services-API](./api/getting-started.md) för mer information.

I den här handboken visas hur du hanterar behörigheter för Privacy Service.

## Komma igång

För att kunna konfigurera åtkomstkontroll för Privacy Service måste du ha administratörsbehörighet för en organisation som har en produktintegrering med Adobe Experience Platform Privacy Service. Minimirollen som kan bevilja eller återkalla behörigheter är en **produktprofiladministratör**. Andra administratörsroller som kan hantera behörigheter är **produktadministratörer** (kan hantera alla profiler i en produkt) och **systemadministratörer** (inga begränsningar). Läs artikeln om [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html) i administrationshandboken för Adobe Enterprise om du vill ha mer information.

I den här handboken förutsätts det att du är bekant med grundläggande produktkoncept som produktprofiler och hur du tilldelar produktbehörigheter till enskilda användare och grupper. Mer information finns i [Användarhandbok för Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html).

## Tillgängliga behörigheter

I följande tabell visas de tillgängliga behörigheterna för Privacy Service med beskrivningar av de specifika funktioner som de ger åtkomst till:

>[!NOTE]
>
>All Privacy Service och [!UICONTROL Opt Out of Sale] behörigheter är åtskilda och åtskilda från varandra utan funktionell överlappning. Detta är möjligt eftersom Privacy Service-API:t betraktas som ideellt.

| Kategori | Behörighet | Beskrivning |
| --- | --- | --- |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Privacy Read Permission] | Avgör om användaren kan visa befintliga begäranden om åtkomst och borttagning, tillsammans med information om dem. |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Privacy Write Permission] | Avgör om en användare kan skapa nya begäranden om åtkomst och borttagning. |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Read (Access) Content Delivery Permission] | När en åtkomstbegäran bearbetas som Privacy Service skickas en ZIP-fil med kundens data till den kunden. När du tittar upp information om en åtkomstbegäran avgör den här behörigheten om användaren kan komma åt nedladdningslänken för förfrågningens ZIP-fil. |
| [!UICONTROL Opt Out of Sale Permissions] | [!UICONTROL Read Permission - Opt Out of Sale] | Avgör om användaren kan visa befintliga begäranden om avanmälan och deras information. |
| [!UICONTROL Opt Out of Sale Permissions] | [!UICONTROL Write Permission - Opt Out of Sale] | Avgör om en användare kan skapa nya begäranden om avanmälan från försäljning. |

{style="table-layout:auto"}

## Hantera behörigheter {#manage}

Om du vill hantera behörigheter för Privacy Service loggar du in på [Admin Console](https://adminconsole.adobe.com/) och markera **[!UICONTROL Products]** i den övre navigeringen. Här väljer du **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Bild som visar Privacy Servicens produktkort i Admin Console](./images/permissions/privacy-service-card.png)

### Välj eller skapa en produktprofil

På nästa skärm visas en lista med tillgängliga produktprofiler för Privacy Service i din organisation. Om det inte finns några produktprofiler väljer du **[!UICONTROL New Profile]** för att skapa en. Om du har flera roller eller användargrupper i organisationen som kräver olika åtkomstnivåer bör du skapa en separat produktprofil för var och en av dem.

![Bild som visar produktprofiler för Privacy Service i Admin Console](./images/permissions/select-or-create-profile.png)

När du har valt en produktprofil kan du använda **[!UICONTROL Permissions]** flik att starta [redigera behörigheter](#edit-permissions) för profilen eller välj **[!UICONTROL Users]** flik att starta [tilldela användare](#assign-users) till profilen.

![Bild som visar fliken Behörigheter för en produktprofil Admin Console](./images/permissions/users-permissions-tabs.png)

### Redigera behörigheter för profilen {#edit-permissions}

På **[!UICONTROL Permissions]** väljer du någon av de behörighetskategorier som visas för att komma åt behörighetens redigeringsvy.

När du redigerar behörigheter för en profil visas tillgängliga behörigheter i den vänstra kolumnen medan de som ingår i profilen visas i den högra kolumnen. Välj de angivna behörigheterna för att flytta dem mellan någon av kolumnerna.

![Bild som visar tillgängliga och inkluderade behörighetskolumner](./images/permissions/edit-permissions.png)

Behörigheter är ordnade i kategorier. Om du vill växla mellan kategorier väljer du önskad kategori i den vänstra navigeringen.

![Bilden visar [!UICONTROL Opt Out of Sale] sektion under behörigheter](./images/permissions/switch-category.png)

Välj **[!UICONTROL Save]** när du är klar med konfigurationen av behörigheter.

![Bild som visar den behörighetskonfiguration som sparas för produktprofilen](./images/permissions/save-permissions.png)

Produktprofilvyn visas igen med de tillagda behörigheterna.

![Bild som visar de tillagda behörigheterna för produktprofilen](./images/permissions/permissions-added.png)

### Tilldela användare till profilen {#assign-users}

Om du vill tilldela användare till produktprofilen (och ge dem profilens konfigurerade behörigheter) väljer du **[!UICONTROL Users]** tabbtecken, följt av **[!UICONTROL Add user]**.

![Bild som visar användarfliken för en produktprofil i Admin Console](./images/permissions/manage-users.png)

Mer information om hur du hanterar användare för en produktprofil finns i [Admin Console dokumentation](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### Migrera tidigare API-autentiseringsuppgifter till profilen {#migrate-tech-accounts}

>[!NOTE]
>
>Det här avsnittet gäller endast befintliga API-autentiseringsuppgifter som skapades innan Privacy Servicens behörigheter integrerades i Adobe Admin Console. För nya autentiseringsuppgifter tilldelas produktprofiler (och deras behörigheter) via [Adobe Developer Console-projekt](https://developer.adobe.com/developer-console/docs/guides/projects/) i stället.<br><br>Se avsnittet om [tilldela produktprofiler till ett projekt](./api/getting-started.md#product-profiles) i guiden Komma igång för Privacy Service-API för mer information.

Tidigare krävdes ingen produktprofil för integrering och behörigheter för tekniska konton. På grund av de senaste förbättringarna av Privacy Servicens behörigheter är det nu nödvändigt att migrera tidigare API-autentiseringsuppgifter till produktprofilen. Denna uppdatering gör det möjligt att ge detaljerad behörighet till innehavare av tekniska konton. Följ stegen nedan för att uppdatera behörigheter för det tekniska kontot för Privacy Service.

#### Uppdatera behörigheter för tekniska konton {#update-tech-account-permissions}

Det första steget för att tilldela en behörighetsgrupp till ditt tekniska konto är att navigera till [Adobe Admin Console](https://adminconsole.adobe.com/) och skapa en ny produktprofil för Privacy Service.

I användargränssnittet för Admin Console väljer du **Produkter** från navigeringsfältet, följt av **[!UICONTROL Experience Cloud]** och **[!UICONTROL Adobe Experience Platform Privacy Service]** till vänster. The [!UICONTROL Product Profiles] visas. Välj **Ny profil** för att skapa en ny produktprofil för Privacy Service.

![Fliken Produktprofiler för Privacy Servicen Experience Platform i Adobe Admin Console med Ny profil markerad.](./images/permissions/create-product-profile.png)

The [!UICONTROL Create a new product profile] visas. Fullständiga anvisningar om hur du skapar en produktprofil finns i [Användargränssnittsguide för att skapa profiler](../access-control/ui/create-profile.md).

När du har sparat din nya produktprofil går du till [Adobe Developer Console](https://developer.adobe.com/console/home) och logga in på produkten eller projektet. Välj **[!UICONTROL Projects]** i den övre navigeringen, följt av kortet för ditt projekt.

>[!NOTE]
>
>Du kanske måste rensa cacheminnet och/eller vänta lite på att det nya projektet ska visas i listan över Developer Console-projekt.

När du har loggat in i ditt projekt väljer du **[!UICONTROL Privacy Service API]** integrering från vänster sidospalt.

![Fliken Projekt i Adobe Developer Console med projekt- och Privacy Service-API:er markerade.](./images/permissions/login-to-dev-console-project.png)

Instrumentpanelen för integrering av Privacy Service-API visas. Från den här kontrollpanelen kan du redigera produktprofilen som är kopplad till det projektet. Välj **[!UICONTROL Edit product profiles]** för att påbörja processen. The [!UICONTROL Configure API] visas.

![Instrumentpanelen för integrering av Privacy Service-API i Adobe Developer Console med produktprofiler markerade](./images/permissions/edit-product-profiles.png)

The [!UICONTROL Configure API] visas de tillgängliga produktprofiler som för närvarande finns i tjänsten. De korrelerar till de produktprofiler som skapas i Admin Console. I listan med tillgängliga produktprofiler markerar du kryssrutan för den nya produktprofilen som du skapade för det tekniska kontot i Admin Console. Det här associerar automatiskt det här tekniska kontot med behörigheterna i den valda produktprofilen. Välj **[!UICONTROL Save configured API]** för att bekräfta inställningarna.

>[!NOTE]
>
>Om ett tekniskt konto redan är associerat med en produktprofil markeras en av kryssrutorna i listan med tillgängliga produktprofiler.

![Dialogrutan Konfigurera API i Adobe Developer Console med en produktprofilkryssruta och Spara konfigurerat API markerat.](./images/permissions/select-profile-for-tech-account.png)

#### Bekräfta att inställningarna har tillämpats {#confirm-applied-settings}

Bekräfta att dina inställningar har tillämpats på kontot. Återgå till [Admin Console](https://adminconsole.adobe.com/) och navigera till din nya produktprofil. Välj **[!UICONTROL API Credentials]** om du vill visa en lista med associerade projekt. Det projekt som används i Developer Console där du tilldelade produktprofilen till det tekniska kontot visas i listan med autentiseringsuppgifter. Namnet på varje API-autentiseringsuppgift består av projektnamnet med ett slumpmässigt genererat nummer som suffix till slutet. Välj en autentiseringsuppgift för att öppna [!UICONTROL Details] -panelen.

![En produktprofil på Admin Console med fliken API-autentiseringsuppgifter och en rad projektautentiseringsuppgifter markerade.](./images/permissions/confirm-credentials-in-admin-console.png)

The [!UICONTROL Details] -panelen innehåller information om API-autentiseringsuppgifter, inklusive associerat tekniskt ID, API-nyckeln, skapad och senast ändrad samt tillhörande Adobe-produkter.

![Den markerade detaljpanelen för en API-referens i Admin Console.](./images/permissions/admin-console-details-panel.png)

## Nästa steg

I den här guiden beskrivs de tillgängliga behörigheterna för Privacy Service och hur du hanterar dem via Admin Console.

Anvisningar om hur du skapar en ny API-integrering när du har konfigurerat produktprofiler finns i [komma igång-guide för Privacy Services-API](./api/getting-started.md). Mer information om hur du hanterar behörigheter för andra Adobe Experience Platform-funktioner finns i [dokumentation om åtkomstkontroll](../access-control/home.md).
