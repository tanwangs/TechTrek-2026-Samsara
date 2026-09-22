# The Tapestry of Monyul

*A 2D narrative exploration game built for TechTrek 2026, by team Samsara.*

> Working title in development docs: *The Forgotten Thread*

[![Tapestry of Monyul](https://img.youtube.com/vi/oOnbAjUEKRI/maxresdefault.jpg)](//www.youtube.com/watch?v=oOnbAjUEKRI "Tapestry of Monyul")


---

## Project Overview

*The Tapestry of Monyul* is a top-down narrative exploration game set
across three sacred sites in Bhutan — **Jomolhari**, **Drakay Pangtsho**,
and **Taktsang (Tiger's Nest Monastery)**. The player controls Tashi, a
young villager who has quietly stopped believing the old teachings about
balance and sacred places matter — until a small, personal moment (being
gently called out by the Village Elder for rushing past a household
shrine) and a strange dream about a fading, glowing tree set them on a
journey to each of the three sites.

Rather than teaching its themes through dialogue and exposition alone,
the game embeds its lessons directly into gameplay mechanics:

- **Jomolhari** — an offering ritual gated by a *pacing mechanic*: rush
  it, and the guardian Aum Jomo makes you slow down and try again,
  mechanically demonstrating that "intention matters more than action."
- **Drakay Pangtsho** — an environmental-observation quest where the
  player must notice what's wrong with the lake themselves before being
  told, rather than being handed the answer.
- **Taktsang** — a story-assembly quest where the player gathers
  fragments of the monastery's history from three monks and chooses how
  to retell it, rather than a simple checklist of tasks.

Each location also includes two side quests exploring a different form
of "paying attention" (stillness, tracking, cooperative care, patience
directed at others), and a functional **Awareness** stat that is earned
through attentive play and shapes the tone of the game's ending.

Built for the TechTrek 2026 challenge theme: *"Code, Create, and
Educate: Cross-Pollination Through Games."*

---

## Educational Focus

This project is designed to introduce players to Bhutanese cultural and
Buddhist values — respect for sacred places, environmental stewardship
of natural water sources, and the transmission of oral history — through
direct gameplay rather than lecture-style content. See `/docs` for the
full project documentation, including the User Requirement Specification
and Academic Integration write-up.

---

## Technologies Used

- **Engine:** [Godot Engine 4.7.2](https://godotengine.org/) (GDScript)
- **AI-assisted development:** [Ziva](https://ziva.sh), an in-editor AI
  development agent plugin for Godot, used throughout development for
  scene construction, scripting, and asset generation
- **Art:** custom pixel-art sprites (48×48, RGBA8) and tile-based terrain
  (TileMapLayer)

---

## Installation & Setup

1. Install [Godot Engine 4.7.2 or later](https://godotengine.org/download)
   (standard build, not required to be the .NET/C# build unless noted
   otherwise).
2. Clone this repository:
   ```
   git clone https://github.com/tanwangs/TechTrek-2026-Samsara.git
   ```
3. Open Godot, select **Import**, and navigate to the cloned project
   folder (the one containing `project.godot`).
4. Once imported, click **Edit** to open the project in the Godot editor,
   or press the **Play** button to run the game directly.

*[If the Godot project files live in a specific subfolder of this repo
rather than the root, update step 2–3 above with the correct path.]*

---

## Usage / Controls

| Action | Key |
|---|---|
| Move | WASD / Arrow keys |
| Interact (talk to NPCs, pick up items, enter the taxi) | E |
| Call the taxi (at a taxi stop) | T |

Start at the village, complete the movement and interaction tutorial,
then follow the dream sequence to the crossroads shrine, where you can
choose which of the three sacred sites to visit first.

---

## Team

| Name | Role |
|---|---|
| Jigme Tshering| Documentation/Storyline/Website |
| Sangay Tharchen | Documentation/Storyline/Sprites |
| Tandin Wangyel | Documentation/Developer |

---

## Documentation

Full project documentation — including the SDLC methodology, User
Requirement Specification, system design, testing notes, and challenges
encountered during development — is maintained in the [`/docs`](./docs)
folder of this repository.

---

## License

*[Fill in if applicable — e.g. an open-source license, or "All rights
reserved" for a competition submission.]*
