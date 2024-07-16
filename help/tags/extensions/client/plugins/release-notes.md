---
title: Versionsinformation för tillägget för Common Analytics-plugin-program
description: Den senaste versionsinformationen om taggtillägget Common Analytics Plugins i Adobe Experience Platform.
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Versionsinformation om Common Analytics-plugin-program

## 3 juni 2022

### Common Analytics Plugins Extension 3.0.7

#### Funktioner

* Plugin-program som anger cookies använder nu flaggan secure

## 23 juni 2021

### Common Analytics Plugins Extension 3.0.6

#### Felkorrigeringar

* Ett problem där getPercentPageViewed skulle krascha när specialtecken användes har åtgärdats

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

* Fast ordalydelse i tilläggsvyer

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

* Tillägget har släppts med sju plugins
* Enskilda åtgärder för att initiera varje plugin-program
