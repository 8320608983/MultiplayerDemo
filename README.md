# MultiplayerDemo
Perfect. You now have the hardest foundational part working: two Fusion players, authority, prediction/reconciliation, movement, and mouse look.

The next thing should be shooting + damage + death/respawn. Don't build the lobby UI yet; gameplay should be proven first.

Your next milestone should be:

Player 1
   ↓
Left Click
   ↓
Raycast
   ↓
Player 2 hit
   ↓
20 damage
   ↓
100 → 80 → 60 → 40 → 20 → 0
   ↓
Death
   ↓
3 seconds
   ↓
Respawn
   ↓
100 HP
Step 1 — Ask Codex to implement shooting only
Send this prompt next:

:::writing{variant="document" id="27461" title="Codex — Fusion Raycast Shooting"} The Photon Fusion 2.1.3 multiplayer foundation and networked player movement are working correctly.

Current working systems:

Photon Fusion 2.1.3
Host Mode
2-player session
Networked Capsule player
NetworkCharacterController
CharacterController
Tick-based Fusion input
WASD movement
Jump
Mouse look
Local input authority
Network synchronization
Prediction/reconciliation
Now implement ONLY the shooting system.

Do NOT implement health, damage, death, respawn, lobby, scoring, match logic, or final UI yet.

GAME REQUIREMENTS:

The player uses a simple Cube as a gun.

Add:

Player ├── Camera └── Gun

Gun:

Use a Unity Cube primitive.
Make it a simple visual gun.
No animation.
No imported model.
SHOOTING:

Left mouse button shoots.
Use a Physics.Raycast hitscan.
Ray starts from the local player's camera.
Ray direction is the camera's forward direction.
Use a configurable shooting range, default 100 meters.
Use a configurable fire rate.
Prevent the player from shooting faster than the configured fire rate.
Do not instantiate physical bullet GameObjects.
Do not create projectile objects.
MULTIPLAYER:

Use the correct Photon Fusion 2.1.3 authority model.

Important:

Only the local input-authority player can request shooting.
The host/state authority must validate the shot before applying gameplay effects.
Do not trust a client to directly modify another player's health.
Do not use ordinary local-only damage logic.
Use the appropriate Fusion RPC/input/state-authority pattern for Fusion 2.1.3.
For now, shooting only needs to detect what was hit and report/log the result.

Example:

Player 1 shoots Player 2:

"Player 1 hit Player 2"

Do NOT implement health yet.

CROSSHAIR:

Add a very simple UI crosshair:

Small white "+" in the center of the screen.
No external assets.
OPTIMIZATION:

Use Physics.Raycast.
Do not Instantiate/Destroy bullets.
Cache camera references.
Avoid GameObject.Find().
Avoid unnecessary Update() logic.
Keep shooting logic simple.
IMPORTANT:

Inspect the existing project before modifying anything.

Do not duplicate:

NetworkRunner
NetworkFoundationBootstrap
PlayerNetworkInput
NetworkPlayerMovement
Preserve all existing working movement and networking.

Use Photon Fusion 2.1.3 APIs already installed in the project.

Do not use old Fusion 1 APIs.

After implementation report:

Files created.
Files modified.
Shooting architecture.
How authority validates shooting.
Gun prefab/hierarchy.
Inspector settings.
How to test Player 1 shooting Player 2.
How to test Player 2 shooting Player 1.
Any compile errors.
Any warnings.
STOP after shooting and hit detection work.

Do not implement health or damage yet. :::

What you should verify
After Codex finishes, test:

Player 1
     🔫
      │
      │ Raycast
      ↓
Player 2
You should be able to see something like:

Player 1 hit Player 2
And importantly:

Player 1 shoots
        ↓
Host validates
        ↓
Player 2 is detected
Don't worry about health yet.

Step 2 — Then add health
Once shooting works, we make a separate milestone:

100 HP
 ↓
80
 ↓
60
 ↓
40
 ↓
20
 ↓
0
We'll make health a networked state, with damage controlled by the appropriate Fusion authority.

Then:

HP: 100
will appear in the HUD.

Step 3 — Then death and respawn
After health:

HP reaches 0
      ↓
IsDead = true
      ↓
Disable movement/shooting
      ↓
3 second timer
      ↓
Spawn position
      ↓
HP = 100
      ↓
IsDead = false
For your simple demo, we don't need to destroy/reinstantiate the player every time. Reusing the networked player object is cleaner and avoids unnecessary spawning.

Step 4 — Then match logic
After combat is working, add:

Player 1 kills Player 2
             ↓
        Round ends
             ↓
      Player 1 Wins
You could keep the match extremely simple:

First player to kill the opponent wins.
Show result screen.
Play Again.
Return to lobby.
No need for complicated rounds unless your exam requires them.

Step 5 — THEN build the lobby
This is where your existing scenes become useful:

Bootstrap
    ↓
MainMenu
    ↓
Lobby
    ↓
Waiting Room
    ↓
Game
    ↓
Result
The lobby can have:

Main Menu
SIMPLE 1V1 FPS

[ CREATE GAME ]

[ JOIN GAME ]

[ EXIT ]
Create Game
CREATE GAME

Room Name:
[ ABC123 ]

[ CREATE ]
[ BACK ]
Join Game
JOIN GAME

Room Code:
[ ABC123 ]

[ JOIN ]
[ BACK ]
Waiting Room
WAITING FOR PLAYER

Player 1     ✓
Player 2     ...

[ START ]
Once two players are connected:

Player 1     ✓
Player 2     ✓

[ START GAME ]
Your project is now at this stage
✅ Unity 6
✅ Photon Fusion 2.1.3
✅ Photon App ID
✅ Fusion Host Mode
✅ Two-player session
✅ NetworkRunner
✅ Networked Capsule
✅ NetworkCharacterController
✅ CharacterController
✅ Fusion tick-based input
✅ WASD
✅ Jump
✅ Mouse look
⬇
🔨 NEXT: Raycast shooting
⬇
🔨 Health 100
⬇
🔨 20 damage
⬇
🔨 Death
⬇
🔨 3-second respawn
⬇
🔨 Match/win
⬇
🔨 Lobby
⬇
🔨 Waiting room
⬇
🔨 HUD
⬇
🔨 Result screen
⬇
🔨 Object pooling/optimization
⬇
🎮 FINAL DEMO
So don't change anything else right now. Give Codex the shooting prompt above and get raycast hit detection working first. Once you have its result, send me that result and we'll build the health system on top of it without breaking your working Fusion architecture.
