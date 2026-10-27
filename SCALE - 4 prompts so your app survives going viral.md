# SCALE: 4 Prompts So Your App Survives Going Viral[cite: 1]

**Author:** `@namansoni.ai` — Ship Without Code *(No Coding Needed)*[cite: 1]

The day your app finally takes off is the day it's most likely to crash[cite: 1]. These four prompts find and fix the weak spots before real users do[cite: 1]. Copy, paste, review, ship[cite: 1]. They work in Claude Code, Cursor, or Codex[cite: 1].

---

## How to Use This[cite: 1]

1. Open your project in Claude Code, Cursor, or Codex[cite: 1].
2. Paste one prompt at a time, in order: 01–04[cite: 1].
3. It shows you its plan first[cite: 1]. Read it, then reply "go ahead"[cite: 1].
4. Run the safety-net prompt (last page) around every fix[cite: 1].

## Inside[cite: 1]

| # | Topic | Goal | Category |
| :--- | :--- | :--- | :--- |
| **01** | **Database indexes** | The app stays fast as data grows[cite: 1] | `database`[cite: 1] |
| **02** | **Caching** | Stop rebuilding the same thing for every user[cite: 1] | `speed`[cite: 1] |
| **03** | **Load testing** | Find the breaking point before users do[cite: 1] | `testing`[cite: 1] |
| **04** | **Scale on your host, not Kubernetes** | Scale on your current host[cite: 1] | `hosting`[cite: 1] |
| **+** | **Bonus** | The safety-net prompt to run around every fix[cite: 1] | `must do`[cite: 1] |

---

## 01. Database Indexes[cite: 2]

*Seedhi baat: data badhega toh app slow hoga[cite: 2]. Indexes isko rokte hain[cite: 2].*

Without an index, your database reads every single row to find what it needs[cite: 2]. With 100 rows nobody notices; with a million, every screen crawls[cite: 2]. An index works like the index at the back of a book: the database jumps straight to the right page[cite: 2]. AI-written apps often ship without the indexes their queries need[cite: 2].

### The Prompt (Copy This)[cite: 2]

> Make my database ready for a lot more data and users without changing how my app behaves[cite: 2].
> 1. Find the queries my app runs most often and the slowest ones[cite: 2]. If my database is Postgres and the `pg_stat_statements` view is available, use it[cite: 2]. Otherwise read my code and list every query my main screens run[cite: 2].
> 2. For each important read query, run `EXPLAIN ANALYZE` and tell me in plain words whether it scans the whole table[cite: 2]. Only do this on read queries, never on queries that change data[cite: 2].
> 3. Add indexes only on the columns those queries use in `WHERE`, `JOIN` and `ORDER BY`, including multi-column indexes where a query filters on several columns together[cite: 2]. For each index, tell me which query it speeds up[cite: 2].
> 4. Don't add indexes "just in case": every index slows down saving data[cite: 2]. Also list any existing indexes that are never used[cite: 2].
> 5. Put every change in a migration file so it can be reviewed and undone[cite: 2]. On large tables that already have live users, create indexes with `CREATE INDEX CONCURRENTLY` so saving data isn't blocked[cite: 2].
> 6. Show me each query's time before and after[cite: 2].

**Check It Worked**[cite: 2]
* The before/after table shows the slow queries got faster[cite: 2].
* Every screen still shows exactly the same data[cite: 2].

**Careful**[cite: 2]
* More indexes ≠ better[cite: 2]. Unused ones only slow down saving[cite: 2].
* Try it on a test copy of your database before your live one[cite: 2].

---

## 02. Caching[cite: 3]

*Seedhi baat: jo cheez sabke liye same hai, usko baar baar mat banao[cite: 3].*

Most screens show the same thing to lots of people[cite: 3]. Without caching, your app rebuilds it from scratch for every visitor and hits the database every single time[cite: 3]. Caching saves the result once and serves it instantly to everyone after, until it expires or the data changes[cite: 3].

### The Prompt (Copy This)[cite: 3]

> Find places where my app does the same expensive work again and again for every visitor: database queries, API calls, AI calls or calculations whose result rarely changes[cite: 3].
>
> Add caching, starting with the simplest option that fits my stack[cite: 3]:
> 1. First use what my framework and host already give me, like HTTP cache headers and CDN caching for public pages and responses, or my framework's built-in data cache[cite: 3].
> 2. Only if that isn't enough, add a shared cache like Redis using the cache-aside pattern: check the cache first, fall back to the database on a miss, then store the result with an expiry time (TTL)[cite: 3].
> 3. For every cached item, decide how long it can safely be out of date and set the TTL to match[cite: 3]. Clear or update the cache whenever the underlying data changes[cite: 3].
> 4. Never cache private or per-user data under a shared key[cite: 3]. Anything user-specific must include the user's ID in the cache key, or not be cached at all[cite: 3].
>
> Before editing, list what you'll cache, where, the TTL for each, and whether it adds any cost (for example a managed Redis service)[cite: 3].

**Check It Worked**[cite: 3]
* Open a screen twice: the second load is noticeably faster[cite: 3].
* Change some data: the screen updates within the TTL[cite: 3].
* Log in as two different users: each sees only their own data[cite: 3].

