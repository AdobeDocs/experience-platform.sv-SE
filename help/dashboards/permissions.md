---
solution: Experience Platform
title: Så här får du och beviljar behörigheter för Experience Platform-kontrollpaneler
type: Documentation
description: Ge användare möjlighet att visa, redigera och uppdatera kontrollpaneler i Experience Platform med Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f138bb0f1b8d289cc872afc065d31c5e55d4b05c
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 6%

---

# Åtkomstbehörigheter för kontrollpaneler

Om du vill att användare ska kunna visa, redigera och uppdatera kontrollpaneler måste du först aktivera behörigheter. I Adobe Experience Platform tillhandahålls åtkomstkontroll via [Adobe Admin Console](https://adminconsole.adobe.com/). Användarna länkas med behörigheter och sandlådor via produktprofiler i [!DNL Admin Console].

Det här dokumentet innehåller en sammanfattning av tillgängliga behörigheter för kontrollpaneler, inklusive de funktioner som de ger åtkomst till och de användarfunktioner som de aktiverar. Detaljerad information om hur du får och tilldelar behörigheter finns i [åtkomstkontroll - översikt](../access-control/home.md).

## Förutsättningar

För att konfigurera åtkomstkontroll för [!DNL Experience Platform]måste du ha administratörsbehörighet för en organisation som har en [!DNL Experience Platform] produktintegrering. Se Adobe Help Center artikel om [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html) för mer information.

## Tillgängliga kontrollpanelsbehörigheter {#available-permissions}

The [!DNL Dashboards] tjänsten ger tre behörigheter som tillsammans ger fullständig åtkomst till [!UICONTROL Profiles], [!UICONTROL Segments], [!UICONTROL Destinations]och [!UICONTROL Licence Usage] paneler i Adobe Experience Platform. Dessa behörigheter är:

| Behörighet | Beskrivning |
|---|---|
| **Hantera standardinstrumentpaneler** | Den här behörigheten är en **global läs- och skrivbehörighet**. Med den kan du [skapa anpassade widgetar](./customize/custom-widgets.md) och [redigera widgetschemat](./customize/edit-schema.md) via [!UICONTROL Widget library]. |
| **Visa standardinstrumentpaneler** | Detta ger **skrivskyddad** för [!UICONTROL Profiles], [!UICONTROL Destinations]och [!UICONTROL Segments] kontrollpaneler och ger åtkomst till dem via plattformens vänstra navigering. Dessutom tilläggs [!UICONTROL Dashboards] till vänster navigering och åtkomst till [!UICONTROL Dashboards] fliken för inventering och integreringar. |
| **Visa kontrollpanel för licensanvändning** | Den här behörigheten tillåter användare **skrivskyddad** behörighet till [kontrollpanelen för licensanvändning](./guides/license-usage.md) i användargränssnittet i Experience Platform. |

Det finns fem behörigheter som inte ingår i [!DNL Dashboard] som kan behövas beroende på dina behov. I följande tabell visas deras kategoriplatser i Admin Console:

>[!IMPORTANT]
>
>Båda **[!DNL Manage Standard Dashboards]** och **[!DNL View Standard Dashboards]** behörigheter **krav** behörighet för att visa eller hantera från [!DNL Profile Management] eller [!DNL Destinations] i Admin Console för att aktivera de relevanta avsnitten i plattformsgränssnittet.

| Behörighet | Admin Console-kategoriplats |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Åtkomstkontrollmatris

Följande åtkomstkontrollsmatris innehåller en beskrivning av vilka behörigheter som krävs och vilken funktion de tillhandahåller för åtkomst till de olika instrumentpanelsfunktionerna. Behörigheter visas på den övre vågräta raden och arbetsytan i användargränssnittet för plattformen visas längs den vänstra kolumnen.

|  | [!UICONTROL View Standard Dashboard] ELLER [!UICONTROL Manage Standard Dashboard] | [!UICONTROL View Profiles],<br/>[!UICONTROL View Segments],<br/> [!UICONTROL View Destinations] | [!UICONTROL Manage Queries] &amp; [!UICONTROL Manage Sandboxes] | [!UICONTROL View License Usage Dashboard] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] i den vänstra navigeringen. | Ej tillämpligt | **En behörighet av typen Visa eller Hantera krävs** för varje kontrollpanel. | Ej tillämpligt | Ej tillämpligt |
| [!DNL Dashboards] i den vänstra navigeringen. | AKTIVERAT | **Minst en KRÄVS**. | Ej tillämpligt | Ej tillämpligt |
| [!DNL Dashboards] [!DNL Inventory] <br/>(fliken Bläddra) | AKTIVERAT | Ej tillämpligt | Ej tillämpligt | Ej tillämpligt |
| [!DNL Dashboards] [!DNL Integrations] tab <br/>(används för att installera Power BI) | AKTIVERAT | **Minst en KRÄVS** | Ej tillämpligt | Ej tillämpligt |
| Knapp för installation av Power BI och arbetsflöde | AKTIVERAT | Ej tillämpligt | **OBLIGATORISKT** | Ej tillämpligt |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] instrumentpaneler.<br/>Möjlighet att redigera widgetscheman och lägga till nya attribut för anpassning av widgetar | **Kontrollpanel som är standard för hantering krävs** | **OBLIGATORISKT (för varje instrumentpanel)** | Ej tillämpligt | Ej tillämpligt |
| [!DNL License Usage Dashboard] | Ej tillämpligt | Ej tillämpligt | Ej tillämpligt | AKTIVERAT |

{style=&quot;table-layout:auto&quot;}

## Lägg till behörigheter i din produktprofil

Använd informationen ovan för att lägga till rätt behörigheter till din produktprofil. Mer information finns i dokumentationen om [lägga till behörigheter via gränssnittet för åtkomstkontroll](../access-control/ui/permissions.md).

Beskrivningar av behörigheter finns i [tillgängliga behörigheter](#available-permissions) tidigare i det här dokumentet.

>[!NOTE]
>
>Du behöver inte aktivera alla behörigheter för alla användare. Beroende på din organisations struktur kanske du vill skapa separata produktprofiler för vissa användare och bevilja begränsad åtkomst (t.ex. skrivskyddad). Mer information finns i dokumentationen om hur du hanterar användare för en produktprofil [tilldela behörigheter till specifika användare](../access-control/ui/users.md).

När du har lagt till de nödvändiga åtkomstbehörigheterna kan användare i organisationen börja visa kontrollpaneler i användargränssnittet för Experience Platform och utföra andra åtgärder baserat på de behörigheter som du har tilldelat.
