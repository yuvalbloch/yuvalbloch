---
title: "Python Data Structures: Biological Examples (in Hebrew)"
description: "A practical guide with **hands-on tasks** for using lists, dictionaries, tuples, and nested data structures in Python, focusing on real-world applications in biology. writed in Hebrew"
---

# 🔬 תרגול במבני נתונים

במשימות הבאות תתרגלו שימוש במבני הנתונים שלמדתם — רשימות, קבוצות, מילונים וזוגות — בהקשר של **מחקר אקולוגי**.

---

## 🐾 חלק 1: רשימות, קבוצות וגיוון ביולוגי

במהלך סקר טבע באזור מדברי תיעדתם את כל בעלי החיים שנצפו, לפי סדר ההיתקלות:

```python
["porcupine", "gazelle", "spiny mouse", "golden jackal", "ibis", "lizard", "gazelle", "rock hyrax", "spiny mouse", "green toad", "ibis", "jackal", "fox", "Megabat", "Megabat", "lizard", "ibis"]
```

### משימות:

1. צרו רשימה בשם `animals` שמכילה את כל בעלי החיים לפי סדר התיעוד.
    
2. הדפיסו את הרשימה וודאו שהיא מוצגת כראוי.
    
3. תיקון טעות בזיהוי: העטלף הראשון הוא בעצם `"Microbat"` ולא `"Megabat"`.  
    השתמשו ב־`()index` כדי לאתר ולתקן את הטעות.
    
4. חשבו את **השכיחות היחסית** של `"ibis"` — כלומר, כמה פעמים הוא מופיע חלקי אורך הרשימה.
    
5. כמה מינים שונים נצפו? צרו `set` מתוך הרשימה כדי לבדוק אילו מינים הופיעו לפחות פעם אחת.
    

---

בסקר שנערך בבית גידול נוסף, נמצאו המינים הבאים:

```python
["sand cat", "desert hedgehog", "rock hyrax", "spiny mouse", "golden jackal", "lizard", "sand cat", "green toad", "golden jackal", "fox", "ibex", "spiny mouse"]
```

6. כמה מינים מופיעים ברשימה החדשה? השתמשו ב־`set` כדי לבדוק.
    
7. כמה מינים משותפים לשני בתי הגידול?
    
8. כמה מינים ייחודיים קיימים בסך הכול (בשני האתרים יחד)?
    
9. אילו מינים נמצאים בבית הגידול הראשון אך לא בשני?
    
10. **מגוון בטא** מבטא את השוני בין שני בתי גידול, ומחושב לפי הנוסחה:
    $$
    1- \frac{a}{a + b + c} $$
    
    כאשר:
    
    - a: מספר המינים המשותפים לשני האתרים
        
    - b: מספר המינים הייחודיים לאתר הראשון
        
    - c: מספר המינים הייחודיים לאתר השני
        
    
    חשבו את מגוון הבטא בין שני בתי הגידול לפי נוסחה זו.
    

---

## 🐜 חלק 2: חרקים לפי בתי גידול (שימוש במילונים)

במהלך סקר נוסף תיעדתם את תפוצת החרקים בשלושה סוגים של בתי גידול:

📍 `under_tree`:

```python
{
  "ants": 23,
  "beetles": 5,
  "grasshoppers": 2,
  "stick insect": 1
}
```

📍 `in_bush`:

```python
{
  "ants": 12,
  "beetles": 8,
  "grasshoppers": 7,
  "butterflies": 5,
  "leafhoppers": 2
}
```

📍 `open_area`:

```python
{
  "ants": 5,
  "grasshoppers": 15,
  "butterflies": 10,
  "dragonflies": 4
}
```

---

### משימות:

1. צרו `dictionary` נפרד עבור כל בית גידול, כאשר המפתח הוא שם החרק והערך הוא מספר התצפיות.
    
2. צרו מילון מקונן בשם `all_habitat` כאשר המפתחות הם בתי הגידול השונים והערכים הם המילונים שיצרתם .  
    ודאו שהשורה הבאה מחזירה 5:
    
    ```python
    all_habitat["open_area"]["ants"]
    ```
    
3. חשבו את **השכיחות היחסית** של `"grasshoppers"` בבית הגידול `open_area`.  
    רמז: השתמשו ב־`()values` וב־`()sum` כדי לחשב את סך כל התצפיות באותו בית גידול.
    
4. כמה **מינים שונים** יש בכלל בתי הגידול? השתמשו ב־`set` ו־`()union` כדי לבדוק.
    

---

## 🌸 חלק 3: רשת האבקה — שימוש בזוגות (`tuples`)

במחקר נוסף תיעדתם אילו חרקים מאביקים אילו פרחים:

### 🐝 `bees`

- Sunflower
    
- Lavender
    
- Clover
    

### 🦋 `butterflies`

- Lavender
    
- Zinnia
    
- Milkweed
    

### 🪰 `hoverflies`

- Clover
    
- Yarrow
    
- Daisy
    

---

### משימות:

1. צרו רשימה בשם `pollination` של זוגות (`tuples`), כאשר כל זוג מייצג קשר בין חרק לפרח.  
    לדוגמה: `("bees", "Sunflower")`
    
2. בדקו האם `"butterflies"` מאביקים את `"Clover"` באמצעות הביטוי:
    
3. נסו לשנות את הקשר הראשון של `"bees"` מ־`"Sunflower"` ל־`"Rose"` כך:
    
    ```python
    pollination[0][1] = "Rose"
    ```
    
    ⚠️ הסבירו מדוע זה לא עובד — מה ההבדל בין `tuple` ל־`list`?
    
4. תקנו את הערך על ידי יצירת `tuple` חדש והחלפתו ברשימה.
    
