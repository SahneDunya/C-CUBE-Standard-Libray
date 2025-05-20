C-CUBE Standard Library: Using Modules
The C-CUBE game engine comes with a set of powerful Standard Library Modules designed to simplify game development. These modules offer ready-to-use functions for common game development needs such as time management, random number generation, debugging tools, scene management, animation control, and 2D tilemaps.

In this document, you will learn how to import and use each standard library module within your C-CUBE code.

Importing Modules (import)
To use a module in C-CUBE, you must first import it at the beginning of your code file using the import keyword. The general syntax is as follows:

import "module_name" as Alias;

module_name: This is the filename of the module you want to import (e.g., "time_utils", "random_utils").

as Alias: This is optional but highly recommended. It allows you to define an alias for the module to call its functions in a shorter and more readable way. For example, using Time instead of time_utils.

Once imported, you can access the module's functions through the alias you defined: Alias.functionName().

Available Standard Library Modules
Here are the main modules available in C-CUBE's Standard Library, along with general information on their usage:

1. time_utils.ccb - Time Management
Provides time-related functions for game loops, animations, and event timing.

Import:

import "time_utils" as Time;

Key Functions:

Time.getGameTimeMs(): Returns the elapsed time in milliseconds since the game started.

Time.getGameTimeS(): Returns the elapsed time in seconds since the game started.

Time.sleepMs(milliseconds): Pauses program execution for the specified milliseconds (usually blocks the game loop, use with caution!).

Time.startStopwatch(): Starts a new stopwatch and returns its ID.

Time.getStopwatchElapsedS(stopwatchId): Returns the elapsed time of a stopwatch in seconds.

Time.getCurrentLocalTime(): Returns the current local time as a string.

Usage Example:
```
var startTime = Time.getGameTimeS();

fun myGameLoop() {
    var currentTime = Time.getGameTimeS();
    var elapsedTime = currentTime - startTime;
     Core.print("Elapsed time: " + elapsedTime + " seconds"); // Assumed Core.print
}
 Core.addLoopCallback(myGameLoop); // Assumed addition to game loop
```
2. random_utils.ccb - Randomness
Offers functions for generating random numbers, shuffling lists, and making probability-based decisions.

Import:

import "random_utils" as Rand;

Key Functions:

Rand.seed(seedValue): Initializes the random number generator. If none is provided, it uses the system time.

Rand.randomFloat(): Returns a floating-point number between 0.0 (inclusive) and 1.0 (exclusive).

Rand.randomRangeInt(min, max): Returns an integer between min (inclusive) and max (inclusive).

Rand.randomBool(probability): Returns true or false with the specified probability.

Rand.shuffle(list): Randomly shuffles the given list in place.

Rand.choose(list): Selects a random element from a list.

Usage Example:
```
Rand.seed(none); // For different results each run

var enemyDamage = Rand.randomRangeInt(10, 25);
 Core.print("Enemy dealt " + enemyDamage + " damage.");

if (Rand.randomBool(0.2)) { // 20% chance
     Core.print("Critical hit!");
}
```
3. debug_utils.ccb - Debugging Tools
Helps in monitoring your code, finding errors, and understanding performance during development.

Import:

import "debug_utils" as Debug;

Key Functions:

Debug.info(message): Prints an informational message to the console.

Debug.warn(message): Prints a warning message to the console.

Debug.error(message): Prints an error message to the console.

Debug.assert(condition, message): Asserts that a condition is true; if false, it throws an error and may halt the program.

Debug.startTimer(timerName) / Debug.stopTimer(timerName): Measures the performance of code blocks.

Debug.drawDebugPoint2D(x, y, r, g, b, duration): Draws a debug point on the screen.

Debug.ifDebug(callbackFunction): Encloses code that only runs in debug mode.

Usage Example:
```
Debug.info("Player is updating...");

var playerHealth = 100;
Debug.assert(playerHealth >= 0, "Player health cannot be negative!");

Debug.startTimer("PlayerUpdate");
// Player update logic goes here
Debug.stopTimer("PlayerUpdate");

Debug.ifDebug(fun () {
    // Draw player position in debug mode
    // Debug.drawDebugPoint2D(player.x, player.y, 1.0, 0.0, 0.0, 0.1);
});
```
4. game_utils.ccb - General Game Utilities
Provides functions that facilitate the overall game flow, state, and basic management.

