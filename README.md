# SCP Echos of the void - Game

## 1. Basic game info.
    The game is about a junior systems administrator who got locked inside a facillity control room during a containment breach. his mission is to protect and guide scientists to shelters before guiding mtfs to escort them and neutralize anomalies
## Gameplay mechanics.

Game splits into 4 distinct tiers in which the player has to operate.

    First is the pre-breach tier. its simple in theorhy. It serves as a tutorial where the player just follows orders of senior systems administrator. Tier ends once the containment breach starts

    **Second tier** is a faster more chaotic experience. Mission is to get as much personale into the saferooms. In this stage its important to save as many as possible as more you save the less enemies and more resources you will have at
    your disposal. During this stage first task is to initiate emergency call into HQ for mtf dispatch starting a timer in untill tier 3 stats

    **Third Tier** This tier starts once timer reached zero. MTF (Mobile task force) arrives into the facility. This stage is the one where player will spend most time. Its complex. Player has to navigate the task force to contaiment chambers and recontain other anomalies. Player can also get many upgrades and other benefits from the escaping scientists. Player has a task force dialup availible at his disposal.

    **Fourth tier** This tier is a last call. If the player has got no reinforcements left and facility is still very much under hostile control the HQ sends a resolution squad. It has simple order. Activate nuclear payload. You have to remotely help them and reactivate the nuke. the squad (Alpha-1) has override keycards which can get into all doors. allowing for unlimited access. The only drawback is that its the last squad. If they die its GAME OVER

### Tools at players disposal
    Since the entire game revolves around a computer screen all/most tools are placed inside the computer.
#### The cli
    This is where all control is placed. It will be powerful and customisable. There will be commands for simple thing like closing doors to complex like nuclear rod realignment
#### Sensor screen
    This screen is a small map cutout of a sector showing sensors. if they've been tripped and show the details of the rooms
    This is the visual feedback of the player it shows everything like if something is in the room. If a defence measurement is active and if the doors are close
#### Sector map
    This is a map of the entire sector or facility. it serves as a way to show the player where they are and where things are. This also shows the player the Doors status. It ONLY shows door status and updates slowly. Not instant as sensor map
#### Mtf 
    This is just the npcs which the player can command extensively. They come in two flavors.
    Specialists - An mtf squad which is specialised in one type of anomaly. Go outside of it and they die
    Generalists - They aren't specialised meaning they are not in advantage nor disadvantage between anomalies. These are the first squad

    These squads will be called from terminal and unlike other games these have only a certain ammount of reinforcements. once depleted stage 4 starts
#### Facility design
    The initial idea is to have sectors. With distinct checkpoints and Sector Gates. GATE can only be opened by the player and they serve as an isolation of the sector.
    The sectors serve as a warning and type of squad the player should choose. 
    OPTIONAL: Procedural Generation of terrain.




## Design / visual identity.
    The design is centered around vector / cli. The wrapper around this all is just a visual operating system allowing for free choice of tiling and managing of windows. The design follows in its footsteps as its grounded in reality its either a simple reskin of windows 98 or a reskin of windows 7.

## Audio. 
    Audio is very simple to do as we don't have any extensive enviroments to work with. since our place of safety is a cotrol room its a very secure place. There will be only humming of servers and sounds of computer.
## Technologies. 
    Technologies which will be used in some / most capacities are
        Godot - Game engine
        Audacity - Game audio
        Gemini - For help with the hellscape that is frontend
        Linux - For terminal/cli perspective.

