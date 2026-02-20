---
title: File Upload Guide — Active Storage
type: doc
status: current
linked-repo: https://github.com/kanya01/COLABS
linked-pr: ""
linked-issue: ""
tags: [services, files, active-storage, uploads]
updated: 2026-02-20
---

# File Upload Guide — Active Storage

> Source: [docs/services/FILE_UPLOAD_GUIDE.md](https://github.com/kanya01/COLABS/blob/main/docs/services/FILE_UPLOAD_GUIDE.md)

Reference for file handling in live.o using Rails Active Storage.

---

## What Uses File Uploads

- **Order deliverables** — sellers upload completed work files; buyers download them
- **Portfolio items** — audio and image files on user profiles
- **User avatars** — profile pictures

---

## Active Storage Setup

Rails Active Storage is configured with a storage backend (local in dev, cloud in prod). Files are served through the Rails API via signed URLs.

## Supported File Types

- Audio: `.mp3`, `.wav`, `.aiff`, `.flac`
- Images: `.jpg`, `.jpeg`, `.png`, `.webp`
- Documents: `.pdf`, `.zip` (for deliverable packages)

## Upload Flow

1. Frontend sends multipart form data to the Rails API
2. Rails validates file type and size
3. File stored via Active Storage
4. Signed URL returned to frontend for download/preview

---

## Related Notes

- [[Docs/services/SELLER_GUIDE]] — Uploading deliverables as a seller
- [[Docs/services/BUYER_GUIDE]] — Downloading deliverables as a buyer
- [[Docs/services/SERVICES_WORKFLOW_ENABLEMENT_PLAN]] — Order delivery context
