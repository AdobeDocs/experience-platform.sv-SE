---
description: På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/testing/template/sample` för att få en testmeddelandetransformeringsmall för ditt mål.
title: Hämta API-åtgärder för exempelmallar
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Hämta API-åtgärder för exempelmallar {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API-slutpunkt**:  `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/testing/template/sample` för att generera en [meddelandetransformeringsmall](./message-format.md#using-templating) för ditt mål. En beskrivning av de funktioner som stöds av den här slutpunkten finns i [skapa mall](./create-template.md).

## Komma igång med API-åtgärder för exempelmallar {#get-started}

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Hämta exempelmall {#generate-sample-template}

Du kan hämta en exempelmall genom att göra en GET-förfrågan till `authoring/testing/template/sample/`-slutpunkten och ange mål-ID:t för målkonfigurationen som du skapar mallen utifrån.

>[!TIP]
>
>* Det mål-ID som du bör använda här är det `instanceId` som motsvarar en målkonfiguration, som skapas med slutpunkten `/destinations`. Se [API-referens för målkonfiguration](./destination-configuration-api.md#retrieve-list).


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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en exempelmall som du kan redigera för att matcha det förväntade dataformatet.

Om det mål-ID som du anger motsvarar en målservermall med `maxUsersPerRequest=1` returnerar begäran en exempelmall som liknar den här:

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
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Om det mål-ID som du anger motsvarar en målservermall med `maxUsersPerRequest` större än en, returnerar begäran en exempelmall som liknar den här:

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
                {#- Alternative syntax for filtering segments by status: -#}
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

SDK API-målslutpunkterna följer de allmänna felmeddelandeprinciperna för Experience Platform-API. Se [API-statuskoder](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) och [begäranrubrikfel](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du genererar en meddelandetransformeringsmall med API-slutpunkten `/authoring/testing/template/sample`. Sedan kan du använda [API-slutpunkten för återgivningsmallen](./render-template-api.md) för att generera exporterade profiler baserat på mallen och jämföra dem med målets förväntade dataformat.