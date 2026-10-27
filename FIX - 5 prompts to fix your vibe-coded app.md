# 5 Prompts to Fix Your Vibe-Coded App

Based on the provided document "FIX - 5 prompts to fix your vibe-coded app.pdf":

COMMENT "FIX" @NAMANSONI.AI[cite: 10]
Your app works, but it feels off[cite: 10]. These are the five problems almost every vibe-coded app has, plus one prompt each to fix them[cite: 10]. Copy, paste, review, ship[cite: 10]. They work in Claude Code, Cursor or Codex[cite: 10].
NO CODING NEEDED[cite: 10]

## HOW TO USE THIS

1. Open your project in Claude Code, Cursor or Codex[cite: 10].
2. Paste one prompt[cite: 10]. Never all five at once[cite: 10].
3. It shows you its plan first[cite: 10]. Read it, then reply "go ahead"[cite: 10].
4. Check it with the steps on that page, then move to the next fix[cite: 10].

## INSIDE

*   **01 Confusing icons**: clean bottom bar + menu (design)[cite: 10]
*   **02 Screen freezes after a tap**: optimistic UI (speed feel)[cite: 10]
*   **03 Pages load everything at once**: pagination (Load time)[cite: 10]
*   **04 Too many database calls**: fix N+1 queries (backend)[cite: 10]
*   **05 Users stuck waiting**: background jobs (backend)[cite: 10]
*   **+ Bonus**: the safety-net prompt to run after every fix (must do)[cite: 10]

---

## 01 Confusing icons

Seedhi baat: users ko samajh hi nahi aata kaunsa button kya karta hai[cite: 11].

AI loves filling the bottom bar with small icons[cite: 11]. You know what each one does because you built it; your users don't[cite: 11]. Tooltips don't help on phones, because there's no hover on a touch screen[cite: 11]. Keep only the obvious icons at the bottom and move everything else into a menu with clear text[cite: 11].

**THE PROMPT - COPY THIS**
> Audit the navigation and buttons on every screen of my app[cite: 11].
> 1. List every button that shows only an icon, with what it does[cite: 11].
> 2. Keep in the bottom navigation bar only the 3-5 most important actions whose icons everyone understands instantly (like home, search, add, profile)[cite: 11].
> 3. Move every other action into a menu that opens from a button in the top-left corner[cite: 11]. Inside the menu, show each item as an icon plus a clear text label[cite: 11].
> 4. Give every icon-only button a hidden accessible label (aria-label on web, accessibilityLabel in React Native) so screen readers can announce it[cite: 11]. Don't rely on tooltips or the title attribute; they don't work on touch screens[cite: 11].
> 5. Show me the full list of changes first[cite: 11]. Only edit after I approve, one screen at a time[cite: 11].

**CHECK IT WORKED**
*   Open the app on your phone: is every bottom icon obvious without explanation?[cite: 11]
*   Tap: does every item have readable text?[cite: 11]
*   Nothing important should be hidden more than one tap away[cite: 11].

**CAREFUL**
*   Don't bury your app's main action in the menu[cite: 11]. If users do it every day, it stays in the bottom bar[cite: 11].

---

## 02 Screen freezes after a tap

Seedhi baat: Save dabao aur screen ruki rehti hai[cite: 12].

Most AI-built apps wait for the server before updating the screen, so every tap feels slow[cite: 12]. Optimistic UI updates the screen instantly and saves in the background, which is why a like button turns red the moment you tap it[cite: 12]. If the save fails, the app undoes the change and shows an error[cite: 12].

