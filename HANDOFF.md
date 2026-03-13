# Amin DnD — Theme Handoff Guide

This is everything you need to manage your Shopify theme. No code changes required for any of these tasks.

---

## Table of Contents
1. [Navigation Menu](#1-navigation-menu)
2. [Homepage](#2-homepage)
3. [Collection Pages](#3-collection-pages)
4. [Product Pages](#4-product-pages)
5. [Projects (Blog)](#5-projects-blog)
6. [Consulting & Direction Pages](#6-consulting--direction-pages)
7. [About Page](#7-about-page)
8. [Contact Widget](#8-contact-widget)
9. [Footer](#9-footer)
10. [Calendly Booking Links](#10-calendly-booking-links)
11. [Order Confirmation Email](#11-order-confirmation-email)
12. [Developer Notes](#12-developer-notes)

---

## 1. Navigation Menu

The slide-out menu pulls from a Shopify navigation menu.

**Setup:**
1. Go to **Online Store → Navigation**
2. Create (or edit) a menu called **`main-menu`**
3. Add links: Lessons, D&D, Cart, About, Contact (or whatever you want)
4. The menu updates automatically — no theme changes needed

**How it works:** Hamburger icon (top-left) opens a full-screen overlay with your menu links in large editorial typography. Cart icon stays visible top-right at all times.

---

## 2. Homepage

The homepage has two sections, each linking to a different part of your site.

**To edit:**
1. Go to **Online Store → Themes → Customize**
2. Select the **Home page** from the page dropdown
3. You'll see two "Editorial Link" sections
4. For each section, you can edit:
   - **Heading** (e.g., "Design")
   - **Subheading** (e.g., "Lessons")
   - **Link URL** (e.g., `/collections/design-lessons`)
   - **Images** — click each image block to upload/replace photos

**Current setup:**
- Section 1: "Design / Lessons" → links to design lessons collection
- Section 2: "Direction / & Consulting" → links to consulting page

---

## 3. Collection Pages

Collection pages (like the lessons page) show location groups: LA, NYC, Virtual.

**To edit:**
1. Go to **Customize → Collection pages**
2. Each location is an "Editorial Link" section in **grid** layout mode
3. Edit heading, subheading, link URL, and images per location
4. Toggle **"Full width"** on individual image blocks to control layout:
   - LA: 4 images, all half-width → 2×2 grid
   - NYC: 1 full-width + 2 half-width
   - Virtual: 2 full-width images stacked

**To add a new location:** Click "Add section" → choose "Editorial Link" → set layout to "Grid"

---

## 4. Product Pages

Products show: title, price, variant selector, add-to-cart, Shopify payment button, Calendly booking link, and product details.

**Calendly link appears automatically** based on product tags:
- Tag `nyc` → links to NYC Calendly
- Tag `la` → links to LA Calendly  
- Tag `virtual` → links to Virtual Calendly

**To change Calendly URLs:**
1. Go to **Customize → Product pages → Product section settings**
2. Under "Calendly Booking" you'll see three URL fields — edit as needed

---

## 5. Projects (Blog)

Projects use Shopify's blog system. Each blog article = one project.

**Initial setup:**
1. Go to **Shopify Admin → Blog posts → Manage blogs**
2. Create a blog called **"Projects"** (or rename the default "News" blog)

**To add a project:**
1. Go to **Blog posts → Add blog post**
2. Set the blog to "Projects"
3. Add a **title** (project name)
4. Add **content** (project description)
5. Add a **featured image** (shows on the projects grid)
6. Publish it

**Project detail pages** have a 24-column image grid:
1. Go to **Customize** and navigate to a project article page
2. Add "Image" blocks in the article section
3. Each image has a **Columns** setting (1–24) controlling its width
4. Each image has a **Rows** setting (1–4) for optional row spanning
5. Mix and match to create unique layouts per project

**Examples:**
- Full-width image: set columns to 24
- Two equal images side by side: set both to 12
- One large + one small: set one to 16, the other to 8
- Three equal: set each to 8

---

## 6. Consulting & Direction Pages

These are custom page templates already wired up.

**To assign them:**
1. Go to **Shopify Admin → Pages**
2. Create (or edit) a page called "Consulting"
3. In the right sidebar under **Theme template**, select **`page.consulting`**
4. Same for Direction — create the page, assign **`page.direction`**

**To edit content:**
1. Go to **Customize** and navigate to the page
2. Consulting has block types: Large Image, Image Pair, Text Block, CTA Button, Spacer
3. Direction has Course Card blocks with image, category, title, and link

---

## 7. About Page

**To set up:**
1. Go to **Pages** → create/edit "About" page
2. Assign template **`page.about`**
3. Write your about content in the page editor
4. In **Customize**, you can optionally add a feature image and subtitle

---

## 8. Contact Widget

The floating contact button (bottom-right corner) appears on every page automatically. Submissions go to your store's email address.

**No setup needed.** It uses Shopify's built-in contact form.

---

## 9. Footer

**To configure:**
1. Go to **Customize → Footer**
2. Assign a **footer menu** (create one in Online Store → Navigation if needed)
3. Toggle **payment icons** on/off

---

## 10. Calendly Booking Links

Calendly links show on product pages based on product tags.

**Current mapping:**

| Product Tag | Calendly URL |
|-------------|-------------|
| `nyc` | https://calendly.com/aminalisaleh/2x-nyc |
| `la` | https://calendly.com/aminalisaleh/2x-la |
| `virtual` | https://calendly.com/aminalisaleh/2x-virtual |

**To add a new Calendly link for a new location:**
This requires a small code change to `snippets/calendly-booking.liquid` — reach out to your developer.

**To change existing URLs:**
Go to **Customize → Product page → section settings → Calendly Booking** and update the URLs.

---

## 11. Order Confirmation Email

To include Calendly booking links in order confirmation emails:

1. Go to **Shopify Admin → Settings → Notifications**
2. Click **Order confirmation**
3. Click **Edit code**
4. Find the order summary table section
5. Paste the code from `snippets/calendly-email-snippet.liquid` after the order items
6. Save

The email will automatically show the correct Calendly link based on what the customer purchased.

---

## 12. Developer Notes

**Tech stack:** Shopify Skeleton Theme + Tailwind CSS v4

**Local development:**
```bash
npm run dev:css     # Watch & compile Tailwind
shopify theme dev   # Preview theme locally
```

**Key files:**
- `sections/editorial-link.liquid` — Reusable section for homepage + collection layouts
- `sections/header.liquid` — Slide-out hamburger menu
- `sections/contact-widget.liquid` — Floating contact form
- `sections/article.liquid` — Individual project pages with 24-col grid
- `sections/blog.liquid` — Projects index grid
- `snippets/calendly-booking.liquid` — Calendly URL resolver (used on product pages)
- `snippets/calendly-email-snippet.liquid` — Code to paste into order confirmation email

**Important:** Inline `<style>` tags are used instead of `{% stylesheet %}` for interactive components (menu, contact widget) because Shopify's stylesheet tag deduplicates and can break JS-toggled classes.
