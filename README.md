# Description
Static website made with Svelte dedicated to the critically endangered leopard subspecies Amur leopard. Made for Zoo of Hackclub!

# Interactive Elements
## /
### facts carousel (facts panel)
just followed the tutorial in slack. main research sources are listed in the footer.
### easter egg
click the fact icon/image 4x to see an easter egg (Raum pops up for a sec!) implemented using $effect to check and respond and svelte's reactivity to control
## meet-raum
### Raum
wrote stats.json for its different states, drew 2 nearly identical sprites, and created a statehandler with stats to interact with it and display current its state (description). the image changes with reactivity (am i using this term right??)
### controls/top buttons
using keydown eventlistener and svelte's onclick&js to modify stats/interact, whose actions effects are both logged and written to the status bar (green, bottom left)
### clicking Raum to pet
onclick&js - same effect as the button
### behind the scenes: interaction
if all three good stats are fulfilled (pet, play, fed; been pet, has played, and been fed respectively) then state is chosen from 3 relatively content states. otherwise if the state is something like hungry and Raum is not fed, corresponding bad stats (eg hungry) are increased. otherwise states are randomly picked from states.json. using $effect, when stats is updated a variable called ratio is updated along and action/effect are logged. the ratio also determines what state Raum gets; a ratio of (good stats)/(bad stats) below 0.4 results in the irritated state.