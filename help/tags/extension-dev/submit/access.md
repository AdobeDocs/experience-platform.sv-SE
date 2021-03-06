---
title: Bevilja användaråtkomst
description: Konfigurera teammedlemmens tagga användarkonton och behörigheter i Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Bevilja användaråtkomst

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Innan du börjar med ditt extension_package måste du konfigurera dina teammedlemmar med användarkonton och behörigheter.  Detta uppnås i [Adobe Admin Console](https://adminconsole.adobe.com/).

Det här dokumentet innehåller steg för hur du beviljar åtkomst till taggar i Adobe Experience Platform via Admin Console.

## Förutsättningar

I den här handboken förutsätts du vara en organisationsadministratör enligt Admin Console. Om du behöver mer information om Admin Console och tilldelning av roller kan du läsa följande resurser:

* [Användarhandbok](https://helpx.adobe.com/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js) för administration: Information om allt i Admin Console
* [Företagsadministrationsroller](https://helpx.adobe.com/au/enterprise/using/admin-roles.html): Mer information om de olika typerna av administrationsroller. I guiden nedan antar vi att du är en organisationsadministratör.

## Välj organisation

Din Adobe Experience Cloud-administratör bör logga in på [Admin Console](https://adminconsole.adobe.com/). Den första skärmen är översikten.

![Översiktsflik i Admin Console](../images/getting-started/admin-console-overview.png)

Vissa av er har kanske tillgång till fler än en organisation (Org). Om du vill lägga till taggfunktioner i rätt organisation markerar du namnet på organisationen som visas i skärmens övre högra hörn. Välj sedan den organisation där du vill använda taggar i listrutan.

![Admin console Org selection dropdown](../images/getting-started/admin-console-choose-org.png)

## Skapa en produktprofil

En produktprofil är en grupp. Enskilda rättigheter tilldelas till produktprofiler och alla användare i profilen ärver dessa rättigheter.

Välj länken **[!UICONTROL Products]** längst upp och **[!UICONTROL Experience Cloud]** till vänster. Om du inte har användargränssnittet för datainsamling i listan bör kunderna kontakta sin kontogrupp och partners bör skicka ett e-postmeddelande till <ExchangeTechEC@adobe.com>.

![Fliken Produkter i Admin Console](../images/getting-started/admin-console-products-launch.png)

På skärmbilden ovan visas en exempelprofil som du kanske inte har ännu. Om du vill skapa en väljer du **[!UICONTROL New Profile]**. På skärmen **Skapa en ny profil** lägger du bara till ett **profilnamn** (till exempel datainsamlingstestning) och en valfri **beskrivning** och väljer sedan **[!UICONTROL Save]**:

![Skapa ny profilvisning](../images/getting-started/admin-console-create-a-new-profile.png)

Produktprofilen har nu lagts till i organisationen. Lägg sedan till användare i produktprofilen.

## Tilldela användare till produktprofilen

Observera att produktprofilen visar noll för **TILLÅTNA ANVÄNDARE** och **ADMINISTRATÖRER**. Välj namnet på produktprofilen som du skapade (datainsamlingstestning i vårt exempel).

![Produktprofiler visas](../images/getting-started/admin-console-profiles-add-user.png)

Klicka på fliken **[!UICONTROL Users]**.  Här kan du söka efter befintliga Adobe ID-användare via e-post eller lägga till nya användare i produktprofilen. Välj **[!UICONTROL Add User link]**.

![Fliken Produktprofiler - användare](../images/getting-started/admin-console-add-launch-user.png)

Ange ett namn, en användargrupp eller en e-postadress i lämpligt textfält. Vi rekommenderar att du tar med ett för- och efternamn där det är möjligt. Välj **[!UICONTROL Save]** om du vill lägga till användaren.

![Lägg till användare i profilvisning](../images/getting-started/admin-console-add-user.png)

När du har alla användare du behöver i den här produktprofilen lägger vi till behörigheter för dem. Klicka på fliken **[!UICONTROL Permissions]**.  På behörighetsskärmen visas **[!UICONTROL Properties]**, **[!UICONTROL Company Rights]** och **[!UICONTROL Property Rights]**. Välj **[!UICONTROL Edit]**.

![Fliken Behörigheter för produktprofiler](../images/getting-started/admin-console-profile-permissions.png)

Om du vill skapa tillägg måste ditt team ha minst följande behörigheter:

* &quot;Hantera egenskaper&quot; från företagsgruppen.
* &quot;Hantera tillägg&quot;, &quot;Hantera miljöer&quot; och &quot;Utveckla&quot; från egenskapsgruppen.

Du kan skapa ytterligare produktprofiler med mer begränsad behörighet senare om du vill, men nu väljer du bara **[!UICONTROL + Add all]** för både **företagsrättigheter** och **Egenskapsrättigheter**. Var noga med att välja **[!UICONTROL Save]** på varje.

![Hantera egenskapsrättigheter](../images/getting-started/admin-console-add-all-property-rights.png)

![Hantera företagsrättigheter](../images/getting-started/admin-console-add-all-company-rights.png)

Hittills har vi valt lämplig organisation, skapat en produktprofil, lagt till användare i produktprofilen och tilldelat behörigheter.

Detta slutför konfigurationen i Admin Console. Du och dina teammedlemmar som har konfigurerats som användare kan nu logga in på [gränssnittet för datainsamling](https://launch.adobe.com/).

## Bekräfta etablering

När ditt företag har fått tillgång till taggar och dina användare är konfigurerade enligt beskrivningen ovan, bör du kunna komma åt produktionsmiljön från [användargränssnittet för datainsamling](https://launch.adobe.com/). Om du har etablerats för taggar och har slutfört Admin Console-stegen ovan, men ändå inte kan logga in i användargränssnittet för datainsamling, kontaktar du supportpersonalen på Adobe.
