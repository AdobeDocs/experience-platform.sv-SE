---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Självstudiekurser i kundprofil i realtid
topic: tutorial
type: Tutorial
description: I det här dokumentet beskrivs de olika stegen och det finns länkar till självstudiekurser för att slutföra varje enskilt arbetsflöde.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---


# Konfigurera [!DNL Real-time Customer Profile] och [!DNL Identity Service]

För att kunna konfigurera [!DNL Real-time Customer Profile] för din organisation måste du slutföra flera separata arbetsflöden. I det här dokumentet beskrivs de olika stegen och det finns länkar till självstudiekurser för att slutföra varje enskilt arbetsflöde.

Om du vill veta mer [!DNL Real-time Customer Profile]börjar du med att läsa [profilöversikten](../profile/home.md).

## Översikt över användargränssnittet för kundprofil i realtid

Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata.

**Den här guiden hjälper dig att:**
- Förstå [!UICONTROL Profiles] användargränssnittet och tillgängliga funktioner.
- Visa och hantera profildata.

Mer information finns i användarhandboken för [kundprofiler i realtid](../profile/ui/user-guide.md)

## Kundprofil-API i realtid

Real-time Customer Profile API innehåller flera slutpunkter. Med en profil kan ni sammanställa olika kunddata från flera olika kanaler, t.ex. online-, offline-, CRM- och tredjepartsdata, i en enhetlig vy med ett användbart tidsstämplat konto för varje kundinteraktion. Läs översikten [över kundprofils-API:t i](../profile/api/overview.md) realtid om du vill ha mer information om de tillgängliga slutpunkterna och deras användningsfall.

**Följande API-utvecklarhandböcker är tillgängliga:**
- [Beräknade attribut (alfa) ](../profile/api/computed-attributes.md) - Lär dig mer om användningsexempel för beräknade attribut samt hur du konfigurerar, får tillgång till, uppdaterar och tar bort ett beräknat attribut.
- [Kantprojektioner](../profile/api/edge-projections.md) - Lär dig hur du skapar, visar, uppdaterar, tar bort och listar projektionsmål. Det här dokumentet innehåller även information om hur du listar och skapar projektionskonfigurationer och exempel på hur du använder väljare.
- [Enheter (profilåtkomst)](../profile/api/entities.md) - Lär dig hur du får åtkomst till profildata via identitet eller en lista med identiteter. Lär dig även hur du får åtkomst till tidsseriehändelser för flera profiler med hjälp av identiteter, en profil per identitet och får åtkomst till flera schemaentiteter.
- [Exportera jobb (profilexport)](../profile/api/export-jobs.md) - Lär dig hur du skapar, visar, övervakar och avbryter exportjobb.
- [Sammanslagningsprinciper](../profile/api/merge-policies.md) - Lär dig mer om komponenterna i sammanfogningsprinciper samt hur du får tillgång till, skapar, uppdaterar och tar bort en sammanfogningsprincip.
- [Förhandsgranska exempelstatus (förhandsgranskning av profil)](../profile/api/preview-sample-status.md) - Lär dig hur du visar din senaste exempelstatus, listar profildistribution efter datauppsättning och listar profildistribution efter namnområde.
- [Profilsystemjobb (Delete-begäranden)](../profile/api/profile-system-jobs.md) - Lär dig hur du visar, skapar och tar bort en borttagningsbegäran för en datauppsättning eller batch i profilarkivet.

Om du vill veta mer och få de värden som krävs för att utföra CRUD-åtgärder med kundprofils-API:t i realtid kan du gå till [Komma igång-guiden](../profile/api/getting-started.md).

## Aktivera ett schema för [!DNL Profile] och [!DNL Identity] tjänst

Innan data kan hämtas in till Adobe Experience Platform och användas för att skapa [!DNL Real-time Customer Profiles]måste ett schema skapas för att ge strukturen för de data som ska importeras och det schemat måste aktiveras för användning i [!DNL Profile] och i Adobe Experience Platform [!DNL Identity Service].

