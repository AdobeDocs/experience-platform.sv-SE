---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;relationship;field;
solution: Experience Platform
title: Definiera relationsfält i användargränssnittet
description: Lär dig hur du definierar ett relationsfält i användargränssnittet i Experience Platform.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definiera relationsfält i användargränssnittet

I Experience Data Model (XDM) är ett [union-schema](../../schema/composition.md#union) en enhetlig vy över alla scheman som tillhör samma klass och som också har aktiverats för [kundprofil i realtid](../../../profile/home.md). Unionsschemat utnyttjas av Profil för att skapa en fullständig representation av en kund utifrån olika upplevelsedata.

I vissa fall kanske du vill importera data som inte nödvändigtvis är en del av en profil, men ändå är relaterade till profilen. Ett exempel på den här typen av data skulle vara ett&quot;favorithotell&quot; för en kund. Eftersom attributen för en persons favorithotell inte är attribut för personen i sig, representeras ett hotell bäst av ett separat schema som baseras på en anpassad klass i stället för [!DNL XDM Individual Profile].

Eftersom unionsscheman bara baseras på scheman som delar samma klass, kommer det inte att ingå i deras fältsunionsschema för [!DNL XDM Individual Profile] om du aktiverar Hotels-schemat för användning i profilen. I stället måste du definiera en relation mellan&quot;Hotels&quot; och ett annat schema som tillhör unionen. Detta innebär att definiera ett **relationsfält** i ett källschema som refererar till den primära identiteten i ett referensschema.

Detaljerade steg för hur du definierar en relation mellan två scheman i Adobe Experience Platform-gränssnittet finns i självstudiekursen [för relationsgränssnittet](../../tutorials/relationship-ui.md).
