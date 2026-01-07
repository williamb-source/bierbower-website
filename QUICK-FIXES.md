# Quick Fixes Implementation Guide

This document provides copy-paste ready code for immediate fixes to bierbower.net.

---

## 1. Security Fixes

### Fix Mixed Content (HTTP to HTTPS)

**Before:**
```html
<img src="http://bierbower.net/pics/bierbowerlogo.png">
```

**After:**
```html
<img src="https://bierbower.net/pics/bierbowerlogo.png">
```

Apply to all image sources:
- `https://bierbower.net/pics/bierbowerlogo.png`
- `https://bierbower.net/pics/H2Ologo.jpg`
- `https://bierbower.net/pics/fishmaster.png`
- `https://bierbower.net/pics/monster-towers01.jpg`
- `https://bierbower.net/pics/easy-awn-logo-240px.png`

### Add Security Headers (Server Configuration)

**For Apache (.htaccess):**
```apache
Header always set X-Content-Type-Options "nosniff"
Header always set X-Frame-Options "SAMEORIGIN"
Header always set X-XSS-Protection "1; mode=block"
Header always set Referrer-Policy "strict-origin-when-cross-origin"
```

**For Nginx:**
```nginx
add_header X-Content-Type-Options "nosniff" always;
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
```

### Force HTTPS Redirect

**For Apache (.htaccess):**
```apache
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

**For Nginx:**
```nginx
server {
    listen 80;
    server_name bierbower.net www.bierbower.net;
    return 301 https://$server_name$request_uri;
}
```

---

## 2. Functionality Fixes

### Complete HTML Head Section

Replace the current head (or add if missing):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <title>Bierbower Enterprises, LLC | Innovation in Marine and Fabric Products</title>
    <meta name="description" content="Bierbower Enterprises, LLC - Innovation in Marine and Fabric Products. Home of H2O Marine, Fishmaster, Monster Tower, and Easy Awn brands.">

    <!-- Open Graph for Social Sharing -->
    <meta property="og:title" content="Bierbower Enterprises, LLC">
    <meta property="og:description" content="Innovation in Marine and Fabric Products">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://www.bierbower.net">
    <meta property="og:image" content="https://bierbower.net/pics/bierbowerlogo.png">

    <!-- Favicon -->
    <link rel="icon" type="image/x-icon" href="/favicon.ico">
    <link rel="apple-touch-icon" href="/apple-touch-icon.png">

    <!-- Basic Responsive Styles -->
    <style>
        * {
            box-sizing: border-box;
        }
        body {
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            line-height: 1.6;
        }
        img {
            max-width: 100%;
            height: auto;
        }
    </style>
</head>
```

---

## 3. Legibility/Accessibility Fixes

### Add Alt Text to All Images

```html
<!-- Logo -->
<img src="https://bierbower.net/pics/bierbowerlogo.png"
     alt="Bierbower Enterprises LLC Logo">

<!-- Brand Links with Proper Alt Text -->
<a href="https://h2omarine.com">
    <img src="https://bierbower.net/pics/H2Ologo.jpg"
         alt="H2O Marine - Marine Products">
</a>

<a href="https://fishmaster.com">
    <img src="https://bierbower.net/pics/fishmaster.png"
         alt="Fishmaster - Fishing Equipment">
</a>

<a href="https://monstertower.com">
    <img src="https://bierbower.net/pics/monster-towers01.jpg"
         alt="Monster Tower - Boat Towers">
</a>

<a href="https://easyawn.com">
    <img src="https://bierbower.net/pics/easy-awn-logo-240px.png"
         alt="Easy Awn - Awning Products">
</a>
```

### Add Semantic HTML Structure

```html
<body>
    <header>
        <img src="https://bierbower.net/pics/bierbowerlogo.png"
             alt="Bierbower Enterprises LLC Logo">
        <h1>Bierbower Enterprises, LLC</h1>
        <p>Innovation in Marine and Fabric Products</p>
        <address>Cumming, GA</address>
    </header>

    <main>
        <h2>Our Brands</h2>
        <nav aria-label="Brand links">
            <ul>
                <li>
                    <a href="https://h2omarine.com">
                        <img src="https://bierbower.net/pics/H2Ologo.jpg"
                             alt="H2O Marine">
                        <span>H2O Marine</span>
                    </a>
                </li>
                <!-- Repeat for other brands -->
            </ul>
        </nav>
    </main>

    <footer>
        <p>&copy; 2026 Bierbower Enterprises, LLC. All rights reserved.</p>
    </footer>
</body>
```

