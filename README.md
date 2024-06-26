# ESP32aceTeam
SpaceTeam for ESP32s

Olivia Bobrownicki, Kevin Medina, Claudia Tang, Alice Wang

See [a blog post with creative documentation HERE.](https://www.notion.so/Lost-in-Space-3715259887e64b67840b59765ff09e9a?pvs=4)

code in espaceteamDone.ino

Added Changes: 
- Leveling system (timer time decreases as levels increase proportionately to progress, At level 3+ implemented a word scramble method that swaps letters around and also make the commands longer, also implemented a way to add red dots all over the screen whenever you allow the timer to run out, which makes it harder to see and increases in number as a function of level).
- Created rooms where you can only communicate with people in the same rooms

Technical Documentation:
For the feature of adding a waiting room where you can choose to enter either room 1 or room 2, we first created a variable to represent the state that we were in. While in the start_screen state, the player would be on a page that prompts them to select a room. Within a while loop, set the screen for start_screen and keep waiting and calling digitalRad on BUTTON_LEFT and BUTTON_RIGHT. Handle logic for both and set the room to 1 or 2 accordingly. After returning from this screen, anytime a broadcast is sent or some “A”, “D” or “P” command is checked, add the room right after the letter at the 0th position of the broadcasted string. Check that the room of the player matches the room of the command or status updates being sent by the other players. All other logic stays the same, but now only allows communication between members in the same room.

For the leveling system, we make it so that every 20 points of progress the player “levels” and something gets harder. For example, the time to complete a task decreases per level and the higher the level, the more red dots appear on the player’s screen when the player’s timer expires. The red dots also increase difficulty by making things harder to see. This just draws red dots in a loop within the range of the screen. The final feature is a letter scrambler that takes place after the player reaches level 3.

To revamp the command system, we decided to add a third noun to the overall nouns following each command. Thus, saying the full command would be harder and take more time. To do this, we made a third array of distinct nouns and randomly chose a third noun to add within genCommand() to introduce increasing complexity as the Spaceteam reads out the commands. To take this one step further, we implemented letter scrambling to make it slightly more confusing when reading out the commands to your teammates. Specifically, we modified the genCommand() function to scramble a letter in any of the three nouns to another random letter. This is done by checking if global Boolean hardLevel is set to True, which controls third noun and letter scrambling implementations. When it is, the rand() function is used to determine a random letter to be used and it is then set to a random substring in the three nouns. All of these changes messed with the font sizing on the UI, so we also changed the font size of the commands so that the whole noun would fit. Overall, these changes should make for a challenging and fun experience!
