<div dir='rtl' align='right' style="    list-style-type: none;">
  <h1>[airbnb-style] המדריך המלא לכתיבה בג'אווה-סקריפט</h1p>
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
  - [1.2](#types--complex) **מורכבים**: כאשר ניגשים לטיפוס מורכב יש לזכור שעובדים על ההפנייה לערך עצמו ולא על הערך המקורי.
    - `object` - עצם
    - `array` - מערך
    - `function` - פונקציה

<code dir="ltr" align="left">

      const foo = [1, 2];
      const bar = foo;
      
      bar[0] = 9;    
      
      console.log(foo[0], bar[0]); // => 9, 9    
      
</code>

**[⬆ חזור למעלה](#תוכן-עניינים)**

## הפניות

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) לפי הקונבציות האחרונות יש להשתמש ב-'const' מאשר ב-'var' עבור כל ההפניות; . eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

    > למה? בכדאי לוודא שלא תהיה האפשרות להקצות מחדש את ההפניות ובכך להימנע משגיאות ומקוד לא ברור.

<code dir="ltr" align="left">
  
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    
</code>

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) אם בכל זאת עלייך להקצות מחדש הפנייה, השתמש ב-'let' במקום ב-'var' . eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

    > למה? 'let' מוגדר לאותו הבלוק שהוא נמצא בו וכך נשמר הסדר הלוגי, לעומת 'var'. 

<code dir="ltr" align="left">
  
    // bad
    var count = 1;
    if (true) {
      count += 1;
    }

    // good, use the let.
    let count = 1;
    if (true) {
      count += 1;
    }
    
</code>

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) יש לשים לב שגם 'let' וגם 'const' מוגדרים באופן מוחלט לאזור ההגדרה הראשוני שלהם.

<code dir="ltr" align="left">

    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    
</code>

**[⬆ חזור למעלה](#תוכן-עניינים)**

## עצמים

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) השתמש בתחביר פשוט יותר ביצירת עצמים. eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

<code dir="ltr" align="left">
  
    // bad
    const item = new Object();

    // good
    const item = {};

</code>

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  - [3.2](#es6-computed-properties) Use computed property הקצו שמות לערכים בצורה מחושבת בעת יצירת עצמים עם שמות דינמים לערכים.

    > Why? למה? בצורה זאת תוכלו להגדיר את כל הערכים של אובייקט בפעולה אחת בלבד.

<code dir="ltr" align="left">

    function getKey(k) {
      return `a key named ${k}`;
    }

    // bad
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // good
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };

</code>

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.3](#es6-object-shorthand) צרו פונקציה לאובייקט בצורה מקוצרת. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)


<code dir="ltr" align="left">
    
    // bad
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // good
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };

</code>

  <a name="es6-object-concise"></a><a name="3.6"></a>
  - [3.4](#es6-object-concise) השתמשו בקיצור בעת השמה של ערך מסוים. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    > Why? It is shorter to write and descriptive.

<code dir="ltr" align="left">

    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
    };
    
</code>


  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  - [3.5](#objects--grouped-shorthand) קבצו את הקיצורים לערכים שלכם בתחילה הגדרת העצם.

    > למה? כי יותר קל להבחין איזה מהערכים משתמשים בקיצור.

<code dir="ltr" align="left">

    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
 
</code>


  <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.6](#objects--quoted-props) השימוש במרכאות בודדות על ערכים בעלי שמות לא מבוססים בלבד. eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)

    > למה? באופן סובייקטיבי זה יותר קריא ומשפר את ההבנה של תחביר הקוד, בנוסף על כך זה עובר אופטימיזציה יותר בקלות ברוב מנועי הג'אווה סקריפט.

<code dir="ltr" align="left">
    
    // bad
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // good
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };

</code>

  <a name="objects--prototype-builtins"></a>
  - [3.7](#objects--prototype-builtins) אין לקרוא לפונקציות של `Object.prototype` באופן ישיר, למשל `hasOwnProperty`, `propertyIsEnumerable`, ו `isPrototypeOf`. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

    > Why? למה? הפונקציות עלולות להיות שייכות לאב טיפוס של הערך עצמו  - שיקלו `{ hasOwnProperty: false }` - או, שהעצם עלול להיות עצם ריק (`Object.create(null)`).

<code dir="ltr" align="left">
    
    // bad
    console.log(Object.hasOwnProperty(key));

    // good
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // best
    const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
    /* or */
    import has from 'has'; // https://www.npmjs.com/package/has
    // ...
    console.log(has.call(object, key));
    
</code>


  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) עדיף להשתמש ב - 'spread' על פני [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) בשביל להעתיק עצמים ואת ההפניות שלהם בצורה מלאה. השתמש ב- ... בכדי ליצור עצם חדש שלא מזניח ערכים מסוימים באב הטיפוס.

<code dir="ltr" align="left">
    
    // very bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
    delete copy.a; // so does this

    // bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // good
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    
</code>

**[⬆ חזור למעלה](#תוכן-עניינים)**

## מערכים

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) יש לעשות שימוש בתחביר הבא בכדי ליצור מערך. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

<code dir="ltr" align="left">

    // bad
    const items = new Array();

    // good
    const items = [];

</code>


  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push)  יש להשתמש ב-[Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) במקום לגשת ישירות לאינדקס במערך.

<code dir="ltr" align="left">
  
    const someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');

</code>

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) יש להשתמש בהרחבת מערך `...` על מנת להעתיק אותו.

<code dir="ltr" align="left">
  
    // bad
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // good
    const itemsCopy = [...items];

</code>

  <a name="arrays--from"></a>
  <a name="arrays--from-iterable"></a><a name="4.4"></a>
  - [4.4](#arrays--from-iterable) יש להמיר עצם מסוג איטרטור למערך באמצעות השימוש בהרחבה ..., מאשר ב- [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from).

<code dir="ltr" align="left">
  
    const foo = document.querySelectorAll('.foo');

    // good
    const nodes = Array.from(foo);

    // best
    const nodes = [...foo];

</code>


  <a name="arrays--from-array-like"></a>
  - [4.5](#arrays--from-array-like) יש להשתמש [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) בכדי להמיר אובייקט שדומה למערך , למערך.
  

<code dir="ltr" align="left">
  
    const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

    // bad
    const arr = Array.prototype.slice.call(arrLike);

    // good
    const arr = Array.from(arrLike);

</code>

  <a name="arrays--mapping"></a>
  - [4.6](#arrays--mapping) השתמש [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) instead of spread `...` for mapping over iterables, because it avoids creating an intermediate array.

<code dir="ltr" align="left">

    // bad
    const baz = [...foo].map(bar);

    // good
    const baz = Array.from(foo, bar);

</code>


  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) Use return statements in array method callbacks. It’s ok to omit the return if the function body consists of a single statement returning an expression without side effects, following [8.2](#arrows--implicit-return). eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

<code dir="ltr" align="left">
  
    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map(x => x + 1);

    // bad - no returned value means `acc` becomes undefined after the first iteration
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      acc[index] = flatten;
    });

    // good
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      acc[index] = flatten;
      return flatten;
    });

    // bad
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // good
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });

</code>

  <a name="arrays--bracket-newline"></a>
  - [4.8](#arrays--bracket-newline) Use line breaks after open and before close array brackets if an array has multiple lines

<code dir="ltr" align="left">
  
    // bad
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // good
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];

</code>

**[⬆ back to top](#תוכן-עניינים)**

</div> <!-- RTL container !-->
