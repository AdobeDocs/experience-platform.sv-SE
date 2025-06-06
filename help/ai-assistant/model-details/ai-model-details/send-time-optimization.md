---
title: Information om optimeringsmodell för sändningstid
description: Läs mer om AI-modellen som används för optimering av sändningstid i Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: 481108135ee6ed5b90547e4e95799ab99edb210e
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# Information om optimeringsmodell för sändningstid

## Modellöversikt {#model-overview}

* **Modellnamn och version**: Sändningsoptimering
* **Modellreleasedatum**: september 2024
* **Modellsyfte**: Adobe Journey Optimizer Send-Time Optimization Model väljer den optimala sändningstiden för e-post och push-meddelanden för att maximera kundengagemanget, baserat på kundernas tidigare öppnings- och klickbeteende.
* **Avsedda användare**: De primära användarna i den här modellen är marknadsförare, produktchefer och kundinteraktionsteam som utnyttjar Adobe Journey Optimizer för att driva datadrivna marknadsföringsstrategier.
* **Användningsfall**: Optimering för sändningstid används bäst för mindre brådskande marknadsföringsmeddelanden, till exempel en veckoannons, kampanjinformation för en ny produkt eller information om en månadsvis försäljning. Sändningsoptimering är endast tillgängligt för Journey Optimizer inbyggda åtgärdstyper för e-post och push och är för närvarande inte tillgängligt för meddelanden som skickas via anpassade åtgärder eller för andra åtgärdstyper.
* **Potentiell missbruk**: Optimering för sändningstid ska inte användas för brådskande, tidskänsliga operativa meddelanden, till exempel en orderbekräftelse, ett meddelande om lösenordsåterställning eller ett meddelande om ändring av flygport.

## Modellinformation {#model-details}

* **Modelltyp**: Modellen för optimering av sändningstid innehåller information om kundbeteenden i din organisation och tittar på öppna- och klickhändelser på användarnivå för att förutsäga när det är mest troligt att dina kunder interagerar med dina meddelanden. Öppnings- och klickbeteenden på användarnivå för varje timma i veckan vägs och kombineras med lookalike och det övergripande användarbeteendet med en [!DNL Bayesian]-uppskattare. [!DNL Bayesian]-prognoserna för varje timma i veckan rangordnas sedan, vilket resulterar i en&quot;värmekarta&quot; för varje mätvärde (e-postöppning, e-postklick och push-öppningar) för varje kund, för att förutsäga hur många timmar i veckan det är mest och minst troligt att kontakten leder till önskat engagemangsresultat.
* **Indata**: Vid optimering av sändningstid används användarens tidszonsdata i fältet `timeZone` i fältgruppen [!UICONTROL Preference Details], om sådan finns, för att fastställa en användares tidszon. Om en användares tidszon inte är tillgänglig i fältet `timeZone` försöker optimering av sändningstid härleda användarens tidszon baserat på den vanligaste tidszonen som matchar den första postadressen som finns lagrad i användarens profil med hjälp av datatypen [för postadresser](../../../xdm/data-types/postal-address.md). Med optimering för sändningstid kan du förutsäga för varje användare utifrån tre typer av beteendedata:
   * Funktionerna för att öppna och klicka på dina användare som helhet.
   * Beteendet att öppna och klicka på ser ut som användare i samma tidszon.
   * Den enskilda användarens beteende att öppna och klicka.
* **Utdata**: Dessa prognoser vägs och kombineras med en [!DNL Bayesian]-metod, vilket resulterar i en&quot;värmekarta&quot; för varje mätvärde (e-postöppning, e-postklick och push-öppningar) för varje kund, som anger antalet timmar i veckan som kontaktar den användaren mest och minst resulterar i önskat engagemangsresultat (öppna/klicka), vilket visas i följande exempelheatmap:

![Värmekartan för optimering av sändningstid.](../../images/models/send-time-optimization.png)

* **Exempel på indata och utdata**: För att minimera modellens påverkan på profilens detaljrikedom lagras och komprimeras modellpoängen i tre profilattribut som lagras i `_experience.intelligentServices.journeyAI.sendTimeOptimization` och är inte utformade för att vara läsbara för människor.

## Modellutbildning {#model-training}

