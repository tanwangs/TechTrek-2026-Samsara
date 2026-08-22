# Development & Implementation Details

## 3.9 Development Methodology (SDLC Model)

### Selected SDLC Model
This project follows an **Agile / Iterative Development Model**. 

### Justification for the Chosen Methodology
Because *The Tapestry of Monyul* relies heavily on narrative storytelling, dialogue pacing, and player reflection, an iterative model allows us to build a prototype of one *Nye* first (e.g., Jhomo Lhari), playtest the educational dialogue mechanics, and make adjustments before building out subsequent locations.

### Development Workflow
1. **Sprint Planning:** Define mechanics and dialogue trees for each specific *Nye*.
2. **Asset Creation & Mapping:** Design 2D sprites, tilemaps, and audio.
3. **Engine Implementation:** Script dialogue events, scene transitions, and environmental triggers.
4. **Testing & Feedback:** Conduct gameplay testing to evaluate cultural clarity and learning retention.

---

## 3.10 Implementation Details

### Game Engine & Core Technologies
*   **Game Engine:** [Godot]
*   **Programming Language:** []
*   **Dialogue Engine:** []
*   **Art & Assets:** 2D Tilemaps, Pixel Art Sprites, and ambient audio loops representing Bhutanese landscapes.

### Engine Mechanics & Structural Functionality
The selected game engine handles four primary systems essential to the gameplay loop:

1. **2D Movement & Physics Engine:** 
   * Uses top-down grid-based.
   * Collision boundaries ensure players stay within the sacred paths of the *Nyes* without clipping through terrain.

2. **Dialogue & Choice Engine:**
   * A node-based dialogue tree manages interactions with NPCs, monks, and deities (*Aum Jomo*, *Tshomen*).
   * Engine event listeners trigger pedagogical choices—allowing the player to ask questions about local traditions and receive reflective insights.

3. **Scene Management & Exploration:**
   * The engine seamlessly switches scenes as players travel between different *Nyes* (Jhomo Lhari $\rightarrow$ Drakay Pangtsho $\rightarrow$ Tak Tsang).
   * Camera tracking script follows the student avatar smoothly across large environmental maps.

4. **Environmental Reflection Triggers:**
   * Trigger volumes (invisible hitboxes) detect player presence near polluted areas or sacred waters, launching UI prompts that display historical and ecological facts.

### Code Structure and Modules
*   `PlayerController`: Manages movement inputs, animations, and interaction triggers.
*   `DialogueManager`: Loads conversation lines, handles branching choices, and updates learning progress flags.
*   `SceneLoader`: Handles fade-ins, fade-outs, and level transitions across different *Nyes*.
*   `UIManager`: Displays dialogue boxes, inventory items, and educational reflection prompts.

### Core Engine Architecture: Godot 4
*The Tapestry of Monyul* is developed using the **Godot Engine**. The architecture relies on Godot’s fundamental design principles: **Nodes** and **Scenes**.

---

### Nodes: The Fundamental Building Blocks
Nodes are the primary components used to create every entity within Godot. Whether building the student avatar, non-player characters (NPCs) like *Aum Jomo*, or dialogue UIs, nodes are combined and extended to achieve specific results.

#### Core Engine Concepts
*   **Specialized Functions:** Each node type serves a distinct purpose, such as displaying sprite graphics, playing environmental audio, or handling collision physics.
*   **The Scene Tree:** All nodes in the game are organized into a hierarchical, tree-like structure known as the **Scene Tree**.
*   **The Root Node:** The node at the very top of a scene's hierarchy serves as the root controller.
*   **Nesting and Reusability:** Nodes are bundled into scenes, acting as modular packages that can be nested within higher-level level maps.

#### Essential Game Nodes Used

| Node Type | Engine Purpose & Application in Project |
| :--- | :--- |
| `CharacterBody2D` | 2D physics body used for player movement and NPC pathing with environmental collision. |
| `AnimatedSprite2D` | Displays and controls frame-by-frame sprite animations for character movement. |
| `CollisionShape2D` | Defines physical boundaries (boxes/circles) for terrain, player hits, and interaction areas. |
| `Camera2D` | Controls the active viewport; set as a child of the player node to smoothly follow movement through *Nyes*. |
| `StaticBody2D` | Immovable physics body used for environmental boundaries, obstacles, and temple walls. |
| `AnimatableBody2D` | Moving physics body used for moving platforms or environmental puzzle elements. |
| `Area2D` | Triggers events without physical stopping power—used for detecting player entry into dialogue zones, lake shores, and story triggers. |
| `RayCast2D` | Invisible directional ray used for line-of-sight checks or detecting nearby terrain. |
| `AnimationPlayer` | Animates properties across nodes (e.g., screen fades, camera transitions, visual effects). |
| `AudioStreamPlayer` | Plays background ambient music (Nye themes) and sound effects. |

---

### Scenes: Reusable Systems & World Design
Scenes allow game elements to be bundled into modular, reusable packages. Instead of building the entire game world in one place, individual components (characters, dialogue boxes, sacred landmarks) are built in isolated scenes and combined to form full levels.

#### Architectural Principles
*   **Modularity:** Scenes range from small interactables (e.g., a prayer wheel or shrine) to entire game levels (e.g., *Tak Tsang* mountain pass).
*   **Nesting:** Individual scenes are nested within main level maps. For example, the `Player.tscn` and `NPC_Monk.tscn` are instanced directly into `TakTsang_Level.tscn`.
*   **Automatic Updates:** Editing a base scene (such as modifying the interaction prompt on an NPC) updates every instance across all *Nyes* automatically.

#### Workflow & Project Organization
*   **Scene Organization:** All `.tscn` files are organized under a dedicated `res://scenes/` directory in the project filesystem.
*   **Main Scene:** The initial entry point of the game (`Main.tscn`) loads the primary menu before transitioning to the student retreat opening sequence.
*   **Instancing:** Scenes are dragged directly into level viewports or spawned via script during runtime.

#### Global Systems (Autoloads / Singletons)
Global systems run independently of active level scenes to persist data across scene transitions:
*   **Global Data Manager (`Autoload`):** Tracks story progression, flags for visited *Nyes*, unlocked cultural dialogue nodes, and background audio states across level changes.
---

## 3.12 Deployment

### Deployment Environment
*   **Target Platform:** [e.g., Windows PC / Web Browser (WebGL) / macOS]

### Installation & Build Procedures
1. **Executable Build:** Generated directly through the engine's build manager.
2. **Web Build (If WebGL):** Hosted on **GitHub Pages** or **Itch.io** for instant browser playability without installation.

### Documentation & Repository Hosting
* **Repository:** Hosted on GitHub using standard Markdown documentation within the `/docs` directory.
* **Asset Storage:** Game builds are uploaded under **GitHub Releases**.
