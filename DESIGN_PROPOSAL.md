# GGH Virtual Supermarket: Design Proposal

## Vision Statement
The GGH Virtual Supermarket is a highly realistic, interactive 3D shopping layer seamlessly integrated into the existing GGH e-commerce ecosystem. It allows customers to experience the spatial context and discovery of a physical hypermarket without losing the convenience of digital commerce. This is an e-commerce platform first and foremost; game mechanics are entirely secondary.

---

## 1. Recommended User Flow
The virtual supermarket is treated as an optional, enhanced shopping mode accessible from the main GGH storefront.

1. **Entry Point:** A prominent "Enter Virtual Store" call-to-action on the existing GGH homepage or department pages.
2. **Environment Loading:** The user transitions smoothly into the 3D environment (loading a lightweight web-based 3D scene) directly in the browser.
3. **Arrival:** The customer spawns at the store entrance, greeted by weekly promotions and clear signage.
4. **Shopping:** The user can either physically walk the aisles (Explore Mode) or use a unified search to locate and teleport to items (Quick Shop).
5. **Selection:** The user approaches a product, clicks to view subtle details (Name, Price, Add to Cart), and adds it.
6. **Cart Sync:** The physical-looking cart updates visually. The items are synchronized in real-time with the existing GGH e-commerce cart.
7. **Checkout Transition:** The user navigates to the physical checkout area in the 3D space, which transitions them into the standard GGH secure 2D checkout flow to complete payment.

---

## 2. Store Structure
The store is structured like a modern, premium hypermarket.

- **Entrance / Foyer:** Turnstiles, shopping carts, and immediate high-value promotional displays.
- **Fresh Produce (Front Right/Left):** Natural lighting, wooden crates, and vibrant colors to set a fresh tone.
- **Core Aisles (Center):** Numbered aisles (Pantry, Snacks, Household, Personal Care) with clear overhead signage.
- **Perimeter Departments:** Dairy (refrigerators), Meat/Seafood (counters), Bakery (warm lighting).
- **Frozen Foods (Back):** Enclosed glass-door freezers.
- **End-Caps:** Promotional displays at the end of every main aisle to mimic real-world merchandising.
- **Checkout Zone (Front Center):** A row of realistic checkout lanes where the customer concludes the 3D experience.

---

## 3. Camera / Navigation Model
The navigation must be intuitive for non-gamers.

- **Perspective:** First-person view provides the most realistic sense of scale and immersion. (An optional third-person mode with a shopping cart could be tested, but first-person is the primary target).
- **Controls (Desktop):** Standard WASD / Arrow keys to move, mouse to look around. Point-and-click pathfinding (click the floor to walk there) will be implemented as an accessible alternative.
- **Controls (Mobile):** See Mobile Strategy.
- **UI Overlay:** Kept minimal. A small, transparent minimap in the corner, a unified search bar at the top, and a cart summary button. No cluttered HUDs or glowing waypoints unless explicitly requested via search.

---

## 4. Shelf / Product Interaction
Interactions must feel subtle and realistic, avoiding arcade-style pop-ups.

- **Visual State:** Products sit on shelves in realistic quantities. We will initially use 2D product photography mapped onto 3D bounding boxes (cards or simple geometries) to save performance, migrating to full 3D models in the future.
- **Proximity:** When a customer is within a few virtual meters and points the cursor at a product, it subtly highlights (e.g., slight brightness increase or a thin, elegant outline).
- **Context Menu:** Clicking the product opens a clean, minimal 2D overlay anchored near the product in 3D space (or a clean sidebar) showing:
  - Product Name
  - Price & Discount
  - "Add to Cart" button
- **Action:** Clicking "Add to Cart" plays a brief, satisfying animation (the product conceptually moving to the cart) and updates the cart counter.

---

## 5. Cart Interaction
The cart bridges the 3D world and the 2D e-commerce system.

