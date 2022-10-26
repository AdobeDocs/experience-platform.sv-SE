---
title: Versionsinformation om Adobe Experience Platform januari 2020
description: Versionsinformation januari 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 15 januari 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Fälttypsbegränsningar för fält med samma hierarki | När ett XDM-fält har definierats som en viss typ måste alla andra fält med samma namn och hierarki använda samma fälttyp, oavsett vilka klasser eller schemafältgrupper de används i. Om det till exempel finns en fältgrupp för XDM [!DNL Profile] klassen innehåller en `profile.age` fält av typen &quot;integer&quot;, en liknande fältgrupp för XDM [!DNL ExperienceEvent] kan inte ha `profile.age` fält av typen &quot;string&quot;. Om du vill använda en annan fälttyp måste fältet ha en annan hierarki än det tidigare definierade fältet (till exempel `profile.person.age`). Den här funktionen är avsedd att förhindra konflikter när scheman sammanförs i en union. Begränsningen påverkar inte befintliga scheman retroaktivt, men vi rekommenderar att du granskar dina scheman för konflikter mellan fälttyper och redigerar dem om det behövs. |
| Skiftlägeskänslig fältvalidering | Anpassade fält på samma nivå måste ha olika namn, oavsett skiftläge. Om du till exempel lägger till ett anpassat fält med namnet&quot;E-post&quot; kan du inte lägga till ett annat anpassat fält på samma nivå med namnet&quot;e-post&quot;. |

**Kända fel**

* Ingen

Mer information om hur du arbetar med XDM med [!DNL Schema Registry] API och [!DNL Schema Editor] användargränssnittet, läs [XDM-systemdokumentation](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful-API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service]kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessregler.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| [!DNL Privacy Service] omprofilering | Det tidigare namnet&quot;GDPR Service&quot; har ändrats till [!DNL Privacy Service] eftersom tjänsten har växt till att stödja andra bestämmelser utöver GDPR. |
| Nya API-slutpunkter | Grundsökväg för [!DNL Privacy Service] API har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs`. |
| Nytt krävs `regulation` property | När nya jobb skapas i [!DNL Privacy Service] API, en `regulation` egenskapen måste anges i nyttolasten för att ange vilken regel som ska gälla för att spåra jobbet under. Godkända värden är `gdpr` och `ccpa`. |
| Stöd för [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] nu accepterar begäranden om åtkomst/borttagning från Adobe [!DNL Primetime Authentication], använda `primetimeAuthentication` som produktvärde. |
| Förbättringar av användargränssnittet för Privacy Service | Separata jobbspårningssidor för GDPR- och CCPA-regler. Ny **Regeltyp **listruta för att växla mellan spårningsdata för GDPR och CCPA. |

**Kända fel**

* Ingen

Mer information om [!DNL Privacy Service], kan du börja med att läsa [Översikt över Privacy Servicen](../../privacy-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Stöd för kundattributdata | Gränssnitt och API-stöd för att skapa direktuppspelningsanslutningar för import av kundattributdata. |
| Ytterligare filformatsstöd för molnlagring | Inläsning av filer från molnlagring har nu stöd för XDM-kompatibla filformaten Parquet och JSON. |
| Stöd för åtkomstkontrollsbehörigheter | Ramverket för åtkomstkontroll i Adobe Experience Platform ger de behörigheter som krävs för att ge åtkomst till källor vid dataöverföring. Beroende på behörighetsnivå kan en användare visa källor, hantera källor eller nekas helt åtkomst. |

**Åtkomstkontrollbehörigheter**

| Kategori | Behörighet | Beskrivning |
|--- | --- | ---|
| Dataintag | Hantera källor | Tillgång till att läsa, skapa, redigera och inaktivera källor. |
| Dataintag | Visa källor | Skrivskyddad åtkomst till tillgängliga källor i **[!UICONTROL Catalog]** och autentiserade källor i **[!UICONTROL Browse]** -fliken. |

**Kända fel**

* Ingen

Mer information om källor finns i [källöversikt](../../sources/home.md)

## Mål  {#destinations}

I [Real-Time CDP](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Stöd för åtkomstkontrollsbehörigheter | Funktionen Destinationer i Real-Time CDP fungerar med Adobe Experience Platform åtkomstkontrollsbehörigheter. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. |

**Åtkomstkontrollbehörigheter**

| Kategori | Behörighet | Beskrivning |
|--- | --- | ---|
| Mål  | Hantera mål | Åtkomst för att läsa, skapa, redigera och inaktivera mål. |
| Mål  | Visa mål | Skrivskyddad åtkomst till tillgängliga destinationer i **[!UICONTROL Catalog]** och autentiserade mål på **Bläddra** -fliken. |
| Mål  | Aktivera destinationer | Möjlighet att aktivera data till destinationer. Den här behörigheten kräver att antingen Hantera destinationer eller Visa destinationer läggs till i produktprofilen. |

**Kända fel**

* Ingen

Se [Översikt över destinationer](../../destinations/home.md) för mer information.