### Add Skip Navigation Link

Add as first element inside `<body>`:

```html
<a href="#main-content" class="skip-link">Skip to main content</a>

<style>
.skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background: #000;
    color: #fff;
    padding: 8px;
    z-index: 100;
}
.skip-link:focus {
    top: 0;
}
</style>
```

---

## 4. Complete Minimal Fixed Page

Here's a complete, minimal HTML page with all quick fixes applied:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bierbower Enterprises, LLC | Innovation in Marine and Fabric Products</title>
    <meta name="description" content="Bierbower Enterprises - Innovation in Marine and Fabric Products. Home of H2O Marine, Fishmaster, Monster Tower, and Easy Awn.">
    <link rel="icon" href="/favicon.ico">
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            line-height: 1.6;
            color: #333;
            text-align: center;
            padding: 20px;
        }
        .skip-link {
            position: absolute;
            top: -40px;
            left: 0;
            background: #000;
            color: #fff;
            padding: 8px;
        }
        .skip-link:focus { top: 0; }
        header { padding: 40px 20px; }
        header img { max-width: 300px; }
        h1 { margin: 20px 0 10px; font-size: 1.5rem; }
        .tagline { color: #666; margin-bottom: 5px; }
        address { font-style: normal; color: #888; }
        main { padding: 40px 20px; }
        h2 { margin-bottom: 30px; }
        .brands {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 30px;
            list-style: none;
            max-width: 800px;
            margin: 0 auto;
        }
        .brands li { flex: 1 1 200px; max-width: 250px; }
        .brands a {
            display: block;
            padding: 20px;
            text-decoration: none;
            color: inherit;
            border-radius: 8px;
            transition: box-shadow 0.2s;
        }
        .brands a:hover, .brands a:focus {
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            outline: none;
        }
        .brands img { max-width: 100%; height: auto; max-height: 80px; object-fit: contain; }
        .brands span { display: block; margin-top: 10px; font-weight: 500; }
        footer {
            margin-top: 60px;
            padding: 20px;
            border-top: 1px solid #eee;
            color: #888;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>
    <a href="#main" class="skip-link">Skip to main content</a>

    <header>
        <img src="https://bierbower.net/pics/bierbowerlogo.png"
             alt="Bierbower Enterprises LLC Logo">
        <h1>Bierbower Enterprises, LLC</h1>
        <p class="tagline">Innovation in Marine and Fabric Products</p>
        <address>Cumming, GA</address>
    </header>

    <main id="main">
        <h2>Our Brands</h2>
        <ul class="brands">
            <li>
                <a href="https://h2omarine.com">
                    <img src="https://bierbower.net/pics/H2Ologo.jpg" alt="H2O Marine logo">
                    <span>H2O Marine</span>
                </a>
            </li>
            <li>
                <a href="https://fishmaster.com">
                    <img src="https://bierbower.net/pics/fishmaster.png" alt="Fishmaster logo">
                    <span>Fishmaster</span>
                </a>
            </li>
            <li>
                <a href="https://monstertower.com">
                    <img src="https://bierbower.net/pics/monster-towers01.jpg" alt="Monster Tower logo">
                    <span>Monster Tower</span>
                </a>
            </li>
            <li>
                <a href="https://easyawn.com">
                    <img src="https://bierbower.net/pics/easy-awn-logo-240px.png" alt="Easy Awn logo">
                    <span>Easy Awn</span>
                </a>
            </li>
        </ul>
    </main>

    <footer>
        <p>&copy; 2026 Bierbower Enterprises, LLC. All rights reserved.</p>
    </footer>
</body>
</html>
```

---

## Implementation Priority

| Priority | Fix | Time to Implement |
|----------|-----|-------------------|
| 1 | Change HTTP to HTTPS in image URLs | 5 minutes |
| 2 | Add DOCTYPE and meta tags | 10 minutes |
| 3 | Add alt text to images | 10 minutes |
| 4 | Add semantic HTML structure | 30 minutes |
| 5 | Configure HTTPS redirect on server | 15 minutes |
| 6 | Add security headers | 15 minutes |
| 7 | Replace with complete fixed page | 1 hour |
