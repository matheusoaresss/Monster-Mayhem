# Monster-Mayhem
feat: add main app entry point to initialize game board, sounds, pathfinding, and character data loading

- Preload hover and click sounds via SoundManager.
- Create and render a 10x10 hex grid GameBoard.
- Initialize pathfinding hover effects on the grid.
- Setup Reset Board button to clear and redraw the grid.
- Load character data asynchronously from JSON and log on success.
- Add error handling for missing DOM elements and data loading failures.

This commit sets up the basic app scaffolding for Monster Mayhem and prepares the environment for future game mechanics integration.

feat: add characters.json with initial monster data for game

- Include 15 monster characters with unique IDs, names, hit points, movement ranges, and image paths.
- Monsters range from low HP (Slime, Imp) to high HP (Golem, Troll).
- Images are stored under assets/images/ with descriptive filenames.
- This JSON file serves as the foundational data source for character loading and future game mechanics.

feat: implement DataLoader utility class for async JSON loading

- Created DataLoader class with static methods to load JSON data via fetch.
- `loadJSON(url)` handles fetch requests, JSON parsing, and error reporting.
- `loadCharacters()` is a specific helper to retrieve data/characters.json.
- Includes error handling with descriptive logs on network or parse failure.
- Class is exposed globally via `window.DataLoader` for easy access in other modules.

This utility supports future scalability for loading various game data assets asynchronously.

Add GameBoard class to render and manage hexagonal grid UI

- Introduced the GameBoard class which:
  - Renders a 10x10 grid of flat-top hexagons.
  - Handles dynamic positioning and responsive layout inside a container.
  - Supports hover and selection highlighting with sound effects via SoundManager.
  - Allows deselection by clicking on empty board space.

- Hexes store their grid coordinates as data attributes for future game logic.
- Provides clean separation of concerns with private helper methods:
  - _setupContainer
  - _drawGrid
  - _createHexElement
  - _attachHexEvents
  - _attachBackgroundDeselect

- Exposes GameBoard class globally via `window.GameBoard` for debugging or integration with other modules.

This commit lays the foundation for interactive game grid UI behaviour and supports upcoming features like pathfinding, character placement, and animations.

Implement hexagonal grid pathfinding using BFS

- Introduced Pathfinding class for managing movement paths across a hexagonal grid.
- Utilises breadth-first search (BFS) to compute the shortest path between hex tiles.
- Adapts to an odd-q vertical offset layout with column-dependent neighbour offsets.
- Dynamically updates path highlights based on mouse movement over the board.
- Clears the path when selection changes or when hovering an invalid target.
- Coordinates are stored using data-col and data-row attributes, enabling quick lookup.
- Exposes the Pathfinding class globally via `window.Pathfinding`.

This module enables future support for visual path previews, movement logic, and tactical gameplay features.

Add SoundManager for UI audio feedback on hover and click

- Introduced SoundManager class to preload and play sound effects.
- Supports named audio file registration via preload() method.
- Ensures hover and click interactions on hex tiles have responsive audio.
- Uses Audio element cloning to allow overlapping playback of the same sound.
- Includes fallback for missing or unpreloaded sounds with warning messages.
- Prevents crash on play() if audio interaction is blocked before user input.
- Exposed globally via `window.SoundManager` for seamless integration.

Provides a flexible audio feedback system essential for enhancing user engagement.

Add modern responsive CSS styling for Monster Mayhem UI

- Introduced a clean, professional visual theme with custom CSS variables.
- Applied a responsive layout for the main container and board area.
- Added base styling for text, header, buttons, footer, and body.
- Defined hexagon grid appearance with clip-path and position-based layout.
- Implemented interactive states: hover, selected, and path-highlighted hexes.
- Used subtle shadows and rounded corners for visual depth and polish.
- Established consistent font, colour, and spacing tokens for maintainability.

Enhances user experience with polished visuals and interaction feedback.
