# Obrador Túria — shop website

The shop page, plus a small server that emails you every completed order form.

```
public/index.html   the shop (English + Spanish)
server.js           serves the page and emails each order to you
package.json        tells Render what to install
```

## 1. Get an email key from Resend (5 min)

Render's free plan blocks normal email sending, so orders are emailed through Resend instead.

1. Sign up at **resend.com** using **davepreston@gmx.de**. This must be the same address the orders go to.
2. Go to **API Keys → Create API Key**, give it a name (e.g. "shop") and copy the key. It starts with `re_`.

Until you verify your own domain, Resend can only send to the email you signed up with. That's all this shop needs.

## 2. Put the files on GitHub

1. Go to **github.com → New repository**, name it `obrador-turia`, and click **Create repository**.
2. Click **uploading an existing file**, drag in everything from this folder (`public`, `server.js`, `package.json`, `package-lock.json`, `.gitignore`, `README.md`), then click **Commit changes**.
   Don't upload a `node_modules` folder if you have one.

## 3. Create the web service on Render

1. Go to **dashboard.render.com → New → Web Service** and connect your GitHub account.
2. Pick the `obrador-turia` repository and fill in:

   | Setting | Value |
   |---|---|
   | Language | Node |
   | Build Command | `npm install` |
   | Start Command | `node server.js` |
   | Instance Type | Free |

3. Under **Environment Variables**, add:

   | Key | Value |
   |---|---|
   | `RESEND_API_KEY` | the `re_…` key from step 1 |
   | `ORDER_EMAIL` | `davepreston@gmx.de` |

4. Click **Deploy Web Service**. After a few minutes your shop is live at `https://obrador-turia.onrender.com` (or similar).

## 4. Test it

Place an order on the live site. The email arrives from `onboarding@resend.dev` with the subject
"New order OT-… · name · total". **Check your GMX spam folder the first time** and mark it as "not spam".

If the customer entered an email address, you can just press Reply to answer them.

## Good to know

- **Free plan sleep:** a free Render service sleeps after 15 minutes without visitors. The next visitor waits about a minute for it to wake up. A paid Render instance stays awake.
- **Changing the site:** edit the files on GitHub (or upload new ones). Render redeploys automatically on every change.
- **Checking it's working:** visit `/healthz` on your site. `"email": true` means both keys are set.
- **Logs:** in Render, open the service and click **Logs**. Every order shows up as "Order OT-… emailed to shop".
- **Prices** are in both `public/index.html` and `server.js`. If you change a price, change it in both files. The email always uses the prices in `server.js`.
