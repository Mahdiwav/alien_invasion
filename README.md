# Alien Invasion

A classic space shooter game built with Python and Pygame. Defend Earth from waves of invading aliens by shooting them down before they reach the planet!

## 🎮 Game Overview

Alien Invasion is a side-scrolling shooter where you control a spaceship at the bottom of the screen, defending against waves of aliens that move horizontally and gradually descend. Your goal is to eliminate all aliens in each wave while avoiding collisions. The game features progressive difficulty, scoring system, and multiple lives.

## ✨ Features

- **Classic Arcade Gameplay**: Simple yet engaging space shooter mechanics
- **Progressive Difficulty**: Game speed and alien point values increase with each level
- **Scoring System**: Track your score and compete for high scores
- **Multiple Lives**: Start with 3 ships - use them wisely!
- **Level Progression**: Clear waves to advance to increasingly challenging levels
- **Fullscreen Mode**: Immersive fullscreen gameplay experience
- **Visual Feedback**: Scoreboard showing current score, high score, level, and remaining ships

## 📋 Requirements

- Python 3.6 or higher
- Pygame library

## 🚀 Installation

1. **Clone or download this repository**

2. **Install Pygame** (if not already installed):
   ```bash
   pip install pygame
   ```

3. **Ensure image assets are present**:
   - The game requires `images/ship.bmp` and `images/alien.bmp` in the `images/` directory

## 🎯 How to Play

### Starting the Game

1. Run the game:
   ```bash
   python alien_invasion.py
   ```

2. Click the **"Play"** button to start a new game

### Controls

- **Left Arrow Key** (←): Move ship left
- **Right Arrow Key** (→): Move ship right
- **Spacebar**: Fire bullets
- **Q**: Quit the game

### Gameplay Mechanics

1. **Movement**: Use arrow keys to move your ship horizontally along the bottom of the screen
2. **Shooting**: Press and hold Spacebar to fire bullets. You can have up to 5 bullets on screen at once
3. **Eliminating Aliens**: Shoot aliens to destroy them and earn points
4. **Avoiding Collisions**: 
   - Don't let aliens touch your ship
   - Don't let aliens reach the bottom of the screen
5. **Level Completion**: Clear all aliens to advance to the next level
6. **Game Over**: The game ends when you run out of ships (lives)

### Scoring

- **Base Points**: Each alien destroyed is worth 50 points (increases with each level)
- **Level Multiplier**: Point values increase by 1.5x each level
- **High Score**: Your best score is tracked and displayed at the top center of the screen

### Difficulty Progression

- Each level increases game speed by 10%
- Alien point values increase by 50% per level
- The fleet moves faster and drops more frequently as levels advance

## 🏗️ Project Structure

```
alien_invasion/
├── alien_invasion.py    # Main game class and game loop
├── settings.py          # Game configuration and settings
├── ship.py             # Player ship class
├── alien.py            # Alien enemy class
├── bullet.py           # Bullet projectile class
├── game_stats.py       # Game statistics (score, level, lives)
├── scoreboard.py       # Score display and rendering
├── button.py           # Play button UI component
├── images/             # Game assets
│   ├── ship.bmp        # Player ship sprite
│   └── alien.bmp       # Alien enemy sprite
└── README.md           # This file
```

## 🔧 For Developers

### Architecture Overview

The game follows an object-oriented design with clear separation of concerns:

#### Core Components

1. **`AlienInvasion`** (`alien_invasion.py`): Main game controller
   - Manages game loop and event handling
   - Coordinates all game objects
   - Handles game state transitions
   - Renders the game screen

2. **`Settings`** (`settings.py`): Configuration management
   - Stores all game parameters (speeds, colors, dimensions)
   - Handles dynamic difficulty scaling
   - Centralized configuration for easy tweaking

3. **Game Objects** (Sprite-based):
   - **`Ship`**: Player-controlled spaceship
   - **`Alien`**: Enemy entities with horizontal movement
   - **`Bullet`**: Projectiles fired by the ship

4. **Game Systems**:
   - **`GameState`**: Tracks score, level, lives, and high score
   - **`Scoreboard`**: Renders HUD elements
   - **`Button`**: UI button for game start

