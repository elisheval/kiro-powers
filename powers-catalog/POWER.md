---
name: "powers-catalog"
displayName: "Powers Catalog"
description: "סורק את ה-GitHub repo של ה-Powers שלך ומציג רשימה מסודרת עם שם, תיאור, מילות מפתח, ו-URL לייבוא. שימושי כשרוצים לדעת מה זמין או לשתף עם חברי צוות."
keywords:
  - "powers"
  - "catalog"
  - "קטלוג"
  - "רשימה"
  - "available"
  - "list powers"
  - "import power"
  - "ייבוא"
author: "MOE Infrastructure Team"
---

# Powers Catalog

Power שסורק את ה-GitHub repository שלך ומציג רשימה מסודרת של כל ה-Powers הזמינים — כולל שם, תיאור, מילות מפתח, ו-URL לייבוא ישיר ל-Kiro.

## איך זה עובד

כש-Kiro מזהה שאת שואלת על Powers זמינים, הוא:
1. ניגש ל-GitHub repo שמוגדר ב-steering
2. סורק את מבנה התיקיות
3. קורא את ה-`POWER.md` של כל power
4. מציג רשימה מסודרת עם כל המידע הרלוונטי

## שימוש

פשוט שאלי משהו כמו:
- "מה ה-Powers שיש לי?"
- "תראה לי את הקטלוג"
- "רשימת powers זמינים"
- "איך מייבאים power?"

---

# When to Load Steering Files
- כשהמשתמש שואל על Powers זמינים, קטלוג, או ייבוא → `steering/scan-github-repo.md`
