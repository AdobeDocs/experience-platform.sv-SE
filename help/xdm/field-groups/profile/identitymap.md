---
keywords: Experience Platform;home;populära topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;union schema;union schema
title: Fältgrupp för IdentityMap-schema
description: Lär dig mer om klassen XDM Individual Profile.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL IdentityMap]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL IdentityMap] är en standardschemafältgrupp för [[!UICONTROL XDM ExperienceEvent] class ](../../classes/experienceevent.md) och en kompatibel fältgrupp för [[!UICONTROL XDM Individual Profile] class](../../classes/individual-profile.md). Fältgruppen innehåller ett enda mappningsfält som innehåller en uppsättning användaridentiteter som angetts av namnutrymmet.

![Ett diagram över [!UICONTROL IdentityMap] schemafältgruppen ](../../images/field-groups/identitymap.png)

I avsnittet om identitetskartor i [grunderna för schemakomposition](../../schema/composition.md#identityMap) finns mer information om användningsfall, inklusive fördelar och nackdelar.

**exempel**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Mer information om fältgruppen finns i det [fullständiga schemat](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) i den offentliga XDM-databasen.
