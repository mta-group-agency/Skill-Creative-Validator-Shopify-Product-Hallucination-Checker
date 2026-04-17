# Creative Validator — Shopify Product Hallucination Checker

**Catch AI-hallucinated products in ad creatives before they go live.**

> Free Claude Code skill by [MTA Group](https://mtagroup.org) / [Force of Nature](https://forceofnature.agency) — built by Marek Ciesla

---

## The Problem: AI Ad Creatives Show Products That Don't Exist

AI tools that generate ad creatives — Canva AI, Meta Advantage+ Creative, Midjourney, DALL-E, Adobe Firefly — frequently **hallucinate products**. They produce realistic-looking items that don't actually exist in the advertiser's store.

The result: a customer clicks the ad, lands on the Shopify store, and the product they saw **is not there**. This wastes ad spend, damages trust, and inflates bounce rates.

**This is a growing problem.** As more e-commerce teams adopt AI-generated creatives at scale, hallucinated products slip through QA undetected — especially when catalogs have hundreds or thousands of SKUs.

## What This Skill Does

Creative Validator is an open-source [Claude Code](https://claude.ai/claude-code) skill that **automatically cross-references every product visible in an ad creative against your real Shopify product catalog** and generates a pass/fail validation report.

It works with any visual ad format: static banners, social media graphics, carousel cards, Meta ads, Google Ads display creatives, TikTok ad images, and more.

### Key Features

- **Automated catalog fetching** — pulls all products, images, prices, and variants from any Shopify store via the `/products.json` endpoint
- **Visual product matching** — compares each product shown in the creative against real catalog product photos
- **Three-tier classification** — PASS (product exists), WARNING (similar but different), FAIL (hallucinated product)
- **HTML validation report** — shareable, mobile-friendly, color-coded report with side-by-side comparisons
- **Multi-language support** — responds in the user's language (English, Polish, and others)
- **Edge case handling** — works with large catalogs (1000+ SKUs), partially obscured products, and multiple products per creative

---

## Who Is This For

- **E-commerce marketing teams** running AI-generated ad creatives at scale
- **Performance marketing agencies** managing Shopify client accounts
- **Creative QA teams** reviewing ad assets before launch
- **Shopify store owners** using AI tools for product-based advertising

If you use AI to generate ad visuals for Shopify stores, you need a hallucination check in your workflow.

---

## How It Works

### Inputs Required

1. **Creative image(s)** — the ad graphic(s) to validate (uploaded by the user)
2. **Shopify store URL** — e.g. `https://storename.myshopify.com` or `https://brand.com`

### Step 1: Fetch the Shopify Product Catalog

The skill runs a catalog fetcher script that pulls all products from the Shopify store:

```bash
python3 <skill-path>/scripts/fetch_shopify_catalog.py "<store-url>" "<output-dir>"
```

This creates:
- `catalog.json` — full product data (titles, images, prices, variants)
- `product_images/` — downloaded product photos organized by product handle

If the store blocks `/products.json` (rare but possible), the user can provide a product feed CSV/XML instead.

### Step 2: Analyze the Ad Creative

The skill examines the uploaded creative image and identifies every product visible in it:
- **Visual appearance** — color, shape, style, distinctive features
- **Text overlays** — product names, prices, descriptions shown in the ad
- **Position mapping** — where each product appears in the creative

AI hallucinations are often subtle: the product looks plausible but has a wrong color, different pattern, or a name that doesn't match any real SKU.

### Step 3: Cross-Reference Against the Real Catalog

For each product identified in the creative:

1. **Text matching** — search `catalog.json` for potential matches by name and description
2. **Visual comparison** — compare the creative's product image against downloaded catalog photos
3. **Classification:**
   - **PASS** (green) — Product clearly exists in catalog. Visual + name/price match confirmed.
   - **WARNING** (yellow) — Product is similar to a catalog item but has differences (wrong color variant, slightly different design, modified price).
   - **FAIL** (red) — Product does not exist in the catalog. **This is a hallucination.** The customer would click the ad and not find this product in the store.

### Step 4: Generate the Validation Report

The skill produces a single-file HTML report containing:

**Header:**
- Store name and URL
- Validation date
- Creative file name
- Overall verdict: PASS / WARNING / FAIL

**Product-by-product breakdown:**
- Creative vs. catalog side-by-side comparison for each product
- Color-coded match status badge (green / yellow / red)
- Explanation of why each product passed or failed
- Closest catalog match suggestions for hallucinated products

**Summary:**
- Total products checked
- Passed / Warning / Failed counts
- Clear recommendation: "Safe to publish" or "DO NOT PUBLISH — contains hallucinated products"

The report is professional, mobile-friendly, and can be shared directly with clients or stakeholders.

---

## Edge Cases Handled

| Scenario | How it's handled |
|---|---|
| Multiple products in one creative | Each validated separately. One red = entire creative fails. |
| Products at unusual angles or crops | Best-effort matching. Uncertain matches marked as WARNING. |
| Large catalogs (1000+ products) | Script paginates automatically. |
| Text overlays hiding products | Noted in report as "partially obscured — manual check recommended." |
| No `/products.json` access | User prompted to provide a product feed or enable the endpoint. |

---

## Trigger Phrases

Use any of these to activate the skill in Claude Code:

`validate creative` · `check creative` · `verify products` · `creative QA` · `product validation` · `hallucination check` · `compare creative to store` · `creative vs catalog` · `are these real products` · `flag fake products` · `AI hallucination check`

Polish: `sprawdź kreację` · `waliduj kreację` · `czy produkty są prawdziwe` · `kreacja produktowa` · `walidator kreacji`

---

## Installation

This skill is designed for [Claude Code](https://claude.ai/claude-code). Install it by adding the skill directory to your Claude Code skills path.

---

## Built By

**[MTA Group](https://mtagroup.org)** / **[Force of Nature](https://forceofnature.agency)** — performance marketing agencies specializing in e-commerce growth, paid advertising, and marketing automation.

**Author:** Marek Ciesla — [MTA Group](https://mtagroup.org) & [Force of Nature](https://forceofnature.agency)

We built this skill because we kept catching AI-hallucinated products in client ad creatives during manual QA. Automating the check saves hours per campaign and prevents embarrassing (and costly) mistakes.

---

## Related Topics

AI ad creative validation, Shopify product catalog verification, e-commerce creative QA, AI hallucination detection in advertising, automated ad asset review, product-based ad validation, Shopify marketing tools, Claude Code skills for e-commerce, performance marketing QA automation

---

*name: creative-validator*
*description: Validate ad creatives against a real Shopify product catalog to catch AI hallucinations. Use this skill whenever someone wants to verify that products shown in an ad creative, banner, social media graphic, or any marketing visual actually exist in their Shopify store. Trigger on: 'validate creative', 'check creative', 'verify products', 'creative QA', 'product validation', 'hallucination check', 'sprawdź kreację', 'waliduj kreację', 'czy produkty są prawdziwe', 'compare creative to store', 'creative vs catalog', 'product-based ads check', 'are these real products', 'flag fake products', 'AI hallucination check', 'kreacja produktowa', 'walidator kreacji'. Also trigger when someone uploads an ad image and shares a Shopify store link asking if the products match, or when they mention concerns about AI-generated creatives showing non-existent products.*
