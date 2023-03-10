---
keywords: Experience Platform;hem;populära ämnen;enhetliga taggar;taggar;
title: (Beta) Översikt över enhetliga taggar
description: Det här dokumentet innehåller information om enhetliga taggar i Adobe Experience Platform
source-git-commit: 6f9787909b8155d2bf032b4a42483f2cb4d44eb4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# (Beta) Översikt över enhetliga taggar

>[!IMPORTANT]
>
>Enhetliga taggar finns i betaversionen. Om du vill lämna feedback markerar du knappen längst upp på sidan Taggar och admin.

Taggar är en funktion i Adobe Experience Platform som gör det möjligt för administratörer att hantera taxonomier för att klassificera affärsobjekt för enklare identifiering och kategorisering. Taggar är metadata som kan tolkas som nyckelord som kan bifogas till ett segment, en datauppsättning, en resa eller andra objekt för att göra det möjligt att söka efter det objektet och relaterade objekt. Taggar delas in i två typer: kategoriserad och okategoriserad.

För att ge ett mer sammanhang och definiera syftet med en tagg organiserar kategorier taggar i användbara uppsättningar. En administratör definierar vilka kategoriserade taggar som är tillgängliga för användare att lägga till i objekt. Nya taggar som inte innehåller kategorier kan också skapas infogade i arbetsflöden där taggar används. Dessa taggar visas i den okategoriserade delen av tagglagret. Taggar kan användas av både administratörer och användare, oavsett vem som skapade dem. Alla typer av taggar är tillgängliga för markering när du tilldelar till ett objekt, söker eller filtrerar.

## Märkordsterminologi

Följande komponenter ingår när du taggar:

| Terminologi | Definition |
| --- | --- |
| Arkiverad | Ett läge för en tagg som behåller aktuella associationer med objekt men begränsar taggen från att tillämpas på ytterligare objekt.  Arkiverade taggar är dolda i taggväljaren. |
| Objekt | Ett Experience Cloud-objekt som kan ha en tagg.  Exempel: Segment, resa, datauppsättning. |
| Tagg | Taggar är metadata och kan betraktas som nyckelord som kan kopplas till ett segment, en datauppsättning, en resa eller andra objekt för att göra det möjligt att söka efter det objektet och relaterade objekt. |
| Kategorin Tagg | Tagga Kategorier grupperar taggar i meningsfulla uppsättningar för att ge ett större sammanhang eller beskriva syftet med taggen.  Administratörer hanterar taggkategorier och taggar inom kategorier. |
| Okategoriserad tagg | En ny tagg som skapas online där märkord används. Dessa taggar kan skapas och användas av alla användare, men de är inte bundna till någon kategori.  Administratörer kan flytta dessa taggar till en kategori för att anpassa dem till andra liknande taggar. |

## Märkordslager

Taggkategori och tagghantering med hjälp av tagglagret är tillgängligt i navigeringen Experience Platform och Journey Optimizer. Ändringar av taggar i lagret återspeglas i alla objekt som stöder taggar. Alla användare kan komma åt och bläddra i tagglagret, men tagghanteringen är begränsad till system- och produktadministratörer.

Tagglagret har tre nivåer av hierarki, vilket gör att användare kan hantera taggkategorier, taggar inom en kategori och enskilda taggar. När du hanterar en enskild tagg kan användarna visa och navigera till objekt där taggen används.

### Märkordskategorier

Kategorier grupperar taggar i meningsfulla uppsättningar för att ge ett större sammanhang eller beskriva syftet med taggen. För alla taggar med en kategori kommer kategorinamnet följt av ett kolon före taggnamnet.

Följande åtgärder är möjliga när du använder taggkategorier:

* [Skapa taggkategori](./ui/tags-categories.md#create-tag-category)
* [Redigera taggkategori](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Ta bort taggkategori](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Hantera taggar inom en kategori

>[!NOTE]
>
>För att kunna hantera taggar för Experience Cloud måste du vara systemadministratör eller produktadministratör för Adobe Experience Platform för din organisation, som har en prenumeration på Experience Cloud.

Inom en kategori (eller standardgruppen&quot;Ej kategoriserad&quot;) kan du skapa och hantera taggar. Följande åtgärder är möjliga vid hantering av taggar:

* [Skapa en tagg](./ui/managing-tags.md#create-a-tag-create-tag)
* [Redigera en tagg](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Flytta en tagg mellan kategorier](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Arkivera en tagg](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Återställa en arkiverad tagg](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Ta bort en tagg](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Visa taggade objekt](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