**Den här guiden hjälper dig att:**
- Bläddra bland befintliga scheman.
- Skapa och namnge ett schema.
- Lägg till och definiera XDM-mixiner.
- Ange dina schemafält som identitetsfält.
- Aktivera profil för ditt schema.

Stegvisa instruktioner om hur du skapar ett schema som är aktiverat för både [!DNL Profile] och [!DNL Identity Service]finns i självstudiekurserna för att [skapa ett schema med API:t](../xdm/tutorials/create-schema-api.md) för schemaregister eller [skapa ett schema med hjälp av gränssnittet](../xdm/tutorials/create-schema-ui.md)i Schema Builder.

## Konfigurera en datauppsättning för [!DNL Profile] och [!DNL Identity]

För att börja inhämta data i [!DNL Profile]måste du ha en datauppsättning som är korrekt konfigurerad för användning med [!DNL Real-time Customer Profile] och [!DNL Identity Service].

**Den här guiden hjälper dig att:**
- Skapa en datauppsättning aktiverad för profil.
- Konfigurera befintliga datauppsättningar.
- Infoga data i datauppsättningen.
- Bekräfta att datauppsättningen är profilaktiverad och använder identitetstjänsten.

Kom igång genom att följa API-självstudiekursen för att [konfigurera en datauppsättning för profil och identitet](../profile/tutorials/dataset-configuration.md).

## Konfigurera sammanslagningsprinciper

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn.

**Den här guiden hjälper dig att:**
- Skapa nya kopplingsprofiler.
- Hantera befintliga kopplingsprofiler.
- Ange en standardprincip för sammanslagning för din organisation.
- Förstå brott mot sammanslagningsprinciper.

Om du vill arbeta med kopplingsprofiler i [!DNL Platform] användargränssnittet går du till [användarhandboken](../profile/ui/merge-policies.md)för kopplingsprofiler. Om du vill arbeta med sammanfogningsprinciper med hjälp av API:t för kundprofil i realtid läser du i utvecklarhandboken för [sammanfogningsprinciper](../profile/api/merge-policies.md).

## Konfigurera kantprognoser

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe [!DNL Experience Platform] ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten.

**Den här guiden hjälper dig att:**
- Visa, skapa, visa, uppdatera och ta bort en kantprojektionsdestination.
- Visa och skapa en kantprojektionskonfiguration.
- Förstå väljare.

Mer information och information om hur du börjar arbeta med kanter finns i [!DNL Real-time Customer Profile] API:ts [underhandbok om kantprojektioner](../profile/api/edge-projections.md).

## Anpassa hur profildata visas i användargränssnittet

I användargränssnittet i Experience Platform kan ni visa och interagera med kundprofildata i realtid i form av kundprofiler. Profilinformationen som visas i användargränssnittet har sammanfogats från flera profilfragment till en enda vy över varje enskild kund. Detta inkluderar information som grundläggande attribut, länkade identiteter och kanalinställningar. Standardfälten som visas i profiler kan också ändras på organisationsnivå för att visa de önskade profilattributen.

**Den här guiden hjälper dig att:**
- Ändra ordning på, ändra storlek på, redigera och ta bort kort.
- Lägg till attribut.
- Lägg till ett nytt kort.
- Återställ standardvärden.

Mer information om hur du anpassar profildata finns i dokumentationen för [profilanpassning](../profile/ui/profile-customization.md)

## Nästa steg

När ni har konfigurerat [!DNL Real-time Customer Profile] för er organisation kan ni börja lägga till data i enskilda kundprofiler och skapa målgruppssegment baserat på specifika kundattribut. Se följande självstudiekurser för att komma igång:

- [Lägg till data i kundprofilen i realtid](../profile/tutorials/add-profile-data.md)
- [Skapa ett segment](../segmentation/tutorials/create-a-segment.md)