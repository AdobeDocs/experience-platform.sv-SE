---
title: Extern granskning av Source-system
description: Läs mer om den externa fältgruppen Source System Audit Details Experience Data Model (XDM).
exl-id: 6aa154f3-620f-4a2e-9e33-a0757d0491c1
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Fältgrupp [!UICONTROL External Source System Audit Details]

[!UICONTROL External Source System Audit Details] är en XDM-fältgrupp (Standard Experience Data Model) som utökar kärndatatypen External Source System Audit Attributes genom att referera till dess egenskaper och lägga till sammanhangsbaserade metadata. Detta möjliggör detaljerad spårning och flexibel dataintegrering från externa källor.

![Ett schemadiagram över fältgruppen Extern Source-systemgranskningsinformation.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL External Source System Audit Details] | `external-source-system-audit-details` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Fältgruppen [!UICONTROL External Source System Audit Details] utökar datatypen External Source System Audit Attributes genom att referera till dess egenskaper och lägga till sammanhangsbaserade metadata. Detta underlättar detaljerad spårning av granskningar och flexibel dataintegrering för externa källor, vilket underlättar asynkron infogning av profiler. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)
