# Empirica Concepts

Empirica is open source JS framework for running experimental games in the browser.

## Game Life Cycle

![Life Cycle](https://docs.empirica.ly/~gitbook/image?url=https:%2F%2F3801646690-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-legacy-files%2Fo%2Fassets%252F-M-Cqf0McgfJZYwXisux%252F-M_5ri7COWVb0gPSVr41%252F-M_5u7cgy5ZsdnOmkqgX%252FPicture3.png%3Falt=media%26token=2ecb38ae-4a04-4b3b-aa64-acd94b0c9169&width=768&dpr=1&quality=100&sign=c543a54cdad4d56fa4bf04ad1490e6d778659a139c9c84b7126b95e6fa77b176)

1. Players join games from batch 
    * creates player id
    * other intro steps

2. Players wait in lobby until all players are ready

3. Game Timee
    * Divided in rounds which are divided into stages
    * Each stage of round must be completed before all players move on to the next stage (players are always on the same stage)

4. Completion / Game End
    * Exit steps (survey, etc.)
    * no longer synchronous


## List of callbacks
The list of callbacks goes as follows in order:

From what I understand, these are just events that control the flow of the game.

Before a round starts, `onRoundStart` is called.

Before a stages starts, `onStageStart` is called.

When a Stage ends, `onStageEnd` is called.

When a Round ends, `onRoundEnd` is called.

* onGameStart: `Required`

* onRoundStart: `Repeated for each Round`

* onStageStart: `Repeated for each Stage`

* onStageEnd: `Repeated for each Stage`

* onRoundEnd: `Repeated for each Round`

* onGameEnd
