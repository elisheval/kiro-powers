---
inclusion: manual
---

# Figma → MOE Angular — הנחיות קריאה מ-Figma

> שלב נוכחי: **קריאה בלבד (Read-only)**.
> הקובץ מגדיר איך לקרוא ולהבין עיצוב מ-Figma. כללי המיפוי והמימוש (mng / PrimeNG / tokens)
> ייכתבו בהמשך לפי הפערים שיתגלו במימוש בפועל.

---

## 1. עקרון על — קריאה בלבד

בשלב הזה ה-power משמש **רק לקריאה והבנה** של העיצוב מ-Figma.

- ✅ מותר: לקרוא מבנה, צילומי מסך, קוד-ייחוס, טוקנים, ו-assets מ-Figma.
- ⛔ אסור: **כתיבה ל-Figma**. אין להשתמש בכלים שמשנים את הקובץ:
  `use_figma`, `generate_figma_design`, `create_new_file`, `add_code_connect_map`,
  `send_code_connect_mappings`, `upload_assets`, `generate_diagram`.
- אם משימה דורשת כתיבה ל-Figma — **עצור ושאל** את המשתמש לפני כל פעולה.

---

## 2. פענוח ה-URL

מבנה ה-URL של Figma:
```
https://www.figma.com/design/<fileKey>/<name>?node-id=<int1>-<int2>
```

- `fileKey` = המקטע אחרי `/design/`. לדוגמה מתוך
  `.../design/eLzbSfqX4H6JqzMDQEs8PG/...` → `fileKey = eLzbSfqX4H6JqzMDQEs8PG`.
- `nodeId` = הערך של `node-id`, **כשממירים מקף לנקודתיים**.
  לדוגמה `node-id=298-8824` → `nodeId = 298:8824`.
- אם ה-URL הוא בפורמט `.../design/<fileKey>/branch/<branchKey>/...` → השתמש ב-`branchKey` כ-`fileKey`.

**חובה:**
- אם ב-URL **אין** `node-id` — אל תנחש. בקש מהמשתמש קישור עם בחירת צומת
  (קליק ימני על ה-frame ב-Figma → *Copy link to selection*).
- **לעולם אל תעביר `nodeId` ריק או מנוחש.**

---

## 3. זרימת קריאה (Workflow)

הסדר המומלץ לקריאת מסך/רכיב:

1. **`get_metadata`** — מפה ראשונה של המבנה (היררכיית שכבות, שמות, מיקומים, גדלים).
   משמש להבנת השלד ולזיהוי ה-node ids הפנימיים לקריאה מעמיקה.
   - אם לא יודעים לאיזה עמוד/צומת להיכנס — אפשר לקרוא בלי `nodeId` כדי לקבל רשימת עמודים.
2. **`get_design_context`** — הכלי המרכזי. מחזיר קוד-ייחוס, צילום מסך, וטוקנים/סגנונות
   של הצומת. זהו המקור העיקרי להבנת העיצוב.
3. **`get_variable_defs`** — הגדרות המשתנים (צבעים, spacing, טיפוגרפיה) של הצומת,
   כשצריך את הערכים הסמנטיים המדויקים.
4. **`get_screenshot`** — צילום מסך ויזואלי לאימות מול מה שהמשתמש רואה.
5. **`download_assets`** — להורדת תמונות/אייקונים/SVG מתוך הצומת, כשצריך נכסים בפועל.

לפעולת מיפוי לרכיבים בקוד (Code Connect) אפשר להיעזר בקריאה בלבד:
`get_code_connect_map`, `get_code_connect_suggestions`, `get_context_for_code_connect`.

---

## 4. בחירת הכלי הנכון

| צריך | כלי |
|------|-----|
| מבנה/היררכיה כללית | `get_metadata` |
| הבנה מלאה של רכיב + קוד-ייחוס + טוקנים | `get_design_context` |
| ערכי צבע/spacing/טיפוגרפיה סמנטיים | `get_variable_defs` |
| אימות ויזואלי | `get_screenshot` |
| תמונות / SVG / אייקונים | `download_assets` |
| אימות מי מחובר | `whoami` |

---

## 5. הערות תפעוליות

- **כלי הקריאה דורשים `fileKey` + `nodeId` מפורשים** — ה-MCP המרוחק אינו יודע מהי
  הבחירה הנוכחית בקובץ. תמיד גוזרים אותם מה-URL.
- **קוד-הייחוס שמוחזר מ-`get_design_context` הוא React+Tailwind** — הוא **reference בלבד**.
  אין להעתיק אותו כמו שהוא; הוא ישמש בשלב המימוש לזיהוי מבנה, טקסטים, וטוקנים.