**Careful**[cite: 3]
* A shared cache key on private data can show one user's data to another[cite: 3]. That's why point 4 is in the prompt[cite: 3].

---

## 03. Load Testing[cite: 4]

*Seedhi baat: users se pehle tum khud apne app ko todo[cite: 4].*

Your app feels fast because you're its only user[cite: 4]. A load test sends hundreds of fake users at it, so you find the breaking point in testing instead of on launch day[cite: 4]. The AI writes the test, runs it and explains the results, using k6, a free, open-source load-testing tool[cite: 4].

### The Prompt (Copy This)[cite: 4]

> Write a k6 load test for my app so I can find its breaking point before real users do[cite: 4].
> 1. Pick the 3-5 most important things users do in my app (for example opening the main screen, logging in, loading a list, saving something) and script them as realistic requests with short pauses between steps[cite: 4].
> 2. Use k6 stages to ramp virtual users up gradually (for example 0 → 20 → 50 → 100), hold each level for a few minutes, then ramp down[cite: 4].
> 3. Add thresholds so the result is clear: `http_req_duration` p(95) under 500 ms and `http_req_failed` rate under 1%[cite: 4].
> 4. Point the test ONLY at my local or staging environment, never production[cite: 4]. Skip or mock any third-party services that cost money per call (payments, email, AI APIs)[cite: 4].
> 5. If you can run commands, install k6 if it's missing, start my app locally if needed, and run the test yourself[cite: 4]. If you can't, give me the exact install and run commands[cite: 4].
> 6. Explain the results in plain words: at how many users does my app start slowing down or failing, and which part breaks first[cite: 4]? Then suggest the top fixes[cite: 4].

**If You Need to Install k6 Yourself**[cite: 4]
* **Windows:** `winget install k6 --source winget`[cite: 4]
* **Mac:** `brew install k6`[cite: 4]
* **Run:** `k6 run script.js`[cite: 4]

**Careful**[cite: 4]
* Never load-test your live app or other companies' APIs[cite: 4]. It can crash it for real users or run up a bill[cite: 4].
* Use a test database with fake data[cite: 4].

---

## 04. Scale on Your Host, Not Kubernetes[cite: 5]

*Seedhi baat: Kubernetes nahi chahiye, database sambhalo[cite: 5].*

Hosts like Vercel already scale your server code automatically[cite: 5]. What usually breaks first is the database: too many connections, slow queries, plan limits[cite: 5]. Fix those before anyone tells you that you need Kubernetes, which is costly and hard to run without a DevOps team[cite: 5].

### The Prompt (Copy This)[cite: 5]

> Check if my app is ready to handle 10x more traffic on its current hosting, without moving to Kubernetes, AWS ECS or any new infrastructure[cite: 5].
> 1. Tell me where my app is hosted, what that host already scales automatically, and the limits of my current plan: concurrency, function timeouts, bandwidth, database connections and storage[cite: 5].
> 2. Make sure my app is stateless: no login sessions, uploaded files or important data kept in server memory or on the server's local disk[cite: 5]. Move them to the database or file storage if needed[cite: 5].
> 3. Check how my app connects to the database[cite: 5]. If it runs on serverless functions, make sure it uses a connection pooler (for example Supabase's transaction pooler on port 6543, or my provider's equivalent) and configure my database client the way the pooler needs, like turning off prepared statements in transaction mode[cite: 5].
> 4. List the 3 things most likely to break first when traffic jumps 10x, with the fix and the monthly cost of each[cite: 5].
> 5. Only recommend Kubernetes or ECS if the numbers clearly show my host can't handle the load, and explain why[cite: 5].

**Check It Worked**[cite: 5]
* You get a clear list: plan limits, what breaks first, what each fix costs[cite: 5].
* Run the load test (03) again: the breaking point should be higher[cite: 5].

**Careful**[cite: 5]
* Upgrading a plan costs money[cite: 5]. Compare the costs it lists before you click upgrade[cite: 5].
* Don't switch hosting in the middle of a launch[cite: 5].

---

## + The Safety-Net Prompt[cite: 6]

*Seedhi baat: har fix ke pehle aur baad, ye ek prompt zaroor chalana[cite: 6].*

All four fixes touch your database or hosting[cite: 6]. This prompt makes the AI prove nothing broke and gives you a clean way to undo any single fix[cite: 6].

### The Prompt (Copy This)[cite: 6]

> Before you change anything, write tests for the screens and endpoints you are about to touch and run them so we know they pass today[cite: 6].
>
> After the change[cite: 6]:
> 1. run the tests again and show me the results[cite: 6],
> 2. tell me exactly how to check the fix myself in the browser or on my phone: what to click and what I should see[cite: 6],
> 3. commit this fix on its own with a clear message so I can undo just this change if needed[cite: 6].

---

## Ship Without Code[cite: 6]

**Build it. Fix it. Ship it. Without code.**[cite: 6]

Ship Without Code is a community for non-technical people building real websites and apps with AI[cite: 6].
* **Handle:** `@namansoni.ai`[cite: 6]