<!-- TITLE:Modern Warfare 2 -->

From the [wikipedia article of the same name](https://en.wikipedia.org/wiki/Call_of_Duty:_Modern_Warfare_2) : *"Call of Duty: Modern Warfare 2 is a 2009 first-person shooter game developed by Infinity Ward and published by Activision. It is the sixth installment in the Call of Duty series and the direct sequel to Call of Duty 4: Modern Warfare"*

The engine Call Of Duty: Modern Warfare 2 runs on is indissociable from the game itself, so the names "MW2 Engine", "IW4" (Infinity Ward 4), or "Modern Warfare 2" are used interchangeably. The same is true for every Call Of Duty installment, where the engine, derived from a previous game, is used to make a single game being derived again. This means the changes from one Call Of Duty to another often come from a form of iterating development, as the engine mutates over the years. Although the game is itself closed source, a lot of its inner workings is similar from other games and knowledge can be derived by studying their differences and shared characteristics.
# Denominations
There are two main branches of the Call Of Duty Engine we will be interested in - the one maintained historically by **Infinity Ward** (IW) and the one maintained by **Treyarch** (T).
Here are the denominations used throughout this wiki:

| Game | Release date | Developer | Referred to as... | 
| -------- | -------- | -------- | -------- | 
| Call Of Duty 2    | 2005     | Infinity Ward | IW2  or CoD 2 |
| Call Of Duty 4 : Modern Warfare    | 2007     | Infinity Ward | IW3 or CoD4 or MW1 |
| Call Of Duty : Modern Warfare 2    | 2009     | Infinity Ward | IW4 or MW2 |
| Call Of Duty : Modern Warfare 3    | 2011     | Infinity Ward and Raven Software | IW5 or MW3|
| Call Of Duty : World At War   | 2008     | Treyarch | T4 |
| Call Of Duty : Black Ops    | 2010     | Treyarch | T5 |

# Genealogy
The single best known ancestor with which Call Of duty shares DNA is **Quake III**, although a closer ancestor would be **Return To Castle: Wolfenstein** which itself is derived from Q3. [Both](https://github.com/id-Software/Quake-III-Arena) are [open source](https://github.com/id-Software/RTCW-SP/tree/master) and studying their code is a good way to understand some parts of Call Of Duty.

The first Call Of Duty is derived from RTC:W,  and then IW2 is derived from Call Of Duty, IW3 from IW2, and so on. Each game brings its shares of modifications over the previous one, but some areas move more than others. 
- Player movement, animations, physics, weaponry, scripting, gets expanded starting from IW2 but is never very far.
- Rendering changes drastically over the years, both the method of rendering and the rendering programs themselves (shaders). Multiplayer, in particular the session/party/server system, undergoes regular changes too.
- Starting from IW3, two branches of the engine coexist: the *treyarch* branch (IW3 => T4 => T5) and the *infinity ward* branch (IW3 => IW4 => IW5). As a result, while IW4 and IW5 are extremely close in all matters, IW4 and T5 are worlds apart.
