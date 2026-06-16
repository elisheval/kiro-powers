---
inclusion: auto
---

# Powers Catalog — הוראות סריקה

## GitHub Repository
- **URL:** https://github.com/elisheval/kiro-powers
- **Branch:** main

## איך לסרוק

1. גש ל-URL הבא כדי לקבל את רשימת התיקיות ב-repo:
   `https://github.com/elisheval/kiro-powers/tree/main`

2. כל תיקיה ברמה הראשונה היא Power. לכל אחת, גש ל:
   `https://github.com/elisheval/kiro-powers/blob/main/<folder-name>/POWER.md`

3. קרא את ה-frontmatter של כל `POWER.md` כדי לחלץ:
   - `displayName` — שם ה-Power
   - `description` — תיאור
   - `keywords` — מילות מפתח

## פורמט תצוגה

הצג את הרשימה בפורמט הבא:

```
## 🔌 Powers זמינים ב-repo

| # | שם | תיאור | מילות מפתח |
|---|-----|--------|------------|
| 1 | {displayName} | {description} | {keywords} |

### ייבוא

כדי לייבא power ל-Kiro, העתיקי את ה-URL הבא להגדרות:
`https://github.com/elisheval/kiro-powers/tree/main/<folder-name>`
```

## כלים לשימוש

- השתמש ב-`webFetch` כדי לגשת לעמודי GitHub
- אם webFetch לא מחזיר תוכן מספיק, נסה mode "rendered"
- חלופה: השתמש ב-`remote_web_search` עם query ממוקד ל-repo

## הערות
- אם ה-repo פרטי ו-web fetch לא עובד, הציע למשתמש להשתמש ב-GitHub API token
- תמיד הצג את ה-URL המלא לייבוא כדי שקל להעתיק
