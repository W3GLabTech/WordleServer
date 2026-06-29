# Wordle Server

## Sections

- [Logic](#logic-)
- [Data](#data-)
- [Struct](#struct-)
- [Future Game Modes](#struct-)

## Logic 🧠

* Each event should be in a particular format, `server/<action>` and `client/<action>`. The former describes actions sent to the server, while the latter describes actions sent to the client.
* If the game has ended:
    * Frontend should display results

* Else:
  * Connect to [[WS] /live]
  * If the session has not ended: User has access to [server/play]

## Data 🗃

* The game requires two memory areas. (Permanent) and (Temporary)

### Permanent (SQL)

* The permanent area stores the list of players and the list of games / rooms.
* Rooms can only write twice to the permanent area (beginning – to fixate the users playing this game and at the end- to store the final results of the game).
* When the results of a game are written to the permanent area, it becomes Read ONLY


### Temporary (In-memory/NoSQL)

* It is a hot write area i.e. number of writes >> number of reads.
* It stores the ongoing game session
* It performs the write to the permanent storage when the game has ended.


## Struct 💾

* **Session**: contains the progress for a single user in a game (session ended means I am done with the current game, **BUT **others might still be playing)
    * Username
    * Max Guessed letters >
    * Used trails >
    * Submission time of max Guessed letters
* **Game**: contains the progress of everyone in the game

# Future Game Modes ✨

* Sprint mode: Unlimited trials (shortest time to guess a word is only used to determine the winner of this game mode)
* Wizard mode: (the smallest trials to guess a word wins, when there is a tie, the first to get the smallest trials win).
