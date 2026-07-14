# Product Siblings Setup Guide

## Overview

The Product Siblings feature allows you to link related products (e.g., different metal colors of the same jewelry piece) and display them as color swatches on the Product Detail Page (PDP).

**Example Display:**
```
METAL: 18ct White Gold
[🟤 Rose Gold] [🟡 Yellow Gold] [⚪ White Gold - Active]
```

---

## How It Works

### System Architecture

1. **Collection-Based Grouping**
   - All sibling products are grouped in a dedicated collection
   - Each product references this collection via metafield

2. **Metafield Configuration**
   - Each product has a `theme.siblings` metafield (collection reference)
   - Each product has a `theme.sibling_color` metafield (metal name)

3. **Metaobject Color Mapping**
   - Metal names are mapped to hex colors via `metal` metaobjects
   - System looks up color by matching metafield value to metaobject title

4. **Dynamic Rendering**
   - Theme retrieves all products from the siblings collection
   - Generates clickable swatches with colors from metaobjects
   - Highlights current product's swatch

### Code Flow

```
Product Page Loads
    ↓
Read product.metafields.theme.siblings (collection handle)
    ↓
Fetch all products from collections[handle].products
    ↓
For each sibling product:
    - Read sibling_color metafield
    - Look up metal metaobject by title
    - Get colour hex value
    - Render swatch with color
```

**Important:** Only **published products** appear in siblings. Draft products are filtered out by Shopify's API.

---

## Step-by-Step Setup Guide

### Prerequisites

- Products must be **Published** (Active status)
- Admin access to Shopify store
- Understanding of metafields and metaobjects

---

### Step 1: Create Metal Metaobjects

Metal metaobjects define the swatch colors for each metal type.

#### 1.1 Navigate to Metaobjects
1. Go to **Shopify Admin**
2. Click **Settings** → **Custom Data**
3. Click **Metaobjects**
4. Find or create **Metal** type

#### 1.2 Create Metal Entries

Create one entry for each metal variant you offer:

| Title | Colour (Hex) | Visual |
|-------|--------------|--------|
| `18ct White Gold` | `#E5E4E2` | Light silver/platinum |
| `18ct Yellow Gold` | `#D4AF37` | Classic gold |
| `18ct Rose Gold` | `#B76E79` | Pink/rose gold |
| `9ct White Gold` | `#E8E8E8` | Lighter silver |
| `9ct Yellow Gold` | `#FFD700` | Brighter gold |
| `9ct Rose Gold` | `#E0BFB8` | Lighter rose |
| `Sterling Silver` | `#C0C0C0` | Silver |
| `Platinum` | `#E5E4E2` | Platinum |

**How to Add:**
1. Click **Add entry** in Metal metaobject
2. **Title:** Enter exact metal name (e.g., `18ct White Gold`)
3. **Colour:** Click color picker, enter hex code (e.g., `#E5E4E2`)
4. Click **Save**

**Critical:** Title must **exactly match** the value you'll use in product metafields (case-sensitive, spacing matters).

---

### Step 2: Create Siblings Collection

Each product family needs a collection to group all color variants.

#### 2.1 Create Collection
1. Go to **Products** → **Collections**
2. Click **Create collection**
3. **Title:** Descriptive name (e.g., "Eternal Love Necklace - All Metals")
4. **Handle:** Auto-generated (e.g., `eternal-love-necklace-all-metals`)
   - **Note the handle** - you'll need it for metafields

#### 2.2 Collection Type

**Option A: Manual Collection** (Recommended for small sets)
- Select **Manual**
- Manually add each sibling product

**Option B: Automated Collection** (For larger sets)
- Select **Automated**
- Set conditions (e.g., Tag equals `eternal-love-necklace`)
- Products matching conditions auto-added

#### 2.3 Collection Settings
- **Visibility:** Can be hidden from navigation (not required to be public)
- **Products:** Add all metal variants of the same design

**Example:**
```
Collection: "Eternal Love Necklace - All Metals"
Products:
  - Eternal Love Necklace - 18ct White Gold
  - Eternal Love Necklace - 18ct Yellow Gold
  - Eternal Love Necklace - 18ct Rose Gold
```

---

### Step 3: Configure Product Metafields

Each product needs two metafields to enable siblings functionality.

#### 3.1 Add Siblings Collection Metafield

1. Go to **Products** → Select product
2. Scroll to **Metafields** section
3. Find or add: `theme.siblings`
   - **Type:** Collection reference
   - **Value:** Select the siblings collection created in Step 2

**Example:**
```
Namespace.Key: theme.siblings
Type: Collection reference
Value: eternal-love-necklace-all-metals
```

#### 3.2 Add Sibling Color Metafield

1. In the same product metafields section
2. Find or add: `theme.sibling_color`
   - **Type:** Single line text
   - **Value:** Exact metal name (must match metaobject title)

