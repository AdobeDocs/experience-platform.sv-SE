---
solution: Experience Platform
title: Så här får du och beviljar behörigheter för Experience Platform Dashboards
type: Documentation
description: Ge användarna möjlighet att visa, redigera och uppdatera Experience Platform-paneler med Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 5%

---

# Åtkomstbehörigheter för kontrollpaneler

Om du vill att användare ska kunna visa, redigera och uppdatera kontrollpaneler måste du först aktivera behörigheter. I Adobe Experience Platform tillhandahålls åtkomstkontroll via [Adobe Admin Console](https://adminconsole.adobe.com/). Användare länkas med behörigheter och sandlådor via produktprofiler i [!DNL Admin Console].

Det här dokumentet innehåller en sammanfattning av tillgängliga behörigheter för kontrollpaneler, inklusive de funktioner som de ger åtkomst till och de användarfunktioner som de aktiverar. Detaljerad information om hur du får och tilldelar åtkomstbehörigheter får du om du börjar med att läsa [åtkomstkontrollsöversikten](../access-control/home.md).

## Förhandskrav

Om du vill konfigurera åtkomstkontroll för [!DNL Experience Platform] måste du ha administratörsbehörighet för en organisation som har en [!DNL Experience Platform]-produktintegrering. Mer information finns i Adobe Help Center-artikeln om [administrativa roller](https://helpx.adobe.com/se/enterprise/using/admin-roles.html).

## Tillgängliga kontrollpanelsbehörigheter {#available-permissions}

Tjänsten [!DNL Dashboards] ger tre behörigheter som tillsammans ger fullständig åtkomst till kontrollpanelerna [!UICONTROL Profiles], [!UICONTROL Segments], [!UICONTROL Destinations] och [!UICONTROL License Usage] i Adobe Experience Platform. Dessa behörigheter är:

| Behörighet | Beskrivning |
|---|---|
| **Hantera standardinstrumentpaneler** | Den här behörigheten är en **global läs- och skrivbehörighet**. Du kan [skapa anpassade widgetar](./customize/custom-widgets.md) och [redigera widgetschemat](./customize/edit-schema.md) via [!UICONTROL Widget library]. |
| **Visa standardinstrumentpaneler** | Detta ger **skrivskyddad** funktionalitet för kontrollpanelerna [!UICONTROL Profiles], [!UICONTROL Destinations] och [!UICONTROL Segments] och ger åtkomst till dem via Experience Platform vänstra navigering. Det lägger även till [!UICONTROL Dashboards] i den vänstra navigeringen och åtkomst till fliken [!UICONTROL Dashboards] för lager och integreringar. |
| **Visa kontrollpanel för licensanvändning** | Den här behörigheten ger användare **skrivskyddad** åtkomst till [kontrollpanelen för licensanvändning](./guides/license-usage.md) i Experience Platform användargränssnitt. |

Det finns fem behörigheter som inte ingår i kategorin [!DNL Dashboard] och som kan behövas beroende på dina behov. I följande tabell visas deras kategoriplatser i Admin Console:

>[!IMPORTANT]
>
>Både **[!DNL Manage Standard Dashboards]** och **[!DNL View Standard Dashboards]** permissions **kräver** en&quot;view&quot;- eller&quot;manage&quot;-behörighet från kategorin [!DNL Profile Management] eller [!DNL Destinations] i Admin Console för att aktivera de relevanta avsnitten i Experience Platform-gränssnittet.

| Behörighet | Admin Console-kategoriplats |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Åtkomstkontrollmatris

Följande åtkomstkontrollsmatris innehåller en beskrivning av vilka behörigheter som krävs och vilken funktion de tillhandahåller för åtkomst till de olika instrumentpanelsfunktionerna. Behörigheterna visas på den övre vågräta raden och Experience Platform UI-arbetsytan visas längs den vänstra kolumnen.

|   | [!UICONTROL View Standard Dashboard] ELLER [!UICONTROL Manage Standard Dashboard] | [!UICONTROL View Profiles],<br/>[!UICONTROL View Segments],<br/> [!UICONTROL View Destinations] | [!UICONTROL Manage Queries] &amp; [!UICONTROL Manage Sandboxes] | [!UICONTROL View License Usage Dashboard] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] i den vänstra navigeringen. | N/A | **En behörighet av typen Visa eller Hantera krävs** för varje instrumentpanel. | N/A | N/A |
| [!DNL Dashboards] i den vänstra navigeringen. | AKTIVERAT | **Minst en KRÄVS**. | N/A | N/A |
| [!DNL Dashboards] [!DNL Inventory] <br/>(fliken Bläddra) | AKTIVERAT | N/A | N/A | N/A |
| [!DNL Dashboards] [!DNL Integrations] tab <br/> (används för att installera Power BI) | AKTIVERAT | **Minst en KRÄVS** | N/A | N/A |
| Power BI Install button &amp; workflow | AKTIVERAT | N/A | **KRÄVS** | N/A |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] instrumentpaneler.<br/>Möjlighet att redigera widgetscheman och lägga till nya attribut för widgetanpassning | **Hantera standardinstrumentpanel KRÄVS** | **OBLIGATORISKT (för varje instrumentpanel)** | N/A | N/A |
| [!DNL License Usage Dashboard] | N/A | N/A | N/A | AKTIVERAT |

{style="table-layout:auto"}

## Lägg till behörigheter i din produktprofil

Använd informationen ovan för att lägga till rätt behörigheter till din produktprofil. I dokumentationen finns fullständiga instruktioner om [hur du lägger till behörigheter via åtkomstkontrollsgränssnittet](../access-control/ui/permissions.md).

Beskrivningar av behörigheter finns i avsnittet [tillgängliga behörigheter](#available-permissions) tidigare i det här dokumentet.

>[!NOTE]
>
>Du behöver inte aktivera alla behörigheter för alla användare. Beroende på din organisations struktur kanske du vill skapa separata produktprofiler för vissa användare och bevilja begränsad åtkomst (till exempel skrivskyddad). Läs dokumentationen om hur du hanterar användare för en produktprofil om du vill veta mer om [hur du tilldelar behörigheter för specifika användare](../access-control/ui/users.md).

När du har lagt till de nödvändiga åtkomstbehörigheterna kan användare i organisationen börja visa kontrollpaneler i Experience Platform-gränssnittet och utföra andra åtgärder baserat på de behörigheter som du har tilldelat.