Import:

import "game_utils" as Game;

Key Functions:

Game.setGameState(stateName): Sets the current state of the game (e.g., "PLAYING", "MENU").

Game.quitGame(): Exits the game.

Game.loadScene(sceneName): Loads a specific scene.

Game.saveGame(data, filename): Saves game data.

Game.loadGame(filename): Loads game data.

Game.createObjectPool(objectType, initialSize): Creates an object pool.

Game.getPooledObject(objectType): Retrieves an object from the pool.

Game.setTimedCallback(delayMs, callbackFunction, repeat): Defines delayed or repeating callbacks.

Usage Example:
```
Game.setGameState("MENU");

// When the play button is clicked from the menu
fun onPlayButtonClicked() {
    Game.loadScene("Level1");
    Game.setGameState("PLAYING");
}

var playerScore = 1250;
Game.saveGame({"score": playerScore, "level": 3}, "my_save.json");
```
5. animation.ccb - Animation Control
Used to play and manage animations for game objects.

Import:

import "animation" as Anim;

Key Functions:

Anim.loadAnimation(path, type): Loads animation data and returns an ID.

Anim.playAnimation(entityId, animationId, loop, speedMultiplier, blendDuration): Plays an animation on an entity.

Anim.stopAnimation(entityId): Stops the animation.

Anim.setAnimationSpeed(entityId, speedMultiplier): Sets the animation playback speed.

Anim.isAnimationPlaying(entityId): Checks if an animation is currently playing.

Anim.registerAnimationFinishedCallback(entityId, callback): Callback triggered when an animation finishes.

Anim.registerAnimationEventCallback(entityId, eventName, callback): Triggers event tags within an animation.

Usage Example:
```
var playerIdleAnim = Anim.loadAnimation("assets/player_idle.anim", "SKELETAL");
var playerWalkAnim = Anim.loadAnimation("assets/player_walk.anim", "SKELETAL");

var playerEntity = Scene.createEntity(none, "Player"); // Assumed from Scene module

Anim.playAnimation(playerEntity, playerIdleAnim, true, 1.0, 0.0); // Start idle animation

fun onPlayerMove() {
    if (Anim.getCurrentAnimationName(playerEntity) != "walk") {
        Anim.playAnimation(playerEntity, playerWalkAnim, true, 1.0, 0.1); // Transition to walk animation (0.1s blend)
    }
}
```
6. scene.ccb - Scene and Game Object Management
Provides core functions for organizing and managing the game world (scene) and its game objects (entities).

Import:

import "scene" as Scene;

Key Functions:

Scene.createScene(sceneName): Creates a new scene and sets it as active.

Scene.createEntity(parentId, name): Creates a new game object (entity).

Scene.destroyEntity(entityId): Removes an entity from the scene.

Scene.setPosition(entityId, x, y, z): Sets an entity's position.

Scene.addComponent(entityId, componentType, config): Adds a component to an entity (e.g., "Renderer", "Physics").

Scene.updateScene(deltaTime): Updates all entities and components in the scene.

Scene.renderScene(): Renders all visible entities in the scene.

Usage Example:
```
Scene.createScene("MyFirstLevel");

var player = Scene.createEntity(none, "PlayerCharacter");
Scene.setPosition(player, 10, 0, 5);
Scene.addComponent(player, "Renderer", {"model": "player.obj", "texture": "player.png"});
Scene.addComponent(player, "Physics", {"type": "DYNAMIC"});

var enemy = Scene.createEntity(none, "Enemy1");
Scene.setPosition(enemy, 20, 0, 15);
```
7. entity.ccb - Specific Game Object Operations
In addition to scene.ccb's general scene management, this module is used to directly manipulate the properties of a specific game object (entity).

Import:

import "entity" as Entity;

Key Functions:

Entity.getName(entityId): Returns the entity's name.

Entity.isActive(entityId) / Entity.setActive(entityId, active): Manages the entity's active state.

