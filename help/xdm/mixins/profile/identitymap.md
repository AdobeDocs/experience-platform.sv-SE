---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: IdentityMap-blandning
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: fd5bd4134bd35d5d87c79bf1e75bc88c67511b2b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] blanda

[!UICONTROL IdentityMap] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). MixIn innehåller ett enda kartfält som innehåller en uppsättning användaridentiteter som skrivs med namnutrymme.

>[!WARNING]
>
>Fältet uppdateras automatiskt av systemet när `IdentityMap` identitetsdata hämtas. Om du vill kunna använda det här fältet för kundprofil [i](../../../profile/home.md)realtid ska du inte försöka uppdatera fältets innehåll manuellt i dataåtgärderna.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

I avsnittet om identitetskartor i [grunderna för schemakomposition](../../schema/composition.md#identityMap) finns mer information om hur de används.