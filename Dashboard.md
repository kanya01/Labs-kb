# System Dashboard

> Last synced: (Claude will update this)

---

## 🔴 Open Issues
```dataview
TABLE status, linked-issue, linked-repo, tags
FROM "Issues/Open"
SORT file.mtime DESC
```

---

## 📄 Docs — In Progress
```dataview
TABLE status, updated, linked-repo
FROM "Docs"
WHERE status = "in-progress"
SORT updated DESC
```

---

## ✅ Recently Closed
```dataview
TABLE status, linked-issue
FROM "Issues/Closed"
SORT file.mtime DESC
LIMIT 10
```

---

## 📅 Progress Log
```dataview
LIST
FROM "Progress"
SORT file.name DESC
LIMIT 14
```

---

## 🗺️ System Map
- [[_System Map/Architecture]]
- [[_System Map/Components]]
- [[_System Map/Decisions]]