Entity.setPosition(entityId, x, y, z): Directly sets the entity's position (similar to Scene module).

Entity.translate(entityId, dx, dy, dz): Moves the entity by a specified amount.

Entity.addComponent(entityId, componentType, config): Adds a component to an entity (similar to Scene module).

Entity.setComponentProperty(entityId, componentType, propertyName, value): Sets a component's property.

Entity.setParent(entityId, parentId): Sets the entity's parent (hierarchy).

Usage Example:
```
var myPlayer = Scene.findEntityByName("MainPlayer"); // Get entity from Scene module

if (myPlayer != none) {
    var currentPos = Entity.getPosition(myPlayer);
    Entity.translate(myPlayer, 0.0, 1.0, 0.0); // Move player 1 unit up on the y-axis

    if (Entity.hasComponent(myPlayer, "Physics")) {
        Entity.setComponentEnabled(myPlayer, "Physics", false); // Disable physics component
    }
}
```
8. tilemap.ccb - Tilemap Management (2D)
Used for creating and managing tile-based worlds in 2D games.

Import:

import "tilemap" as Tilemap;

Key Functions:

Tilemap.loadTilemap(path): Loads a map from a tilemap definition file (e.g., Tiled export).

Tilemap.setTile(tilemapId, layerIndex, x, y, tileId): Sets the tile ID at specific grid coordinates.

Tilemap.getTile(tilemapId, layerIndex, x, y): Returns the tile ID at specific coordinates.

Tilemap.worldToGrid(tilemapId, worldX, worldY): Converts world coordinates to grid coordinates.

Tilemap.checkCollision(tilemapId, entityX, entityY, entityWidth, entityHeight, collisionLayers): Checks for collision between an entity and the tilemap.

Tilemap.renderTilemap(tilemapId, cameraX, cameraY): Renders the tilemap to the screen.

Usage Example:
```
var levelMap = Tilemap.loadTilemap("levels/forest_level.json");

fun playerCollisionCheck(playerEntity, deltaTime) {
    var playerPos = Entity.getPosition(playerEntity);
    var playerWidth = 32; // Assumed
    var playerHeight = 32; // Assumed

    var collisionInfo = Tilemap.checkCollision(levelMap, playerPos.x, playerPos.y, playerWidth, playerHeight, [0, 1]); // Check first 2 layers

    if (collisionInfo.collided) {
        // Core.print("Collision type: " + collisionInfo.collisionType + " tile: " + collisionInfo.tileX + "," + collisionInfo.tileY);
        // Apply player logic based on collision type
    }
}
```
9. camera.ccb - Camera Control
Manages camera properties that control how the game world is displayed to the player.

Import:

import "camera" as Cam;

Key Functions:

Cam.createCamera(): Creates a new camera.

Cam.setActiveCamera(cameraId): Sets the active rendering camera.

Cam.setPosition(cameraId, x, y, z): Sets the camera's position.

Cam.setRotation(cameraId, pitch, yaw, roll): Sets the camera's rotation.

Cam.lookAt(cameraId, targetX, targetY, targetZ, upX, upY, upZ): Makes the camera look at a specific point.

Cam.setFOV(cameraId, fovDegrees): Sets the camera's field of view (3D).

Cam.setOrthographic(cameraId, width, height): Sets the camera to 2D orthographic mode.

Cam.followTarget(cameraId, targetEntityId, offsetX, offsetY, offsetZ, smoothFactor): Makes the camera follow an entity.

Usage Example:

var mainGameCamera = Cam.createCamera();
Cam.setActiveCamera(mainGameCamera);

Cam.setPosition(mainGameCamera, 0, 10, -15);
Cam.lookAt(mainGameCamera, 0, 0, 0, 0, 1, 0);

var player = Scene.findEntityByName("PlayerCharacter"); // Assumed

if (player != none) {
    Cam.followTarget(mainGameCamera, player, 0, 5, -8, 0.1); // Follow player from slightly behind and above
}

These standard library modules will provide you with a powerful starting point for your C-CUBE game development journey. Exploring and utilizing the functions offered by each module will help you bring your games to life faster and more efficiently.

Please don't hesitate if you need details or usage examples for another module!
