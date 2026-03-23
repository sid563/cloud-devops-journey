# Project 02 — S3 Static Website + CloudFront CDN

**Goal:** Host a static website on S3 and serve it globally through CloudFront.

**Status:** ✅ Complete

---

## What Was Built

- S3 bucket with static website hosting enabled
- Static HTML page uploaded and made publicly accessible
- CloudFront distribution pointing to the S3 website as origin

---

## Architecture

```
User
 │
 ├─ Direct S3 (slow, no HTTPS, single region)
 │   └─ http://static-website-sid-test.s3-website.ap-south-1.amazonaws.com/
 │
 └─ CloudFront CDN (fast, HTTPS, global edge locations)
     └─ https://d2tmw3rbftddol.cloudfront.net/
```

---

## Key Concepts

**S3 static website hosting** — S3 can serve files directly over HTTP. You enable it in bucket settings and set an index document (e.g. `index.html`). The bucket must have public read access.

Limitations of S3 direct:
- HTTP only (no HTTPS)
- Single region — users far from `ap-south-1` get higher latency
- No caching

**CloudFront** is AWS's CDN (Content Delivery Network). It caches your content at ~450+ edge locations worldwide. Users get served from the nearest edge, not from your S3 bucket directly.

Benefits of CloudFront in front of S3:
- HTTPS out of the box
- Much lower latency globally
- Caching reduces S3 requests (cheaper)
- Can later attach a custom domain + SSL certificate via ACM

---

## What I Observed

- S3 URL is HTTP only, sluggish, region-locked (`ap-south-1`)
- CloudFront URL is HTTPS, served from nearest edge location
- Both serve the same content — CloudFront just does it better

---

## Real World Usage

This pattern is standard for:
- Frontend React/Next.js apps (build output uploaded to S3, served via CloudFront)
- Documentation sites
- Any static assets (images, JS bundles, CSS)

In production you'd add:
- Custom domain via Route 53
- SSL certificate via ACM (free)
- CloudFront cache invalidation in CI/CD pipeline on each deploy

---

## Cleanup Note

S3 storage is nearly free at this scale. CloudFront has a free tier (1TB data transfer/month).
Leave running or delete the bucket + distribution when done experimenting.
