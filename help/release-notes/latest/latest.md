---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation från februari 2023 för Adobe Experience Platform.
source-git-commit: ff276de35ca2aaeec168f4c4386d849f3352ad57
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 22 februari 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Frågetjänst](#query-service)
- [Relaterade konton i Real-Time CDP B2B Edition](#related-accounts)
- [Källor](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner** {#destinations-new-updated-features}

| Funktion | Beskrivning |
| ----------- | ----------- |
| [Förbättrad profil för samtycke](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) för integrering med [filbaserade (batch) mål](/help/destinations/destination-types.md#file-based) | <p> När profiler inte längre är kvalificerade för en samtyckespolicy meddelar Experience Platform nu aktivt sin policy att avsluta sina filbaserade destinationer. Detta följer [från februari 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) av samma funktionalitet för direktuppspelningsdestinationer. </p> <p> <b>Anteckning</b>: Den här funktionen är endast tillgänglig för kunder som har **[!UICONTROL Privacy and Security Shield]** och **[!UICONTROL Healthcare Shield]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Ny eller uppdaterad dokumentation** {#destinations-new-updated-documentation}

| Dokumentation | Beskrivning |
| ----------- | ----------- |
| Dokumentation om hur destinationer fungerar | <p>Vi har publicerat tre nya artiklar om hur destinationer fungerar, baserat på vanliga frågor från användarna:</p> <p><ul><li>[Konfigurerbara och gemensamma exportinställningar för destinationer](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Profilexportbeteende för olika måltyper](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Identitetshantering i arbetsflödet för målaktivering](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Uppdaterade funktioner**
&#x200B; | Funktion | Beskrivning | | — | — | | Borttagning av fält via användargränssnittet | Du kan nu ersätta fält från dina scheman efter att data har importerats. Med XDM-fältborttagning kan du ta bort fält från användargränssnittsvyn samtidigt som du behåller dem för användning. Du kan visa inaktuella fält igen om det behövs, och eventuella segment, frågor eller lösningar längre fram i kedjan som refererar till fälten kommer att fungera som vanligt. |

{style=&quot;table-layout:auto&quot;} &#x200B; Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md). &#x200B;
<!-- Field deprecation: https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation.html -->

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform [!DNL Data Lake]. Du kan ansluta alla datauppsättningar från datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas i rapporter, Data Science Workspace eller för att matas in i kundprofilen i realtid.

**Uppdaterade funktioner**
&#x200B; | Funktion | Beskrivning | | — | — | | Aktivera datauppsättningar för profil med SQL | Använd LABEL i CTAS-frågor för att göra en datauppsättning &quot;profile enabled&quot;, eller använd ALTER för att uppdatera befintliga datauppsättningar som ska aktiveras för profilen. | | Övervaka schemalagda frågor | Använd fliken Schemalagda frågor för att hitta viktig information om frågekörningar och prenumerera på aviseringar. Övervaka frågor för schemainformation, status och felmeddelanden/koder om de misslyckas.  | | Funktionen Komplettera automatiskt | Eliminera vissa metadatakommandon och förbättra bearbetningstiden genom att växla funktionen för automatisk komplettering av frågeredigeraren. Den här funktionen föreslår automatiskt möjliga SQL-nyckelord och tabelldetaljer för frågan när du skriver den. | | Datauppsättningsexempel | Ange en samplingsfrekvens i frågan och använd datauppsättningsexempel för att skapa ett enhetligt slumpmässigt urval, eller skapa villkorsstyrda exempel baserat på specifika kriterier. |

{style=&quot;table-layout:auto&quot;} &#x200B; Mer information om Query Services finns i [Översikt över frågetjänsten](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Relaterade konton i Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>Funktionen för relaterade konton är endast tillgänglig för kunder som har Real-Time CDP B2B Edition.

Närliggande konton, [!DNL Real-Time CDP B2B] gör att du kan visa en lista med konton som liknar det konto du bläddrar i. Du kan inkludera de relaterade kontona i dina segmentdefinitioner för att bredda din räckvidd eller tillämpa fler kriterier i dina segment.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aktivera tjänsten för relaterade konton | Med den nya växlingsfunktionen kan du aktivera den relaterade kontotjänsten på ditt konto. Mer information finns i guiden [aktivera tjänsten för relaterade konton](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Läs mer om funktionerna för relaterade konton på följande dokumentationssidor:

- [Samhörande konton i Real-Time CDP B2B Edition - översikt](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Fliken Relaterade konton i gränssnittsguiden för kontoprofiler](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Så här använder du relaterade konton i segmentdefinitioner](../../rtcdp/segmentation/b2b.md#related-accounts)

Läs mer om Real-Time CDP B2B Edition i [Real-Time CDP B2B Edition - översikt](../../rtcdp/overview.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ange åtkomst på prenumerationsnivå med [!DNL Google PubSub] | Nu kan du definiera åtkomst till en specifik ämnesprenumeration när du använder [!DNL Google PubSub] genom att ange prenumerations-ID vid autentisering. Mer information finns i [!DNL Google PubSub] självstudiekurs om autentisering [med API:t för Flow Service](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) eller [Plattformsgränssnitt](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Infoga anpassade aktivitetsdata från [!DNL Marketo] | Nu kan du hämta anpassade aktivitetsdata från [!DNL Marketo] -instans till Experience Platform. Om du vill importera anpassade aktivitetsdata måste du skapa anpassade aktivitetsfältgrupper i B2B-aktivitetsschemat och skapa ett dataflöde med aktivitetsdatauppsättningen. När dataflödet är klart innehåller den inkapslade datauppsättningen både standardaktiviteter och anpassade aktiviteter från din [!DNL Marketo] -instans. Du kan sedan använda [Frågetjänst](../../query-service/home.md) för att få tillgång till dina anpassade aktivitetsposter på Platform. Mer information finns i guiden [skapa ett dataflöde för anpassade aktivitetsdata](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Exkludera ej begärda konton från [!DNL Marketo] | Du kan nu konfigurera om du vill exkludera eller ta med ej ianspråktagna konton från inmatningen när du skapar ett dataflöde för företagsdata. Mer information finns i guiden [skapa en källanslutning och ett dataflöde för [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Läs mer om källor i [källöversikt](../../sources/home.md).