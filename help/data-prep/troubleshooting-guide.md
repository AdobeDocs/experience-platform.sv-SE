---
keywords: Experience Platform;hemmabruk;populära ämnen;
title: Felsökningsguide för dataprep
description: Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform Data Prep.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# [!DNL Data Prep] felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform [!DNL Data Prep] samt en felsökningsguide för vanliga fel. Om du har frågor och felsökningsinformation om plattforms-API:er i allmänhet kan du läsa [felsökningsguiden för Adobe Experience Platform API](../landing/troubleshooting.md).

## Vanliga frågor och svar

Nedan följer en lista med vanliga frågor om [!DNL Data Prep] och deras svar.

### Hur åtgärdas transformeringsfel?

[!DNL Data Prep] lokaliserar alla transformeringsfel till den kolumn där de inträffade. Det innebär att kolumnen har värdet null och att resten av raden kommer att fortsätta att bearbetas. Dessa transformeringsproblem loggas som **Varningar**. Vi rekommenderar att du granskar varningarna med jämna mellanrum och justerar omformningslogiken för att ta hänsyn till omformningsproblemen. Detta kommer att öka kvaliteten på de data som hämtas in till Experience Platform.

Om kolumnerna som markerats som **Obligatorisk** har värdet null på grund av transformeringsproblem, kommer raden inte att kapslas in. När partiell datainmatning är aktiverat kan du ange tröskelvärdet för sådana avvisningar innan hela flödet misslyckas. Om attributet null inte påverkade några valideringar på schemanivå kommer raden att fortsätta att kapslas.

Alla rader som är ogiltiga, även utan omformningsfel, kommer också att refuseras. Ett datainmatningsflöde kan till exempel ha en genomströmningsmappning (ingen omformningslogik) till ett obligatoriskt fält och det finns inget inkommande värde för det attributet. Den här raden kommer att refuseras.

### Hur kan jag undgå specialtecken i ett fält?

