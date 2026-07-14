# Client Guide: Setting Up Product Siblings (Metal Swatches)

## What Are Product Siblings?

Product siblings allow you to display different metal variations of the same jewelry piece as clickable color swatches on the product page.

**Example:**
When viewing an "18ct Rose Gold & Platinum Diamond Aurora Ring", customers will see swatches for:
- 18ct Yellow Gold
- 18ct Rose Gold
- 18ct White Gold
- Platinum
- Mixed metals (e.g., Rose Gold & Platinum)

Clicking a swatch takes them to that metal variant's product page.

---

## Before You Start: One-Time Setup

### Step 1: Create Metal Color Definitions

You only need to do this **once per metal type**. These define what color each metal swatch will display.

#### How to Create Metal Metaobjects

1. **Go to Shopify Admin**
2. Click **Settings** (bottom left)
3. Click **Custom Data**
4. Click **Metaobjects**
5. Find **Metal** (if it doesn't exist, contact your developer)
6. Click **Add entry**

#### Required Metal Entries

Create one entry for each metal you offer. Use these **exact values**:

| Metal Name (Title) | Color Code (Colour) | Notes |
|-------------------|---------------------|-------|
| `18ct Yellow Gold` | `#e1c340` | Classic yellow gold |
| `18ct Rose Gold` | `#c08a71` | Pink/rose gold |
| `18ct White Gold` | `#d9d9d9` | Light silver/white |
| `Platinum` | `#b4b4b4` | Darker silver/platinum |
| `9ct Yellow Gold` | `#FFD700` | Brighter yellow gold |
| `9ct Rose Gold` | `#E0BFB8` | Lighter rose gold |
| `9ct White Gold` | `#E8E8E8` | Very light silver |
| `Sterling Silver` | `#C0C0C0` | Standard silver |

**Important:** 
- The **Title** must match exactly (including capitalization and spacing)
- The **Colour** is a hex code (copy exactly as shown)

#### Example: Creating "18ct Yellow Gold"

1. Click **Add entry** in Metal metaobject
2. **Title field:** Type `18ct Yellow Gold` (exactly as shown)
3. **Colour field:** Click the color picker
4. Paste `#e1c340` in the hex field
5. Click **Save**

**Repeat for all metals you offer.**

---

## For Each New Product: Setup Process

### Step 2: Create a Siblings Collection

Each product family (e.g., "Aurora Ring") needs one collection containing all its metal variants.

#### How to Create a Siblings Collection

1. **Go to Products → Collections**
2. Click **Create collection**
3. **Title:** Use format: `[Product Name] - All Metals`
   - Example: `Aurora Ring - All Metals`
4. **Collection type:** Choose **Manual**
5. Click **Save**
6. **Note the handle** (shown in URL): `aurora-ring-all-metals`

#### Add Products to Collection

1. In the collection, click **Add products**
2. Select **all metal variants** of this design:
   - Aurora Ring - 18ct Yellow Gold
   - Aurora Ring - 18ct Rose Gold
   - Aurora Ring - 18ct White Gold
   - Aurora Ring - Platinum
   - Aurora Ring - 18ct Rose Gold & Platinum
   - etc.
3. Click **Save**

**Important:** Only add products that are **published** (not drafts).

---

### Step 3: Configure Each Product's Metafields

Every product in the siblings group needs two metafields configured.

#### How to Add Metafields to a Product

1. **Go to Products**
2. **Select a product** (e.g., "Aurora Ring - 18ct Yellow Gold")
3. Scroll down to **Metafields** section
4. Find or add the required metafields (see below)

---

#### Metafield 1: Siblings Collection

**What it does:** Links this product to its siblings collection

| Field | Value |
|-------|-------|
| **Namespace and key** | `theme.siblings` |
| **Type** | Collection reference |
| **Value** | Select the collection you created in Step 2 |

**Example:**
```
Namespace.Key: theme.siblings
Type: Collection reference
Value: Aurora Ring - All Metals
```

**How to set:**
1. Find the metafield labeled `theme.siblings`
2. Click the dropdown
3. Select your siblings collection (e.g., "Aurora Ring - All Metals")
4. The system will save the collection handle automatically

---

#### Metafield 2: Sibling Color (Metal Name)

**What it does:** Defines this product's metal type and swatch label

| Field | Value |
|-------|-------|
| **Namespace and key** | `theme.sibling_color` |
| **Type** | Single line text |
| **Value** | Exact metal name (must match metaobject title) |

**Example for Yellow Gold variant:**
```
Namespace.Key: theme.sibling_color
Type: Single line text
Value: 18ct Yellow Gold
```

**Example for Rose Gold variant:**
```
Namespace.Key: theme.sibling_color
Type: Single line text
Value: 18ct Rose Gold
```

**Example for mixed metal variant:**
```
Namespace.Key: theme.sibling_color
Type: Single line text
Value: 18ct Rose Gold & Platinum
```

---

### Step 4: Repeat for All Products in the Family

**For each metal variant:**
1. Add the **same** `theme.siblings` collection reference
2. Add a **different** `theme.sibling_color` value matching that product's metal

**Example for Aurora Ring family:**

| Product | theme.siblings | theme.sibling_color |
|---------|---------------|---------------------|
| Aurora Ring - 18ct Yellow Gold | `Aurora Ring - All Metals` | `18ct Yellow Gold` |
| Aurora Ring - 18ct Rose Gold | `Aurora Ring - All Metals` | `18ct Rose Gold` |
| Aurora Ring - 18ct White Gold | `Aurora Ring - All Metals` | `18ct White Gold` |
| Aurora Ring - Platinum | `Aurora Ring - All Metals` | `Platinum` |
| Aurora Ring - Rose Gold & Platinum | `Aurora Ring - All Metals` | `18ct Rose Gold & Platinum` |

---

## Exact Values Reference

### Metal Names to Use

**Copy these exactly** when filling in `theme.sibling_color`:

#### Single Metals
- `18ct Yellow Gold`
- `18ct Rose Gold`
- `18ct White Gold`
- `Platinum`
- `9ct Yellow Gold`
- `9ct Rose Gold`
- `9ct White Gold`
- `Sterling Silver`

#### Mixed Metals (Two-Tone)
Use format: `[Metal 1] & [Metal 2]`

Examples:
- `18ct Rose Gold & Platinum`
- `18ct Yellow Gold & Platinum`
- `18ct Rose Gold & 18ct Yellow Gold`
- `18ct White Gold & 18ct Rose Gold`

**Important:** 
- Use ` & ` (space before and after the ampersand)
- Both metals must exist as separate metaobject entries
- Order matters: left metal appears on left side of swatch

---

## Visual Guide: What Goes Where

### Product Page Display

```
┌─────────────────────────────────────────────────┐
│ METAL: 18ct Rose Gold & Platinum                │ ← From theme.sibling_color
│                                                  │
│ [🟡] [🟤] [⚪] [⬜] [🟤⬜] [🟡⬜]              │ ← Swatches
│                                                  │
│ Each swatch:                                     │
│ - Color from metal metaobject                    │
│ - Links to that product                          │
│ - Current product highlighted                    │
└─────────────────────────────────────────────────┘
```

### Data Flow

```
Product Metafields
├─ theme.siblings → "Aurora Ring - All Metals"
│  └─ Fetches all products in this collection
│
└─ theme.sibling_color → "18ct Rose Gold & Platinum"
   └─ Displays as current selection label

For Each Product in Collection:
├─ Read their theme.sibling_color
├─ Look up matching metal metaobject
├─ Get color hex code
└─ Render colored swatch
```

---

## Step-by-Step Example: Adding a New Product

Let's add "Eternal Love Necklace - 18ct Yellow Gold" with siblings.

### 1. Create Metal Metaobjects (if not already done)

✓ Already created: `18ct Yellow Gold`, `18ct Rose Gold`, `18ct White Gold`

### 2. Create Siblings Collection

1. Go to **Products → Collections**
2. Click **Create collection**
3. **Title:** `Eternal Love Necklace - All Metals`
4. **Type:** Manual
5. Click **Save**
6. **Handle:** `eternal-love-necklace-all-metals` (auto-generated)

### 3. Add Products to Collection

1. In the collection, click **Add products**
2. Select:
   - Eternal Love Necklace - 18ct Yellow Gold
   - Eternal Love Necklace - 18ct Rose Gold
   - Eternal Love Necklace - 18ct White Gold
3. Click **Save**

### 4. Configure Yellow Gold Product

1. Go to **Products**
2. Select **Eternal Love Necklace - 18ct Yellow Gold**
3. Scroll to **Metafields**

**Add Metafield 1:**
- **Field:** `theme.siblings`
- **Type:** Collection reference
- **Value:** Select "Eternal Love Necklace - All Metals"

**Add Metafield 2:**
- **Field:** `theme.sibling_color`
- **Type:** Single line text
- **Value:** Type `18ct Yellow Gold` (exactly)

4. Click **Save**

### 5. Configure Rose Gold Product

1. Select **Eternal Love Necklace - 18ct Rose Gold**
2. Scroll to **Metafields**

**Add Metafield 1:**
- **Field:** `theme.siblings`
- **Value:** Select "Eternal Love Necklace - All Metals"

**Add Metafield 2:**
- **Field:** `theme.sibling_color`
- **Value:** Type `18ct Rose Gold` (exactly)

3. Click **Save**

### 6. Configure White Gold Product

1. Select **Eternal Love Necklace - 18ct White Gold**
2. Scroll to **Metafields**

**Add Metafield 1:**
- **Field:** `theme.siblings`
- **Value:** Select "Eternal Love Necklace - All Metals"

**Add Metafield 2:**
- **Field:** `theme.sibling_color`
- **Value:** Type `18ct White Gold` (exactly)

3. Click **Save**

### 7. Verify on Storefront

1. Go to any product page (e.g., Yellow Gold variant)
2. Look for **METAL:** section
3. You should see 3 colored swatches
4. Click each swatch to navigate between variants

---

## Troubleshooting Checklist

### Swatches Not Appearing

**Check:**
- [ ] All products are **Published** (not Draft)
- [ ] All products have `theme.siblings` metafield set
- [ ] All products are in the siblings collection
- [ ] Collection handle is correct

**Fix:**
- Publish all draft products
- Add missing metafields
- Add products to collection

---

### Swatches Are Gray/White (No Color)

**Check:**
- [ ] Metal metaobject exists for this metal name
- [ ] `theme.sibling_color` value **exactly matches** metaobject title
- [ ] Metaobject has `colour` field filled in

**Common mistakes:**
```
❌ Product: "18ct yellow gold" 
   Metaobject: "18ct Yellow Gold"
   → Case doesn't match

❌ Product: "18ct Yellow Gold " (extra space)
   Metaobject: "18ct Yellow Gold"
   → Extra space causes mismatch

✓ Product: "18ct Yellow Gold"
  Metaobject: "18ct Yellow Gold"
  → Perfect match
```

**Fix:**
- Check spelling and capitalization
- Remove extra spaces
- Create missing metaobject if needed

---

### Wrong Products Showing as Siblings

**Check:**
- [ ] `theme.siblings` points to correct collection
- [ ] Collection contains only related products

**Fix:**
- Verify collection handle in metafield
- Remove unrelated products from collection

---

### Duplicate Swatches

**Check:**
- [ ] Each product has unique `theme.sibling_color` value
- [ ] No duplicate products in collection

**Fix:**
- Give each variant a unique metal name
- Remove duplicate products

---

### Two-Tone Swatches Not Working

**Check:**
- [ ] Using format: `Metal 1 & Metal 2` (with spaces)
- [ ] Both metal names exist as separate metaobjects
- [ ] Both metaobjects have color values

**Example:**
```
theme.sibling_color: "18ct Rose Gold & Platinum"

Required metaobjects:
1. Title: "18ct Rose Gold" | Colour: #c08a71
2. Title: "Platinum" | Colour: #b4b4b4
```

**Fix:**
- Add space before and after `&`
- Create both metal metaobjects
- Ensure exact name matching

---

## Quick Reference Card

### What You Need for Each Product Family

| Task | Where | What to Add |
|------|-------|-------------|
| **1. Create metals** | Settings → Custom Data → Metaobjects → Metal | One entry per metal type |
| **2. Create collection** | Products → Collections | One collection per product family |
| **3. Add products** | In the collection | All metal variants |
| **4. Set metafields** | Each product → Metafields | `theme.siblings` + `theme.sibling_color` |

### Metafield Quick Copy

**For every product in a family:**

```
Metafield 1:
Namespace.Key: theme.siblings
Type: Collection reference
Value: [Your Collection Name]

Metafield 2:
Namespace.Key: theme.sibling_color
Type: Single line text
Value: [Exact Metal Name]
```

### Metal Names Quick Copy

**Single metals:**
```
18ct Yellow Gold
18ct Rose Gold
18ct White Gold
Platinum
9ct Yellow Gold
9ct Rose Gold
9ct White Gold
Sterling Silver
```

**Two-tone format:**
```
[Metal 1] & [Metal 2]
```

---

## Common Workflows

### Adding a New Metal Type

1. **Create metaobject:**
   - Settings → Custom Data → Metaobjects → Metal
   - Add entry with title and color

2. **Update products:**
   - Add products with this metal
   - Set `theme.sibling_color` to new metal name

3. **Verify:**
   - Check swatch appears with correct color

---

### Adding a New Product Family

1. **Create collection:**
   - Products → Collections → Create
   - Name: `[Product Name] - All Metals`

2. **Add all variants to collection**

3. **For each variant:**
   - Set `theme.siblings` → collection
   - Set `theme.sibling_color` → metal name

4. **Publish all products**

5. **Test on storefront**

---

### Adding a New Variant to Existing Family

1. **Create product**

2. **Add to existing siblings collection**

3. **Set metafields:**
   - `theme.siblings` → existing collection
   - `theme.sibling_color` → metal name

4. **Publish product**

5. **Check all family members now show new swatch**

---

## Best Practices

### Naming Conventions

**Collections:**
- Use format: `[Product Name] - All Metals`
- Examples:
  - `Aurora Ring - All Metals`
  - `Eternal Love Necklace - All Metals`
  - `Classic Band - All Metals`

**Metal Names:**
- Always include karat/purity: `18ct`, `9ct`, etc.
- Capitalize properly: `Yellow Gold`, not `yellow gold`
- Use consistent format across all products

### Organization Tips

1. **Create all metal metaobjects first** (one-time setup)
2. **Create collection before adding products**
3. **Add all variants to collection at once**
4. **Configure metafields in batches** (all Yellow Gold products, then all Rose Gold, etc.)
5. **Test one product family completely before moving to next**

### Quality Checks

**Before publishing:**
- [ ] All variants in collection
- [ ] All variants have both metafields
- [ ] All metal names match metaobjects exactly
- [ ] All products published
- [ ] Tested on storefront

**After publishing:**
- [ ] Correct number of swatches appear
- [ ] All swatches have colors (not gray)
- [ ] Clicking swatches navigates correctly
- [ ] Current product highlighted
- [ ] Label shows correct metal name

---

## Time Estimates

### One-Time Setup
- Create metal metaobjects (8 metals): **15 minutes**

### Per Product Family
- Create collection: **2 minutes**
- Add products to collection: **2 minutes**
- Configure metafields (per product): **2 minutes**
- Total for 3-variant family: **10 minutes**

### Adding New Variant to Existing Family
- **5 minutes** (create product, add to collection, set metafields)

---

## Support

### When to Contact Developer

Contact your developer if:
- Metal metaobject type doesn't exist
- Metafield definitions are missing
- Siblings block not appearing on product pages
- Technical errors or bugs

### What You Can Do Yourself

You can handle:
- Creating metal metaobject entries
- Creating siblings collections
- Adding products to collections
- Setting product metafields
- Publishing products

---

## Appendix: Field Definitions

### Metaobject: Metal

| Field Name | Type | Purpose | Example |
|------------|------|---------|---------|
| `title` | Single line text | Metal identifier (must match product metafield) | `18ct Yellow Gold` |
| `colour` | Color | Hex color for swatch display | `#e1c340` |

### Product Metafields

| Namespace.Key | Type | Purpose | Example Value |
|---------------|------|---------|---------------|
| `theme.siblings` | Collection reference | Links to siblings collection | `aurora-ring-all-metals` |
| `theme.sibling_color` | Single line text | This product's metal name | `18ct Yellow Gold` |

### Alternative Metafield Names

The system also checks these variations (use any one):
- `theme.sibling_colour` (UK spelling)
- `theme.siblings_color`
- `theme.siblings_colour`

**Recommendation:** Use `theme.sibling_color` for consistency.

---

## Visual Examples

### Single-Tone Swatch
```
Product metafield: "18ct Yellow Gold"
         ↓
Looks up metaobject: title = "18ct Yellow Gold"
         ↓
Gets color: #e1c340
         ↓
Renders: [🟡] (solid yellow circle)
```

### Two-Tone Swatch
```
Product metafield: "18ct Rose Gold & Platinum"
         ↓
Splits: ["18ct Rose Gold", "Platinum"]
         ↓
Looks up: #c08a71 (rose) + #b4b4b4 (platinum)
         ↓
Renders: [🟤⬜] (diagonal split circle)
```

### Complete Product Page
```
┌──────────────────────────────────────────────┐
│ Aurora Ring - 18ct Rose Gold & Platinum      │
│                                               │
│ METAL: 18ct Rose Gold & Platinum             │
│                                               │
│ [🟡] [🟤] [⚪] [⬜] [🟤⬜] [🟡⬜]          │
│  ↑    ↑    ↑    ↑     ↑      ↑              │
│  │    │    │    │     │      │              │
│  │    │    │    │     │      └─ Yellow & Platinum│
│  │    │    │    │     └─ Rose & Platinum (active)│
│  │    │    │    └─ Platinum                 │
│  │    │    └─ White Gold                    │
│  │    └─ Rose Gold                          │
│  └─ Yellow Gold                             │
│                                               │
│ [Add to Cart]                                │
└──────────────────────────────────────────────┘
```

---

**Document Version:** 1.0  
**Last Updated:** June 18, 2026  
**For:** Alexandra Theme - Product Siblings Feature
