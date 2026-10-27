# LAUNCH: The Website Launch Checklist (Don't Launch Your Website Without This List)[cite: 7]

**Author:** `@namansoni.ai` — Ship Without Code *(Checklist + Prompts)*[cite: 7]

15 things to add before launch, so Google can find your site, it looks right when shared, and visitors trust it[cite: 7]. Includes a checklist, the prerequisites, and detailed copy-paste prompts for Claude Code, Cursor, or Codex[cite: 7].

---

## How to Use This[cite: 7]

1. Get the prerequisites ready (Section 01)[cite: 7].
2. Run prompts A–D one at a time, or the master prompt in the last section[cite: 7].
3. Tick each item on the checklist (Section 02) as it's done[cite: 7].
4. After going live, do the 4 manual steps in the last section[cite: 7].

## Inside[cite: 7]

| Section | Topic | Page |
| :--- | :--- | :--- |
| **01** | **Prerequisites:** What to have ready[cite: 7] | Page 2[cite: 7] |
| **02** | **The 15-item launch checklist**[cite: 7] | Page 3[cite: 7] |
| **A** | **Prompt A:** Get found on Google (6 items)[cite: 7] | Page 4[cite: 7] |
| **B** | **Prompt B:** Share previews & images (2 items)[cite: 7] | Page 5[cite: 7] |
| **C** | **Prompt C:** Forms, tracking & privacy (4 items)[cite: 7] | Page 6[cite: 7] |
| **D** | **Prompt D:** Trust (3 items)[cite: 7] | Page 7[cite: 7] |
| **+** | **Master prompt + after-launch steps**[cite: 7] | Page 8[cite: 7] |

---

## 01. Prerequisites[cite: 8]

*Seedhi baat: ye cheezein pehle ready rakho, phir prompts chalao.*[cite: 8]

The prompts do the building[cite: 8]. These are the things only you can provide: accounts, your domain, and real content[cite: 8]. Get them ready first and every prompt runs in one go[cite: 8].

**Tools & Access**[cite: 8]
* Your website's code open in Claude Code, Cursor, or Codex[cite: 8]
* The site deployed on a host (e.g., Vercel, Netlify) with your own domain connected[cite: 8]
* A Google account (free) for Search Console and Google Analytics[cite: 8]
* Access to your domain's DNS settings (to verify it with Google)[cite: 8]

**Accounts to Create (Free)**[cite: 8]
* **Google Search Console:** `search.google.com/search-console`[cite: 8]
* **Google Analytics 4:** `analytics.google.com` — Create a property and copy the Measurement ID (starts with `G-`)[cite: 8]
* **Optional:** Cloudflare Turnstile (free CAPTCHA), only if your forms get spam[cite: 8]

**Content Only You Can Give**[cite: 8]
* Real customer reviews, with each customer's permission to publish[cite: 8]
* 5–8 questions people actually ask you (for the FAQ)[cite: 8]
* One share image for your brand, 1200 x 630 px[cite: 8]
* Your business name and contact email (for the privacy policy)[cite: 8]

**Know Before You Start**[cite: 8]
* List what your site collects: forms, cookies, analytics, payment, or chat tools[cite: 8]. The privacy policy must match it[cite: 8].
* Do this on a test/preview version first, then publish[cite: 8].

---

## 02. The Launch Checklist[cite: 9]

*Seedhi baat: pandrah tick, phir launch.*[cite: 9]

### Google Can Find You (`Prompt A`)[cite: 9]
- [ ] **1. Custom 404 page:** Helpful "page not found" page that still returns a real 404 status[cite: 9]
- [ ] **2. A unique title on every page:** Short, descriptive, site name at the end[cite: 9]
- [ ] **3. A meta description on every page:** 1–2 plain sentences per page[cite: 9]
- [ ] **6. Internal links between pages:** Descriptive link text, no broken links[cite: 9]
- [ ] **7. Sitemap, submitted in Search Console:** Lists every public page[cite: 9]
- [ ] **8. `robots.txt` checked:** Points to the sitemap, no leftover `Disallow: /`[cite: 9]

### Looks Right When Shared (`Prompt B`)[cite: 9]
- [ ] **4. Share preview image:** Open Graph + Twitter card tags on every page[cite: 9]
- [ ] **5. Alt text on every image:** Specific descriptions; empty alt for decorative images[cite: 9]

### Forms, Tracking & Privacy (`Prompt C`)[cite: 9]
- [ ] **10. Spam protection on forms:** Honeypot + rate limit; CAPTCHA only if needed[cite: 9]
- [ ] **11. Thank-you page after a form:** Counted as a key event in Google Analytics[cite: 9]
- [ ] **12. Google Analytics 4:** With a consent banner for EU / UK / Swiss visitors[cite: 9]
- [ ] **13. Privacy policy:** Matches what your site really collects[cite: 9]

