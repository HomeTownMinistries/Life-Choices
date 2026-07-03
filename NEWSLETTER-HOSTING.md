# Philippines Newsletter — Hosting Options

## Goal
Provide a direct link that opens the newsletter in-browser with no download, no extra clicks, and minimal third-party branding.

---

## Option 1: Host on Your Own Website (Recommended)

Upload the newsletter HTML file to **www.hometownministries.com** or **www.homemanager4u.com** in a dedicated folder.

### Benefits
- Clean, professional URL (e.g., `www.hometownministries.com/newsletter/philippines-2026-07/`)
- No Google toolbar or third-party branding
- Full control over appearance and analytics
- Stronger credibility for a major giving ask
- Can add your own header/footer, donation links, etc.

### How to Set It Up

**If your site runs WordPress:**
1. Install the "File Manager" plugin (or use your hosting panel's file manager)
2. Create a folder: `/newsletter/` under your site root
3. Upload the HTML file (e.g., `philippines-july-2026.html`)
4. Link becomes: `www.hometownministries.com/newsletter/philippines-july-2026.html`

**If you have cPanel/hosting panel access:**
1. Log in to your hosting control panel
2. Open File Manager → navigate to `public_html`
3. Create a `newsletter` folder
4. Upload your HTML file there
5. The file is immediately live at `yourdomain.com/newsletter/filename.html`

**If you use FTP:**
1. Connect with FileZilla or similar FTP client
2. Navigate to your site's root directory
3. Create a `newsletter` folder and upload the HTML file

### Tips
- Keep file names short and descriptive: `philippines-july-2026.html`
- Create an `index.html` in the `/newsletter/` folder that lists all past newsletters (optional archive page)
- Test the link on both desktop and mobile before sending

---

## Option 2: Google Drive (Current Approach)

Share the file via Google Drive with "Anyone with the link" access.

### Benefits
- No hosting setup required
- Free and familiar
- Works immediately

### Drawbacks
- Google toolbar/preview header appears at the top
- URL is long and not branded (can shorten with bit.ly or similar)
- Less professional for a giving ask
- Google can change the viewer interface without notice

### Improve the Google Drive Experience
- Use the `/preview` URL format instead of `/view` to reduce the toolbar:
  Replace `/view` at the end of your Drive link with `/preview`
- Create a short link using bit.ly or your domain's URL shortener

---

## Option 3: Free Static Hosting (Alternative)

If modifying your website isn't feasible, these free services host HTML files with clean URLs:

| Service         | URL Format                          | Setup Time | Notes                        |
|-----------------|-------------------------------------|------------|------------------------------|
| GitHub Pages    | yourname.github.io/newsletter/     | 15 min     | Free, reliable, version history |
| Netlify         | your-newsletter.netlify.app        | 10 min     | Drag-and-drop upload, free tier |
| Cloudflare Pages| your-newsletter.pages.dev          | 10 min     | Fast global delivery, free tier |

These give you a clean, branded-ish URL with no download prompts and no third-party viewer chrome.

---

## Recommendation

For a **major giving ask** like the Philippines newsletter, **host it on your own website** (Option 1). It looks more professional, builds trust, and keeps everything under your ministry's brand. The setup is a one-time effort — once the `/newsletter/` folder exists, future newsletters are just a file upload.

If you need something working **today** with zero setup, the Google Drive link is fine — just switch the URL to use `/preview` instead of `/view` to minimize the toolbar.