**THE PROMPT - COPY THIS**
> Find every action in my app where the user taps something and has to wait for the server before the screen updates (saving, editing, toggling, liking, adding, removing or reordering items in a list)[cite: 12].
> For each one, add optimistic UI[cite: 12]:
> - update the screen immediately,[cite: 12]
> - send the request in the background,[cite: 12]
> - if the request fails, roll the screen back to how it was and show a clear error with a retry option[cite: 12].
> Use the data library my project already has if there is one (for example TanStack Query optimistic updates or React's useOptimistic)[cite: 12].
> Do NOT use optimistic updates for payments, permanently deleting data, or anything that can't be undone[cite: 12]. Keep a normal loading state for those[cite: 12].
> List the actions you plan to change before editing anything[cite: 12].

**CHECK IT WORKED**
*   Tap Save: the screen should change instantly, with no spinner[cite: 12].
*   Turn off your internet and tap again: the change should undo itself and show an error[cite: 12].

**CAREFUL**
*   Never on payments or deletes[cite: 12]. The screen would say "done" before the server agrees[cite: 12].
*   The rollback isn't optional[cite: 12]. Without it users see data that was never saved[cite: 12].

---

## 03 Pages load everything at once

Seedhi baat: page saara data ek saath utha raha hai[cite: 13].

With 10 test records your app feels fast[cite: 13]. With 10,000 real ones the same page crawls, because it loads every row at once[cite: 13]. Pagination loads a small page of data at a time, with "load more" or infinite scroll for the rest[cite: 13].

**THE PROMPT - COPY THIS**
> Find every screen and API endpoint in my app that loads a whole list of records at once[cite: 13].
> Add pagination[cite: 13]:
> - return results in pages of 20 (make the size easy to change),[cite: 13]
> - always sort by a stable, unique order (for example created date, then id) so items never repeat or go missing between pages,[cite: 13]
> - for large or fast-growing tables, use cursor-based (keyset) pagination instead of big OFFSET values, which get slow,[cite: 13]
> - on the screen, add "Load more" or infinite scroll with a loading indicator and an empty state[cite: 13].
> Keep existing search and filters working with the pagination[cite: 13].
> Show me which screens and endpoints you will change before editing[cite: 13].

**CHECK IT WORKED**
*   Open a long list: only the first page should load, quickly[cite: 13].
*   Scroll or tap "Load more": no duplicates, nothing skipped[cite: 13].
*   Search and filters still work[cite: 13].

**CAREFUL**
*   Without a stable sort order, items can repeat or vanish between pages[cite: 13]. That's why the prompt insists on one[cite: 13].

---

## 04 Too many database calls

Seedhi baat: har item ke liye database ko alag call[cite: 14].

This one is called an N+1 query[cite: 14]. Your app fetches a list (1 call), then makes one more call for every item in it (N calls)[cite: 14]. A list of 50 items means 51 trips to the database[cite: 14]. One join gets everything in a single trip, and it's one of the most common hidden slowdowns in AI-written backends[cite: 14].

**THE PROMPT - COPY THIS**
> Check my backend for N+1 database queries: places where the code fetches a list and then runs a separate query for each item, often inside a loop[cite: 14].
> 1. Turn on query logging (or count queries) for my main screens and report how many database queries each one runs[cite: 14].
> 2. Fix every N+1 by loading the related data in one go with a join or eager loading in my ORM (for example Prisma include, Django select_related / prefetch_related, or Supabase nested selects)[cite: 14].
> 3. Add database indexes on the columns used for these lookups if they are missing[cite: 14].
> 4. Show me the query count for each screen before and after the fix[cite: 14].
> Explain the plan before making changes[cite: 14].

**CHECK IT WORKED**
*   The before/after table should show far fewer queries per screen[cite: 14].
*   Every list should show exactly the same data as before[cite: 14].

**CAREFUL**
*   This touches how your data is fetched[cite: 14]. Run the safety-net prompt (last page) before and after[cite: 14].

---

## 05 Users stuck waiting

Seedhi baat: heavy kaam chal raha hai aur user ruka hua hai[cite: 15].

Sending emails, calling AI, processing files or images: when your app does these while the user waits, the whole app feels broken[cite: 15]. Background jobs move that heavy work behind the scenes[cite: 15]. The user gets a "we're on it" message and keeps using the app while it finishes[cite: 15].

**THE PROMPT - COPY THIS**
> Find slow tasks that make the user wait during a request, such as sending emails, calling AI APIs, generating or processing files, images or video, and calling other services through webhooks[cite: 15].
> Move each one into a background job[cite: 15]:
> - the request should return quickly so the user can keep using the app,[cite: 15]
> - show a status like "Processing... we'll let you know when it's ready" and update it when the job finishes,[cite: 15]
> - retry failed jobs automatically and log the errors[cite: 15].
> Use a proper job queue that works with my hosting setup (for example BullMQ with Redis on a Node server, or the background-job / queue feature my host or database provides)[cite: 15]. Do not use fire-and-forget code inside the request[cite: 15].
> Keep normal reads and saves that the user needs to see immediately exactly as they are[cite: 15].
> Before editing, tell me which queue option you recommend for my project and whether it costs anything[cite: 15].

**CHECK IT WORKED**
*   Trigger the heavy action: the app should respond within a second and show a status[cite: 15].
*   The result should arrive a bit later, and the status should update[cite: 15].

**CAREFUL**
*   Only heavy work goes to the background[cite: 15]. Normal saves stay instant[cite: 15].
*   A queue can need extra services (like Redis)[cite: 15]. Check the cost first[cite: 15].

---

## + The safety-net prompt

Seedhi baat: har fix ke pehle aur baad, ye ek prompt zaroor chalana[cite: 16].

Fixes 3, 4 and 5 change how your app loads and saves data[cite: 16]. This prompt makes the AI prove nothing broke and gives you a clean way to undo any single fix[cite: 16].

**COPY THIS**
> Before you change anything, write tests for the screens and endpoints you are about to touch and run them so we know they pass today[cite: 16].
> After the change:
> 1. run the tests again and show me the results,[cite: 16]
> 2. tell me exactly how to check the fix myself in the browser or on my phone: what to click and what I should see,[cite: 16]
> 3. commit this fix on its own with a clear message so I can undo just this change if needed[cite: 16].

**SHIP WITHOUT CODE**
Build it[cite: 16]. Fix it[cite: 16]. Ship it[cite: 16]. Without code[cite: 16].
Ship Without Code is my community for non-technical people building real websites and apps with AI[cite: 16].
JOIN NOW LINK IN BIO @NAMANSONI.AI[cite: 16]