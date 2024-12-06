---
title: sendMediaEvent
description: Lär dig hur du använder kommandot sendMediaEvent för att spåra mediesessioner i Web SDK.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 877e12f1d53bb4a8d7c2564490d4e8f3e9e34e34
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---

# `sendMediaEvent`

Kommandot `sendMediaEvent` är en del av Web SDK `streamingMedia` -komponenten. Du kan använda den här komponenten för att samla in data relaterade till mediesessioner på din webbplats. Mer information om hur du konfigurerar den här komponenten finns i `streamingMedia` [documentation](configure/streamingmedia.md).

Använd kommandot `sendMediaEvent` om du vill spåra medieuppspelningar, pauser, slutföranden, uppdateringar av spelartillstånd och andra relaterade händelser.

Web SDK kan hantera mediahändelser baserat på typen av mediessionsspårning:

* **Händelsehantering för automatiskt spårade sessioner**. I det här läget behöver du inte skicka `sessionID` till mediahändelsen eller till spelhuvudsvärdet. Web SDK hanterar detta åt dig, baserat på det spelar-ID som anges och återanropsfunktionen `getPlayerDetails` som tillhandahölls när mediesessionen startades.
* **Händelsehantering för manuellt spårade sessioner**. I det här läget måste du skicka `sessionID` till mediahändelsen tillsammans med spelhuvudet (heltalsvärde). Du kan även skicka informationen om Experience-data om det behövs.

## Hantera mediahändelser efter typ {#handle-by-type}

Markera flikarna nedan om du vill se exempel på händelsetypshantering för varje händelsetyp och sessionsspårningsmetod (automatisk eller manuell).


### Spela upp {#play}

Händelsetypen `media.play` används för att spåra när medieuppspelningen startar. Den här händelsen ska skickas när spelaren ändrar läge till &quot;spela upp&quot; från ett annat läge. Andra lägen från vilka spelaren övergår till&quot;uppspelning&quot; är&quot;buffring&quot;, användaren återgår från&quot;pausad&quot;, spelaren återställs från ett fel eller automatisk uppspelning.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Pausa {#pause}

Händelsetypen `media.pauseStart` används för att spåra när en medieuppspelning pausas. Den här händelsen ska skickas när användaren trycker på **[!UICONTROL Pause]**. Det finns ingen CV-händelsetyp. En CV-händelse härleds när du skickar en `media.play`-händelse efter en `media.pauseStart`.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Fel {#error}

Händelsetypen `media.error` används för att spåra när ett fel inträffar under medieuppspelningen. Den här händelsen ska skickas när ett fel inträffar.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Annonsradbrytning - start {#ad-break-start}

Händelsetypen `media.adBreakStart` används för att spåra när en annonsbrytning startar. Den här händelsen ska skickas när en annonsbrytning börjar.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Annonsbrytning slutförd {#ad-break-complete}

Händelsetypen `media.adBreakComplete` används för att spåra när en annonsbrytning har slutförts. Denna händelse ska skickas när en annonsbrytning har slutförts.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Annonsstart {#ad-start}

Händelsetypen `media.adStart` används för att spåra när en annons startar. Den här händelsen ska skickas när en annons börjar.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### Annonsen är klar {#ad-complete}

Händelsetypen `media.adComplete` används för att spåra när en annons har slutförts. Denna händelse ska skickas när en annons är klar.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Annonshoppa {#ad-skip}

Händelsetypen `media.adSkip` används för att spåra när en annons hoppas över. Den här händelsen ska skickas när en annons hoppas över.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Kapitelstart {#chapter-start}

Händelsetypen `media.chapterStart` används för att spåra när ett kapitel börjar. Den här händelsen ska skickas när ett kapitel börjar.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### Kapitel fullständigt {#chapter-complete}

Händelsetypen `media.chapterComplete` används för att spåra när ett kapitel har slutförts. Den här händelsen ska skickas när ett kapitel har slutförts.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Kapitelhopp {#chapter-skip}

Händelsetypen `media.chapterSkip` används för att spåra när ett kapitel hoppas över. Den här händelsen ska skickas när ett kapitel hoppas över.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Buffertstart {#buffer-start}

Händelsetypen `media.bufferStart` används för att spåra när buffring startas. Den här händelsen ska skickas när buffringen startar. Det finns ingen `bufferResume`-händelsetyp. En `bufferResume` härleds när du skickar en play-händelse efter `bufferStart`.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Bithastighetsändring {#bitrate-change}

Händelsetypen `media.bitrateChange` används för att spåra när bithastigheten ändras. Den här händelsen ska skickas när bithastigheten ändras.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Tillståndsuppdateringar {#state-updates}

Händelsetypen `media.statesUpdate` används för att spåra när spelarläget ändras. Den här händelsen ska skickas när spelarläget ändras.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.statesUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### Sessionsslut {#session-end}

Händelsetypen `media.sessionEnd` används för att meddela Media Analytics-backend-objektet att omedelbart stänga sessionen när användaren har avbrutit sin visning av innehållet och det är osannolikt att de kommer att returnera.

Om du inte skickar en `sessionEnd`-händelse kommer en övergiven session att gå över efter att inga händelser har tagits emot under 10 minuter, eller när ingen spelhuvudrörelse sker under 30 minuter. Sessionen tas automatiskt bort.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Sessionen slutförd {#session-complete}

Händelsetypen `media.sessionComplete` används för att spåra när en mediesession har slutförts. Den här händelsen ska skickas när slutet av huvudinnehållet nås.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Manuell sessionsspårning]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]
