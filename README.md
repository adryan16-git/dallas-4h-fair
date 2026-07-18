# Dallas County 4-H Fair Schedule Site

Live at: **https://4h.richardsonfamily.us**  
GitHub repo: **https://github.com/adryan16-git/dallas-4h-fair**

---

## How It Works

- Single self-contained `index.html` file — no frameworks, no dependencies
- Hosted free on **GitHub Pages** (`main` branch)
- Custom domain `4h.richardsonfamily.us` via **Cloudflare DNS** (CNAME record, DNS-only / gray cloud)
- HTTPS provided automatically by GitHub Pages (Let's Encrypt)

---

## Every Year Checklist

### 1. Remove the archived banner

Delete these lines near the top of `index.html` (just above `<nav class="day-tabs">`):

```html
<div class="archived-banner">
  <strong>The 20XX Dallas County 4-H Fair has concluded.</strong> ...
</div>
```

And remove the `.archived-banner` CSS block in the `<style>` section.

### 2. Update the page title and header dates

In `<head>`:
```html
<title>2027 Dallas County 4-H Fair Schedule</title>
```

In `<header>`:
```html
<h1>2027 Dallas County 4-H Fair Schedule</h1>
<p>July X–X &nbsp;·&nbsp; Adel, Iowa ...</p>
```

### 3. Update the day tab labels

Find the `<nav class="day-tabs">` block and update each tab's label and `data-day` date hint:
```html
<div class="day-tab" data-day="mon">Mon 7/7</div>
```
The `data-day` keys (`mon`, `tue`, etc.) don't need to change — just the visible label text.

### 4. Update the auto-advance date map

In the `<script>` block, find `const dayMap` and update the dates (month is 0-indexed: June = 5, July = 6):
```js
const dayMap = [
  { day: 'setup', date: new Date(y, 5, 27) },  // June 27
  { day: 'mon',   date: new Date(y, 6,  7) },  // July 7
  { day: 'tue',   date: new Date(y, 6,  8) },
  // ...
];
```

### 5. Update the day panel headings

Each panel starts with a heading like:
```html
<section class="day-panel" id="panel-mon">
  <h2 class="day-heading">Monday, July 6</h2>
```
Update the date in each `<h2>`.

### 6. Update the schedule events

Each event is a card like:
```html
<div class="event-card" data-cats="beef clover">
  <div class="event-time">9:00 AM</div>
  <div class="event-body">
    <div class="event-title">Beef Showmanship</div>
    <div class="event-location">Show Arena</div>
    <div>
      <span class="badge cat-beef">Beef</span>
      <span class="badge cat-clover">Clover Kids</span>
    </div>
  </div>
</div>
```

`data-cats` drives the filter buttons — valid values: `beef`, `swine`, `sheep`, `goat`, `horse`, `rabbit`, `poultry`, `dog`, `static`, `clover`, `food`, `entertainment`, `admin`

### 7. Update the Deadlines tab

Find `id="panel-deadlines"` and update the entry/fair dates listed there.

### 8. Update the footer

```html
<strong>Last updated: July X, 2027</strong>
```

---

## Pushing Changes

```bash
cd ~/projects/dallas-4h-fair
git add index.html
git commit -m "Update for 2027 fair"
git push
```

GitHub Pages deploys automatically within ~30 seconds.

---

## End of Fair

Add this banner just above `<nav class="day-tabs">` in `index.html`, and add the CSS below to the `<style>` block:

**HTML:**
```html
<div class="archived-banner">
  <strong>The 2027 Dallas County 4-H Fair has concluded.</strong> Thanks for a great fair — check back next summer for the 2028 schedule!
</div>
```

**CSS:**
```css
.archived-banner {
  background: var(--gold-pale);
  border-bottom: 2px solid var(--gold);
  text-align: center;
  padding: .7rem 1.5rem;
  font-size: .9rem;
  color: #5a4000;
}
.archived-banner strong { font-weight: 700; }
```

---

## Cloudflare DNS (if ever needed to reconfigure)

- Record type: **CNAME**
- Name: `4h`
- Target: `adryan16-git.github.io`
- Proxy: **DNS only (gray cloud)** — orange/proxied breaks GitHub's HTTPS cert

If HTTPS breaks after a DNS change, remove the custom domain via GitHub Pages settings, let it rebuild, then re-add it and wait ~15 min for the cert.

---

## Claude Prompt for Next Year

Copy and paste this to start a Claude Code session for the annual update:

```
I need to update the Dallas County 4-H Fair schedule website for 2027.

The site is a single index.html file at ~/projects/dallas-4h-fair/index.html,
hosted on GitHub Pages at https://4h.richardsonfamily.us.

The README has the full yearly checklist. Here's what I need to do:

1. Remove the archived banner from last year
2. Update the year/dates throughout (title, header, tab labels, day headings, auto-advance date map, footer)
3. Update the schedule events based on the new fair schedule (I'll provide it)
4. Update the Deadlines tab with new entry deadlines

The fair runs [DATES HERE]. Here is the new schedule:
[PASTE SCHEDULE HERE]

Please start by reading the README and the current index.html to understand the structure,
then walk me through the changes before applying them.
```
