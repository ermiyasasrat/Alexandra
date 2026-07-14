# Quick Guide: Setting Up Product Siblings

## What This Does

Displays metal color swatches on product pages so customers can switch between metal variants (e.g., Yellow Gold, Rose Gold, Platinum).

---

## Setup: 3 Simple Steps

### Step 1: Add Color to Each Product

**Where:** Shopify Admin → Products → [Select Product] → Metafields section

**What to do:** Find the **Color** metafield and set the swatch color

**Recommended colors:**

| Metal Type | Hex Code |
|-----------|----------|
| 18ct Yellow Gold | `#e1c340` |
| 18ct Rose Gold | `#c08a71` |
| 18ct White Gold | `#d9d9d9` |
| Platinum | `#b4b4b4` |
| 9ct Yellow Gold | `#FFD700` |
| 9ct Rose Gold | `#E0BFB8` |
| 9ct White Gold | `#E8E8E8` |
| Sterling Silver | `#C0C0C0` |

**How to set:**
1. Go to product in admin
2. Scroll to **Metafields** section
3. Find **Color** field
4. Click the color picker
5. Paste hex code from table above
6. Click **Save**

---

### Step 2: Create Collection for Each Product Family

**Where:** Shopify Admin → Products → Collections

**What to do:** Create one collection per product design (e.g., one for "Aurora Ring", one for "Eternal Love Necklace")

**How:**
1. Click **Create collection**
2. **Title:** `[Product Name] - All Metals`
   - Example: `Aurora Ring - All Metals`
3. **Collection type:** Select **Manual**
4. Click **Save**
5. Click **Add products**
6. Select all metal variants of this design
7. Click **Save**

**Important:** Only add **published** products (not drafts)

---

### Step 3: Add Metafields to Each Product

**Where:** Shopify Admin → Products → [Select Product] → Metafields section

**What to do:** For every product, fill in 3 metafields

---

#### Metafield 1: Color (Swatch Color)

**Find:** `Color`

**What to enter:** Click color picker, paste hex code from Step 1 table

**Example:**
- Product: "Aurora Ring - 18ct Yellow Gold"
- Color: `#e1c340`

---

#### Metafield 2: Link to Collection

**Find:** `theme.siblings`

**What to enter:** Select the collection you created in Step 2

**Example:**
- Product: "Aurora Ring - 18ct Yellow Gold"
- Select: "Aurora Ring - All Metals"

---

#### Metafield 3: Metal Name

**Find:** `theme.sibling_color`

**What to enter:** Exact metal name

**Copy these exact values:**

**Single Metals:**
- `18ct Yellow Gold`
- `18ct Rose Gold`
- `18ct White Gold`
- `Platinum`
- `9ct Yellow Gold`
- `9ct Rose Gold`
- `9ct White Gold`
- `Sterling Silver`

**Mixed Metals (Two-Tone):**
- `18ct Rose Gold & Platinum`
- `18ct Yellow Gold & Platinum`
- `18ct White Gold & Platinum`
- `18ct Rose Gold & 18ct Yellow Gold`

**Important:** 
- Copy exactly (including capitalization and spacing)
- For two-tone, use ` & ` (space before and after &)

---

## Complete Example: Aurora Ring

### Products in Family:
- Aurora Ring - 18ct Yellow Gold
- Aurora Ring - 18ct Rose Gold
- Aurora Ring - 18ct White Gold
- Aurora Ring - Platinum
- Aurora Ring - 18ct Rose Gold & Platinum

### Step-by-Step:

**1. Create Collection:**
- Go to: Products → Collections
- Click: Create collection
- Title: `Aurora Ring - All Metals`
- Type: Manual
- Add all 5 products above
- Save

**2. Configure Each Product:**

**Product 1: Aurora Ring - 18ct Yellow Gold**
- Go to: Products → Aurora Ring - 18ct Yellow Gold
- Scroll to: Metafields
- `Color` → Click color picker, paste `#e1c340`
- `theme.siblings` → Select "Aurora Ring - All Metals"
- `theme.sibling_color` → Type `18ct Yellow Gold`
- Save

