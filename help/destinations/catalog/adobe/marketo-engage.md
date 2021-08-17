---
title: Marketo Engage destination
description: Marketo Engage är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# (Beta) Marketo Engage {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>Destination Marketo Engage i Adobe Experience Platform är för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

## Översikt {#overview}

Marketo Engage är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.

Segmentkopplingen gör det möjligt för marknadsförare att skicka segment som skapats i Adobe Experience Platform till Marketo där de visas som statiska listor.

## Identiteter som stöds {#supported-identities}

| Målidentitet | Beskrivning |
|---|---|
| ECID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras till av följande alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Mer information finns i följande dokument på [ECID](/help/identity-service/ecid.md). |
| E-post | Ett namnutrymme som representerar en e-postadress. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |

## Exporttyp {#export-type}

Segmentexport - du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i Marketo Engage-målet.

## Konfigurera {#set-up}

Instruktioner om hur du ställer in målet [finns här](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en).

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

## Dataanvändning och -styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] framtvingar datastyrning finns i [Datastyrningsöversikten](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till mål.
