---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;enum;field;
solution: Experience Platform
title: Definiera uppräkningsfält och föreslagna värden i användargränssnittet
description: Lär dig hur du definierar enum och föreslagna värden för strängfält i användargränssnittet för Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: e515e32588991e468429c9256533732d04a4339f
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# Definiera uppräkningar och föreslagna värden i användargränssnittet {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Uppräkning och föreslagna värden"
>abstract="An **Enum** begränsar ett strängfält så att endast data som matchar en fördefinierad uppsättning värden kan importeras. Varje begränsning kan tilldelas en **Visningsnamn** som fyller i attributlistrutor i segmenteringsgränssnittet. **Föreslagna värden** för ett fält inte begränsa inträngning och endast avgöra vilka visningsnamn som visas i Segmentering. Om du har flera scheman som delar ett fält som tillhör en gemensam klass eller fältgrupp, och du definierar olika uppräkningar eller föreslagna värden för det fältet mellan varje schema, sammanfogas dessa värden och läggs till i unionsschemat."

I Experience Data Model (XDM) kan ett strängfält få en fördefinierad uppsättning godkända eller föreslagna värden för att bättre kontrollera vilka värden som hämtas till det fältet eller hur det fungerar i segmenteringen.

An **enum** begränsar de värden som kan importeras för ett strängfält till en fördefinierad uppsättning. Om du försöker importera data till ett uppräkningsfält och värdet inte matchar någon av dem som definierats i konfigurationen, nekas intag.

I motsats till enum lägger du till **föreslagna värden** till ett strängfält begränsar inte de värden som kan importeras. Föreslagna värden påverkar i stället vilka fördefinierade värden som är tillgängliga i [Segmenteringsgränssnitt](../../../segmentation/ui/overview.md) när strängfältet inkluderas som ett attribut.