### Trust (`Prompt D`)[cite: 9]
- [ ] **9. HTTPS everywhere:** `http` redirects to `https`, no mixed-content warnings[cite: 9]
- [ ] **14. FAQ section:** For visitors; FAQ markup no longer gets special Google results[cite: 9]
- [ ] **15. Only real reviews:** Placeholders until you paste real ones; never AI-written[cite: 9]

---

## A. Get Found on Google (Items 1, 2, 3, 6, 7, 8)[cite: 10]

*Seedhi baat: Google ko pata chale tumhari website exist karti hai.*[cite: 10]

### The Prompt (Copy This)[cite: 10]

> Prepare my website for Google before launch[cite: 10]. Work page by page and show me your plan before editing[cite: 10].
> 1. Custom 404 page: create a helpful "page not found" page with a link back to the homepage and my main pages, in my site's design[cite: 10]. Make sure missing pages still return a real HTTP 404 status code, not 200[cite: 10]. Test it by requesting a made-up URL and show me the status code[cite: 10].
> 2. Page titles: give every page a unique, short, descriptive title that says what that page is about, with my site name at the end after a separator (for example "Pricing | Brand")[cite: 10]. No keyword stuffing[cite: 10].
> 3. Meta descriptions: write a unique 1-2 sentence description for every page that summarises it in plain words[cite: 10].
> 4. Internal links: make sure every important page is linked from at least one other page, using descriptive link text instead of "click here"[cite: 10]. Find and fix broken links[cite: 10].
> 5. Sitemap: generate `sitemap.xml` at the root of the site listing every public page[cite: 10]. Leave out admin, login, thank-you and test pages[cite: 10]. Keep it updated automatically when pages change[cite: 10].
> 6. `robots.txt`: create or fix it so it allows crawling of the public site and includes a line pointing to the sitemap[cite: 10]. Make sure it does NOT contain `"Disallow: /"` left over from development[cite: 10].
>
> At the end, show me a table of every page with its title and description so I can review them[cite: 10].

**Check It Worked**[cite: 10]
* Open `yourdomain.com/a-page-that-doesnt-exist`: you see your 404 page[cite: 10].
* Open `/sitemap.xml` and `/robots.txt`: both load[cite: 10].

**Careful**[cite: 10]
* One wrong line in `robots.txt` can hide your whole site from Google[cite: 10]. Read it before you launch[cite: 10].

---

## B. Share Previews & Images (Items 4, 5)[cite: 11]

*Seedhi baat: link share karo toh mast preview aaye.*[cite: 11]

When someone shares your link on WhatsApp, LinkedIn, or X, the preview card comes from Open Graph tags[cite: 11]. Without them, your link shows up as plain text[cite: 11]. Alt text describes images for Google and for people using screen readers[cite: 11].

### The Prompt (Copy This)[cite: 11]

> 1. Share previews: add Open Graph tags to every page: `og:title`, `og:description`, `og:type`, `og:url` and `og:image`, plus Twitter card tags with `twitter:card` set to `summary_large_image`[cite: 11]. Use one default share image for the whole site at 1200 x 630 px, and page-specific images where they make sense[cite: 11]. If I haven't given you an image, add a clearly named placeholder and tell me exactly which file to replace and at what size[cite: 11].
> 2. Alt text: go through every image on the site[cite: 11]. For meaningful images, write short, specific alt text describing what's actually in the image[cite: 11]. For purely decorative images, use an empty alt attribute (`alt=""`) so screen readers skip them[cite: 11]. Don't stuff keywords[cite: 11].
>
> Show me the full list of images with the alt text you plan to add before editing[cite: 11].

