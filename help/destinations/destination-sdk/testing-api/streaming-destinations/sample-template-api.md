---
description: Lär dig hur du använder API:t för måltestning för att generera en omformningsmall för testmeddelanden för ditt mål.
title: Generera en omformningsmall för exempelmeddelanden
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Generera en omformningsmall för exempelmeddelanden {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API-slutpunkt**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/testing/template/sample` för att generera en [meddelandetransformeringsmall](../../functionality/destination-server/message-format.md#using-templating) för ditt mål. En beskrivning av de funktioner som stöds av den här slutpunkten finns i [Skapa mall](create-template.md).

## Komma igång med API-åtgärder för exempelmallar {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Hämta exempelmall {#generate-sample-template}

Du kan hämta en exempelmall genom att göra en GET-förfrågan till `authoring/testing/template/sample/`-slutpunkten och ange mål-ID:t för målkonfigurationen baserat på vilken du skapar mallen.

>[!TIP]
>
>* Mål-ID som du bör använda här är `instanceId` som motsvarar en målkonfiguration, som skapas med slutpunkten `/destinations`. Mer information finns i [Hämta en målkonfiguration](../../authoring-api/destination-configuration/retrieve-destination-configuration.md).

**API-format**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID:t för målkonfigurationen som du genererar en meddelandetransformeringsmall för. |

**Begäran**

Följande begäran genererar en ny exempelmall som konfigurerats med parametrarna i nyttolasten.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en exempelmall som du kan redigera för att matcha det förväntade dataformatet.

Om det mål-ID som du anger motsvarar en målkonfiguration med [bästa ansträngningsaggregering](../../functionality/destination-configuration/aggregation-policy.md) och `maxUsersPerRequest=1` i aggregeringsprincipen returnerar begäran en exempelmall som liknar den här:

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Om det mål-ID som du anger motsvarar en målservermall med [konfigurerbar aggregering](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) eller [bästa ansträngningsaggregering](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) med `maxUsersPerRequest` större än en, returnerar begäran en exempelmall som liknar denna:

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering audiences by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du genererar en meddelandetransformeringsmall med API-slutpunkten `/authoring/testing/template/sample`. Sedan kan du använda [Återgivningsmallens API-slutpunkt](render-template-api.md) för att generera exporterade profiler som är baserade på mallen och jämföra dem med målets förväntade dataformat.