När [definiera ett nytt fält](./overview.md#define) i Adobe Experience Platform användargränssnitt och ange typen till [!UICONTROL String]kan du definiera [enum](#enum) eller [föreslagna värden](#suggested-values) för det fältet.

![Bild som visar alternativet Uppräkning och föreslagna värden aktiverat för ett strängfält i användargränssnittet](../../images/ui/fields/enum/enum-options-selected.png)

## Definiera en uppräkning {#enum}

Välj **[!UICONTROL Enums and Suggested Values]** väljer **[!UICONTROL Enums]**. Ytterligare kontroller visas, så att du kan ange värdebegränsningar för uppräkningen. Om du vill lägga till en begränsning väljer du **[!UICONTROL Add row]**.

![Bild som visar alternativet Numrera som valts i användargränssnittet](../../images/ui/fields/enum/enum-add-row.png)

Under **[!UICONTROL Value]** måste du ange det exakta värdet som du vill begränsa fältet till. Du kan även ange en användarvänlig **[!UICONTROL Display Name]** för begränsningen, vilket påverkar hur värdet kommer att representeras i segmenteringen.

Fortsätt använda **[!UICONTROL Add row]** om du vill lägga till önskade begränsningar och valfria etiketter i uppräkningen, eller markera ikonen Ta bort (![Bild av ikonen Ta bort](../../images/ui/fields/enum/remove-icon.png)) bredvid en rad som lagts till tidigare för att ta bort den. När du är klar väljer du **[!UICONTROL Apply]** för att tillämpa ändringarna i schemat.

![Bild som visar uppräkningsvärden och visningsnamn som fyllts i för strängfältet i användargränssnittet](../../images/ui/fields/enum/enum-confirm.png)

Arbetsytan uppdateras för att återspegla ändringarna. När du utforskar det här schemat i framtiden kan du visa och redigera begränsningarna för uppräkningsfältet i den högra listen.

## Definiera föreslagna värden {#suggested-values}

Välj **[!UICONTROL Enums and Suggested Values]** väljer **[!UICONTROL Suggested Values]** om du vill att fler kontroller ska visas. Här väljer du **[!UICONTROL Add row]** om du vill lägga till föreslagna värden.

![Bild som visar alternativet Föreslagna värden som valts i användargränssnittet](../../images/ui/fields/enum/suggested-add-row.png)

Under **[!UICONTROL Display Name]** -kolumnen anger du ett användarvänligt namn för värdet som du vill att det ska visas i segmenteringsgränssnittet. Om du vill lägga till fler föreslagna värden väljer du **[!UICONTROL Add row]** och upprepa processen efter behov. Om du vill ta bort en rad som lagts till tidigare markerar du ikonen Ta bort (![Bild av ikonen Ta bort](../../images/ui/fields/enum/remove-icon.png)) bredvid raden i fråga.

När du är klar väljer du **[!UICONTROL Apply]** för att tillämpa ändringarna i schemat.

![Bild som visar uppräkningsvärden och visningsnamn som fyllts i för strängfältet i användargränssnittet](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Det finns en fördröjning på ungefär fem minuter för ett fälts uppdaterade föreslagna värden som ska återspeglas i segmenteringsgränssnittet.

### Hantera föreslagna värden för standardfält

Vissa fält från standard-XDM-komponenter innehåller egna föreslagna värden, till exempel `eventType` från [[!UICONTROL XDM ExperienceEvent] class](../../classes/experienceevent.md). När du använder dessa fält i dina scheman kan du använda de tillgängliga växlarna för att styra vilka befintliga föreslagna värden som ska användas.

![Bild som visar uppräkningsvärden och visningsnamn som fyllts i för strängfältet i användargränssnittet](../../images/ui/fields/enum/suggested-standard.png)

Välj på liknande sätt som anpassade fält **[!UICONTROL Add row]** om du vill lägga till egna föreslagna värden för standardfält.

![Bild som visar uppräkningsvärden och visningsnamn som fyllts i för strängfältet i användargränssnittet](../../images/ui/fields/enum/suggested-standard.png)

### Ta bort föreslagna värden för standardfält

Endast föreslagna värden som du definierar kan tas bort från ett standardfält. Befintliga föreslagna värden kan inaktiveras så att de inte längre visas i segmenteringslistrutan, men de kan inte tas bort direkt.

Ta till exempel ett profilschema där ett föreslaget värde för standarden `person.gender` fältet är inaktiverat:

![Bild som visar uppräkningsvärden och visningsnamn som fyllts i för strängfältet i användargränssnittet](../../images/ui/fields/enum/standard-enum-disabled.png)

I det här exemplet är visningsnamnet[!UICONTROL Non-specific]&quot; är nu inaktiverat för att visas i listrutan för segmentering. Värdet `non_specific` är fortfarande en del av listan med uppräknade fält och är därför fortfarande tillåten vid förtäring. Du kan alltså inte inaktivera det faktiska uppräkningsvärdet för standardfältet eftersom det skulle strida mot principen att bara tillåta ändringar som gör ett fält mindre restriktivt.

Se [avsnitt nedan](#evolution) om du vill ha mer information om reglerna för uppdatering av uppräkningar och föreslagna värden för befintliga schemafält.

## Utvecklingsregler för enum och föreslagna värden {#evolution}

När ett schema med ett uppräkningsfält har använts för att importera data till plattformen, måste alla ytterligare ändringar som görs i schemadefinitionen överensstämma med de data som redan finns i systemet. I allmänhet kan ändringar som görs i ett befintligt fält bara göra det fältet **mindre** restriktiv. Ett fält kan inte göras mer restriktivt än det redan är.

När det gäller enum och föreslagna värden gäller följande regler för postinmatning:

* Du **KAN** lägga till föreslagna värden för standardfält och anpassade fält med befintliga föreslagna värden.
* Du **KAN** ta bort föreslagna värden från anpassade fält med befintliga föreslagna värden.
* Du **KAN** lägga till nya uppräkningsvärden för ett befintligt anpassat uppräkningsfält.
* Du **KAN** ändra uppräkningsvärdena för ett anpassat fält till endast föreslagna värden eller konvertera det till en sträng utan uppräkning eller föreslagna värden. **Det går inte att ångra den här växeln när den har använts.**
* Du **KAN INTE** ta bort uppräkningar eller föreslagna värden från standardfält.
* Du **KAN INTE** lägg till uppräkningsvärden i ett fält utan befintlig uppräkning.
* Du **KAN INTE** tar bort färre än alla befintliga uppräkningsvärden för ett anpassat fält.
* Du **KAN INTE** växla från föreslagna värden till en uppräkning.

## Sammanfoga regler för uppräkningar och föreslagna värden {#merging}

Om flera scheman använder samma uppräkningsfält med olika konfigurationer, och dessa scheman ingår i en union, gäller vissa regler när det gäller hur uppräkningsskillnader avstäms. De exakta reglerna beror på om scheman refererar till samma standardfält (som `eventType`) eller om de refererar till samma anpassade fältsökväg i olika fältgrupper.

Om samma standardfält refereras:

* Ytterligare föreslagna värden är **BIFOGAD** i unionen.
* Uppdateringar av de föreslagna värdena för samma uppräkningsnyckel är **UPPDATERAD** i unionen.

Om samma anpassade fältsökväg refereras i olika fältgrupper:

* Ytterligare föreslagna värden är **BIFOGAD** i unionen.
* Om samma ytterligare föreslagna värde definieras i mer än ett schema är dessa värden **SAMMANSLAGNA** i unionen. Med andra ord visas inte samma föreslagna värde två gånger efter sammanslagningen.

## Nästa steg

I den här handboken beskrivs hur du definierar enum och föreslagna värden för strängfält i användargränssnittet. Mer information om hur du hanterar uppräkningar och föreslagna värden med API:t för schemaregister finns i följande [självstudiekurs](../../tutorials/suggested-values.md).

Så här definierar du andra XDM-fälttyper i [!DNL Schema Editor], se översikten på [definiera fält i användargränssnittet](./overview.md#special).
