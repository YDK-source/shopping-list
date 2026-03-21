# הגדרת סנכרון בין שני משתמשים

## מה זה נותן?
- יוסי ומרים יכולים לסמן מוצרים **מכל מכשיר** — פלאפון, טאבלט, מחשב
- השינויים מסתנכרנים **בזמן אמת** (שניות)
- הרשימה נשמרת בין כניסות — ביום הקנייה פותחים ורואים הכל
- עובד גם **ללא אינטרנט** (עם localStorage כגיבוי)

---

## הגדרה חד-פעמית — 10 דקות

### שלב 1: צור פרויקט Firebase (חינמי)

1. כנס ל-**console.firebase.google.com**
2. לחץ **"Add project"** → תן שם (למשל `yosi-maryam-shopping`) → המשך
3. ביטול Google Analytics (לא צריך) → **Create project**

### שלב 2: הפעל Realtime Database

1. בתפריט שמאל: **Build → Realtime Database**
2. לחץ **"Create Database"**
3. בחר **United States** (או כל אזור) → Next
4. בחר **"Start in test mode"** → Enable
   - _(Test mode = כל אחד יכול לקרוא/לכתוב — מתאים לשימוש פרטי)_

### שלב 3: קבל את פרטי הפרויקט

1. לחץ על **גלגל השיניים ⚙️** → **Project settings**
2. גלול למטה ל-**"Your apps"**
3. לחץ על סמל `</>` (Web app)
4. תן שם לאפליקציה → **Register app**
5. תראה קוד כזה — **שמור אותו:**

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "yosi-maryam-shopping.firebaseapp.com",
  databaseURL: "https://yosi-maryam-shopping-default-rtdb.firebaseio.com",
  projectId: "yosi-maryam-shopping",
  storageBucket: "yosi-maryam-shopping.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

### שלב 4: הכנס את הפרטים לקובץ index.html

פתח את `index.html`, חפש את הבלוק:

```javascript
const FIREBASE_CONFIG = {
  apiKey:            "REPLACE_WITH_YOUR_API_KEY",
  ...
```

והחלף כל `REPLACE_WITH_...` בערכים האמיתיים מ-Firebase.

### שלב 5: Deploy ל-GitHub Pages

```bash
git init
git add .
git commit -m "Shopping list with Firebase sync"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/shopping-list.git
git push -u origin main
```

ב-GitHub: **Settings → Pages → Source: main branch** → Save

תקבל URL כמו: `https://YOUR_USERNAME.github.io/shopping-list`

---

## שימוש

- שתף את ה-URL עם מרים
- שניכם פותחים את אותו ה-URL
- כל שינוי שאחד עושה — השני רואה תוך שניות
- 🟢 **"מסונכרן"** = הכל שמור בענן
- 🟡 **"שומר..."** = ממתין לשמירה
- 🔴 **"מנותק"** = ללא אינטרנט (נשמר מקומית ויסתנכרן בחזרה)

---

## עדכון רשימת המוצרים בעתיד

ערוך את מערך `RAW` ב-`index.html` — כל שורה בפורמט:
```javascript
['קטגוריה', 'שם מוצר', כמות_ברירת_מחדל, 'יחידת מידה'],
```

קטגוריות קיימות: `fruits`, `dairy`, `sauces`, `bread`, `drinks`, `frozen`, `spices`, `canned`, `grains`, `sweets`, `cleaning`, `misc`
