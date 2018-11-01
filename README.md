<div dir='rtl' align='right' style="    list-style-type: none;">
  <h1>המדריך המלא לכתיבה בג'אווה-סקריפט</h1p>
  <h2>תוכן עיניינים</h2>

בימים אלו אנו עובדים על מנת לתרגם מדריך זה לעברית. צרו קשר אם ברצונכם לעזור!<a href="https://github.com/airbnb/javascript"> המדריך המקורי</a>
## תוכן עניינים
  1. [טיפוסים](#types)
  1. [הפניות](#references)
  1. [עצמים](#objects)
  1. [מערכים](#objects)
  1. [Destructuring](#destructuring)
  1. [מחרוזות](#strings)
  1. [פונקציות](#functions)
  1. [Arrow Functions](#arrow-functions)
  1. [מחלקות & בנאים](#classes--constructors)
  1. [תבניות](#modules)
  1. [Iterators and Generators](#iterators-and-generators)
  1. [מאפיינים](#properties)
  1. [משתנים](#variables)
  1. [Hoisting](#hoisting)
  1. [Comparison Operators & Equality](#comparison-operators--equality)
  1. [חסמים](#blocks)
  1. [Control Statements](#control-statements)
  1. [הערות](#comments)
  1. [רווחים](#whitespace)
  1. [Commas](#commas)
  1. [נקודה פסיק](#semicolons)
  1. [Type Casting & Coercion](#type-casting--coercion)
  1. [Naming Conventions](#naming-conventions)
  1. [Accessors](#accessors)
  1. [אירועים](#events)
  1. [jQuery](#jquery)
  1. [ECMAScript 5 Compatibility](#ecmascript-5-compatibility)
  1. [ECMAScript 6+ (ES 2015+) Styles](#ecmascript-6-es-2015-styles)
  1. [Standard Library](#standard-library)
  1. [בדיקות](#testing)
  1. [ביצועים](#performance)
  1. [משאבים](#resources)
  1. [In the Wild](#in-the-wild)
  1. [תרגום](#translation)
  1. [המדריך השלם לג'אווה-סקריפט](#the-javascript-style-guide-guide)
  1. [שוחח איתנו על ג'אווה-סקריפט](#chat-with-us-about-javascript)
  1. [מפיצים](#contributors)
  1. [רישיון](#license)
  1. [Amendments](#amendments)

## טיפוסים

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **.פרימיטיבים**: כאשר ניגשים לטיפוס פרימיטבי הפעולה תשפיע על הערך שלו באופן ישיר 
  
    - `string` - מחרוזת
    - `number` - מספר
    - `boolean` - ערך בוליאני
    - `null` - מקביל לריק
    - `undefined` - לא מוגדר
    - `symbol` - סמל
<code dir="ltr" align="left">
  
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
</code>
    - טיפוס סימלי הוא לא אמין במיוחד ולכן אין להשתמש בו בדפדפנים שלא תומכים בו באופן עקרוני.
  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **מורכבים**: כאשר ניגשים לטיפוס מורכב יש לזכור שעובדים על ההפנייה לערך עצמו ולא על הערך המקורי.

    - `object` - עצם
    - `array` - מערך
    - `function` - פונקציה
<code dir="ltr" align="left">
  
      const foo = [1, 2];
      const bar = foo;
      
      bar[0] = 9;    
      
      console.log(foo[0], bar[0]); // => 9, 9    
      
</code>
**[⬆ חזור למעלה](#table-of-contents)**
</div>
