# GGH Virtual Supermarket: Environment Design

## 1. Spatial Layout & Floor Plan
The environment is designed to emulate the predictable, efficient layout of a premium modern hypermarket. The goal is to provide intuitive navigation without relying heavily on a minimap.

### 1.1 Zone Adjacency (The "Loop")
The store follows a classic supermarket "racetrack" layout, ensuring smooth customer flow and logical product discovery:

1. **Entrance / Foyer:** Bottom center. Brightly lit, wide open. Features turnstiles, a cart/basket pickup area, and an immediate view down the "Power Aisle."
2. **Fresh Produce:** Front right. Low shelving, wooden textures, natural lighting. Creates an immediate impression of freshness.
3. **Perimeter Loop:**
   - **Right Wall:** Bakery (warm lighting) leading into Meat & Seafood counters.
   - **Back Wall:** Dairy (refrigerators) and Frozen Foods (glass-door freezers).
   - **Left Wall:** Beverages and high-volume staples.
4. **Core Center Aisles:** Tall, numbered shelving.
   - Groceries (Pasta/Rice/Grains, Canned Food, Pantry)
   - Snacks & Sweets
   - Non-Food (Household, Personal Care) near the checkout side (left).
5. **The Power Aisle (Center Promenade):** A wide central walkway separating the front and back halves of the core aisles, heavily featuring seasonal/weekly Promotional End-Caps.
6. **Checkout Zone:** Front left, extending across the front wall. Clearly visible from almost any main aisle.

## 2. Realistic Proportions & Scale
To ensure realism and prevent a claustrophobic or "maze-like" feel:

- **Main Aisles (Promenade/Perimeter):** ~3 to 3.5 meters wide. Allows comfortable two-way traffic conceptually, ensuring a wide field of view.
- **Core Aisles (Between Shelves):** ~2 to 2.5 meters wide. Tight enough to feel like a real aisle, wide enough to view both sides comfortably on a screen.
- **Shelf Height:** Center aisle shelves max out at ~2 meters (slightly above eye level in first-person view). The camera height should be set around 1.6 - 1.7 meters to simulate human height.
- **Ceiling Height:** High ceilings (~5-6 meters) with exposed industrial/clean architecture and drop lighting to give a sense of open volume.

## 3. Navigation UX (Spatial Awareness)
Customers must always know where they are. We achieve this through aggressive, clear, and realistic environmental wayfinding:

### 3.1 Overhead Aisle Signage
- Large, suspended signs hang directly above the entrance to every core aisle.
- Signs display large numbers (e.g., "Aisle 4") and 2-3 prominent category keywords (e.g., "Pasta | Rice | Canned Goods").
- Visible from a distance down the main promenades.

### 3.2 Department Wayfinding
- Perimeter departments (Produce, Bakery, Dairy) use large, wall-mounted, high-contrast typography (e.g., giant backlit letters spelling "DAIRY" over the fridges).
- Color-coding by department (e.g., green accents for produce, blue for frozen, warm wood for bakery) applied to the floor tiles or ceiling baffles immediately surrounding the zone.

### 3.3 Visual Landmarks & Lines of Sight
- The layout relies on straight lines of sight. When standing in a main perimeter aisle, a user can look left/right and see all the way to the other end of the store.
- **Checkout Visibility:** The checkout area features a distinct, lowered ceiling canopy or unique lighting. A user looking towards the "front" of the store will always recognize the checkout area.

## 4. Logical Product Adjacency
Products are grouped realistically to aid organic discovery:
- *Canned Foods* are adjacent to *Pasta/Grains*.
- *Snacks* are adjacent to *Drinks*.
- *Household* items (cleaning supplies) are physically separated from Fresh Produce.

## 5. Avoiding the "Maze" Effect
- No dead ends. Every aisle connects back to the perimeter or the central promenade.
- The tops of shelves in the core are not infinitely high; users can see the ceiling overhead and the distant department wall signs to maintain their bearings.
- The lighting is uniform and bright (no dark, moody video game corners).
