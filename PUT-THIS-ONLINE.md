# Sonic Brands — putting it online

Two files. Ten minutes. The same route we used for Sonic Legacy, so if
anything here feels familiar it is because it is.

The address this is built for: **brands.sonicrewrite.com**
If you want a different one, say so before you start — it is written into
three places and I will change all three for you.

---

## What you have

| File | What it is |
|---|---|
| `index.html` | The whole website. One file, 764 KB. All the album covers are baked inside it, so nothing on the page depends on Google Drive or any other server staying up. |
| `CNAME` | One line of text: `brands.sonicrewrite.com`. This is how GitHub knows which address to answer on. |

---

## Step 1 — Make the repository

1. Go to **github.com** and sign in.
2. Top right, the **+** button, then **New repository**.
3. Repository name: **`brands`**
4. Set it to **Public**. (Private repositories cannot host a free site.)
5. Do **not** tick "Add a README file".
6. Click **Create repository**.

## Step 2 — Put the two files in it

1. On the empty repository page, click **uploading an existing file**.
2. Drag **both** `index.html` and `CNAME` into the box.
3. At the bottom, click **Commit changes**.

## Step 3 — Turn the website on

1. In the repository, click **Settings** (top row).
2. Left sidebar, click **Pages**.
3. Under "Build and deployment", Source should say **Deploy from a branch**.
4. Branch: choose **main**, folder **/ (root)**. Click **Save**.
5. Under "Custom domain" it should already say `brands.sonicrewrite.com`,
   picked up from the CNAME file. If it is empty, type it in and click Save.

GitHub will now say it is checking the DNS. It will fail, because we have
not done step 4 yet. That is expected.

## Step 4 — Point the address at GitHub

This is in **Squarespace**, where sonicrewrite.com lives.

1. Squarespace → **Settings** → **Domains** → **sonicrewrite.com** → **DNS Settings**.
2. **Add record**, with exactly these values:

   - Type: **CNAME**
   - Host / Name: **brands**
   - Data / Value: **sonicrewrite.github.io**
   - TTL: leave the default

   (Note: `sonicrewrite.github.io`, with no `https://` and no trailing slash.
   Squarespace may add a dot on the end by itself. That is fine.)

3. Save.

## Step 5 — Wait, then force GitHub to look again

DNS takes anywhere from ten minutes to four hours. Have a coffee.

Then, in **Settings → Pages**, if it still shows an error:

1. **Delete** the custom domain from the box and click Save.
2. Type `brands.sonicrewrite.com` back in and click Save.

That forces a fresh lookup instead of GitHub reusing its cached answer.
This is the exact step that fixed Sonic Legacy when it looked stuck.

## Step 6 — Turn on HTTPS

Once the green tick appears, the **Enforce HTTPS** checkbox becomes
available. Tick it. It can take another hour before it is tickable.

Done. The site is live at **https://brands.sonicrewrite.com**

---

## If something looks wrong

**"Domain does not resolve to the GitHub Pages server"**
The DNS record has not spread yet, or GitHub is showing you a cached check.
Do step 5 again. If it persists after four hours, send me a screenshot and
I will query the nameservers directly and tell you what is actually there,
rather than guessing from the error message.

**The page loads but has no styling**
The file did not upload completely. Delete `index.html` in GitHub and
upload it again.

**A player shows a grey box**
That is SoundCloud being slow, or a network that blocks it. Reload.

---

## When you want to change something

Do not edit the file in GitHub. Tell me what you want changed, I will
rebuild it and send you a new `index.html`. In GitHub you then click the
old `index.html`, the pencil icon, delete everything, paste the new
content, and commit — or simply upload the new file and let it overwrite.

The page is generated from source files I keep, so hand-edits in GitHub
would be silently lost the next time I rebuild it.

---

## What the form does, tested end to end on 2 September 2026

Someone fills it in →
→ the browser posts to a Make webhook
→ Make writes a row in **Enquiries**, in Vanessa's Airtable base, with the
  albums they ticked, the number the page showed them, and their company,
  job title and website
→ Make emails **vanessa@sonicrewrite.com** with the same information

I ran a live test through the whole chain. Both ends confirmed. The test
row is in Enquiries, labelled `TEST — Vera, Sonic Brands wiring`, and it
stays there as proof.
