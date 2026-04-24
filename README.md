# KIET_FSD_DebugChallenge

Bug Sheet — ShopEasy Debugging Assignment
Instructions: Find and fix all 9 bugs spread across 4 files. The app compiles and runs without errors — all bugs are logical/behavioral.

Bug 1 — App.js | Easy
Symptom: Price range filters exclude products at the exact boundary price (e.g. "Under ₹500" won't show the ₹499 product; "₹500–₹1,000" won't show the ₹500 or ₹1,000 products).

Cause->Strict comparison operators (> and <) were used.
Fix->Use inclusive conditions.
price >= min && price <= max


Bug 2 — App.js | Hard
Symptom: Clicking any Category button (Electronics, Footwear, etc.) has no effect — the product grid never changes.

Cause->Selected category state not properly applied in filtering logic.
fix->Update state and filter correctly.
setSelectedCategory(category);
const filteredProducts = products.filter(
  (p) => selectedCategory === "All" ||p.category === selectedCategory
);


Bug 3 — App.js | Easy
Symptom: Clicking the 🗑️ delete button in the cart removes all other items and keeps only the one you tried to delete.

Cause->Wrong filter condition used (=== instead of !==).
Fix->Use correct condition to remove selected item.
cart.filter(item => item.id !== id)



Bug 4 — App.js | Medium
Symptom: The cart badge on the header button always shows nothing (or 0) even after adding multiple items.

Cause->Used cart.length instead of total quantity.
Fix->Calculate total quantity using reduce.
const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);


Bug 5 — App.js | Hard
Symptom: The "+ Add to Cart" button never turns green and never says "✓ Added", even after a product is in the cart.

Cause->Incorrect condition to check if product exists in cart.
Fix->Use some() to check presence in cart.
const isInCart = cart.some(item => item.id === product.id);


Bug 6 — Cart.jsx | Medium
Symptom: The cart total always shows ₹0, no matter how many items or quantities are added.

Cause->Total calculation missing price * quantity logic.
Fix->Use reduce with multiplication.
const total = cart.reduce((sum, item) => sum + item.price * item.quantity, 0);


Bug 7 — Cart.jsx | Medium
Symptom: The − (decrease) button in the cart is never disabled, allowing quantity to drop to 0 (and below), breaking the total.

Cause->No condition applied to disable button.
Fix->Disable button when quantity is 1.
<!-- <button disabled={item.quantity <= 1}>-</button> -->


Bug 8 — Filters.jsx | Easy
Symptom: The sort order is inverted — selecting "Price: Low to High" sorts highest-priced items first, and vice versa.

Cause->Comparator function reversed.
Fix->Use correct sorting logic.
(a, b) => a.price - b.price
(b, a) => b.price - a.price

Bug 9 — ProductCard.jsx | Easy
Symptom: A product rated 4.5 shows only 4 filled stars instead of 5. All half-star ratings are rounded down.

Cause->Math.floor() used which always rounds down.
Fix->Use Math.round() to correctly round values.
Math.round(rating)
