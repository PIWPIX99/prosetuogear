# NexusGear Store — Coolify Deployment Guide

## ══ OPTION A: HTML Store Only (fastest, 2 minutes) ══

### What you need
- A GitHub account (free)
- Coolify running on a server

### Steps

1. **Create a GitHub repository**
   - Go to github.com → New repository
   - Name it: `nexusgear-store`
   - Set to Public

2. **Upload these 2 files to the repo**
   - `index.html`  (your store file)
   - `Dockerfile`  (included in this folder)

3. **In Coolify dashboard**
   - Click: New Resource → Application → Public Repository
   - Paste your GitHub repo URL
   - Build Pack: select **Dockerfile**
   - Click: **Deploy**

4. **Get your URL**
   - Coolify gives you a URL like: `https://abc123.yourdomain.com`
   - Your store is live! ✓

### ⚠️ Limitation
This option has NO WordPress admin panel.
Products are hardcoded in the HTML file.
To change products, edit index.html and push to GitHub.

---

## ══ OPTION B: Full WordPress + Plugin (recommended) ══

### What you need
- Coolify running on a server
- The nexusgear-store-v3.zip plugin file

### Steps

1. **In Coolify dashboard**
   - Click: New Resource → Docker Compose
   - Paste the contents of `docker-compose.yml`
   - ⚠️ IMPORTANT: Change these 2 passwords before deploying:
     ```
     MYSQL_PASSWORD:      CHANGE_THIS_PASSWORD_123
     MYSQL_ROOT_PASSWORD: CHANGE_ROOT_PASSWORD_456
     ```

2. **Add your domain**
   - In Coolify → your resource → Domains
   - Add your domain or use the auto-generated one

3. **Click Deploy**
   - Wait ~2 minutes for WordPress + MySQL to start
   - Status should show: Running ✓

4. **Finish WordPress setup**
   - Go to: `https://yourdomain.com/wp-admin`
   - Complete the WordPress 5-step setup wizard
   - Create your admin username & password

5. **Install the NexusGear plugin**
   - WP Admin → Plugins → Add New → Upload Plugin
   - Upload: `nexusgear-store-v3.zip`
   - Click Install Now → Activate

6. **Create your store page**
   - WP Admin → Pages → Add New
   - Title: "Store" (or any name)
   - Add a Shortcode block → type: `[nexusgear_store]`
   - Click Publish

7. **Open the Live Customizer**
   - WP Admin → NexusGear → Customizer
   - Change store name, icon, colors, sections
   - Click Save

8. **Fix REST API (if store shows blank)**
   - WP Admin → Settings → Permalinks
   - Select "Post name"
   - Click Save Changes
   This resets .htaccess and fixes the REST API.

---

## ══ TROUBLESHOOTING ══

| Problem | Fix |
|---------|-----|
| Store page shows loading forever | WP Settings → Permalinks → Save |
| Can't upload plugin (file too large) | Make sure uploads.ini is in same folder as docker-compose.yml |
| 502 Bad Gateway | Wait 1-2 min for MySQL to fully start, then refresh |
| White screen in WordPress | Check Coolify logs for the wordpress container |
| SSL not working | Coolify → your resource → enable SSL (Let's Encrypt) |

---

## ══ PASSWORDS TO CHANGE ══

In docker-compose.yml, find and replace:
- `CHANGE_THIS_PASSWORD_123` → your strong database password
- `CHANGE_ROOT_PASSWORD_456` → your strong root password

Use a password generator: passwordgenerator.net