**Example:**
```
Namespace.Key: theme.sibling_color
Type: Single line text
Value: 18ct White Gold
```

**Supported Metafield Names:**
The theme checks multiple variations (use any one):
- `theme.sibling_color` (recommended)
- `theme.sibling_colour` (UK spelling)
- `theme.siblings_color`
- `theme.siblings_colour`

#### 3.3 Repeat for All Siblings

Apply the same metafields to **every product** in the siblings group:
- Same `theme.siblings` collection reference
- Different `theme.sibling_color` value for each metal

---

### Step 4: Publish Products

**Critical:** Products must be **Active** (published) to appear in siblings.

#### 4.1 Check Product Status
1. Go to **Products** → Select product
2. Check **Status** in top-right
3. If "Draft", change to **Active**

#### 4.2 Visibility Options

If products shouldn't be publicly visible yet:

**Option A: Schedule Availability**
- Set **Availability** to future date
- Products are published but not buyable until date

**Option B: Remove from Sales Channels**
- Uncheck **Online Store** in sales channels
- Products exist but not visible on storefront

**Option C: Password-Protected Collection**
- Add to password-protected collection
- Accessible only with password

---

### Step 5: Enable Siblings Block in Theme

The siblings block should already be configured in your theme, but verify:

#### 5.1 Check Theme Configuration
1. Go to **Online Store** → **Themes**
2. Click **Customize** on active theme
3. Navigate to a product page
4. In left sidebar, check for **Siblings** block

#### 5.2 Block Settings

The block should have these settings:
- **Product siblings collection handle:** `{{ product.metafields.theme.siblings.value }}`
- **Product color metafield:** `{{ product.metafields.theme.sibling_color.value }}`
- **Sibling swatch size:** Large (or your preference)

**These are already configured in your theme template.**

---

## Verification Checklist

Use this checklist for each new product setup:

### Product Configuration
- [ ] Product status is **Active** (not Draft)
- [ ] Product has `theme.siblings` metafield with collection reference
- [ ] Product has `theme.sibling_color` metafield with metal name
- [ ] Metal name exactly matches a metaobject title (check spelling/case)
- [ ] Product is added to the siblings collection

### Collection Configuration
- [ ] Siblings collection exists
- [ ] Collection contains all metal variants
- [ ] All products in collection are published

### Metaobject Configuration
- [ ] Metal metaobject exists for this metal type
- [ ] Metaobject title exactly matches `sibling_color` value
- [ ] Metaobject has `colour` field with hex value

### Visual Verification
- [ ] View product on storefront (not theme editor)
- [ ] Siblings section appears on PDP
- [ ] Correct number of swatches displayed
- [ ] Swatches show correct colors
- [ ] Current product's swatch is highlighted
- [ ] Clicking swatch navigates to correct product

---

## Common Issues & Troubleshooting

### Issue 1: Siblings Not Appearing at All

**Symptoms:** No siblings section on PDP

**Possible Causes:**
1. Products are in Draft status
2. `theme.siblings` metafield is empty or incorrect
3. Collection doesn't exist or is empty
4. Siblings block is disabled in theme

**Solutions:**
- Publish all sibling products
- Verify `theme.siblings` metafield has correct collection handle
- Check collection contains products
- Enable Siblings block in theme customizer

---

### Issue 2: Swatches Appear But No Colors

**Symptoms:** Gray/white circles instead of colored swatches

**Possible Causes:**
1. Metal metaobject doesn't exist
2. Metaobject title doesn't match `sibling_color` value
3. Metaobject `colour` field is empty

**Solutions:**
- Create metal metaobject if missing
- Check exact spelling/capitalization match:
  ```
  Product metafield: "18ct White Gold"
  Metaobject title:  "18ct White Gold"  ✓ Match
  
  Product metafield: "18ct white gold"
  Metaobject title:  "18ct White Gold"  ✗ No match (case)
  ```
- Add hex color to metaobject `colour` field

---

### Issue 3: Wrong Products in Siblings

**Symptoms:** Unrelated products appear as siblings

**Possible Causes:**
1. Wrong collection referenced in `theme.siblings`
2. Collection contains incorrect products

**Solutions:**
- Verify `theme.siblings` metafield points to correct collection
- Review collection products, remove unrelated items
- Create separate collections for different product families

---

### Issue 4: Some Siblings Missing

**Symptoms:** Only some metal variants appear

**Possible Causes:**
1. Missing products are in Draft status
2. Missing products not in collection
3. Missing products lack metafields

**Solutions:**
- Publish all sibling products
- Add missing products to collection
- Apply metafields to all products in family

---

### Issue 5: Duplicate Swatches

**Symptoms:** Same color appears multiple times

**Possible Causes:**
1. Multiple products with same `sibling_color` value in collection
2. Duplicate products in collection

**Solutions:**
- Ensure each product has unique `sibling_color` value
- Remove duplicate products from collection
- If intentional (e.g., different sizes), consider separate collections

