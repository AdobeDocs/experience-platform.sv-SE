---
keywords: Experience Platform;hem;populära ämnen;Kundprofil i realtid;Identitetstjänst;
solution: Experience Platform
title: Självstudiekurser i kundprofil i realtid
topic: självstudiekurs
type: Självstudiekurs
description: I det här dokumentet beskrivs de olika stegen och det finns länkar till självstudiekurser för att slutföra varje enskilt arbetsflöde.
translation-type: tm+mt
source-git-commit: 0aa59a5375757f81d63ac43d778ff2c7179d449b
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---


# Konfigurera [!DNL Real-time Customer Profile]

Om du vill konfigurera [!DNL Real-time Customer Profile] för din organisation måste du slutföra flera separata arbetsflöden. I det här dokumentet beskrivs de olika stegen och det finns länkar till självstudiekurser för att slutföra varje enskilt arbetsflöde.

Om du vill veta mer om [!DNL Real-time Customer Profile] börjar du med att läsa [profilöversikten](../profile/home.md).

## Översikt över användargränssnittet för kundprofil i realtid

Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata.

**Den här guiden hjälper dig att:**
- Förstå användargränssnittet för [!UICONTROL Profiles] och tillgängliga funktioner.
- Visa och hantera profildata.

Mer information finns i [Användarhandbok för kundprofil i realtid](../profile/ui/user-guide.md)

## Kundprofil-API i realtid

Real-time Customer Profile API innehåller flera slutpunkter. Läs översikten [Kundprofil-API i realtid](../profile/api/overview.md) om du vill ha mer information om de tillgängliga slutpunkterna och deras användningsfall.

Om du vill veta mer och få de värden som krävs för att utföra CRUD-åtgärder med kundprofils-API:t i realtid kan du gå till [guiden ](../profile/api/getting-started.md) Komma igång.

## Aktivera ett schema för tjänsten [!DNL Profile] och [!DNL Identity]

Innan data kan importeras till Adobe Experience Platform och användas när [!DNL Real-time Customer Profiles] skapas, måste ett schema skapas för att ge strukturen för de data som ska importeras och det schemat måste aktiveras för användning i [!DNL Profile] och Adobe Experience Platform [!DNL Identity Service].

**Den här guiden hjälper dig att:**
- Bläddra bland befintliga scheman.
- Skapa och namnge ett schema.
- Lägg till och definiera XDM-mixiner.
- Ange dina schemafält som identitetsfält.
- Aktivera profil för ditt schema.

Stegvisa instruktioner om hur du skapar ett schema som är aktiverat för både [!DNL Profile] och [!DNL Identity Service] finns i självstudiekurserna för [att skapa ett schema med API:t för schematabellen](../xdm/tutorials/create-schema-api.md) eller [skapa ett schema med hjälp av gränssnittet för Schema Builder](../xdm/tutorials/create-schema-ui.md).

## Konfigurera en datauppsättning för [!DNL Profile] och [!DNL Identity]

Om du vill börja inhämta data i [!DNL Profile] måste du ha en datauppsättning som har konfigurerats korrekt för användning med [!DNL Real-time Customer Profile] och [!DNL Identity Service].

**Den här guiden hjälper dig att:**
- Skapa en datauppsättning aktiverad för profil.
- Konfigurera befintliga datauppsättningar.
- Infoga data i datauppsättningen.
- Bekräfta att datauppsättningen är profilaktiverad och använder identitetstjänsten.

Kom igång genom att följa API-självstudiekursen för [konfigurera en datauppsättning för profil och identitet](../profile/tutorials/dataset-configuration.md).

## Konfigurera sammanslagningsprinciper

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanfogar dessa data är sammanfogningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn.

**Den här guiden hjälper dig att:**
- Skapa nya kopplingsprofiler.
- Hantera befintliga kopplingsprofiler.
- Ange en standardprincip för sammanslagning för din organisation.
- Förstå brott mot sammanslagningsprinciper.

Om du vill arbeta med sammanfogningsprinciper i användargränssnittet för [!DNL Platform] går du till [användarhandboken för sammanfogningsprinciper](../profile/ui/merge-policies.md). Mer information om hur du arbetar med sammanfogningsprinciper med hjälp av API:t för kundprofil i realtid finns i [Utvecklarhandbok för sammanfogningsprinciper](../profile/api/merge-policies.md).

## Konfigurera kantprognoser

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe [!DNL Experience Platform] ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten.

**Den här guiden hjälper dig att:**
- Visa, skapa, visa, uppdatera och ta bort en kantprojektionsdestination.
- Visa och skapa en kantprojektionskonfiguration.
- Förstå väljare.

Mer information och information om hur du börjar arbeta med kanter finns i [!DNL Real-time Customer Profile] API [underhandboken om kantprojektioner](../profile/api/edge-projections.md).

## Anpassa hur profildata visas i användargränssnittet

I användargränssnittet i Experience Platform kan ni visa och interagera med kundprofildata i realtid i form av kundprofiler. Profilinformationen som visas i användargränssnittet har sammanfogats från flera profilfragment till en enda vy över varje enskild kund. Detta inkluderar information som grundläggande attribut, länkade identiteter och kanalinställningar. Standardfälten som visas i profiler kan också ändras på organisationsnivå för att visa de önskade profilattributen.

**Den här guiden hjälper dig att:**
- Ändra ordning på, ändra storlek på, redigera och ta bort kort.
- Lägg till attribut.
- Lägg till ett nytt kort.
- Återställ standardvärden.

Mer information om hur du anpassar profildata finns i [dokumentationen för profilanpassning](../profile/ui/profile-customization.md)

## Nästa steg

När du har konfigurerat [!DNL Real-time Customer Profile] för din organisation kan du börja lägga till data i enskilda kundprofiler och skapa målgruppssegment baserat på specifika kundattribut. Se följande självstudiekurser för att komma igång:

- [Lägg till data i kundprofilen i realtid](../profile/tutorials/add-profile-data.md)
- [Skapa ett segment](../segmentation/tutorials/create-a-segment.md)