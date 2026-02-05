# Stripe Payment Link Setup Guide

## Problem
Customers complete payment but cannot download files because the success page doesn't know which product they purchased.

## Root Cause
Stripe Payment Links need the Success URL configured in the Stripe Dashboard, not passed as a URL parameter.

## Solution: Configure Success URLs in Stripe Dashboard

### For Each Payment Link:

1. **Go to Stripe Dashboard**: https://dashboard.stripe.com
2. Navigate to: **Products** → **Payment Links**
3. Find and edit each Payment Link
4. In the "After payment" section, set the **Success URL**

### Success URLs for Each Product:

#### 1. Gaussian Splat Editor
- **Payment Link**: `https://buy.stripe.com/14A4gseg9fKS5d0bRi7kc06`
- **Success URL**: `https://simulacrum.dk/success.html?product=unity-gsplat-editor`

#### 2. VHS 1980 VR Effects
- **Payment Link**: `https://buy.stripe.com/14A3co7RL9mufRE2gI7kc01`
- **Success URL**: `https://simulacrum.dk/success.html?product=vhs-vr-effects`

#### 3. Worldlabs Unity API
- **Payment Link**: `https://buy.stripe.com/7sYcMYb3X42a0WK7B27kc08`
- **Success URL**: `https://simulacrum.dk/success.html?product=worldlabs-api`

#### 4. Gaussian Relighting (when available)
- **Payment Link**: `https://buy.stripe.com/eVq28k0pj8iq5d04oQ7kc04`
- **Success URL**: `https://simulacrum.dk/success.html?product=gaussian-relighting`

## Testing

After configuring the Success URLs:

1. Go to your shop: https://simulacrum.dk/Shop.html
2. Add a product to cart
3. Click "Proceed to Checkout"
4. Use Stripe test card: `4242 4242 4242 4242` (any future date, any CVC)
5. Complete payment
6. Verify you're redirected to success page with the correct product and download link

## Important Notes

- ✅ Success URLs are configured **per Payment Link** in Stripe Dashboard
- ❌ You cannot dynamically change the success URL by appending parameters to the Payment Link
- 🔒 The success page will show "contact support" if the product parameter is missing (this prevents serving wrong downloads)
- 📧 Customers always receive a receipt email from Stripe with their order details

## For Immediate Customer Support

If a customer already paid but couldn't download:

1. Check their Stripe payment receipt for the order ID
2. Look up the payment in Stripe Dashboard to see which product they purchased
3. Send them the direct download link:
   - VHS Effects: `https://simulacrum.dk/Products/1980VREffects/VHSWorld.zip`
   - Gaussian Splat Editor: `https://simulacrum.dk/Products/GaussianSplatEditor/GaussianSplatEditor.zip`
   - Worldlabs API: `https://simulacrum.dk/Products/WorldlabsAPI/WorldlabsAPI.zip`