**Product 2: Aurora Ring - 18ct Rose Gold**
- Go to: Products → Aurora Ring - 18ct Rose Gold
- Scroll to: Metafields
- `Color` → Click color picker, paste `#c08a71`
- `theme.siblings` → Select "Aurora Ring - All Metals"
- `theme.sibling_color` → Type `18ct Rose Gold`
- Save

**Product 3: Aurora Ring - 18ct White Gold**
- Go to: Products → Aurora Ring - 18ct White Gold
- Scroll to: Metafields
- `Color` → Click color picker, paste `#d9d9d9`
- `theme.siblings` → Select "Aurora Ring - All Metals"
- `theme.sibling_color` → Type `18ct White Gold`
- Save

**Product 4: Aurora Ring - Platinum**
- Go to: Products → Aurora Ring - Platinum
- Scroll to: Metafields
- `Color` → Click color picker, paste `#b4b4b4`
- `theme.siblings` → Select "Aurora Ring - All Metals"
- `theme.sibling_color` → Type `Platinum`
- Save

**Product 5: Aurora Ring - 18ct Rose Gold & Platinum**
- Go to: Products → Aurora Ring - 18ct Rose Gold & Platinum
- Scroll to: Metafields
- `Color` → Click color picker, paste `#c08a71` (for rose gold base)
- `theme.siblings` → Select "Aurora Ring - All Metals"
- `theme.sibling_color` → Type `18ct Rose Gold & Platinum`
- Save

**3. Verify:**
- Go to any Aurora Ring product page on your store
- You should see: **METAL:** section with 5 colored swatches
- Click swatches to switch between variants

---

## Quick Checklist

For each new product family:

- [ ] **Create collection** (Products → Collections)
  - Title: `[Product Name] - All Metals`
  - Type: Manual
  - Add all metal variants

- [ ] **For each product in family:**
  - [ ] Go to product in admin
  - [ ] Scroll to Metafields
  - [ ] Set `Color` → click color picker, paste hex code
  - [ ] Set `theme.siblings` → select collection
  - [ ] Set `theme.sibling_color` → type exact metal name
  - [ ] Save
  - [ ] Ensure product is **Published** (not Draft)

- [ ] **Test on storefront:**
  - [ ] Swatches appear
  - [ ] Correct colors show
  - [ ] Clicking navigates between products

---

## Troubleshooting

### No swatches appearing
**Fix:** Make sure all products are **Published** (not Draft)

### Swatches are gray/white
**Fix:** Check `theme.sibling_color` exactly matches metal name in Step 1
- Example: `18ct Yellow Gold` not `18ct yellow gold`

### Wrong products showing
**Fix:** Check all products have correct collection in `theme.siblings`

---

## Metal Names Reference (Copy/Paste)

```
18ct Yellow Gold
18ct Rose Gold
18ct White Gold
Platinum
9ct Yellow Gold
9ct Rose Gold
9ct White Gold
Sterling Silver
18ct Rose Gold & Platinum
18ct Yellow Gold & Platinum
18ct White Gold & Platinum
```

---

## Where to Input in Shopify Admin

### Collections (Per Product Family)
```
Shopify Admin
  └─ Products
      └─ Collections
          └─ Create collection
              ├─ Title: [Product Name] - All Metals
              ├─ Type: Manual
              └─ Add products: [select all variants]
```

### Product Metafields (Per Product)
```
Shopify Admin
  └─ Products
      └─ [Select Product]
          └─ Metafields (scroll down)
              ├─ Color → [click color picker, paste hex]
              ├─ theme.siblings → [select collection]
              └─ theme.sibling_color → [type metal name]
```

---

**Time Required:**
- Per product family (3 variants): 15 minutes
- Per additional variant: 3 minutes