### Key Design Patterns

- **Sprite Groups**: Uses Pygame's sprite groups for efficient collision detection and rendering
- **State Management**: Game active/inactive states control gameplay flow
- **Event-Driven**: Keyboard and mouse events drive player interaction

### Adding New Features

#### Adding New Enemy Types

1. Create a new class in a file (e.g., `alien_boss.py`) inheriting from `Sprite`
2. Add sprite image to `images/` directory
3. Import and instantiate in `alien_invasion.py`
4. Add to aliens group or create a new group for different behavior

#### Adding Power-ups

1. Create `powerup.py` with a `PowerUp` class (Sprite)
2. Add collision detection in `_check_bullet_collisions()` or `_update_aliens()`
3. Implement power-up effects in `Settings` or `Ship` class
4. Add visual feedback in `_update_screen()`

#### Modifying Game Speed

Edit values in `settings.py`:
- `ship_speed`: Player movement speed
- `bullet_speed`: Projectile velocity
- `alien_speed`: Enemy movement speed
- `speedup_scale`: Multiplier for level progression

#### Adding Sound Effects

1. Add sound files to a `sounds/` directory
2. Initialize mixer in `AlienInvasion.__init__()`:
   ```python
   pygame.mixer.init()
   ```
3. Load sounds and play at appropriate events (shooting, collisions, etc.)

#### Changing Screen Mode

In `alien_invasion.py`, modify the screen initialization:
- **Windowed mode**: Replace line 18 with:
  ```python
  self.screen = pygame.display.set_mode((self.settings.screen_width, self.settings.screen_height))
  ```
- **Fullscreen** (current): Uses `pygame.FULLSCREEN`

### Code Customization Points

#### Adjusting Fleet Formation

Modify `_create_fleet()` in `alien_invasion.py`:
- Change spacing by adjusting multipliers (currently `2 * alien_width`)
- Modify starting position logic
- Add randomization or patterns

#### Changing Bullet Behavior

Edit `Bullet` class in `bullet.py`:
- Modify `update()` for different trajectories
- Change appearance in `draw_bullet()`
- Adjust collision detection in `_check_bullet_collisions()`

#### Modifying Scoring

In `_check_bullet_collisions()`:
- Change point calculation logic
- Add multipliers for combos
- Implement bonus scoring conditions

### Common Modifications

#### Increase/Decrease Difficulty

**Easier Game**:
- Increase `ship_speed` in `settings.py`
- Increase `bullets_allowed`
- Decrease `speedup_scale`
- Increase `ship_limit`

**Harder Game**:
- Decrease `ship_speed`
- Decrease `bullets_allowed`
- Increase `speedup_scale`
- Decrease `ship_limit`

#### Visual Customization

- **Background Color**: Change `bg_color` in `Settings.__init__()`
- **Bullet Appearance**: Modify `bullet_color`, `bullet_width`, `bullet_height` in `Settings`
- **Button Styling**: Edit `button_color` and `text_color` in `Button.__init__()`

### Debugging Tips

1. **Print Statements**: Add print statements in update methods to track object positions
2. **Visual Debugging**: Draw rectangles around sprites to see collision boundaries
3. **Frame Rate**: The game runs at 60 FPS (see `self.clock.tick(60)`)
4. **Collision Detection**: Use `pygame.sprite.groupcollide()` for efficient collision checking

### Performance Considerations

- Sprite groups are used for efficient rendering and collision detection
- Bullets are removed when they leave the screen to prevent memory leaks
- The game uses a fixed timestep (60 FPS) for consistent gameplay

## 🐛 Known Issues / Future Improvements

- High score is not persisted between game sessions
- No sound effects or background music
- Limited visual variety (single alien type)
- No pause functionality
- No save/load game state

## 📝 License

This project is open source and available for educational purposes.

## 🤝 Contributing

Feel free to fork this project and add your own features! Some ideas:
- Sound effects and music
- Different alien types with unique behaviors
- Power-ups (rapid fire, multi-shot, shields)
- Boss battles
- High score persistence
- Pause menu
- Different difficulty modes
- Particle effects for explosions

---

**Enjoy the game and happy coding!** 🚀👾
