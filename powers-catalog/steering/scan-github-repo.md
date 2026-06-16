---
inclusion: auto
---

# Powers Catalog — הוראות סריקה

## GitHub Repository
- **URL:** https://github.com/elisheval/kiro-powers
- **Branch:** main

## איך לסרוק

1. גש ל-GitHub API כדי לקבל רשימת תיקיות:
   `https://api.github.com/repos/elisheval/kiro-powers/contents`

2. כל תיקיה מסוג `"type": "dir"` היא Power. לכל אחת, קרא את ה-POWER.md:
   `https://raw.githubusercontent.com/elisheval/kiro-powers/main/<folder-name>/POWER.md`

3. חלץ מה-frontmatter:
   - `displayName` — שם ה-Power
   - `description` — תיאור
   - `keywords` — מילות מפתח

## פורמט תצוגה בצ'אט

הצג רשימה מסודרת בפורמט הבא:

```
## 🔌 Powers זמינים (מקור: GitHub)

- **{displayName}**
  תיאור: {description}
  URL: `https://github.com/elisheval/kiro-powers/tree/main/{folder}`

- **{displayName}**
  תיאור: {description}
  URL: `https://github.com/elisheval/kiro-powers/tree/main/{folder}`
```

## כלים לשימוש

- השתמש ב-`webFetch` עם URL של GitHub API (`https://api.github.com/repos/elisheval/kiro-powers/contents`)
- לקריאת POWER.md השתמש ב: `https://raw.githubusercontent.com/elisheval/kiro-powers/main/<folder>/POWER.md`

## הערות
- אם ה-repo פרטי ו-web fetch לא עובד, הציע למשתמש להשתמש ב-GitHub API token
- הצג תמיד את ה-URL המלא לייבוא
- **חשוב:** הנתונים חייבים לבוא מ-GitHub, לא מקבצים מקומיים!
- **שפה:** תמיד ענה בעברית בלבד.
