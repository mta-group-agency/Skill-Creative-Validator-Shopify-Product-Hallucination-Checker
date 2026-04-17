# Creative Validator — Shopify Product Hallucination Checker

**Catch AI-hallucinated products in ad creatives before they go live.**

> Free [Claude Code](https://claude.ai/claude-code) skill by [MTA Group](https://mtagroup.org) / [Force of Nature](https://forceofnature.agency) — built by Marek Ciesla

---

## The Problem

AI creative tools (Canva AI, Meta Advantage+, Midjourney, DALL-E, Adobe Firefly) frequently **hallucinate products** — they generate realistic-looking items that don't actually exist in your store.

A customer clicks the ad, lands on your Shopify store, and the product they saw **is not there**. Wasted ad spend, damaged trust, inflated bounce rates.

As more e-commerce teams adopt AI-generated creatives at scale, this problem is growing fast.

## The Solution

Creative Validator **automatically cross-references every product visible in an ad creative against your real Shopify product catalog** and generates a pass/fail validation report.

Works with any visual ad format: static banners, social media graphics, carousel cards, Meta ads, Google Ads display, TikTok ads, and more.

## Key Features

- **Automated catalog fetching** — pulls all products, images, prices, and variants from any Shopify store
- **Visual product matching** — compares each product in the creative against real catalog photos
- **Three-tier classification** — PASS (exists), WARNING (similar but different), FAIL (hallucinated)
- **HTML validation report** — shareable, mobile-friendly, color-coded with side-by-side comparisons
- **Multi-language support** — English, Polish, and others
- **Large catalog support** — handles 1000+ SKUs with automatic pagination

## Quick Start

### Requirements

- [Claude Code](https://claude.ai/claude-code) installed
- Python 3.8+
- Access to a Shopify store URL

### Installation

Add this skill to your Claude Code skills directory:

```bash
# Clone the repository
git clone https://github.com/mta-group-agency/Skill-Creative-Validator-Shopify-Product-Hallucination-Checker.git

# Add to your Claude Code skills path
# See Claude Code documentation for skill installation
```

### Usage

In Claude Code, use any of these trigger phrases:

```
validate creative
check creative
verify products
creative QA
hallucination check
```

Then provide:
1. **Creative image(s)** — upload the ad graphic(s) to validate
2. **Shopify store URL** — e.g. `https://storename.myshopify.com`

The skill will fetch your catalog, analyze the creative, and generate a validation report.

## How It Works

```
Ad Creative (image)          Shopify Store (URL)
        │                            │
        ▼                            ▼
  Identify every              Fetch all products
  product in the ad           images, prices, variants
        │                            │
        └──────────┬─────────────────┘
                   ▼
        Cross-reference each product
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
     ✅ PASS    ⚠️ WARNING   ❌ FAIL
    (exists)   (similar)  (hallucinated)
                   │
                   ▼
         HTML Validation Report
```

### Classification

| Status | Meaning | Action |
|--------|---------|--------|
| **PASS** (green) | Product exists in catalog. Visual + name/price match. | Safe to publish |
| **WARNING** (yellow) | Similar to a catalog item but with differences (wrong color, modified price). | Review manually |
| **FAIL** (red) | Product does not exist in the catalog. This is a hallucination. | **Do not publish** |

## Validation Report

The skill generates a single-file HTML report with:

- Color-coded banner (green = all clear, red = hallucinations detected)
- Side-by-side creative vs. catalog comparison for each product
- Match explanation and closest catalog suggestions for failures
- Summary with pass/warning/fail counts
- Mobile-friendly layout for sharing with clients

## Edge Cases

| Scenario | Handling |
|----------|----------|
| Multiple products in one creative | Each validated separately. One FAIL = entire creative fails |
| Products at unusual angles/crops | Best-effort matching. Uncertain = WARNING |
| Large catalogs (1000+ products) | Automatic pagination |
| Text overlays hiding products | Noted as "partially obscured — manual check recommended" |
| No `/products.json` access | User prompted to provide product feed CSV/XML |

## Who Is This For

- **E-commerce marketing teams** running AI-generated ad creatives at scale
- **Performance marketing agencies** managing Shopify client accounts
- **Creative QA teams** reviewing ad assets before launch
- **Shopify store owners** using AI tools for product advertising

## Built By

**[MTA Group](https://mtagroup.org)** / **[Force of Nature](https://forceofnature.agency)** — performance marketing agencies specializing in e-commerce growth, paid advertising, and marketing automation.

**Author:** Marek Ciesla — [MTA Group](https://mtagroup.org) & [Force of Nature](https://forceofnature.agency)

We built this because we kept catching AI-hallucinated products in client ad creatives during manual QA. Automating the check saves hours per campaign and prevents costly mistakes.

## License

MIT

## Contributing

Issues and pull requests welcome. If you've found a creative hallucination edge case we don't handle, [open an issue](https://github.com/mta-group-agency/Skill-Creative-Validator-Shopify-Product-Hallucination-Checker/issues).
