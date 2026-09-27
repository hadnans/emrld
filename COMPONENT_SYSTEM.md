# GGH Virtual Supermarket: Component System

## 1. Concept: Data-Driven 3D
To ensure scalability, the 3D environment cannot be manually modeled for every single product. Instead, the store is constructed from a library of reusable 3D environment components (prefabs). These components act as "containers" that are dynamically populated at runtime using data from the existing GGH Product API.

## 2. Reusable Environment Components
The store environment is built by assembling the following modular components:

### 2.1 Standard Shelf (Gondola)
- **Structure:** A standard metal supermarket shelving unit (approx 2m high, 1.2m wide per segment, 4-5 adjustable shelves).
- **Usage:** Snapped together to form long aisles for Pantry, Snacks, Household, etc.
- **Population:** Includes predefined "slots" along each shelf. The frontend maps a category ID to a shelf, queries the API, and instantiates 2D/3D product representations into those slots.

### 2.2 Double-Sided Aisle Shelf
- **Structure:** Two Standard Shelves placed back-to-back.
- **Usage:** The core building block of the center store aisles.

### 2.3 Refrigerator (Open & Glass-Door)
- **Structure:**
  - *Open Chiller:* Multi-deck open fridge for Dairy and Meats. Emits a subtle hum and cool lighting.
  - *Glass-Door:* For Drinks and Frozen foods.
- **Usage:** Placed along the back and side perimeter walls.

### 2.4 Produce Display
- **Structure:** Low-angled, wooden or black plastic bins.
- **Usage:** Specifically for the fresh produce section. Configured to display bulk items (apples, bananas) using instanced meshes or high-quality textures rather than individual item slots to save performance.

### 2.5 Promotional End-Cap
- **Structure:** A prominent, outward-facing shelf placed at the end of a double-sided aisle.
- **Usage:** Tied to the GGH Promotions API. Dynamically highlights weekly deals, bundles, or sponsored products. Features built-in digital signage (a plane that renders a promotional banner texture).

### 2.6 Floor Display (Pallet / Dump Bin)
- **Structure:** A standalone cardboard or wood display sitting directly on the floor.
- **Usage:** Placed in the main promenade or foyer for high-volume sale items (e.g., a massive stack of soda cases).

### 2.7 Hanging Signage
- **Structure:** Ceiling-suspended placards.
- **Usage:** Procedurally generated text. A script reads the metadata of the shelves below it and updates the 3D text (e.g., "Aisle 4: Snacks") so if product categories move, the signs update automatically.

### 2.8 Checkout Station
- **Structure:** A realistic conveyor belt, register, and bagging area.
- **Usage:** Acts as the physical transition zone. Interacting with it triggers the handoff to the 2D e-commerce checkout page.

### 2.9 Shopping Cart & Basket
- **Structure:** 3D models representing the user's current session.
- **Usage:** Visually fills up as the cart API returns a higher item count, bridging the physical metaphor with the digital cart state.

## 3. Dynamic Population Strategy (Scalability)

### Phase 1: 2D Photography mapping (The "Sprite" Approach)
To render thousands of products without crashing the browser:
1. The backend API provides product data, including the front-facing image URL and dimensions.
2. The 3D component (e.g., a Standard Shelf) calculates how many items fit in its physical width based on the API dimensions.
3. The renderer generates simple 3D planes (cards) or simple boxes positioned on the shelf, mapping the real product photography onto the front face.
4. Instanced rendering is used to draw identical products (e.g., a row of 10 identical cans) with minimal draw calls.

### Phase 2: Hybrid 3D
- High-value, common, or heavily promoted items are swapped out for actual low-poly 3D models.
- Standard inline items remain as 2D planes/boxes.
- The component system handles this seamlessly: if a `modelUrl` exists in the API response, it loads the GLTF; if not, it falls back to the 2D texture map.

## 4. Summary
By decoupling the environment architecture from the specific product data, we create a highly scalable system. The store layout (the arrangement of shelves and fridges) is designed once, while the merchandising (what sits on the shelves) is handled dynamically by the existing GGH e-commerce infrastructure.