* **Utbildningsdata och förbearbetning**: Utbildningsdata för varje organisation hämtas endast från deras egna data inom Adobe Experience Platform.
   * När optimeringsfunktionen för Skicka-tid är aktiverad för din organisation är modellen utbildad i e-post- och push-, send-, open- och click-händelser för alla organisationens resor och åtgärder de senaste 16 veckorna - oavsett om dessa åtgärder använder Send-Time Optimization. Detta gör att optimering av sändningstid kan dra nytta av alla data som genereras av dina kunder.
   * Modeller är initialt utbildade och poängsätts varje vecka. Efter 16 veckor får modellerna ny utbildning och ny kodning varje månad. Modellpoängsättningen omfattar alla kundprofiler - både befintliga och nya - sedan den senaste poängsättningen.
   * Meddelanden som skickas av optimering av sändningstid får något av följande:
      * Skicka-tid för meddelande om att utforska ett meddelande, valt att testa olika sändningstider och observera hur kunderna svarar
      * En&quot;optimerad&quot; sändningstid för meddelanden som valts för att maximera klickfrekvensen/öppningshastigheten. 5 % av sändningshändelserna får en utforskande sändningstid och 95 % av sändningshändelserna är&quot;optimerade&quot;.
   * Utforska sändningstider väljs slumpvis bland de sändningstider som är tillgängliga med den konfigurerade maximala väntetiden. Om ett meddelande till exempel markeras på onsdag 09:00 med optimering för Skicka-tid aktiverat och en 3-timmars maximal väntetid, kommer frågesändningstiderna för meddelandet att delas jämnt mellan 09:00, 10:00 och 12:00.

## Modellutvärdering {#model-evaluation}

* **Modellutvärdering**: Optimering av sändningstid kan öka e-postklickfrekvensen och öka öppningsfrekvensen i intervallet mellan cirka 2 % och 10 % för alla meddelanden som optimeras av en organisation.
   * Om en organisation som skickar e-postmeddelanden utan tidsoptimering för sändning till exempel har en klickfrekvens på i genomsnitt 5,0 %, kan samma uppsättning e-postmeddelanden med tidsoptimering för sändning resultera i en klickfrekvens på i genomsnitt 5,5 % (5,0 % * (1+10 %) = 5,5 %).
   * På grund av variationer inom små provstorlekar är det inte säkert att fördelarna med optimering av sändningstid kan observeras vid enskilda meddelanden.
   * Det är troligare att organisationer får större fördelar av att använda optimering vid sändning när:
      * Befintliga resor använder fasta och inte optimerade sändningstider.
      * Variabilitet i kundbeteende (klickningar och öppningar) motsvarar kundens placering och kundernas preferenser.
      * Organisationer använder Send-Time Optimization för en större del av e-post och push-meddelanden.
      * Organisationer väljer maximal väntetid inom det rekommenderade intervallet på 6-12 timmar.

## Modelldistribution {#model-deployment}

* **Modelluppdatering**: Modeller utbildas och utvärderas varje vecka. Efter 16 veckor får modellerna ny utbildning och ny kodning varje månad. Modellpoängen innehåller alla kundprofiler - både befintliga och nya sedan den senaste poängsättningen.

## Fairness and bias {#fairness-and-bias}

* **Modellens rättvisa**: Felaktig härledning av en användares tidszon kan resultera i att ett meddelande skickas tidigare än optimalt för en viss användare eller senare än optimalt för en viss användare. Alla användare i ett meddelande som använder optimering av sändningstid får dock ett meddelande och har möjlighet att interagera med ett meddelande. Dessutom använder den här modellen inte användarens demografiska data eller proxies för demografiska data - endast användarbeteendes- och användartidszonsdata används. Därför är risken för rättvisa begränsad och mildras.
* **Dataavvikelser**: Felaktig härledning av en användares tidszon kan resultera i att ett meddelande skickas tidigare än optimalt för en viss användare eller senare än optimalt för en viss användare. Alla användare i ett meddelande som använder optimering av sändningstid får dock ett meddelande och har möjlighet att interagera med ett meddelande. Dessutom använder den här modellen inte användarens demografiska data eller proxies för demografiska data - endast användarbeteendes- och användartidszonsdata används. Därför är de partiska oron begränsade och mildras.

## Robusitet {#robustness}

* **Modellens tillförlitlighet**: Profiler utan tillräckliga interaktionshändelsedata (ofta för nya profiler) får antingen en omedelbar sändningstid, en undersökningstid inom det valda fönstret eller en sändningstid som baseras på den mest effektiva sändningstiden för alla kunder.

## Etiska överväganden {#ethical-considerations}

* **Etiska överväganden som är kopplade till modellen**: Felaktig härledning av en användares tidszon kan resultera i att ett meddelande skickas tidigare än optimalt för en viss användare eller senare än optimalt för en viss användare. Alla användare i ett meddelande som använder optimering av sändningstid får dock ett meddelande och har möjlighet att interagera med ett meddelande. Dessutom använder den här modellen inte användarens demografiska data eller proxies för demografiska data - endast användarbeteendes- och användartidszonsdata används. Därför är etiska frågor begränsade och mildras.
