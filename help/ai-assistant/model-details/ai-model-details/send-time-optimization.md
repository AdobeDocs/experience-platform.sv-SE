---
title: Information om optimeringsmodell för sändningstid
description: Läs mer om AI-modellen som används för optimering av sändningstid i Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: 4c3f6ead150a2f793db92d2418df3177eba2d255
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# Information om optimeringsmodell för sändningstid

## Modellöversikt {#model-overview}

* **Modellnamn och version**: Sändningsoptimering
* **Modellreleasedatum**: september 2024
* **Modellsyfte**: Adobe Journey Optimizer Send-Time Optimization Model väljer den optimala sändningstiden för e-post och push-meddelanden för att maximera konsumenternas engagemang, baserat på kundernas tidigare öppnings- och klickbeteende.
* **Avsedda användare**: De primära användarna i den här modellen är marknadsförare, produktchefer och kundinteraktionsteam som utnyttjar Adobe Journey Optimizer för att driva datadrivna marknadsföringsstrategier.
* **Användningsfall**: Optimering för sändningstid används bäst för mindre brådskande marknadsföringsmeddelanden, till exempel en veckoannons, kampanjinformation för en ny produkt eller information om en månadsvis försäljning. Sändningsoptimering är endast tillgängligt för Journey Optimizer inbyggda åtgärdstyper för e-post och push och är för närvarande inte tillgängligt för meddelanden som skickas via anpassade åtgärder eller för andra åtgärdstyper.
* **Potentiell missbruk**: Optimering för sändningstid ska inte användas för brådskande, tidskänsliga operativa meddelanden, till exempel en orderbekräftelse, ett meddelande om lösenordsåterställning eller ett meddelande om ändring av flygport.

## Modellinformation {#model-details}

* **Modelltyp**: Modellen för optimering av sändningstid innehåller information om din organisations Adobe Journey Optimizer konsumentbeteendedata och tittar på öppna- och klickhändelser på användarnivå för att förutsäga när kunderna är mest benägna att interagera med dina meddelanden. Öppnings- och klickbeteenden på konsumentnivå för varje timma i veckan vägs och kombineras med lookalike och konsumentbeteendet med en [!DNL Bayesian]-skattare. [!DNL Bayesian]-prognoserna för varje timma i veckan rangordnas sedan, vilket resulterar i en&quot;värmekarta&quot; för varje mätvärde (e-postöppning, e-postklick och push-öppning) för varje kund, för att förutsäga hur många timmar i veckan det är mest och minst troligt att kontakten med varje konsument leder till önskat engagemangsresultat.
* **Indata**: För optimering av sändningstid används konsumenttidszonsdata i fältet `timeZone` i fältgruppen [!UICONTROL Preference Details], om sådana anges, för att fastställa en konsuments tidszon. Om en konsuments tidszon inte är tillgänglig i fältet `timeZone` försöker optimering av sändningstid härleda konsumentens tidszon, baserat på den vanligaste tidszonen som matchar den första postadressen som finns lagrad i konsumentprofilen med hjälp av datatypen [för postadresser](../../../xdm/data-types/postal-address.md). Med optimering för sändningstid kan man förutse för varje konsument utifrån tre typer av beteendedata:
   * Konsumenternas öppna och klickande beteende som helhet.
   * Beteendet med öppna och klickningar hos lookalike-konsumenter i samma tidszon.
   * Den enskilda konsumentens öppna och klickbeteende.
* **Utdata**: Dessa prognoser vägs och kombineras med en [!DNL Bayesian]-metod, vilket resulterar i en&quot;värmekarta&quot; för varje mätvärde (e-postöppning, e-postklick och push-öppningar) för varje kund, som anger de timmar i veckan som kontaktar den konsumenten mest och minst resulterar i önskat engagemangsresultat (öppna/klicka), vilket visas i följande exempelheatmap:

![Värmekartan för optimering av sändningstid.](../../images/models/send-time-optimization.png)

* **Exempel på indata och utdata**: För att minimera modellens påverkan på profilens detaljrikedom lagras och komprimeras modellpoängen i tre profilattribut som lagras i `_experience.intelligentServices.journeyAI.sendTimeOptimization` och är inte utformade för att vara läsbara för människor.

## Modellutbildning {#model-training}