---

## Advanced Features

### Dual-Tone Swatches

The theme supports two-tone swatches for mixed-metal products.

**Setup:**
1. Use `&` separator in `sibling_color` metafield
2. Both metal names must exist as metaobjects

**Example:**
```
sibling_color: "18ct Rose Gold & 18ct Yellow Gold"
```

**Result:** Swatch displays diagonal split with both colors

**Requirements:**
- Both `18ct Rose Gold` and `18ct Yellow Gold` metaobjects must exist
- Order matters: left side & right side

---

### Alternative: Product List Metafield

For advanced control (including draft products in theme editor):

1. Create metafield: `theme.sibling_products`
   - **Type:** Product list
   - **Value:** Manually select sibling products

2. This overrides collection-based lookup
3. Useful for testing with draft products in theme editor

**Note:** Still requires products to be published for storefront visibility.

---

## Quick Reference

### Metafield Summary

| Metafield | Type | Purpose | Example Value |
|-----------|------|---------|---------------|
| `theme.siblings` | Collection reference | Links to siblings collection | `eternal-love-necklace-all-metals` |
| `theme.sibling_color` | Single line text | Metal name for this product | `18ct White Gold` |
| `theme.sibling_products` | Product list | Alternative to collection (optional) | [Product A, Product B] |

### Metaobject Summary

| Metaobject Type | Field | Type | Purpose | Example |
|-----------------|-------|------|---------|---------|
| `metal` | `title` | Single line text | Metal name identifier | `18ct White Gold` |
| `metal` | `colour` | Color | Hex color for swatch | `#E5E4E2` |

### File Locations

| File | Purpose |
|------|---------|
| `snippets/product-siblings.liquid` | Main siblings rendering logic |
| `snippets/product-information.liquid` | Calls siblings snippet |
| `sections/main-product.liquid` | Siblings block definition |
| `templates/product.json` | Product template configuration |

---

## Workflow for New Products

### Quick Setup Process

1. **Create Metal Metaobjects** (one-time per metal type)
   - Add new metals as needed

2. **Create Siblings Collection**
   - One collection per product family

3. **For Each Product:**
   - Set status to **Active**
   - Add to siblings collection
   - Add `theme.siblings` metafield → collection
   - Add `theme.sibling_color` metafield → metal name

4. **Verify on Storefront**
   - Check all swatches appear
   - Verify colors are correct
   - Test swatch navigation

### Estimated Time
- First product family: ~15 minutes
- Subsequent families: ~5 minutes per family
- Per product: ~2 minutes

---

## Support & Resources

### Theme Documentation
- [Fuel Themes - Product Siblings](https://documentation.fuelthemes.net/kb/how-to-setup-product-siblings/)

### Shopify Resources
- [Metafields Documentation](https://help.shopify.com/en/manual/custom-data/metafields)
- [Metaobjects Documentation](https://help.shopify.com/en/manual/custom-data/metaobjects)
- [Collections Documentation](https://help.shopify.com/en/manual/products/collections)

### Technical Support
- Check metafield values match metaobject titles exactly
- Verify all products are published
- Test in incognito/private browsing to avoid cache issues

---

## Appendix: Example Setup

### Complete Example: "Eternal Love Necklace"

#### Metal Metaobjects Created
```
Title: "18ct White Gold"  | Colour: #E5E4E2
Title: "18ct Yellow Gold" | Colour: #D4AF37
Title: "18ct Rose Gold"   | Colour: #B76E79
```

#### Collection Created
```
Name: "Eternal Love Necklace - All Metals"
Handle: eternal-love-necklace-all-metals
Type: Manual
Products: 3
```

#### Product 1: White Gold Variant
```
Title: Eternal Love Necklace - 18ct White Gold
Status: Active
Metafields:
  - theme.siblings: eternal-love-necklace-all-metals
  - theme.sibling_color: 18ct White Gold
In Collection: ✓
```

#### Product 2: Yellow Gold Variant
```
Title: Eternal Love Necklace - 18ct Yellow Gold
Status: Active
Metafields:
  - theme.siblings: eternal-love-necklace-all-metals
  - theme.sibling_color: 18ct Yellow Gold
In Collection: ✓
```

#### Product 3: Rose Gold Variant
```
Title: Eternal Love Necklace - 18ct Rose Gold
Status: Active
Metafields:
  - theme.siblings: eternal-love-necklace-all-metals
  - theme.sibling_color: 18ct Rose Gold
In Collection: ✓
```

#### Result on PDP
```
METAL: 18ct White Gold
[🟤] [🟡] [⚪ - Active]

Clicking rose gold swatch → navigates to rose gold product
Clicking yellow gold swatch → navigates to yellow gold product
```

---

**Last Updated:** June 18, 2026  
**Version:** 1.0  
**Theme:** Alexandra (Fuel Themes)