**Check It Worked**[cite: 11]
* Paste your link into a WhatsApp or LinkedIn message (don't send it): the preview card shows your image and title[cite: 11].

**Careful**[cite: 11]
* Apps cache previews[cite: 11]. If an old preview shows, wait a while or test with a new page link[cite: 11].

---

## C. Forms, Tracking & Privacy (Items 10, 11, 12, 13)[cite: 12]

*Seedhi baat: spam band, leads count, privacy sorted.*[cite: 12]

### The Prompt (Copy This)[cite: 12]

> 1. Spam protection: on every form, add a hidden honeypot field and basic rate limiting on the server, and validate every field on the server, not just in the browser[cite: 12]. Only if spam still gets through, add a free CAPTCHA such as Cloudflare Turnstile[cite: 12].
> 2. Thank-you page: after a successful form submission, send the visitor to a dedicated `/thank-you` page that confirms what happens next[cite: 12]. Keep it out of the sitemap and mark it `noindex`[cite: 12].
> 3. Google Analytics 4: add GA4 with my Measurement ID: `G-XXXXXXXXXX`[cite: 12]. For visitors in the EU, UK and Switzerland, load it only after they accept cookies through a simple consent banner[cite: 12]. Tell me how to mark the `/thank-you` page view as a key event so form submissions are counted[cite: 12].
> 4. Privacy policy: create a `/privacy` page and link it in the footer[cite: 12]. Base it only on what my site actually collects[cite: 12]. First list every form, cookie, analytics or third-party tool you find in my code, then write the policy from that list, including Google Analytics[cite: 12]. Mark it clearly as a template I must review[cite: 12].
>
> Show me your plan for all four before editing[cite: 12].

**Check It Worked**[cite: 12]
* Submit your form: you land on `/thank-you`[cite: 12].
* Open GA4 Realtime: your visit shows up[cite: 12].
* The footer links to `/privacy`[cite: 12].

**Careful**[cite: 12]
* An AI-written privacy policy is a template, not legal advice[cite: 12]. Check it matches your site before going live[cite: 12].

---

## D. Trust (Items 9, 14, 15)[cite: 13]

*Seedhi baat: visitor ko lage ye website asli hai.*[cite: 13]

### The Prompt (Copy This)[cite: 13]

> 1. HTTPS: make sure every page loads over `https`, `http` redirects to `https`, and there are no mixed-content warnings (no images, scripts or fonts loaded over `http`)[cite: 13]. Most hosts give free HTTPS automatically; just confirm it's on and fix anything still using `http`[cite: 13].
> 2. FAQ section: add an FAQ section where it fits best, with the questions I give you[cite: 13]. Draft the answers from what's already on my site, and mark anything you're unsure about for me to confirm[cite: 13]. Don't add FAQ schema expecting special Google results; Google no longer shows them[cite: 13].
> 3. Reviews: create a reviews/testimonials section with clearly marked placeholders only[cite: 13]. Do NOT write, invent or reword any review, name, rating or photo[cite: 13]. I will paste real reviews from real customers myself, with their permission[cite: 13]. Don't add review-star schema for reviews about my own business[cite: 13].
>
> Show me your plan before editing[cite: 13].

**Check It Worked**[cite: 13]
* Type `http://yourdomain.com`: it switches to `https`[cite: 13].
* The reviews section shows placeholders until you add real ones[cite: 13].

**Careful**[cite: 13]
* Fake or AI-written reviews are illegal in the US (FTC rule, 2024) and misleading everywhere[cite: 13]. Only publish real ones[cite: 13].

---

## + Master Prompt + After Launch[cite: 14]

*Seedhi baat: ek prompt, saari pandrah cheezein.*[cite: 14]

### The Prompt (Copy This)[cite: 14]

> I'm about to launch my website[cite: 14]. Add everything on my launch checklist in four rounds, showing me your plan before each round and how to check it after[cite: 14]:
>
> Round 1, Google: custom 404 page with a real 404 status, unique page titles, meta descriptions, internal links, `sitemap.xml`, and a `robots.txt` that points to the sitemap with no `"Disallow: /"`[cite: 14].
>
> Round 2, sharing: Open Graph + Twitter card tags with a 1200 x 630 share image, and specific alt text on every meaningful image (empty alt for decorative ones)[cite: 14].
>
> Round 3, forms and tracking: honeypot + rate limiting + server validation on forms, a `noindex` `/thank-you` page, GA4 (ID: `G-XXXXXXXXXX`) behind a consent banner for EU/UK/Swiss visitors, and a privacy policy based only on what the site actually collects[cite: 14].
>
> Round 4, trust: `https` everywhere with no mixed content, an FAQ section from my questions, and a reviews section with placeholders only[cite: 14]. Never invent reviews[cite: 14].

### After Launch: 4 Manual Steps[cite: 14]

1. **Search Console:** Add your domain and verify it (the DNS option is easiest)[cite: 14].
2. **Search Console – Sitemaps:** Submit `yourdomain.com/sitemap.xml`[cite: 14].
3. **Search Console – URL Inspection:** Inspect your homepage and request indexing[cite: 14].
4. **GA4 Realtime:** Open your site and check your visit appears[cite: 14].

---

## Ship Without Code[cite: 14]

**Build it. Fix it. Ship it. Without code.**[cite: 14]

Ship Without Code is a community for non-technical people building real websites and apps with AI[cite: 14].
* **Handle:** `@namansoni.ai`[cite: 14]