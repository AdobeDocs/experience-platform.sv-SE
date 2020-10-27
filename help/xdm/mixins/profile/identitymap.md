---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: IdentityMap-blandning
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] blanda

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om uppdatering [av](../name-updates.md) blandade namn.

[!UICONTROL IdentityMap] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). MixIn innehåller ett enda kartfält som innehåller en uppsättning användaridentiteter som skrivs med namnutrymme.

>[!WARNING]
>
>Fältet uppdateras automatiskt av systemet när `IdentityMap` identitetsdata hämtas. Om du vill kunna använda det här fältet för kundprofil [i](../../../profile/home.md)realtid ska du inte försöka uppdatera fältets innehåll manuellt i dataåtgärderna.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

I avsnittet om identitetskartor i [grunderna för schemakomposition](../../schema/composition.md#identityMap) finns mer information om hur de används.