- **assets מ-Figma** הם URLs קצרי-טווח (כ-7 ימים). יש להוריד מיד.
  - בהורדה ב-Windows/PowerShell: `curl` ממופה ל-`Invoke-WebRequest`. השתמש ב-`curl.exe`,
    ואם יש שגיאת revocation של TLS — הוסף `--ssl-no-revoke`.
  - יש להתייחס ל-URL כמו לסוד (לא לשתף/להדפיס מיותר).
- **Figma Make** (`/make/`) ו-**FigJam** (`/board/`) אינם בתחום השימוש הנוכחי.

---

## 6. חילוץ Design Tokens

### צבעים — הכלל הקריטי

כל צבע שמופיע בעיצוב (hex מ-Figma) **חייב** להתמפות לטוקן מהפלטה — אסור להשאיר hex גולמי.

מקורות הצבע מוגדרים בתוך ספריית התשתית `@moe/mng-lib`. מאתרים אותם תחת
`node_modules/@moe/mng-lib` (הטוקנים מקומפלים ב-`fesm2022/moe-mng-lib.mjs` —
חפש שם `mngPalette` / `israel-blue` וכד'). סדר עדיפות:
1. טוקנים סמנטיים (`igds.*`, `mng.*`).
2. הפלטה הגולמית (`israel-blue`, `coral-red`, `galil-green`, `negev-orange`,
   `steel-grey`, `dawn-blue`, `mist-blue`, `dim-grey`, `bright-grey`...).

בקוד הסופי משתמשים ב-`var(--p-{token})` **בלבד — ללא fallback גולמי**:
- ❌ `var(--p-igds-background-default, #f1f5fb)`
- ❌ `#0068f5` / `rgb(...)`
- ✅ `var(--p-igds-background-default)`
- ✅ `var(--p-israel-blue-500)`

### מיפוי hex → טוקן

1. חפש התאמה מדויקת ל-hex מ-Figma בתוך הפלטה (`mngPalette` ב-`@moe/mng-lib`).
2. נמצאה התאמה מדויקת → השתמש בטוקן שלה.
3. **אין התאמה מדויקת** → בחר את הגוון הקרוב ביותר (מרחק צבע מינימלי), השתמש בטוקן שלו,
   **והתרע** למשתמש. לדוגמה:
   > ⚠️ הצבע `#xxxxxx` מהעיצוב לא קיים בפלטה. השתמשתי בקרוב ביותר: `israel-blue.500`. כדאי לשקול הוספה לפלטה ב-`@moe/mng-lib`.
4. **אסור להמציא** צבע או להשאיר hex גולמי. הוספת צבע לפלטה — רק באישור המשתמש.

### שאר הטוקנים

ערכים שאינם צבע (px, rem, font-weight) — מותר לקחת ישירות מ-Figma:
- **טיפוגרפיה**: font-family, size, weight, line-height.
- **ריווחים (spacing)**: gap, padding, margin. העדף PrimeFlex classes על ערכים קשיחים כשאפשר.
- **border-radius**: px מ-Figma.
- **shadows**: אם קיים טוקן צל — השתמש בו; אחרת ציין למשתמש.

---

## 7. מיפוי אלמנט Figma → רכיב

סדר עדיפויות לבחירת רכיב מימוש (קריטי):
1. **רכיב `mng-X` קיים** — חפש קודם ב-`@moe/mng-lib`. אם יש רכיב שעושה מה שצריך — חובה להשתמש בו.
2. **רכיב PrimeNG (`p-X`)** — אם אין רכיב `mng` מתאים (`p-select`, `p-button`, `p-checkbox`,
   `p-radioButton`, `p-dialog`, `pInputText`...). **אסור HTML/CSS גולמי כשיש רכיב PrimeNG שעושה את אותו דבר.**
3. **PrimeFlex classes** — לפריסה ומרווחים (`flex`, `gap-2`, `p-3`, `align-items-center`).
4. **HTML + SCSS מותאם** — מוצא אחרון בלבד, כשאין שום אלטרנטיבה.

---

## 8. Layout, CSS ו-RTL

- **CSS מינימלי** — כתוב את המינימום ההכרחי. העדף PrimeFlex classes ו-PrimeNG built-in styling
  על פני SCSS מותאם. אם אפשר להשיג את התוצאה עם PrimeFlex בלבד — אל תכתוב SCSS.
- **RTL** — הפרויקט עברית/RTL. השתמש ב-`start`/`end` במקום `left`/`right`. PrimeFlex תומך RTL אוטומטית.

---

## 9. מה עדיין לא מוגדר (פערים מכוונים)

- טיפוגרפיה במונחי theme (מעבר לערכי px ישירים מ-Figma).
- אנטי-פטרנים נוספים שיתגלו במימוש בפועל.
