---
title: Behörighetshantering för datainsamling i Experience Platform
description: En översikt på hög nivå över hur du hanterar behörigheter och styr åtkomsten till datainsamlingsfunktioner i Adobe Experience Platform.
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---

# Behörighetshantering för datainsamling i Experience Platform {#permission-management}

>[!CONTEXTUALHELP]
>id="platform_tags_permissions"
>title="Behörigheter"
>abstract="Förstå de nyckelbehörigheter som krävs för att arbeta med datastreams, scheman, identiteter och sandlådor i Adobe Experience Platform."

[Datainsamling i Adobe Experience Platform](./home.md) består av flera olika tekniker som arbetar tillsammans för att samla in och överföra dina data. Åtkomsten till dessa tekniker regleras genom detaljerade rollbaserade behörigheter i Adobe Admin Console.

I den här handboken visas hur du hanterar behörigheter för datainsamlingsfunktioner.

## Komma igång

Om du vill konfigurera åtkomstkontroll för datainsamling måste du ha administratörsbehörighet för en organisation som har en produktintegrering med Adobe Experience Platform Data Collection. Den minsta rollen som kan bevilja eller återkalla behörigheter är en **produktprofiladministratör**. Andra administratörsroller som kan hantera behörigheter är **produktadministratörer** (kan hantera alla profiler i en produkt) och **systemadministratörer** (inga begränsningar). Mer information finns i artikeln om [administrativa roller](https://helpx.adobe.com/se/enterprise/using/admin-roles.html) i administrationshandboken för Adobe Enterprise.

I den här handboken förutsätts det att du känner till grundläggande Admin Console-koncept som produktprofiler och hur de ger produktbehörigheter till enskilda användare och grupper. Mer information finns i användarhandboken för [Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html).

## Tillgängliga behörigheter

Behörigheterna för datainsamling anges med två produktbeteckningar i Admin Console: **Adobe Experience Platform** och **Adobe Experience Platform Data Collection**. I avsnitten nedan beskrivs de behörigheter som ges för respektive produkt tillsammans med beskrivningar av de specifika funktioner som de ger tillgång till.

### Adobe Experience Platform-behörigheter

Behörigheter under Adobe Experience Platform innefattar åtkomst till datastreams, identiteter, scheman och sandlådor. Anvisningar om hur du konfigurerar Adobe Experience Platform-behörigheter finns i användarhandboken för [åtkomstkontroll](../access-control/ui/overview.md).

| Kategori | Behörighet | Beskrivning |
| --- | --- | --- |
| Sandlådor | (Ej tillämpligt) | Beroende på vilka [sandlådor](../sandboxes/home.md) som har skapats under din organisation kan du styra åtkomsten till var och en av dem via den här behörighetskategorin i Admin Console. |
| Datamodellering | Hantera scheman | Ger möjlighet att visa, skapa och redigera [XDM-scheman (Experience Data Model)](../xdm/home.md). |
| Datamodellering | Visa scheman | Ger skrivskyddad åtkomst till scheman. |
| Identity Management | Hantera identitetsnamnutrymmen | Ger möjlighet att visa, skapa och redigera [identitetsnamnutrymmen](../identity-service/features/namespaces.md). |
| Identity Management | Visa identitetsnamnutrymmen | Ger skrivskyddad åtkomst till identitetsnamnutrymmen. |
| Datainsamling | Hantera datastreams | Ger möjlighet att visa, skapa och redigera [datastreams](../datastreams/overview.md). |
| Datainsamling | Visa datastreams | Ger skrivskyddad åtkomst till datastreams. |

{style="table-layout:auto"}

### Behörigheter för Adobe Experience Platform Data Collection

Behörigheter under Adobe Experience Platform Data Collection styr åtkomsten till taggar och funktioner för vidarebefordran av händelser, inklusive egenskaper, tillägg och miljöer. Anvisningar om hur du konfigurerar behörigheter för Adobe Experience Platform Data Collection finns i avsnittet [nedan](#manage).

| Kategori | Behörighet | Beskrivning |
| --- | --- | --- |
| Plattformar | Webb | Ger åtkomst till [webbegenskaper](../tags/ui/administration/companies-and-properties.md) i kombination med andra egenskapsrättigheter. |
| Plattformar | Mobil | Ger åtkomst till [mobila egenskaper](../tags/ui/administration/companies-and-properties.md) i kombination med andra egenskapsrättigheter. |
| Plattformar | Edge | Ger åtkomst till [händelsevidarebefordrande Edge-egenskaper](../tags/ui/event-forwarding/getting-started.md) i kombination med andra egenskapsrättigheter. |
| Egenskaper | (Ej tillämpligt) | Beroende på vilka egenskaper som har skapats under din organisation kan du styra åtkomsten till var och en av dem genom den här behörighetskategorin i Admin Console.<br><br>En användares tilldelade egenskapsrättigheter gäller bara för de egenskaper som de har fått åtkomst till via den här behörighetskategorin. |
| Egendomsrättigheter | Godkänn | Ger möjlighet att godkänna ett biblioteksbygge som en del av [publiceringsflödet](../tags/ui/publishing/publishing-flow.md). |
| Egendomsrättigheter | Utveckla | Ger möjlighet att utveckla ett bibliotek som en del av [publiceringsflödet](../tags/ui/publishing/publishing-flow.md). |
| Egendomsrättigheter | Redigera egenskap | Ger möjlighet att redigera den grundläggande konfigurationen för de egenskaper som en användare har åtkomst till. |
| Egendomsrättigheter | Hantera miljöer | Ger möjlighet att hantera [miljöerna](../tags/ui/publishing/environments.md) för egenskaperna som en användare har åtkomst till. |
| Egendomsrättigheter | Hantera tillägg | Ger möjlighet att hantera [tilläggen](../tags/ui/managing-resources/extensions/overview.md) för egenskaperna som en användare har åtkomst till. |
| Egendomsrättigheter | Publicera | Ger möjlighet att publicera ett biblioteksbygge som en del av [publiceringsflödet](../tags/ui/publishing/publishing-flow.md). |
| Företagsrättigheter | Utveckla tillägg | Ger möjlighet att skapa och ändra tilläggspaket som ägs av organisationen, inklusive privata releaser och förfrågningar om allmän spridning. |
| Företagsrättigheter | Hantera appkonfigurationer | Detta tillstånd gäller endast om du har en licens för Adobe Journey Optimizer eller en annan lösning som ger åtkomst till mobilmeddelanden i appen och push-meddelanden. På så sätt kan du hantera de appar som Adobe Experience Cloud känner till tillsammans med de push-autentiseringsuppgifter som krävs för att kommunicera med meddelandetjänsten i Firebase Cloud och Apple Push Notification-tjänsten. |
| Företagsrättigheter | Hantera egenskaper | Ger dig möjlighet att skapa och hantera taggar (webbegenskaper), vidarebefordra händelser (edge-egenskap) och mobila egenskaper. |

{style="table-layout:auto"}

>[!NOTE]
>
>Mer information om hur dessa behörigheter påverkar funktioner i taggar, inklusive administrationsstrategier för vanliga scenarier, finns i taggdokumentationen för [användarbehörigheter](../tags/ui/administration/user-permissions.md).

## Hantera behörigheter {#manage}

Behörigheter för datainsamling hanteras med två produktbeteckningar: **Adobe Experience Platform** och **Adobe Experience Platform Data Collection**.

Se underavsnitten nedan för steg om hur du hanterar behörigheter för respektive produkt i Admin Console:

* [Adobe Experience Platform-behörigheter](#manage-platform)
* [Behörigheter för Adobe Experience Platform Data Collection](#manage-collection)

### Hantera behörigheter i Adobe Experience Platform {#manage-platform}

>[!NOTE]
>
>Om du vill hantera behörigheter för en roll måste du ha administratörsbehörighet. Kontakta systemadministratören om du inte har administratörsbehörighet.

I Experience Cloud **[!UICONTROL Permissions]**-avsnittet kan du definiera användarroller och profiler för att hantera åtkomst för funktioner och objekt i ett produktprogram.

Genom [!UICONTROL Permissions] kan du skapa och hantera roller och tilldela önskade resursbehörigheter för dessa roller.

![Adobe Experience Cloud markerar produkten Behörigheter.](./images/permissions/permissions-product.png)

Om du vill komma åt datainsamlingsfunktioner måste du aktivera alla behörigheter i kategorierna **[!UICONTROL Sandboxes]**, **[!UICONTROL Data Modeling]**, **[!UICONTROL Identity Management]** och **[!UICONTROL Data Collection]**.

![Bild som visar produktkortet för datainsamling i Admin Console](./images/permissions/platform-permission-card.png)

Mer information om hur du hanterar Experience Platform-behörigheter finns i [användargränssnittshandboken för åtkomstkontroll](../access-control/ui/overview.md).

>[!NOTE]
>
>Beroende på vilka SKU:er din organisation har tillgång till kanske du inte har alla Experience Platform-behörigheter.

### Hantera behörigheter i Adobe Experience Platform Data Collection {#manage-collection}

Om du vill hantera de här behörigheterna loggar du in på Admin Console och väljer **[!UICONTROL Products]** i den översta navigeringen. Välj sedan **[!UICONTROL Adobe Experience Platform Data Collection]**.

![Bild som visar produktkortet för datainsamling i Admin Console](./images/permissions/data-collection-card.png)

#### Välj eller skapa en produktprofil

På nästa skärm visas en lista med tillgängliga produktprofiler för datainsamling i din organisation. Standardprofilen är **[!DNL Default Data Collection All Access]**. Du kan välja att redigera standardproduktprofilen om du vill, eller så kan du välja **[!UICONTROL New Profile]** och skapa en. Om du har flera roller eller användargrupper i organisationen som kräver olika åtkomstnivåer bör du skapa en separat produktprofil för var och en av dem.

![Bild som visar produktprofilerna för datainsamling i Admin Console](./images/permissions/new-profile.png)

När du har valt eller skapat en produktprofil kan du använda ikonerna **[!UICONTROL Edit]** för att starta [redigeringsbehörigheter](#edit-permissions) för profilen eller välja fliken **[!UICONTROL Users]** för att börja [tilldela användare](#assign-users) till profilen.

![Bild som visar fliken Behörigheter för en produktprofil, Admin Console](./images/permissions/edit-permission-categories.png)

#### Redigera behörigheter för produktprofilen {#edit-permissions}

När du redigerar behörigheter för en profil visas tillgängliga behörigheter i den vänstra kolumnen medan de som ingår i profilen visas i den högra kolumnen. Välj de angivna behörigheterna för att flytta dem mellan någon av kolumnerna.

![Bild som visar behörigheter som lagts till under den inkluderade kolumnen](./images/permissions/added-permissions.png)

Behörigheter är ordnade i kategorier. Om du vill växla mellan kategorier väljer du önskad kategori i den vänstra navigeringen.

![Bild som visar företagsrättighetsavsnittet under behörigheter](./images/permissions/switch-category.png)

Välj **[!UICONTROL Save]** när du har slutfört konfigurationen av behörigheter.

![Bild som visar behörighetskonfigurationen som sparas för produktprofilen](./images/permissions/save-permissions.png)

Produktprofilvyn visas igen med de tillagda behörigheterna.

![Bild som visar tillagda behörigheter för produktprofilen](./images/permissions/permissions-added.png)

#### Tilldela användare till produktprofilen {#assign-users}

Om du vill tilldela användare till produktprofilen (och ge dem profilens konfigurerade behörigheter) väljer du fliken **[!UICONTROL Users]** följt av **[!UICONTROL Add user]**.

![Bild som visar användarfliken för en produktprofil i Admin Console](./images/permissions/manage-users.png)

Mer information om hur du hanterar användare för en produktprofil finns i [Admin Console-dokumentationen](https://helpx.adobe.com/se/enterprise/using/manage-product-profiles.html).

## Nästa steg

I den här guiden beskrivs de tillgängliga behörigheterna för datainsamling och hur du hanterar dem via Admin Console. Mer information om hur du hanterar behörigheter för andra Adobe Experience Platform-funktioner finns i [åtkomstkontrollsdokumentationen](../access-control/home.md).
