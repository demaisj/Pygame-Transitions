Pygame-Transitions
==================

Beautiful &amp; easy transitions for pygame programs

##How does it works ?

It's very simple to implement this plugin, just follow theses 3 steps.

###1. Initialization

First, import the library: `import transitions`
And then after opening the window with `pygame.display.set_mode` call this function:
```python
transitions.init ( screen, window_width, window_height [ , background_color = [0, 0, 0] ] )
```
List of the parameters:
* `screen`: The screen variable returned by `pygame.display.set_mode` for draw
* `window_width`: The current window width
* `window_height`: The current window height
* `background_color`: *OPTIONNAL* The background color of the screen *(DEFAULT: [0, 0, 0] wich is black)*

**NOTE**: When resize the window, you should call again this initialization function.

###2. Refreshing screen

You should modify something in your program before using the transitions.
On the base of the main program loop suggested by [Paul Vincent Craven](http://simpson.edu/author/pcraven/) in [Program Arcade Games With Python And Pygame - Chapter 5.5](http://programarcadegames.com/index.php?lang=fr&chapter=introduction_to_graphics), like this below:

```python
#Loop until the user clicks the close button.
done = False
  
# Used to manage how fast the screen updates
clock = pygame.time.Clock()
  
# -------- Main Program Loop -----------
while not done:
    # ALL EVENT PROCESSING SHOULD GO BELOW THIS COMMENT
    for event in pygame.event.get(): # User did something
        if event.type == pygame.QUIT: # If user clicked close
            done = True # Flag that we are done so we exit this loop
    # ALL EVENT PROCESSING SHOULD GO ABOVE THIS COMMENT
  
  
    # ALL GAME LOGIC SHOULD GO BELOW THIS COMMENT
 
    # ALL GAME LOGIC SHOULD GO ABOVE THIS COMMENT
 
 
    # ALL CODE TO DRAW SHOULD GO BELOW THIS COMMENT
      
    # ALL CODE TO DRAW SHOULD GO ABOVE THIS COMMENT
      
    # Limit to 60 frames per second
    clock.tick(60)
```

You should add a condition to do game logic and draw processing, like this:
```python
# [...]
# -------- Main Program Loop -----------
while not done:
    # ALL EVENT PROCESSING SHOULD GO BELOW THIS COMMENT
    for event in pygame.event.get(): # User did something
        if event.type == pygame.QUIT: # If user clicked close
            done = True # Flag that we are done so we exit this loop
    # ALL EVENT PROCESSING SHOULD GO ABOVE THIS COMMENT
  
    if transitions.updateScreen() == False:
        # ALL GAME LOGIC SHOULD GO BELOW THIS COMMENT
 
        # ALL GAME LOGIC SHOULD GO ABOVE THIS COMMENT
 
 
        # ALL CODE TO DRAW SHOULD GO BELOW THIS COMMENT
      
        # ALL CODE TO DRAW SHOULD GO ABOVE THIS COMMENT
      
    # Limit to 60 frames per second
    clock.tick(60)
```

`transitions.updateScreen` returns `False` when no transition is processing. So you can continue the game. But if it returns a string (the name of the current processing transition), don't do anything.

You should never call `screen.fill` before calling `transitions.updateScreen` otherwise the transition will be a plain color. But keep on updating the screen after doing the transition/game logic.

###3. Calling a transition

```python
transitions.run ( name [ , duration = 1 [ , x = -1 [ , y = -1 ] ] ] )
```
List of parameters:
* `name`: The name of the transition.
  Available transitions:
  * `fadeOutUp`: Fades the page, change its orientation and zooms in to the selected point.
  * `fadeOutDown`: Fades the page and zooms out from the selected point.
* `duration`: *OPTIONNAL* The duration of the transition in seconds *(DEFAULT: 1 second)*
* `x`: *OPTIONNAL* X of the selected point for compatible transitions *(DEFAULT: -1 wich means center)*
* `y`: *OPTIONNAL* Y of the selected point for compatible transitions *(DEFAULT: -1 wich means center)*

NOTE: The transition will run at the next frame, but the screen will be copied at the call. So if you draw something after this call, it will be hidden on the transition.

##Contributing

Fell free to report any bug, or add your custom transitions !

##License

[The MIT License](https://github.com/DeathMiner/Pygame-Transitions/blob/master/LICENSE)
