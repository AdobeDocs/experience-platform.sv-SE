---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Självstudiekurser i kundprofil i realtid
topic: tutorial
type: Tutorial
description: I det här dokumentet beskrivs de olika stegen och det finns länkar till självstudiekurser för att slutföra varje enskilt arbetsflöde.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Konfigurera [!DNL Real-time Customer Profile] och [!DNL Identity Service]

För att kunna konfigurera [!DNL Real-time Customer Profile] för din organisation måste du slutföra flera separata arbetsflöden. I det här dokumentet beskrivs de olika stegen och det finns länkar till självstudiekurser för att slutföra varje enskilt arbetsflöde. Om du vill veta mer [!DNL Real-time Customer Profile]börjar du med att läsa [profilöversikten](../profile/home.md).

## Aktivera schema för [!DNL Profile] och [!DNL Identity]

Innan data kan hämtas in till Adobe Experience Platform och användas för att skapa [!DNL Real-time Customer Profiles]måste ett schema skapas för att ge strukturen för de data som ska importeras och det schemat måste aktiveras för användning i [!DNL Profile] och i Adobe Experience Platform [!DNL Identity Service]. Stegvisa instruktioner om hur du skapar ett schema som är aktiverat för både [!DNL Profile] och [!DNL Identity Service]finns i självstudiekurserna för att [skapa ett schema med API:t](../xdm/tutorials/create-schema-api.md) för schemaregister eller [skapa ett schema med hjälp av gränssnittet](../xdm/tutorials/create-schema-ui.md)i Schema Builder.

## Konfigurera en datauppsättning för [!DNL Profile] och [!DNL Identity]

För att börja inhämta data i [!DNL Profile]måste du ha en datauppsättning som är korrekt konfigurerad för användning med [!DNL Real-time Customer Profile] och [!DNL Identity Service]. Kom igång genom att följa självstudiekursen [Konfigurera en datauppsättning för profil och identitet](../profile/tutorials/dataset-configuration.md).

## Konfigurera sammanslagningsprinciper

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Om du vill arbeta med kopplingsprofiler i [!DNL Platform] användargränssnittet går du till [användarhandboken](../profile/ui/merge-policies.md)för kopplingsprofiler. Om du vill arbeta med sammanfogningsprinciper med hjälp av API:t för kundprofil i realtid läser du i utvecklarhandboken för [sammanfogningsprinciper](../profile/api/merge-policies.md).

## Konfigurera kantprognoser

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe [!DNL Experience Platform] ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Mer information och information om hur du börjar arbeta med kanter finns i [!DNL Real-time Customer Profile] API:ts [underhandbok om kantprojektioner](../profile/api/edge-projections.md).

## Nästa steg

När ni har konfigurerat [!DNL Real-time Customer Profile] för er organisation kan ni börja lägga till data i enskilda kundprofiler och skapa målgruppssegment baserat på specifika kundattribut. Se följande självstudiekurser för att komma igång:

* [Lägg till data i kundprofilen i realtid](../profile/tutorials/add-profile-data.md)
* [Skapa ett segment](../segmentation/tutorials/create-a-segment.md)