* **Utbildningsdata och förbearbetning**: Utbildningsdata för varje organisation hämtas endast från deras egna data inom Adobe Experience Platform.
   * När optimeringsfunktionen för Skicka-tid är aktiverad för din organisation är modellen utbildad i e-post- och push-, send-, open- och click-händelser för alla organisationens resor och åtgärder de senaste 16 veckorna - oavsett om dessa åtgärder använder Send-Time Optimization. Detta gör att optimering av sändningstid kan dra nytta av alla data som genereras av era kunder.
   * Modeller är initialt utbildade och poängsätts varje vecka. Efter 16 veckor får modellerna ny utbildning och ny kodning varje månad. Modellpoängsättningen omfattar alla kundprofiler - både befintliga och nya - sedan den senaste poängsättningen.
   * Meddelanden som skickas av optimering av sändningstid får något av följande:
      * Ett meddelande om att utforska sändningstiden som valts ut för att testa olika sändningstider och observera hur konsumenterna svarar.
      * En&quot;optimerad&quot; sändningstid för meddelanden som valts för att maximera klickfrekvensen/öppningshastigheten. 5 % av sändningshändelserna får en utforskande sändningstid och 95 % av sändningshändelserna är&quot;optimerade&quot;.
   * Utforska sändningstider väljs slumpvis bland de sändningstider som är tillgängliga med den konfigurerade maximala väntetiden. Om ett meddelande till exempel markeras på onsdag 09:00 med optimering för Skicka-tid aktiverat och en 3-timmars maximal väntetid, kommer frågesändningstiderna för meddelandet att delas jämnt mellan 09:00, 10:00 och 12:00.

## Modellutvärdering {#model-evaluation}

* **Modellutvärdering**: Optimering av sändningstid kan öka e-postklickfrekvensen och öka öppningsfrekvensen i intervallet mellan cirka 2 % och 10 % för alla meddelanden som optimeras av en organisation.
   * Om en organisation som skickar e-postmeddelanden utan tidsoptimering för sändning till exempel har en klickfrekvens på i genomsnitt 5,0 %, kan samma uppsättning e-postmeddelanden med tidsoptimering för sändning resultera i en klickfrekvens på i genomsnitt 5,5 % (5,0 % * (1+10 %) = 5,5 %).
   * På grund av variationer inom små provstorlekar är det inte säkert att fördelarna med optimering av sändningstid kan observeras vid enskilda meddelanden.
   * Det är troligare att organisationer får större fördelar av att använda optimering vid sändning när:
      * Befintliga resor använder fasta och inte optimerade sändningstider.
      * Variationer i konsumentbeteenden (klickningar och öppningar) motsvarar konsumenternas placering och preferenser.
      * Organisationer använder Send-Time Optimization för en större del av e-post och push-meddelanden.
      * Organisationer väljer maximal väntetid inom det rekommenderade intervallet på 6-12 timmar.

## Modelldistribution {#model-deployment}

* **Modelluppdatering**: Modeller utbildas och utvärderas varje vecka. Efter 16 veckor får modellerna ny utbildning och ny kodning varje månad. Modellbedömningen innehåller alla konsumentprofiler - både befintliga och nya sedan den senaste poängsättningen.

## Fairness and bias {#fairness-and-bias}

* **Modellens rättvisa**: Felaktig härledning av en konsuments tidszon kan leda till att ett meddelande skickas tidigare än optimalt för en viss konsument eller senare än optimalt för en viss konsument. Alla kunder i ett meddelande som använder optimering av sändningstid får dock ett meddelande och har möjlighet att interagera med ett meddelande. Dessutom använder den här modellen inte demografiska uppgifter eller proxies för demografiska data - endast konsumentbeteendedata och konsumentdata används. Därför är risken för rättvisa begränsad och mildras.
* **Datafördomar**: Felaktig härledning av en konsuments tidszon kan leda till att ett meddelande skickas tidigare än optimalt för en viss konsument eller senare än optimalt för en viss konsument. Alla kunder i ett meddelande som använder optimering av sändningstid får dock ett meddelande och har möjlighet att interagera med ett meddelande. Dessutom använder den här modellen inte demografiska uppgifter eller proxies för demografiska data - endast konsumentbeteendedata och konsumentdata används. Därför är de partiska oron begränsade och mildras.

## Robusitet {#robustness}

* **Modellens tillförlitlighet**: Profiler utan tillräckliga interaktionshändelsedata (ofta för nya profiler) får antingen en omedelbar sändningstid, en undersökningstid inom det valda fönstret eller en sändningstid som baseras på den mest effektiva sändningstiden för alla kunder.

## Etiska överväganden {#ethical-considerations}

* **Etiska överväganden som är kopplade till modellen**: Felaktig härledning av en konsuments tidszon kan resultera i att ett meddelande skickas tidigare än optimalt för en viss konsument eller senare än optimalt för en viss konsument. Alla kunder i ett meddelande som använder optimering av sändningstid får dock ett meddelande och har möjlighet att interagera med ett meddelande. Dessutom använder den här modellen inte demografiska uppgifter eller proxies för demografiska data - endast konsumentbeteendedata och konsumentdata används. Därför är etiska frågor begränsade och mildras.