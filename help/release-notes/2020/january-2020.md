---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 15 januari 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 5199a344a66381ef9d7eea1ea8314e5de7152e3b

---


# Versionsinformation om Adobe Experience Platform

## Releasedatum: 15 januari 2020

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [Experience Data Model (XDM) System](#xdm)
* [Integritetstjänst](#privacy)
* [Källor](#sources)
* [Mål](#destinations)

## Experience Data Model (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Fälttypsbegränsningar för fält med samma hierarki | När ett XDM-fält har definierats som en viss typ måste alla andra fält med samma namn och hierarki använda samma fälttyp, oavsett vilka klasser eller blandningar de används i. Om till exempel en blandning för klassen XDM Profile innehåller ett `profile.age` fält av typen &quot;integer&quot;, kan en liknande blandning för XDM ExperienceEvent inte ha ett `profile.age` fält av typen &quot;string&quot;. Om du vill använda en annan fälttyp måste fältet ha en annan hierarki än det tidigare definierade fältet (till exempel `profile.person.age`). Den här funktionen är avsedd att förhindra konflikter när scheman sammanförs i en union. Begränsningen påverkar inte befintliga scheman retroaktivt, men vi rekommenderar att du granskar dina scheman för konflikter mellan fälttyper och redigerar dem om det behövs. |
| Skiftlägeskänslig fältvalidering | Anpassade fält på samma nivå måste ha olika namn, oavsett skiftläge. Om du till exempel lägger till ett anpassat fält med namnet&quot;E-post&quot; kan du inte lägga till ett annat anpassat fält på samma nivå med namnet&quot;e-post&quot;. |

**Kända fel**

* Ingen

Mer information om hur du arbetar med XDM med API:t för schemaregister och användargränssnittet för Schemaredigeraren finns i [XDM-systemdokumentationen](../../xdm/home.md).

## Integritetstjänst {#privacy}

Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Integritetstjänsten för Adobe Experience Platform tillhandahåller ett RESTful API och användargränssnitt som hjälper er att hantera dessa dataförfrågningar från era kunder. Med Integritetstjänsten kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Omprofilering av integritetstjänsten | Den tidigare benämningen&quot;GDPR-tjänsten&quot; har ändrats till Privacy Service eftersom tjänsten har utvecklats för att stödja andra bestämmelser utöver GDPR. |
| Nya API-slutpunkter | Bassökvägen för sekretesstjänstens API har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs`. |
| Ny obligatorisk `regulation` egenskap | När du skapar nya jobb i sekretesstjänstens API måste en `regulation` egenskap anges i nyttolasten för begäran för att ange vilken regel som ska spåra jobbet under. Godkända värden är `gdpr` och `ccpa`. |
| Stöd för Adobe Primetime-autentisering | Integritetstjänsten accepterar nu begäranden om åtkomst/borttagning från Adobe Primetime Authentication, med `primetimeAuthentication` som produktvärde. |
| Förbättringar av användargränssnittet för sekretesstjänster | Separata jobbspårningssidor för GDPR- och CCPA-regler. Ny _regeltypsmeny_ för att växla mellan spårningsdata för GDPR och CCPA. |

**Kända fel**

* Ingen

Mer information om sekretesstjänsten finns i översikten över [sekretesstjänsten](../../privacy-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som ni kan strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, programvara från tredje part och ditt CRM-system.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

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
| Dataintag | Visa källor | Skrivskyddad åtkomst till tillgängliga källor på fliken *Katalog* och autentiserade källor på fliken *Bläddra* . |

**Kända fel**

* Ingen

Mer information om källor finns i [Källor - översikt](../../sources/home.md)

## Mål {#destinations}

I [Adobe Real-time CDP](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Stöd för åtkomstkontrollsbehörigheter | Funktionen Destinationer i CDP i realtid fungerar med åtkomstkontrollsbehörigheter i Adobe Experience Platform. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. |

**Åtkomstkontrollbehörigheter**

| Kategori | Behörighet | Beskrivning |
|--- | --- | ---|
| Mål  | Hantera mål | Åtkomst för att läsa, skapa, redigera och inaktivera mål. |
| Mål  | Visa mål | Skrivskyddad åtkomst till tillgängliga mål på fliken _Katalog_ och autentiserade mål på fliken _Bläddra_ . |
| Mål  | Aktivera destinationer | Möjlighet att aktivera data till destinationer. Den här behörigheten kräver att antingen Hantera destinationer eller Visa destinationer läggs till i produktprofilen. |

**Kända fel**

* Ingen

Mer information finns i Översikt över [](../../rtcdp/destinations/destinations-overview.md) Destinationer.