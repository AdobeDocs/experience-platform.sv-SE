---
title: Versionsinformation för tillägget Common Analytics-plugin-program
description: Den senaste versionsinformationen om taggtillägget Common Analytics Plugins i Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 6%

---

# Versionsinformation om Common Analytics-plugin-program

## 20 maj 2021

### Common Analytics Plugins Extension 3.0.5

#### Felkorrigeringar

* Ett problem där getTimeParting inte initierades korrekt när den generiska initieringsåtgärden användes har åtgärdats

## 26 mars 2021

### Common Analytics Plugins Extension 3.0.4

#### Felkorrigeringar

* Ett problem har korrigerats där getPageLoadTime felaktigt angav variabler för fönsterobjektet
* Ett problem har korrigerats där getQueryParam returnerade undefined i stället för &quot;&quot; om queryParam inte fanns i frågesträngen
* Ett problem där felaktiga versionsnummer visades i initieringsåtgärden har korrigerats

## 19 mars 2021

### Common Analytics Plugins Extension 3.0.2

#### Funktioner

* Alla plugin-program har uppdaterats för att automatiskt inkludera versionsinformation som kontextdata
* Lagt till plugin-programmet getPercentPageViewed
* Lagt till dataelement för följande plugin-program
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* Uppdaterade format

## 9 april 2020

### Common Analytics Plugins Extension 2.2.0

#### Felkorrigeringar

* Fasta ord i tilläggsvyer

#### Funktioner

* Uppdaterad dokumentation i initieringsåtgärden

## 5 december 2019

### Common Analytics Plugins Extension 2.1.1

#### Felkorrigeringar

* Ett problem som förhindrade bakåtkompatibilitet med version 2.0.X har korrigerats
* Ett problem där dokumentationslänkar pekade på fel dokumentation har åtgärdats
* Ett problem där `getTimeSinceLastVisit` påträffades två gånger i initieringsåtgärden har korrigerats

## 15 november 2019

### Common Analytics Plugins Extension 2.1.0

#### Felkorrigeringar

* Omarbetade enskilda plugin-åtgärder för bakåtkompatibilitet
* Ett problem med plugin-programmet `cleanStr` har korrigerats
* Ett problem med plugin-programmet `getResponsiveLayout` har korrigerats
* Ett problem med plugin-programmet `getPageName` har korrigerats

#### Funktioner

* Versionsuppdatering för `getTimeParting`
* Versionsuppdatering för `numberSuite`
* Versionsuppdatering för `getNewRepeat`
* Uppdaterad dokumentation för alla plugin-program

## 30 oktober 2019

### Common Analytics Plugins Extension 2.0.3

#### Felkorrigeringar

* Ett problem där dokumentationslänkar bröts har korrigerats

## 11 oktober 2019

### Common Analytics Plugins Extension 2.0.2

#### Funktioner

* 15 plugin-program har lagts till i tillägget
* Skapade en ny initieringsåtgärd för att underlätta implementeringen

## 11 juli 2019

### Common Analytics Plugins Extension 1.0.4

#### Funktioner

* Tillägget har släppts med sju plugin-program
* Enskilda åtgärder för att initiera varje plugin-program
