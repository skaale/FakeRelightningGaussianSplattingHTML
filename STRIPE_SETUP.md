# Stripe Payment Setup Guide

## Setting Up Stripe Payment Links

### Step 1: Create Payment Links in Stripe Dashboard

1. Log in to your [Stripe Dashboard](https://dashboard.stripe.com)
2. Navigate to **Products** → **Payment Links**
3. Click **Create payment link** for each product:

#### Product 1: Gaussian Splat Editor
- **Price**: $2.00 USD
- **Product Name**: Gaussian Splat Editor
- **Description**: Unity Editor plugin for editing 3D Gaussian Splats
- **Success URL**: `https://simulacrum.dk/success.html?product=unity-gsplat-editor`
- Copy the Payment Link URL and update `Shop.html` line 610

#### Product 2: Gaussian Splatting Re-Lightning ✅
- **Price**: $299.00 USD
- **Product Name**: Gaussian Splatting Re-Lightning
- **Description**: Real-time dynamic lighting system for 3D Gaussian Splats
- **Success URL**: `https://simulacrum.dk/success.html?product=gaussian-relighting`
- **Payment Link**: `https://buy.stripe.com/eVq28k0pj8iq5d04oQ7kc04` ✅ Configured

#### Product 3: Worldlabs Unity API ✅
- **Price**: $29.00 USD
- **Product Name**: Worldlabs Unity API
- **Description**: Comprehensive Unity API integration for Worldlabs platform
- **Success URL**: `https://www.simulacrum.dk/success.html?product=worldlabs-api`
- **Payment Link**: (see Shop.html) ✅ Configured

#### Product 4: VHS 1980 VR Effects
- **Price**: $36.00 USD
- **Product Name**: VHS 1980 VR Effects
- **Description**: Authentic 1980s VHS tape aesthetic effects for Unity (VR compatible)
- **Success URL (required)**: `https://www.simulacrum.dk/success.html?product=vhs-vr-effects`  
  ⚠️ Do **not** use `https://www.simulacrum.dk/success.html` alone — the `?product=vhs-vr-effects` is required so the correct download is shown.
- **Payment Link**: (see Shop.html) ✅ Configured

#### Product 5: TRIPO API UNITY HDRP
- **Price**: $9.95 USD
- **Product Name**: TRIPO API UNITY HDRP
- **Description**: TRIPO API integration for Unity HDRP — real-time 3D capture, streaming, and cloud workflows
- **Success URL (required)**: `https://www.simulacrum.dk/success.html?product=trip-api-unity-hdrp`
- **Payment Link**: Create in Stripe Dashboard, then paste the URL into `Shop.html` (replace `placeholder_trip_api_hdrp` in `STRIPE_PAYMENT_LINKS`)

### Step 2: Update Shop.html

Replace the placeholder URLs in `Shop.html`:

```javascript
const STRIPE_PAYMENT_LINKS = {
    'vhs-vr-effects': 'https://buy.stripe.com/14A3co7RL9mufRE2gI7kc01',
    'unity-gsplat-editor': 'YOUR_STRIPE_LINK_HERE',
    'gaussian-relighting': 'YOUR_STRIPE_LINK_HERE',
    'worldlabs-api': 'YOUR_STRIPE_LINK_HERE',
    'trip-api-unity-hdrp': 'YOUR_STRIPE_LINK_HERE'   // $9.95 — create Payment Link, set Success URL to success.html?product=trip-api-unity-hdrp
};
```

### Step 3: Prepare Product Download Files

Create the following directory structure and add your product ZIP files:

```
Products/
├── 1980VREffects/
│   └── VHSWorld.zip (already exists)
├── GaussianSplatEditor/
│   └── GaussianSplatEditor.zip
├── Relighting/
│   └── Relighting.zip
├── WorldlabsAPI/
│   └── WorldlabsAPI.zip
└── TRIPOAPIHDRP/
    └── TRIPOAPIHDRP.zip
```

### Step 4: Configure Stripe Success URLs

In each Stripe Payment Link settings:
- Set **After payment** → **Redirect to a URL**
- **Must include** the product parameter. Examples:
  - VHS 1980 VR Effects: `https://www.simulacrum.dk/success.html?product=vhs-vr-effects`
  - Worldlabs Unity API: `https://www.simulacrum.dk/success.html?product=worldlabs-api`
  - Gaussian Splatting Re-Lightning: `https://www.simulacrum.dk/success.html?product=gaussian-relighting`
  - Gaussian Splat Editor: `https://www.simulacrum.dk/success.html?product=unity-gsplat-editor`
  - TRIPO API UNITY HDRP: `https://www.simulacrum.dk/success.html?product=trip-api-unity-hdrp`
- Using only `https://www.simulacrum.dk/success.html` (no `?product=`) will show the wrong/empty download state.

The success page will automatically:
1. Detect which product was purchased
2. Show the correct download link
3. Display product-specific information
4. Clear the cart

### Step 5: Test the Flow

1. Add a product to cart
2. Click "Proceed to Checkout"
3. Complete test payment (use Stripe test card: 4242 4242 4242 4242)
4. Verify redirect to success page
5. Verify correct download link appears
6. Test download functionality

## Notes

- Domain: `simulacrum.dk`
- Use Stripe test mode for testing
- Ensure download files are accessible via web server
- Consider adding download expiration/time limits if needed
- You may want to add email delivery of download links via Stripe webhooks