- **Visual Representation:** Depending on camera mode, the physical cart is either visible in front of the user (first-person) or represented by a highly polished 3D icon in the UI.
- **Synchronization:** The cart is strictly tied to the existing GGH backend cart. If the user adds an item in 3D, the GGH cart API is immediately called.
- **UI Panel:** Clicking the cart icon slides out a clean 2D sidebar showing the current manifest, total price, and applied promotions—exactly as it functions in the standard web store.

---

## 6. Search / Navigation (Quick Shop)
Customers must not feel trapped by the physical space. The Quick Shop features guarantee e-commerce efficiency.

- **Unified Search:** A standard search bar remains visible on the UI layer.
- **Search Results:** Searching for an item (e.g., "Milk") drops down a list of results.
- **Actionable Results:** For each result, the user has two options:
  1. **Direct Add:** Add to cart immediately without moving.
  2. **Take Me There:** Teleport the user to the correct aisle facing the product, or draw a subtle, elegant path on the floor (like an AR navigation line) guiding them to the physical location.

---

## 7. Checkout Transition
Payment and security must remain firmly in the established 2D e-commerce infrastructure.

- **Physical Trigger:** The user walks up to the checkout lanes at the front of the virtual store.
- **Interaction:** Interacting with a checkout lane triggers a "Proceed to Checkout" prompt.
- **Transition:** A clean, realistic animation (e.g., items scanning, a receipt printing on screen) plays briefly, showing the final total and savings.
- **Handoff:** The 3D canvas fades out, and the user is seamlessly redirected to the standard, secure GGH web checkout page to enter shipping and payment details.

---

## 8. Mobile Strategy
3D on mobile browsers requires careful optimization and simplified controls.

- **Performance:** Aggressive LOD (Level of Detail) scaling. Textures will be down-resed, and rendering distance reduced to maintain 30-60 FPS on mid-range smartphones.
- **Controls:** Virtual joysticks are often clunky. Instead, we will rely on **Point-and-Click / Tap-to-Move** navigation. Tapping the floor moves the camera there. Swiping pans the camera.
- **Gyroscope (Optional):** Allow users to look around by physically moving their phone.
- **Fallback:** If a device fails performance checks upon loading, the user is gracefully offered the standard 2D GGH storefront instead.

---

## 9. Existing GGH Systems That Should Be Reused
To avoid breaking current functionality, this virtual layer will act as a "smart frontend client" consuming existing GGH backend services via API. We will reuse:

- **Product Catalog API:** Product names, IDs, categories, pricing, and variants.
- **Asset Library:** Existing 2D product photography (used as textures/sprites on the shelves).
- **Cart API:** `addToCart`, `updateQuantity`, `getCartTotal`. The 3D store holds no independent cart state.
- **Authentication:** The user's existing login session dictates their cart and personalized pricing.
- **Promotions Engine:** Discount logic, weekly deals, and bundle pricing.
- **Checkout / Payment Gateway:** The entire secure checkout flow.

---

## 10. Phased Implementation Plan

### Phase 1: Core Foundation (Design Now)
- **Architecture:** Setup WebGL framework (e.g., Three.js / React Three Fiber) alongside the existing frontend.
- **Environment:** Build a single, medium-sized, highly polished supermarket environment (lighting, shelves, aisles).
- **Product Integration:** Map 2D product photography to 3D shelf locations via automated scripts based on category.
- **Basic Interactions:** Walk, look, select product, view minimal UI, add to cart (API integration).
- **Quick Shop:** Implement the search bar with "Teleport to Aisle" and "Direct Add" functionality.
- **Checkout Handoff:** Walk to the register to redirect to the standard 2D checkout.

### Phase 2: Refinement & Merchandising (Deferred)
- **Promotions:** Dynamic end-cap displays pulling from the GGH promotions API.
- **Mobile Optimization:** Deep performance tuning and Tap-to-Move mobile controls.
- **Wayfinding:** The AR-style "guide line" on the floor for search navigation.

### Phase 3: High Fidelity & Gamification (Deferred indefinitely until proven)
- **True 3D Products:** Replacing 2D photography with full 3D scans/models of popular products.
- **Game Mechanics:** Shopping missions, loyalty point discovery, or seasonal environment changes.

---
*End of Proposal*
