---
title: sendMediaEvent
description: Lär dig hur du använder kommandot sendMediaEvent för att spåra mediesessioner i Web SDK.
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# `sendMediaEvent`

The `sendMediaEvent` kommandot ingår i Web SDK `streamingMedia` -komponenten. Du kan använda den här komponenten för att samla in data relaterade till mediesessioner på din webbplats. Se `streamingMedia` [dokumentation](configure/streamingmedia.md) om du vill lära dig hur du konfigurerar den här komponenten.

Använd `sendMediaEvent` för att spåra mediespelningar, pauser, complete, player state updates, och andra relaterade händelser.

Web SDK kan hantera mediahändelser baserat på typen av mediessionsspårning:

* **Händelsehantering för automatiskt spårade sessioner**. I det här läget behöver du inte skicka `sessionID` till mediahändelsen eller spelhuvudet. Web SDK hanterar detta åt dig, baserat på det spelare-ID som anges och `getPlayerDetails` callback-funktionen som tillhandahålls när mediesessionen startas.
* **Händelsehantering för manuellt spårade sessioner**. I det här läget måste du skicka `sessionID` till mediahändelsen tillsammans med spelhuvudet (heltalsvärde). Du kan även skicka informationen om Experience-data om det behövs.

## Hantera mediahändelser efter typ {#handle-by-type}

Markera flikarna nedan om du vill se exempel på händelsetypshantering för varje händelsetyp och sessionsspårningsmetod (automatisk eller manuell).


### Spela upp {#play}

The `media.play` händelsetypen används för att spåra när medieuppspelningen startar. Den här händelsen ska skickas när spelaren ändrar läge till &quot;spela upp&quot; från ett annat läge. Andra lägen från vilka spelaren övergår till&quot;uppspelning&quot; är&quot;buffring&quot;, användaren återgår från&quot;pausad&quot;, spelaren återställs från ett fel eller automatisk uppspelning.

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

The `media.pauseStart` händelsetyp används för att spåra när en mediouppspelning pausas. Den här händelsen ska skickas när användaren trycker på **[!UICONTROL Pause]**. Det finns ingen CV-händelsetyp. En meritförteckning visas när du skickar en `media.play` händelse efter `media.pauseStart`.

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

The `media.error` händelsetyp används för att spåra när ett fel inträffar under medieuppspelning. Den här händelsen ska skickas när ett fel inträffar.

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

The `media.adBreakStart` händelsetyp används för att spåra när en annonsbrytning startar. Den här händelsen ska skickas när en annonsbrytning börjar.

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

The `media.adBreakComplete` händelsetypen används för att spåra när en annonsbrytning har slutförts. Denna händelse ska skickas när en annonsbrytning har slutförts.

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

The `media.adStart` händelsetypen används för att spåra när en annons börjar. Den här händelsen ska skickas när en annons börjar.

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

The `media.adComplete` händelsetypen används för att spåra när en annons har slutförts. Denna händelse ska skickas när en annons är klar.

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

The `media.adSkip` händelsetypen används för att spåra när en annons hoppas över. Den här händelsen ska skickas när en annons hoppas över.

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

The `media.chapterStart` händelsetyp används för att spåra när ett kapitel börjar. Den här händelsen ska skickas när ett kapitel börjar.

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

The `media.chapterComplete` händelsetypen används för att spåra när ett kapitel har slutförts. Den här händelsen ska skickas när ett kapitel har slutförts.

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

The `media.chapterSkip` händelsetyp används för att spåra när ett kapitel hoppas över. Den här händelsen ska skickas när ett kapitel hoppas över.

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

The `media.bufferStart` händelsetypen används för att spåra när buffring startas. Den här händelsen ska skickas när buffringen startar. Det finns inga `bufferResume` händelsetyp. A `bufferResume` visas när du skickar en uppspelningshändelse efter `bufferStart`.

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

The `media.bitrateChange` händelsetypen används för att spåra när bithastigheten ändras. Den här händelsen ska skickas när bithastigheten ändras.

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

The `media.stateUpdate` händelsetypen används för att spåra när spelarläget ändras. Den här händelsen ska skickas när spelarläget ändras.

>[!BEGINTABS]

>[!TAB Automatisk sessionsspårning]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.stateUpdate",
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

The `media.sessionEnd` händelsetypen används för att meddela Media Analytics-backend att sessionen omedelbart ska stängas när användaren har avbrutit sin visning av innehållet och de troligtvis inte kommer att returneras.

Om du inte skickar `sessionEnd` -händelsen kommer en övergiven session att gå över efter att inga händelser har tagits emot under 10 minuter, eller när ingen spelhuvudrörelse inträffar under 30 minuter. Sessionen tas automatiskt bort.

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

The `media.sessionComplete` händelsetypen används för att spåra när en mediesession har slutförts. Den här händelsen ska skickas när slutet av huvudinnehållet nås.

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



