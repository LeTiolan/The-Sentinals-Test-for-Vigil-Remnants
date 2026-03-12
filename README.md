1. The State Machine (The "Brain")
Instead of just "moving toward the player," each Sentinel will have a variable that tracks its current State. This dictates how it moves and how the orb pulses.

STAGNANT (Dormant Mode): * Logic: The Sentinel is "powered down." It stays in one spot.

Visuals: The blue orb pulses very slowly, like a heartbeat. The head plates might be closed tight.

Trigger: It only "wakes up" if the player shines their light directly on it or gets within a very small radius.

IDLE (Patrol Mode): * Logic: The Sentinel picks an empty cell in the maze and moves toward it slowly.

Visuals: The head scans left and right. The walking animation is heavy and rhythmic.

CHASING (Active Hunt): * Logic: The player has been detected. The Sentinel calculates the shortest path to your coordinates.

Visuals: The orb turns a sharper, flickering blue (or perhaps red). The head plates flare out, and the walking speed doubles.

2. Procedural Walking (The "Bone Math")
Since we don't have a 3D animation file, we use Joint Relationships to simulate bones.

The Hip Pivot: Everything starts at the pelvis. When the Sentinel moves, the pelvis "bobs" up and down slightly.

The Sine Wave Stride: We use a mathematical wave to move the legs. When the "Wave" is at its peak, the left leg is forward and the knee is bent. When the "Wave" is at its trough, the right leg moves forward.

Foot-Planting Logic: To prevent the Sentinel from "skating" across the floor, we sync the speed of the leg swing to the speed of the ground movement. If the Sentinel moves 1 meter forward, the leg must swing exactly 1 meter back relative to the body.

3. Sensory Awareness (The "Vision")
Your current enemies simply know where you are at all times. To make the Antagonist feel fair and scary, we give it "Sensors":

Line of Sight (LOS): We draw an invisible line (a Raycast) from the Sentinel’s orb to the Player’s camera. If a wall is in the way, the Sentinel "loses" you and returns to its last known position to investigate.

Flashlight Detection: If the player's flashlight is ON and pointed toward the Sentinel, it detects the light from much further away than it would see the player in the dark.

Proximity Hearing: If the player is moving at full speed nearby, the Sentinel "hears" the footsteps and rotates its head toward the sound before deciding to chase.

4. Dynamic Animation (The "Personality")
We can use math to make the Sentinel look "alive" through small, reactive movements:

The "Apex Twitch": Every few seconds, we can add a tiny, random "shiver" to the head plates or the finger talons. This makes it look like a malfunctioning, high-strung machine.

Target Tracking: We can calculate the angle between the Sentinel's head and the player. We then use "Smoothing" (Lerping) to make the head slowly turn and "stare" at you as you move past, even if it hasn't started chasing yet.

Breathing Sync: When the Sentinel enters "Chase" mode, we increase the frequency of the chest expansion and the orb pulse. This creates a psychological "pressure" on the player—they can hear and see the machine getting more aggressive.

5. Integration into the "Vigil Remnants" Loop
When we do the surgery, we will modify the update() function in your game code:

The Loop: Instead of 12 Phantoms, we loop through our 4 Sentinels.

The Decision: Each Sentinel asks: "Can I see the player?"

The Movement: If yes, it calculates the "Bone Math" to walk toward you. If no, it continues its slow patrol.

The Animation: It updates its orb scale and head position based on its current state (Fast pulse for Chase, slow for Stagnant).
