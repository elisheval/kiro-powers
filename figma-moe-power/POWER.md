---
name: "figma-moe-power"
displayName: "Figma → MOE Angular"
description: "כללים והנחיות מדויקים להמרת עיצובי Figma לקוד Angular/PrimeNG לפי תשתית @moe/mng-lib. בשלב פיתוח — יהפוך לתשתית רוחבית למשרד."
keywords:
  - "figma"
  - "עיצוב"
  - "design"
  - "angular"
  - "primeng"
  - "mng-lib"
  - "tokens"
  - "design-to-code"
author: "MOE Infrastructure Team"
---

# Figma → MOE Angular

Power ייעודי להמרת עיצובים מ-Figma לקוד Angular בהתאם למוסכמות ולתשתית של משרד האנרגיה והתשתיות. Kiro טוען אותו אוטומטית כשמופיעות מילות מפתח כמו "figma" / "עיצוב".

> **סטטוס:** בפיתוח (`0.1.0`). ההנחיות מחודדות כרגע על קוד אמיתי בפרויקט `energy-inquiries`, ובהמשך יופצו כתשתית רוחבית לכל המשרד.

## מה ה-Power מספק
- כללי המרה מ-Figma לרכיבי תשתית: סדר עדיפויות `mng-X ← p-X ← PrimeFlex ← SCSS`.
- שימוש ב-design tokens במקום ערכי צבע גולמיים (hex/rgb).
- מינימום CSS — הישענות על PrimeFlex ועל theme.

---

# Onboarding (אופציונלי)
אין שלבי הכנה בשלב זה. ההנחיות המפורטות נמצאות בקובץ ה-steering.

---

# When to Load Steering Files
- עבודה על המרת עיצוב Figma → קוד Angular → `steering/figma-guidelines.md`
