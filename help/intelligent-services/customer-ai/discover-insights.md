---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Identifiera insikter med kundens AI
topic: Discovering insights
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Identifiera insikter med kundens AI

Customer AI, som en del av Intelligent Services ger marknadsförarna möjlighet att utnyttja Adobe Sensei för att förutse vad era kunder kommer att göra härnäst. Kundens AI används för att generera anpassade benägenhetspoäng som bortfall och konvertering för enskilda profiler i stor skala. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, utbildning eller driftsättning.

Det här dokumentet fungerar som en guide för interaktion med Service Instance Insights i användargränssnittet för AI för Intelligent Services.

## Komma igång

För att kunna utnyttja insikter om kundens AI måste du ha en tjänstinstans med status lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till användarhandboken [för](./user-guide.md)Customer AI. Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

## Översikt över tjänstinstans

Klicka på **Tjänster** i den vänstra navigeringen i användargränssnittet för Adobe Experience Platform. Webbläsaren *Services* visas och visar tillgängliga Intelligent Services. Klicka på **Öppna** i behållaren för kundens AI.

![Åtkomst till din instans](./images/insights/navigate-to-service.png)

Kundens AI-tjänstsida visas. På den här sidan visas tjänstinstanser för kundens AI och information om dem, inklusive namnet på instansen, typ av benägenhet, hur ofta instansen körs och status för den senaste uppdateringen.

>[!NOTE] Det är bara tjänstinstanser som har slutfört poängsättningen som har insikter.

![Skapa instans](./images/insights/dashboard.png)

Klicka på ett tjänstinstansnamn för att börja.

![Skapa instans](./images/insights/click-the-name.png)

Därefter visas informationssidan för den tjänstinstansen, där du får visualiseringar av dina data. Visualiseringarna och vad du kan göra med data beskrivs mer ingående i den här handboken.

![konfigurationssida](./images/insights/landing-page.png)


### Information om tjänstinstans

Det finns två sätt att visa tjänstinstansinformation, det första från kontrollpanelen och det andra från tjänstinstansen.

Om du vill visa information från kontrollpanelen klickar du på en tjänstinstansbehållare och undviker den hyperlänk som är kopplad till namnet. Detta öppnar en höger ratt med ytterligare information som beskrivning, poängfrekvens, förutsägelsemål och stödberättigad population. Dessutom kan du välja att redigera och ta bort instansen genom att klicka på **Redigera** eller **Ta bort**.

![höger räl](./images/insights/success-run.png)

>[!NOTE] Om en poängkörning misslyckas visas ett felmeddelande. Felmeddelandet visas under *Senaste körningsinformation* i den högra listen, som bara är synlig för misslyckade körningar.

![meddelande om misslyckad körning](./images/insights/failed-run.png)

Det andra sättet att visa ytterligare information för en tjänstinstans finns på sidan med insikter. Du kan klicka på **Visa mer** i det övre högra hörnet för att fylla i en listruta. Detaljer visas, till exempel poängdefinitionen, när den skapades och benägenhetstypen. Mer information om egenskaperna finns i användarhandboken för [AI](./user-guide.md).

![visa mer](./images/insights/landing-show-more.png)

![visa mer](./images/insights/show-more.png)

### Redigera en instans

Om du vill redigera en instans klickar du på **Redigera** i den övre högra navigeringen.

![klicka på redigeringsknappen](./images/insights/edit-button.png)

Dialogrutan Redigera visas. Du kan redigera *beskrivning* och *bedömningsfrekvens* för instansen. Om du vill bekräfta ändringarna och stänga dialogrutan klickar du på **Redigera** längst ned till höger.

![redigera poesi](./images/insights/edit-instance.png)

### Fler åtgärder

Knappen **Fler åtgärder** finns i den övre högra navigeringen bredvid **Redigera**. Om du klickar på **Fler åtgärder** öppnas en listruta där du kan välja någon av följande åtgärder:

- **Ta bort**: Tar bort instansen.
- **Åtkomstpoäng**: När du klickar på *Åtkomstpoäng* öppnas en dialogruta med en länk till [nedladdningspoängen för Kundens AI](./download-scores.md) -självstudiekurs. Dialogrutan innehåller även det datauppsättnings-ID som krävs för att göra API-anrop.
- **Visa körningshistorik**: En dialogruta med en lista över alla poängserier som är associerade med tjänstinstansen visas.

![fler åtgärder](./images/insights/more-actions.png)

## Poängsammanfattning

Betygsningssammanfattning visar det totala antalet profiler med poäng och kategoriserar dem i grupper som innehåller hög, medelhög och låg benägenhet. Propensitetsbucketerna baseras på poängintervall, låg är mindre än 24, medel är 25 till 74 och hög är över 74. Varje hink har en färg som motsvarar teckenförklaringen.

>[!NOTE] Om det är en konverteringsbenägenhetspoäng visas de höga poängen i grönt och de låga poängen i rött. Om du förutser kurvbenägenheten att detta vänds är de höga poängen röda och de låga poängen gröna. Mediefiltret förblir gult oavsett vilken typ av benägenhet du väljer.

![poängsammanfattning](./images/insights/scoring-summary.png)

## Distribution av bakgrundsmusik

Distributionen av Scores ** - kortet ger en visuell sammanfattning av populationen baserat på poängen. Färgerna som visas på *Distribuera poäng* representerar den typ av poäng som genereras.

![fördelning av poäng](./images/insights/distribution-of-scores.png)

## Influensafaktorer

För varje poänggrupp skapas ett kort som visar de tio viktigaste inflytelserika faktorerna för den aktuella bucket. Inflytelserika faktorer ger er ytterligare information om varför era kunder tillhör olika poänggrupper.

![Influensafaktorer](./images/insights/influential-factors.png)

### Skapa ett segment

Om du klickar på knappen **Skapa segment** i någon av verktygen Låg, Medel och Hög benägenhet dirigeras du om till segmentbyggaren.

![Klicka för att skapa segment](./images/insights/influential-factors-create-segment.png)

![Skapa ett segment](./images/insights/create-segment.png)

Segmentbyggaren används för att definiera ett segment, men kundens AI har redan gjort jobbet åt dig. Slutför segmentskapandet genom att fylla i behållarna *Namn* och *Beskrivning* som finns till höger i segmentbyggarens användargränssnitt. När du har gett segmentet ett namn och en beskrivning klickar du på **Spara** överst till höger.

>!![NOTE] Eftersom benägenhetspoängen skrivs till den enskilda profilen är de tillgängliga i segmentbyggaren som andra profilattribut. När du navigerar till segmentbyggaren för att skapa nya segment kan du se alla olika benägenhetspoäng under din namnområdes-AI för kunder.

![Segmentfyllning in](./images/insights/segment-saving.png)

Om du vill visa det nya segmentet i plattformsgränssnittet klickar du på **Segment** i den vänstra navigeringen. Sidan *Bläddra* visas och alla tillgängliga segment visas.

![Alla segment](./images/insights/Segments-dashboard.png)

## Nästa steg

I det här dokumentet beskrevs de insikter som en kundens AI-tjänstinstans har gett. Du kan nu fortsätta med självstudiekursen om [nedladdning av poäng i Customer AI](./download-scores.md) eller gå till de andra [Adobe Intelligent Services](../home.md) -guiderna som erbjuds.