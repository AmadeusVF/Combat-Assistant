# Combat Assistant

**Combat Assistant** is a lightweight Roll20 Mod script for D&D 5e that automates common combat bookkeeping directly from chat while keeping Roll20's normal character sheets, tokens, and Turn Order at the center of play.

It can read attacks, damage, healing, saving throws, initiative, character resources, spell slots, attacks, and spells from compatible D&D 5e sheets; resolve damage against token defenses; manage concentration and area effects; and turn Roll20's Turn Order into an interactive turn-by-turn combat interface.

> Combat Assistant was originally extracted from the abandoned **Trinkets & Trackers v1.3.8** codebase. It now continues as a standalone combat-focused script and is designed to work especially well alongside the new **Trinkets & Trackers v2.3.0**.

**Current version:** `1.2.8`  
**Author:** [AmadeusVF](https://www.patreon.com/cw/AmadeusVF/home)

---

## Contents

- [Overview](#overview)
- [Main Features](#main-features)
- [Turn Tracker](#turn-tracker)
- [Resources](#resources)
- [Combat List](#combat-list)
- [Spell List](#spell-list)
- [Damage, Healing & Defenses](#damage-healing--defenses)
- [Saving Throws & Initiative](#saving-throws--initiative)
- [Player Combat Controls](#player-combat-controls)
- [Area Effects](#area-effects)
- [Concentration](#concentration)
- [Combat Visual Effects](#combat-visual-effects)
- [Compatibility](#compatibility)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Commands](#commands)
- [Configuration](#configuration)
- [Token Bar Configuration](#token-bar-configuration)
- [Animated Tokens](#animated-tokens)
- [Trinkets & Trackers](#trinkets--trackers)
- [Notes](#notes)

---

# Overview

Combat Assistant is intended to reduce the amount of time a GM and players spend opening character sheets, manually changing HP, checking AC, tracking resources, resolving saving throws, counting movement, and moving through the Turn Order.

It does **not** replace Roll20's normal combat tools.

Instead, it builds automation around them:

- Roll20 chat remains the source of normal attack, damage, healing, and spell rolls.
- Roll20 tokens remain the physical representation of creatures.
- Roll20 token bars remain available for HP, AC, and Temporary HP.
- Roll20's Turn Order remains the initiative tracker.
- Character sheets remain the source of attacks, spells, resources, saving throws, initiative, and defenses.

Combat Assistant connects those systems and adds a layer of automation on top.

---

# Main Features

### Combat automation

- Reads Roll20 attack, damage, healing, and spell rolls.
- Generates compact combat action cards.
- Resolves attacks against the target's configured AC bar.
- Applies damage and healing to selected tokens.
- Supports Temporary HP.
- Reads compatible sheet resistances, immunities, and vulnerabilities.
- Can request or roll saving throws.
- Supports half damage on successful saves.
- Supports critical attacks and multi-part damage.
- Can keep token names private in public combat logs.

### Turn management

- Tracks the active combatant from Roll20's Turn Order.
- Tracks combat rounds.
- Generates a Turn Card for the active token.
- Lets controlled players advance their own turn.
- Can automatically focus the table on the current combatant.
- Supports a configurable visual Turn Marker.
- Can track movement and Dash.
- Can remove defeated NPCs from the Turn Order.
- Can process finite concentration durations on turns.

### Character access

- Lists attacks without opening the character sheet.
- Lists combat spells without opening the character sheet.
- Displays limited resources and spell slots.
- Lets resources be spent or recovered from chat.
- Supports both player-controlled characters and NPC workflows.

### Area combat

- Creates movable Roll20 area markers.
- Supports circular/radius areas.
- Supports squares and cubes.
- Supports cones.
- Supports lines.
- Can keep area markers active until all saving throws finish.
- Can preserve concentration-based area markers.
- Can perform range checks from the caster.

### Visual feedback

- Optional Roll20 FX for damage.
- Optional projectile FX.
- Optional area-hit FX.
- Healing and Temporary HP FX.
- Customizable marker images and chat background.

---

# Turn Tracker

The **Turn Tracker** turns Roll20's normal Turn Order into an interactive combat flow.

When combat is active, Combat Assistant identifies the token whose turn is currently at the top of the Turn Order and can generate a dedicated **Turn Card** for that creature.

The Turn Card can provide access to:

**Dash · Disengage · Dodge · Combat · Spells**

Depending on configuration, it can also show limited resources and spell slots.

Players can use **Next** to finish a turn they control. Combat Assistant advances Roll20's Turn Order, updates the active combatant, refreshes the Turn Card, and keeps track of the current round.

The GM retains full control and can manually remove turns or stop the active combat.

## Turn Tracker settings

| Setting | Description |
| --- | --- |
| **Turn Tracker** | Enables Combat Assistant's turn management system. Tracks the current combatant and rounds directly from Roll20's Turn Order and generates Turn Cards during combat. |
| **Turn Auto Focus** | Automatically pings and moves everyone's view to the token whose turn has just started. |
| **Turn Token Action** | Adds quick action controls to the Turn Card, including **Dash, Disengage, Dodge, Combat, and Spells**. |
| **Turn Movement Tracker** | Tracks how much movement the active token spends during its turn. Warns the player and GM when the token exceeds its available speed, while Dash increases the movement allowance automatically. |
| **Conc. Turn Tracker** | Connects finite concentration duration to the Turn Tracker. Remaining turns decrease when the concentrating creature reaches its turn and concentration ends automatically at zero. |
| **Round Counter** | Tracks combat rounds and shows the GM a Round Counter card containing the tokens currently participating in combat. |
| **Public Round Counter** | Also displays the Round Counter publicly to the players. Requires **Round Counter**. |
| **Remove NPC Dead Tokens** | Automatically removes defeated unlinked NPCs from the Turn Order at 0 HP. When disabled, the GM receives a manual **Remove** control. |
| **Turn Marker** | Places a visual marker around the token whose turn is currently active. |
| **Turn Marker Token Public** | Controls whether the Turn Marker is visible to everyone or remains on the GM layer. |
| **Turn Marker Token Image** | Sets the Roll20 image or animated asset used by the Turn Marker. |
| **Turn Marker Token Size %** | Controls how much larger the marker is than the active token. `20` means 20% larger. |
| **Turn Marker Follow** | Keeps the marker centered and scaled when the current token moves or is resized. |

---

# Resources

Combat Assistant can read limited-use character resources and spell slots and display them directly in chat.

This is especially useful during combat because the GM or player can see relevant resources without repeatedly opening the character sheet.

Examples include resources such as class features, limited-use abilities, and spell slots when they are exposed by the supported sheet.

Resource controls can also adjust the current amount and report the remaining value.

## Resource settings

| Setting | Description |
| --- | --- |
| **Show Player Resources** | Shows the active player-controlled token's limited resources and spell slots directly on its Turn Card. |
| **Show NPC Resources** | Shows limited resources and spell slots for NPCs on the GM's Turn Card only. |
| **Player Public Usage** | When enabled, player resource use/recovery updates are sent to public chat. When disabled, they remain private. |

Resources can also be opened independently:

```text
!ca resources
!ca resources <sheet name>
```

---

# Combat List

Combat Assistant can build an attack list directly from a character sheet.

```text
!ca combat
```

With a token selected, the command opens the combat list for that character.

You can also open a specific sheet by name:

```text
!ca combat <sheet name>
```

The combat list is designed to give quick access to sheet attacks without requiring the user to keep the full character sheet open during every turn.

When **Turn Token Action** is enabled, the active creature's Turn Card includes a **Combat** button that opens this list directly.

---

# Spell List

Combat Assistant can also read and display combat spells from compatible character sheets.

```text
!ca spells
```

or:

```text
!ca spells <sheet name>
```

The spell interface can expose relevant spell information and casting controls while using the underlying Roll20 sheet for the actual character data.

Spell-slot information can be integrated with the Resource system.

When **Turn Token Action** is enabled, the active creature's Turn Card includes a **Spells** button for direct access.

---

# Damage, Healing & Defenses

Combat Assistant can process damage and healing manually or from compatible Roll20 chat rolls.

## Damage

Damage can be resolved against:

- Armor Class
- Saving Throw DC
- Damage type
- Resistances
- Immunities
- Vulnerabilities
- Temporary HP
- Current HP

A direct manual example:

```text
!ca deal manual 10 Fire
```

Attack-style resolution:

```text
!ca deal manual 10 Fire 13
```

Saving throw resolution:

```text
!ca deal manual 10 Fire 13 Dexterity
```

Half damage on a successful save:

```text
!ca deal manual 10 Fire 13 Dexterity yes
```

## Healing

Normal HP:

```text
!ca heal manual hp 10
```

Temporary HP:

```text
!ca heal manual temp 10
```

Combat Assistant uses the configured token bars and supported sheet APIs to keep token/sheet health behavior consistent where possible.

---

# Saving Throws & Initiative

Combat Assistant provides tools for individual and grouped saving throw / initiative workflows.

```text
!ca save <ability>
!ca init
```

Supported abilities:

- Strength
- Dexterity
- Constitution
- Intelligence
- Wisdom
- Charisma

Depending on the sheet and configuration, Combat Assistant can either use Roll20's native sheet buttons or resolve supported rolls itself.

Player-controlled tokens can optionally be asked to make their own saving throw or initiative roll.

The script includes separate handling for compatible **2014** and **2024** D&D 5e sheet behavior.

---

# Player Combat Controls

Combat Assistant can generate actionable buttons for players when compatible chat rolls are detected.

## Player Attack Button

Captured attacks can be sent to the controlling player. The player can select a target and Combat Assistant can resolve the attack against its AC and apply damage.

## Player Healing Button

Captured healing can be sent to the controlling player so they can choose a target and apply the healing.

## Player Manual Roll

Player-controlled tokens can be asked to make their own saving throws or initiative rolls when Roll20 exposes a usable sheet roll.

## Player Target Range Check

Generated player actions can validate the distance between the acting token and the chosen target.

---

# Area Effects

Combat Assistant can create movable area-marker tokens for compatible area spells and actions.

The player places the marker on the tabletop and presses **Roll**. Combat Assistant then determines which tokens are inside the affected area.

Supported area handling includes:

- Radius / circular areas
- Spheres
- Cylinders
- Squares
- Cubes
- Cones
- Lines
- Emanation-style areas where detectable

Area markers can use custom Roll20-hosted images and configurable opacity.

## Area options

### Keep Marker Until Rolls Finish

Keeps the marker visible while affected creatures are still resolving saving throws and damage.

### Marker Free Movement

Allows the marker to move freely. When disabled, applicable markers can use grid-oriented positioning behavior.

### Area Range Checking

Combat Assistant can restrict marker placement based on the caster's range.

### Multiple detected areas

When an action exposes multiple possible area interpretations, Combat Assistant can create alternatives and let the user keep the relevant marker.

---

# Concentration

Combat Assistant includes concentration tracking for compatible spell workflows.

It can:

- Record the concentrating caster.
- Keep compatible concentration area markers active.
- Request concentration checks when the caster takes damage.
- Provide controls to inspect or end concentration.
- Remove linked area markers when concentration ends.
- Optionally track finite concentration durations through the Turn Tracker.

Useful command:

```text
!ca conc
```

When **Conc. Turn Tracker** is enabled, finite durations can count down as the concentrating creature reaches its turns.

---

# Combat Visual Effects

Combat Assistant can optionally use Roll20 FX to provide visual feedback when combat actions are resolved.

Supported visual categories include:

- Projectile effects
- Direct-hit effects
- Area-hit effects
- Healing effects
- Temporary HP effects
- Cone / breath-style effects
- Line / beam-style effects
- Self-centered area effects

Built-in effects can use damage-type-aware visual colors, while exact Roll20 Custom FX names can also be configured.

Visual effects are optional and can be disabled without affecting combat resolution.

---

# Compatibility

Combat Assistant contains dedicated handling for compatible:

- **D&D 5e 2024 Roll20 sheets**
- **D&D 5e 2014 Roll20 sheets**

The implementation detects sheet behavior and uses the appropriate Roll20 mechanisms where available.

Because the two sheet generations expose data differently, not every automated workflow is necessarily identical between 2014 and 2024.

Combat Assistant also uses Roll20 token bars for configurable combat data:

- HP
- AC
- Temporary HP

---

# Installation

1. Open the Roll20 game where you want to use Combat Assistant.
2. Open the game's **Mod / API Scripts** area.
3. Create a new script.
4. Copy the contents of `combatassistant.js` into the script editor.
5. Save the script and allow the Roll20 Mod sandbox to restart.
6. In game chat, run:

```text
!ca menu
```

Then open:

```text
!ca settings
```

and confirm that the HP, AC, and Temporary HP bars match your token setup.

Combat Assistant is a standalone script. Trinkets & Trackers is **not required** to run it.

---

# Quick Start

The three most useful commands after installation are:

```text
!ca menu
!ca settings
!ca help
```

A typical setup is:

1. Configure HP, AC, and Temporary HP token bars.
2. Enable the desired chat/combat automation.
3. Enable Turn Tracker.
4. Add creatures to Roll20's Turn Order normally.
5. Use Combat Assistant's Turn Cards, Combat list, Spell list, Resources, and action buttons during play.

---

# Commands

## Main

| Command | Description |
| --- | --- |
| `!ca menu` | Opens the main Combat Assistant menu. |
| `!ca help` | Shows the built-in help card. |
| `!ca settings` | Opens Combat Assistant settings. |
| `!ca deal manual <dmg> <type> <DC> <Attr> <half>` | Applies manual damage. Most parameters after damage are optional. |
| `!ca heal manual <hp/temp> <value>` | Restores HP or grants Temporary HP. |
| `!ca save <ability>` | Rolls the selected token's saving throw. |
| `!ca init` | Rolls initiative for the selected token. |

## Combat & Spells

| Command | Description |
| --- | --- |
| `!ca combat` | Opens the attack list for the selected token. |
| `!ca combat <sheet name>` | Opens the attack list for a named character sheet. |
| `!ca spells` | Opens the spell list for the selected token. |
| `!ca spells <sheet name>` | Opens the spell list for a named character sheet. |
| `!ca dash` | Declares Dash for the token currently in turn. |
| `!ca disengage` | Declares Disengage for the token currently in turn. |
| `!ca dodge` | Declares Dodge for the token currently in turn. |

## Turn Tracker

| Command | Description |
| --- | --- |
| `!ca turn` | Shows the Turn Card for the token currently in turn. |
| `!ca turnnext` | Ends the current turn and advances to the next token. |
| `!ca turnfocus` | Focuses the view on the current token. Players may use it only for a turn they control. |
| `!ca turnstop yes` | Ends the active combat and stops the Turn Tracker. |

Equivalent subcommands are also available through the `turn` route, such as:

```text
!ca turn next
!ca turn focus
```

GM-only turn-management controls include removing turns and stopping combat.

## Resources

| Command | Description |
| --- | --- |
| `!ca resources` | Shows resources for the selected token. |
| `!ca resources <sheet name>` | Shows resources for a named character sheet. |

---

# Configuration

Combat Assistant's settings are available through:

```text
!ca settings
```

The configuration is divided into several areas.

## Main

- Chat Tracking
- Concentration Tracking
- 2024 Combat Assistant Rolls Initiative
- 2014 Combat Assistant Rolls
- HP Bar
- AC Bar
- Temporary HP Bar
- Damage Round Up
- Read Sheet Resistances
- Reveal Damage Source in Log
- Reveal Token Names in Log

## Players

- Player Manual Roll
- Player Healing Button
- Player Attack Button
- Player Target Range Check
- Player Token Area Mark

## Effects

- Keep Marker Until Rolls Finish
- Marker Free Movement
- Square Marker Roll20 URL
- Radius Marker Roll20 URL
- Marker Opacity
- Combat Visual Effects
- Projectile Effect Name
- Direct Hit Effect Name
- Area Hit Effect Name

## Turn Tracker

- Turn Tracker
- Turn Auto Focus
- Turn Token Action
- Turn Movement Tracker
- Conc. Turn Tracker
- Round Counter
- Public Round Counter
- Remove NPC Dead Tokens
- Turn Marker
- Turn Marker Token Public
- Turn Marker Token Image
- Turn Marker Token Size %
- Turn Marker Follow

## Resources

- Show Player Resources
- Show NPC Resources
- Player Public Usage

## Extra

- Chat background image
- Temporary advanced debugging controls

Debug controls are intentionally session-only and return to their defaults when the Roll20 API sandbox restarts.

---

# Token Bar Configuration

Combat Assistant can be configured to use different token bars.

```text
!ca set hpbar <1-4>
!ca set acbar <1-4>
!ca set tempbar <0-4>
```

Example:

```text
!ca set hpbar 1
!ca set acbar 2
!ca set tempbar 3
```

Temporary HP can be disabled by setting its bar to `0`:

```text
!ca set tempbar 0
```

---

# Animated Tokens

Combat Assistant supports Roll20 animated token assets in chat interfaces.

Roll20 animated library assets use formats such as WEBM, which cannot be rendered directly through a normal chat `<img>` element. Combat Assistant uses Roll20's static `sample.png` preview for those assets when displaying token portraits in cards.

This lets an animated tabletop token appear as a clean static portrait in Combat Assistant's chat UI without requiring the character avatar to replace it.

---

# Trinkets & Trackers

Combat Assistant was extracted from the original **Trinkets & Trackers v1.3.8** codebase, which is now abandoned.

The new generation of **Trinkets & Trackers** is a separate project focused on inventory, items, shops, automation, and broader campaign systems.

Combat Assistant is designed as a companion to **Trinkets & Trackers v2.3.0**. They can be used independently, but using both provides a more integrated Roll20 experience.

[T&T Roll20 Forum Post](https://app.roll20.net/forum/post/12758022/t-and-t-chat-based-inventory-dynamic-shops-auto-healing-loot-and-item-automation-for-roll20-d-and-d-2024)

---

# Design Goals

Combat Assistant is built around a few simple principles:

- **Keep Roll20 recognizable.** Use the Turn Order, tokens, sheets, and chat instead of replacing them.
- **Reduce bookkeeping.** Automate repetitive combat operations without taking decisions away from the GM.
- **Keep players involved.** Give players buttons and controls for actions they are allowed to perform.
- **Support both sheet generations.** Maintain separate handling where 2014 and 2024 behave differently.
- **Make automation optional.** Major systems can be enabled or disabled individually.
- **Stay lightweight.** Combat Assistant remains focused on combat instead of rebuilding the full Trinkets & Trackers feature set.

---

# Notes

Combat Assistant depends on information exposed by Roll20 and the active character sheet. Some custom sheets, unusual sheet configurations, or data that Roll20 does not expose in a consistent way may require manual handling.

When testing new automation, start with a copy of the campaign or with disposable test tokens until the HP/AC/resource configuration has been verified.

For built-in command documentation at any time, use:

```text
!ca help
```

---

## Author

Created by **[AmadeusVF](https://www.patreon.com/cw/AmadeusVF/home)**.

Combat Assistant is an independent community project for Roll20 and D&D 5e automation.
