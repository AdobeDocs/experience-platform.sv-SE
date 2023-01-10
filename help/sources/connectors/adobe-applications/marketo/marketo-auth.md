---
keywords: Experience Platform;hemmabruk;populära ämnen;Marketo Engage;markering för att engagera;markering för
solution: Experience Platform
title: Autentisera din Marketo-källanslutning
description: Det här dokumentet innehåller information om hur du genererar autentiseringsuppgifter för Marketo.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Autentisera [!DNL Marketo Engage] källkoppling

Innan du kan skapa en [!DNL Marketo Engage] (nedan kallad[!DNL Marketo]&quot;) källanslutning måste du först konfigurera en anpassad tjänst via [!DNL Marketo] samt hämta värden för ditt Munchkin ID, klient-ID och klienthemlighet.

I dokumentationen nedan beskrivs hur du hämtar inloggningsuppgifter för att skapa en [!DNL Marketo] källkoppling.

## Konfigurera en ny roll

Det första steget när du ska hämta inloggningsuppgifter är att konfigurera en ny roll via [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) gränssnitt.

Logga in på [!DNL Marketo] och markera **[!DNL Admin]** i det övre navigeringsfältet.

![Administratör för en ny roll](../images/marketo/home.png)

The *[!DNL Users & Role]s* sidan innehåller information om användare, roller och inloggningshistorik. Om du vill skapa en ny roll väljer du **[!DNL Roles]** i det övre sidhuvudet och välj **[!DNL New Role]**.

![new-role](../images/marketo/new-role.png)

The **[!DNL Create New Role]** visas. Ange ett namn och en beskrivning och välj sedan de behörigheter du vill ge för den här rollen. Behörigheterna är begränsade till vissa arbetsytor och användarna kan bara utföra åtgärder i arbetsytor som de har behörighet till i.

När du har valt de behörigheter du vill ge väljer du **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

Du kan hantera begränsade behörigheter i API när du skapar roller med [!DNL Marketo]. I stället för att välja&quot;Access API&quot; kan du ange en roll med lägsta åtkomstnivå genom att välja följande behörigheter:

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## Konfigurera en ny användare

På liknande sätt som roller kan du konfigurera en ny användare från **[!DNL Users & Roles]** sida. The **[!DNL Users]** På sidan finns en lista med aktiva användare som för närvarande är etablerade i Marketo. Välj **[!DNL Invite New User]** för att etablera en ny användare.

![Invitation-new-user](../images/marketo/invite-new-user.png)

En snabbmeny visas. Ange lämplig information för e-post, förnamn, efternamn och orsak. Under det här steget kan du även ange ett förfallodatum för åtkomst till det nya användarkontot som du bjuder in. När du är klar väljer du **[!DNL Next]**.

>[!IMPORTANT]
>
>När du konfigurerar en ny användare måste du tilldela åtkomst till en användare som är dedikerad till den anpassade tjänst som du skapar.

![user-info](../images/marketo/new-user-info.png)

Välj lämpliga fält i dialogrutan **[!DNL Permissions]** steg och sedan väljer **[!DNL API Only]** för att ge den nya användaren en API-roll. Välj **[!DNL Next]** för att fortsätta.

![behörigheter](../images/marketo/permissions.png)

För att slutföra processen väljer du **[!DNL Send]**.

![message](../images/marketo/message.png)

## Konfigurera en anpassad tjänst

När du har etablerat en ny användare kan du konfigurera en anpassad tjänst för att hämta dina nya inloggningsuppgifter. Välj **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

The **[!DNL Installed services]** sidan innehåller en lista över befintliga tjänster. Om du vill skapa en ny anpassad tjänst väljer du **[!DNL New]** och sedan markera **[!DNL New Service]**.

![ny tjänst](../images/marketo/new-service.png)

Ange ett beskrivande visningsnamn för den nya tjänsten och välj sedan **[!DNL Custom]** från **[!DNL Service]** nedrullningsbar meny. Ange en lämplig beskrivning och välj sedan den användare som du vill tilldela från **[!DNL API Only User]** nedrullningsbar meny. När du har fyllt i de nödvändiga uppgifterna väljer du **[!DNL Create]** för att skapa en ny anpassad tjänst.

![skapa](../images/marketo/create.png)

## Hämta klient-ID och klienthemlighet

När en ny anpassad tjänst har skapats kan du nu hämta värden för ditt klient-ID och din klienthemlighet. Från **[!DNL Installed Services]** väljer du den anpassade tjänst som du vill använda **[!DNL View Details]**.

![view-details](../images/marketo/view-details.png)

En dialogruta med ditt klient-ID och din klienthemlighet visas.

![autentiseringsuppgifter](../images/marketo/credentials.png)

## Skaffa ett Munchkin-ID

Det sista steget du måste slutföra för att kunna autentisera [!DNL Marketo] källanslutaren är att hämta ditt Munchkin-ID. Välj **[!DNL Munchkin]** under **[!DNL Integration]** -panelen.

![admin-munchkin](../images/marketo/admin-munchkin.png)

The *[!DNL Munchkin]* visas med ditt unika Munchkin-ID överst på panelen.

![munchkin-ID](../images/marketo/munchkin-id.png)

I kombination med ditt klient-ID och din klienthemlighet kan du använda ditt Munchkin-ID för att konfigurera ett nytt konto och [skapa en ny [!DNL Marketo] källanslutning](../../../tutorials/ui/create/adobe-applications/marketo.md) på Experience Platform.
