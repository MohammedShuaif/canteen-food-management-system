# Canteen Food Management System

A single-file web application for managing a campus canteen — student ordering,
kitchen counter operations, and admin menu/stock/report management.

## Files

| File | Purpose |
|---|---|
| `canteen.html` | The complete application — HTML, CSS and JavaScript in one file |
| `README.md` | This document |

## How to run

1. Download `canteen.html`.
2. Double-click it, or open it in any modern browser (Chrome, Edge, Firefox, Safari).

No server, database installation, or internet connection is required. Data is
stored in the browser's `localStorage`, so it survives refreshes and restarts on
the same machine.

## Modules

**1. Order food (student / customer)**
- Menu browsing with category filter (Breakfast, Meals, Snacks, Beverages, Desserts)
- Keyword search across dish names and descriptions
- Veg / non-veg indicators, price and live portions-remaining
- Cart with quantity steppers, subtotal, 5% GST and grand total
- Order placement with name/roll number and Dine-in or Takeaway
- Token number generation and a live "ready" token board
- Personal order history with live status

**2. Kitchen counter (staff)**
- Live order queue grouped as New → On the stove → Ready
- Status transitions: Start cooking, Mark ready, Handed over
- Order cancellation with automatic stock restoration
- Closed-order log with token, customer, item count, total, status and time

**3. Manage canteen (admin)**
- Dashboard: orders today, revenue today, plates served, queue size, low-stock count
- Revenue-by-category bar chart and best-selling item of the day
- Menu management: add dish, remove dish, edit price, edit portion count
- Availability toggle to take a dish off the menu without deleting it
- Reset to seed data

## Data model

```
menu[]   : { id, name, cat, price, veg, stock, available, desc }
orders[] : { id, token, customer, mode, items[], subtotal, gst, total,
             status, placedAt, updatedAt }
items[]  : { id, name, price, qty }
nextToken: running token counter (starts at 101)
```

`status` moves through: `placed → preparing → ready → completed`, or `cancelled`
from `placed`/`preparing`.

## Business rules implemented

- An item cannot be ordered beyond its available portions.
- Placing an order decrements stock; cancelling an order restores it.
- Items marked unavailable or at zero stock show as "Sold out" and cannot be added.
- Bill = item total + 5% GST, rounded to the nearest rupee.
- Tokens are issued in sequence and never reused.

## Technology

- HTML5, CSS3 (custom properties, grid, flexbox, light/dark themes)
- Vanilla JavaScript (ES5-compatible, no build step, no external libraries)
- `localStorage` for persistence; optional shared database when hosted on claude.ai

## Possible extensions

- Online payment and printed bill
- Login with roll number and a prepaid wallet
- Daily and monthly sales export to Excel
- Feedback and ratings per dish