Du kan undvika specialtecken i ett fält genom att använda `${...}`. JSON-filer som innehåller fält med en punkt (`.`) stöds dock inte av den här funktionen. Om ett underordnat attribut har en punkt (`.`) vid interaktion med hierarkier måste du använda ett omvänt snedstreck (`\`) för att undvika specialtecken. `address` är till exempel ett objekt som innehåller attributet `street.name`, som sedan kan kallas `address.street\.name` i stället för `address.street.name`.

### Vilken är maxlängden för beräknade fält?

Beräknade fält får innehålla högst 4 096 tecken.

### Det gick inte att fylla i på grund av validering av ett attribut, men attributet finns korrekt i min fil. Exakt vad är fel?

Kontrollera att datatypen för varje fält matchar den typ som är definierad i schemat. Dessutom måste villkor som&quot;Obligatorisk&quot;,&quot;Uppräkning&quot; och&quot;format&quot; följas.

De data som importeras måste överensstämma med XDM-schemat (Experience Data Model) som definieras i Experience Platform. Om attributet inte matchar den förväntade typen eller det förväntade formatet som anges i schemat, kommer importen att misslyckas.

Om dataförinställningsfunktionerna används kontrollerar du att omvandlingen resulterar i rätt attribut. Du kan granska attributen under konfigurationen av arbetsflödet för källor. Under mappningssteget väljer du **[!UICONTROL New field type]** och sedan **[!UICONTROL Add calculated field]**. Använd sedan beräkningsfältets gränssnitt för att förhandsgranska varje funktion.

### Hur tar jag bort felaktiga datavärden från direktuppspelnings- eller batchmatningsposter?

Du kan använda gränssnittet Data Prep-mappning för att utföra filtrering på kolumnnivå endast genom att mappa kolumner som har nödvändiga data. Du kan också använda beräkningsfält för att omforma data med hjälp av stödfunktionerna.

Filtrering på radnivå är för närvarande bara tillgängligt för [Adobe Analytics-källkopplingen](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Efter intag kan du använda databearbetaren för att rengöra, forma och hantera data med hjälp av SQL. Den här processen kräver dock att gruppen tas bort med de felaktiga posterna och att en ny grupp som skapats från SQL-resultatet hämtas igen.

>[!IMPORTANT]
>
>* Datasjön: Du kan bara ta bort poster som redan har importerats genom att ta bort och importera om gruppen som posten finns i.
>
>* Kundprofil i realtid: Du kan skriva över attributbaserade poster genom att importera nya poster, men upplevelsehändelseposter kan inte tas bort.
>
>* Identitetstjänst: Du kan inte ta bort poster direkt i identitetstjänsten. Du måste ta bort hela profilen och överföra profilen igen med rätt poster med hjälp av API:t för profilborttagning.

### Vad är bästa sättet att använda beräkningsfält i data från GIF?

Du kan använda funktionerna för dataprep-mappning under mappningssteget för källdata till XDM-schema för att skapa ett nytt beräknat fält.

### När du hämtar in Adobe Analytics-data som en källa, aktiveras schemat automatiskt för profilen?

Analysdata konfigureras inte automatiskt för profilen. När du har konfigurerat källkopplingen måste du gå in i datauppsättningen och schemat och aktivera dem för profilinmatning.

När du skapar ett datakällflöde för Analytics i en produktionssandlåda skapas två dataflöden:

* Ett dataflöde som gör en 13-månaders efterfyllning av historiska rapportsvitdata till datasjön. Det här dataflödet avslutas när bakgrundsfyllningen är slutförd.
* Ett dataflöde som skickar livedata till datavjön och till Profil. Det här dataflödet körs kontinuerligt.

### Hur kan jag skriva ned ett värde i ett kartobjekt med dataförinställningsfunktionerna?

Du kan hämta värdet med funktionen `map_get_values` och sedan göra det med gemener med hjälp av funktionen lower:

```shell
lower(map_get_values(mapObject, 'keyName'))
```

Du kan använda samma funktion för att skapa ett mappningsobjekt med gemener. Du kan emellertid inte göra en slinga genom en hel karta och göra varje objekt i gemener.

### Kan jag använda dataprep-funktioner på ett kapslat sätt?

Ja, du kan använda en Data Prep-funktion i en annan funktion för att lösa komplex dataförberedelsefunktion under dataimporten.

Om du till exempel vill definiera ett fält som null baserat på ett visst villkor, kan du använda funktionen&quot;iif&quot; för att kontrollera det fältet. Om funktionen returnerar `true` kan du använda &quot;nullify()&quot; och om den returnerar `false` kan du använda respektive fält.

Om marketing_type var fältet kan du använda &quot;.equals&quot; för att kontrollera värdet i fältet marketing_type och det kan kapslas i en &quot;iif&quot;-funktion. Om den returnerar `true` kan du använda funktionen &quot;nullify()&quot; enligt nedan:

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

I följande exempel visas exempel på hur du kan kapsla förinställningsfunktioner för data med if, equals och null:

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| --- | --- | --- | --- | --- | --- |
| iif | Utvärderar ett givet booleskt uttryck och returnerar det angivna värdet baserat på resultatet. | <ul><li>UTTRYCK: **Obligatoriskt** Det booleska uttryck som utvärderas.</li><li>TRUE_VALUE: **Required** Värdet som returneras om uttrycket utvärderas till true.</li><li>FALSE_VALUE: **Required** Värdet som returneras om uttrycket utvärderas till false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Sant&quot; |
| är lika med | Jämför två strängar för att bekräfta om de är lika. Den här funktionen är skiftlägeskänslig. | <ul><li>STRING1: **Required** Den första strängen som du vill jämföra.</li><li>STRING2: **Required** Den andra strängen som du vill jämföra. | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| null | Anger värdet för attributet till null. Detta bör användas när du inte vill kopiera fältet till målschemat. | | nullify() | nullify() | noll |

{style="table-layout:auto"}

Följande är ett exempel på hur funktionerna kan kapslas, under förutsättning att fältet som utvärderas är &quot;marketing_type&quot;.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Nu när du har följande tre fält:

* marketing_type: (email, phyMail, push, sms, phone)
* total_consents: nummerintervall från 4 000 till 5 500
* datum: från feb till mars 2024

Du kan använda och kapsla de tre funktionerna som listas ovan för att ändra de tre fälten:

* iif(marketing_type.equals(&quot;email&quot;), null(), if(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;), null(), if(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type))
* iif(total_consents > 5000, iif(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;otillräckliga-consents&quot;)
* iif(date.equals(&quot;3/21/24&quot;), if(marketing_type.equals(&quot;push&quot;), nullify(), marketing_type), &quot;not-March&quot;)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-medgivande-sms&quot;, marketing_type), &quot;high-consents&quot;)
* iif(marketing_type.equals(&quot;email&quot;), if(total_consents > 5000, nullify(), &quot;email-low-consents&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_consents &lt; 4500, &quot;low-medgivande-push&quot;, nullify()), marketing_type)
* iif(total_consents >= 5500, iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;high-consents&quot;), marketing_type)