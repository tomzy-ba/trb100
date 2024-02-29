### Getting started


The game world consists of interconnected rooms. A room is a closed space 50x50 cells in size. It may have from 1 to 4 exits to other rooms. The world is seperated into **shards** which are connected by intershard portals

**Energy Sources** are the main game resource. They can be harvested by worker creeps, the amount of energy is limited but resumes every 300 ticks.

**Spawns** are your colony centers, they can accumulate mined energy and use it to create your units. There may be no more than 3 spawns in a room

### Creeps
You build units called creeps the same way in other strategy games, but with one exception; you construct the body of a new creep out of body parts, with thousands of creep types possible.

You can have workers, construction machines, couriers, fighters, healers etc.
However creeps only have a life cycle of 1500 ticks (~30 mins). So you need to fully automate the process of spawning them.

#### Creep skills
- WORK, ability to harvest energy, constuct structures
- MOVE
- CARRY, ability to transfer energy
- ATTACK, short-range attack
- RANGED ATTACK
- HEAL
- CLAIM, ability to claim territory
- TOUGH, defense ability

#### Movement
Each body part has its own weight, the more parts a creep bears, the slower it moves and the quicker it gets fatigued.
A creep needs as many MOVE body parts as other parts to move at 1 square per tick.
Carry parts don't generate fatigue 

A [CARRY, WORK, MOVE] Creep will move 1 square per tick.
A [TOUGH, ATTACK, ATTACK, MOVE, MOVE, MOVE] will move at a maximum of 1 square per tick
A [TOUGH, ATTACK, ATTACK, MOVE, MOVE] will move at 2 square per tick.


