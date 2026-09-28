# GGH Virtual Supermarket: Interaction Model

## 1. Core Philosophy
The interaction model bridges physical exploration with frictionless e-commerce. It caters equally to "Explorers" (who want to browse the physical space) and "Quick Shoppers" (who want maximum efficiency).

## 2. Product Interaction (The Shelf Experience)

### 2.1 The "Resting" State
When walking through an aisle, products look completely natural. There are no glowing outlines, floating text boxes, or arcade-style indicators. The store looks exactly like a high-end physical supermarket.

### 2.2 Hover & Focus
When a user approaches a shelf (within ~1.5 meters) and centers their crosshair/pointer on a product:
- **Visual Feedback:** A subtle, elegant highlight activates (e.g., a slight brightness increase, a soft shadow drop, or a thin white outline).
- **Contextual Tooltip (Quick View):** A minimal 2D UI element fades in anchored near the product in 3D space. It contains:
  - Product Name (Truncated if necessary)
  - Price (EGP)
  - Discount Badge (if applicable)
  - Stock Status (e.g., "In Stock", "Few Left")
  - A primary **[ + Add to Cart ]** action prompt.

### 2.3 Quick Add vs. Detail View
- **Quick Add:** Clicking the primary action instantly adds 1 unit to the cart. The tooltip updates to show a quantity selector `[ - 1 + ]` for rapid bulk adding.
- **Product Detail (Optional):** If the user needs more information, they can trigger an "Inspect" action (e.g., secondary click, or a subtle "Details" button in the tooltip).

### 2.4 Product Detail Panel
The detail view does *not* take over the whole screen. It slides in as a clean 2D side-panel or an elegant modal overlay without losing the 3D context in the background. It connects to the GGH Product API to display:
- High-res Product Image
- Full Name & Brand
- Size/Weight
- Price & Discount Details
- Full Description
- Nutritional Info / Specifications
- Primary **[ Add to Cart ]** button.

## 3. Cart & Feedback System

### 3.1 Adding an Item
When a user clicks "Add to Cart":
- **Physical Feedback:** A swift, subtle animation shows the product conceptually moving from the shelf toward the user's cart (or bottom of the screen).
- **Audio Feedback:** A quiet, satisfying audio cue (e.g., a soft 'click' or rustle). No loud arcade sounds.
- **UI Update:** The Cart Icon in the main HUD briefly scales up/down and updates the item count and total price in real-time.

### 3.2 The Cart View
The user can press a hotkey (e.g., 'C') or click the Cart Icon at any time to open the Cart Review Panel (a 2D sidebar).
- **Contents:** Displays exactly what the standard GGH e-commerce cart displays (Products, Quantities, Unit Prices, Discounts, Total Savings, Final Total).
- **Synchronization:** This panel is a direct reflection of the backend GGH Cart API. If a user adds an item here or in the 3D world, both stay perfectly synchronized.

## 4. Search & Navigation (The Quick Shopper)
For users who do not want to walk the aisles to find specific items, the unified Search Bar is permanently accessible on the HUD.

### 4.1 Search Results
Typing "Barilla Penne" yields a rich dropdown of results, powered by the GGH Search API.
Each result row displays:
- Thumbnail, Name, Size, Price, Stock Status
- Physical Location (e.g., *Aisle 8 - Pasta*)

### 4.2 Search Actions
The user has three immediate options directly from the search result:
1. **[ Add to Cart ]:** Frictionless e-commerce. Buys the item immediately without ever moving the avatar.
2. **[ Go to Product ]:** Instantly teleports the user's avatar to Aisle 8, standing directly in front of the product, focused on it.
3. **[ Guide Me ]:** For users who want the physical experience but need help. This activates a subtle AR-style navigation line on the floor leading from their current position directly to the product.

## 5. Checkout Flow
1. **Physical Prompt:** The user walks to the front of the store and approaches an open checkout lane.
2. **Trigger:** The lane highlights; clicking it triggers the "Proceed to Checkout?" prompt.
3. **Handoff:** The screen transitions cleanly out of WebGL/3D, routing the user into the standard, secure 2D GGH checkout page. The user's physical cart contents are already securely waiting in their GGH session.

## 6. Integration Checklist
To realize this design, the frontend 3D engine will consume the following existing GGH services:
- **Product API:** For the hover tooltips and detail panels.
- **Cart API:** For `addToCart()`, `updateQuantity()`, and pulling cart manifests.
- **Search API:** To power the Quick Shop search bar.
- **Session Auth:** To ensure the user's cart and personalized pricing carry over into the 3D environment and finally to the secure checkout.
