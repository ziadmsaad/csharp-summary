# C# Conditional Statements Summary

### 🚀 C# Fundamentals: Session 3, Part 12 - Conditional Statements Example 04 \[Switch With Goto]

اهلا بيك وسهلا في موقع zee.com هنا بنقدملك كل جديد وnew

<p align="right">اهلا وسهلا بيك في موقغ elzee.com</p>

<p align="right">أهلاً بيك في ملخص شامل ومفصل لأهم النقط اللي اتكلمنا عنها في السيشن دي، واللي بتركز على استخدام الـ <code>goto</code> statement مع الـ <code>switch</code> في C#، وإزاي ده بيأثر على الـ <code>readability</code> والـ <code>maintainability</code> بتاعة الكود.</p>

***

### Introduction to `goto` Statement

الـ `goto` statement في C# هي `control flow statement` بتسمحلك تنقل الـ `execution` بتاع البرنامج لنقطة معينة في الكود اسمها `label`. يعني كأنك بتقول للبرنامج: 'روح نفذ الكود اللي عند الـ `label` ده'.

في السيشن دي، اتكلمنا عن استخدام الـ `goto` تحديدًا مع الـ `switch` statement، وده عشان نفهم إزاي ممكن نستخدمها عشان نتجنب تكرار الكود (`code duplication`) بين الـ `cases` المختلفة في الـ `switch`.

🤔 **Why is this important to know?**

مع إن الـ `goto` statement مش `recommended` استخدامها في معظم الأوقات، إلا إن معرفتك بيها مهمة لسببين: أولاً، عشان لو شفتها في كود قديم أو كود كتبه حد تاني، تبقى فاهم إيه اللي بيحصل. ثانيًا، عشان تفهم ليه هي مش `recommended`، وده بيساعدك تكتب كود أفضل وأكثر `readability`.

***

### `switch` with `goto` Example: Budget Options

المثال اللي اتشرح في السيشن كان عن `budget` بيدخله اليوزر، وبناءً عليه بنحدد إيه الـ `options` المتاحة ليه. الـ `budget` ده بيكون `integer`.

**الـ Scenario الأصلي (بدون `goto`):**

* لو الـ `budget` بـ `1000`، اليوزر عنده `Option 1`.
* لو الـ `budget` بـ `2000`، اليوزر عنده `Option 1` و `Option 2`.
* لو الـ `budget` بـ `3000`، اليوزر عنده `Option 1` و `Option 2` و `Option 3`.

لو كتبنا ده بـ `switch` عادي، هنلاقي إن فيه `code duplication`، يعني نفس السطور بتتكرر في أكتر من `case`:

\`\`\`csharp int budget = int.Parse(Console.ReadLine()); // Assuming valid integer input

switch (budget) { case 1000: Console.WriteLine("Option 1"); break; case 2000: Console.WriteLine("Option 1"); Console.WriteLine("Option 2"); break; case 3000: Console.WriteLine("Option 1"); Console.WriteLine("Option 2"); Console.WriteLine("Option 3"); break; } \`\`\`

**استخدام `goto` لتجنب تكرار الكود:**

الفكرة هنا إن لو اليوزر دخل `3000`، هو كده كده عنده `Option 3`، وبعدين عنده نفس الـ `options` اللي عند `2000`، واللي هي بدورها عندها نفس الـ `options` اللي عند `1000`. فبدل ما نكرر الكود، ممكن نستخدم `goto` عشان ننط للـ `case` اللي فيها الكود اللي عايزينه يتنفذ.

\`\`\`csharp int budget = int.Parse(Console.ReadLine()); // Assuming valid integer input

switch (budget) { case 1000: Console.WriteLine("Option 1"); break; case 2000: Console.WriteLine("Option 2"); goto case 1000; // Go to case 1000 to print Option 1 case 3000: Console.WriteLine("Option 3"); goto case 2000; // Go to case 2000 to print Option 2 and then Option 1 } \`\`\`

**شرح اللي بيحصل:**

* لو الـ `budget` بـ `3000`:
  1. هيطبع `"Option 3"`.
  2. هينفذ `goto case 2000;`، فهينط للـ `case 2000`.
  3. في الـ `case 2000`، هيطبع `"Option 2"`.
  4. هينفذ `goto case 1000;`، فهينط للـ `case 1000`.
  5. في الـ `case 1000`، هيطبع `"Option 1"`.
  6. هيلاقي `break;` في الـ `case 1000`، فهينهي الـ `switch`.

النتيجة النهائية هي إنه هيطبع `Option 3`، `Option 2`، `Option 1`، وده نفس الـ `output` اللي كنا عايزينه من غير تكرار الكود.

🤔 **Why is this important to know?**

استخدام `goto` بالشكل ده بيقلل الـ `code duplication`، وده ممكن يكون مفيد في بعض الـ `scenarios` المعقدة اللي فيها `shared logic` بين الـ `cases`. لكن زي ما هنشوف، ده بيجي على حساب الـ `readability`.

***

### Readability and Maintainability: The "Spaghetti Code" Problem

مع إن استخدام `goto` ممكن يحل مشكلة تكرار الكود في بعض الحالات، إلا إنه بيخلق مشكلة أكبر بكتير وهي الـ `readability` والـ `maintainability` بتاعة الكود. لما بتستخدم `goto`، بتخلي الـ `execution flow` بتاع البرنامج غير خطي، يعني مش بيمشي بالترتيب الطبيعي من فوق لتحت.

**ليه ده بيعمل مشكلة؟**

* **صعوبة التتبع (`Hard to Follow`)**: لما بتقرا كود فيه `goto`، بتلاقي نفسك بتنط من مكان لمكان في الكود، وده بيخلي تتبع الـ `logic` صعب جدًا. كأنك بتقرا كتاب وكل شوية حد يقولك: "روح صفحة 50، وبعدين ارجع لصفحة 10، وبعدين روح صفحة 120". ده بيخلي فهم الكود `complex` ومربك.
* **"Spaghetti Code"**: المصطلح ده بيستخدم لوصف الكود اللي بيكون فيه `control flow` متشابك ومعقد بسبب استخدام `goto` بشكل مفرط. الكود بيبقى عامل زي طبق المكرونة الاسباجتي، كله داخل في بعضه وصعب تفككه.
* **صعوبة الـ `Debugging`**: لما الكود بيكون صعب تتبعه، بيكون أصعب إنك تلاقي الـ `bugs` وتصلحها. الـ `unexpected jumps` ممكن تؤدي لـ `errors` مش سهلة الاكتشاف.
* **صعوبة الـ `Maintenance`**: تعديل الكود اللي فيه `goto` بيكون `risky` جدًا، لأن أي تغيير بسيط ممكن يؤثر على أماكن تانية في الكود بطرق غير متوقعة بسبب الـ `jumps`.

🤔 **Why is this important to know?**

النقطة دي هي السبب الرئيسي اللي بيخلي الـ `goto` statement `discouraged` في البرمجة الحديثة. الـ `best practices` في البرمجة بتركز على كتابة كود `clean`، `readable`، و `maintainable`. عشان كده، دايماً بنفضل نستخدم `loops` (`for`, `while`, `do-while`) و `functions` و `structured control flow statements` (زي `if-else if` و `switch` بشكلها العادي) عشان ننظم الكود بتاعنا ونخليه سهل الفهم والتعديل.

***

### `goto` Outside `switch`

الـ `goto` statement مش مقتصرة على استخدامها داخل الـ `switch` statement بس. ممكن تستخدمها في أي مكان في الكود عشان تنط لـ `label` معين. المثال اللي اتشرح في السيشن كان عن `input validation`.

**مثال عملي:**

لو عايز تطلب من اليوزر يدخل اسمه، ولو الاسم ده كان `"Hamada"`، تطلب منه يدخل الاسم تاني، ممكن تعمل كده:

\`\`\`csharp Console.WriteLine("Hello Hamada"); // This line might be somewhere else in the code

RetryInput: Console.Write("Please enter your name: "); string name = Console.ReadLine();

if (name == "Hamada") { goto RetryInput; // If name is "Hamada", go back to RetryInput label }

Console.WriteLine($"Hello {name}"); \`\`\`

**شرح اللي بيحصل:**

1. البرنامج هيطبع `"Hello Hamada"` (السطر ده ممكن يكون في أي حتة في الكود، مش لازم يكون قبله مباشرة).
2. هيلاقي الـ `label` اللي اسمه `RetryInput:`.
3. هيطلب من اليوزر يدخل اسمه.
4. لو اليوزر دخل `"Hamada"`، الـ `if` condition هتكون `true`، وهينفذ `goto RetryInput;`، فهينط تاني للـ `label` اللي اسمه `RetryInput`، ويطلب من اليوزر يدخل اسمه من جديد.
5. الـ `loop` ده هيفضل شغال لحد ما اليوزر يدخل اسم غير `"Hamada"`.
6. لما اليوزر يدخل اسم غير `"Hamada"`، الـ `if` condition هتكون `false`، وهيكمل عادي ويطبع `"Hello [اسم اليوزر]"`.

🤔 **Why is this important to know?**

المثال ده بيوضح خطورة استخدام `goto` خارج الـ `switch`، خصوصًا في حالات الـ `looping` أو الـ `input validation`. مع إنها ممكن تبدو كحل سريع، إلا إنها بتخلي الكود صعب جدًا في الفهم والـ `debugging`. في C#، فيه `constructs` أفضل بكتير للـ `looping` زي `while` أو `do-while` loops، واللي بتخلي الكود بتاعك `structured` و `readable` أكتر بكتير.

***

### Conclusion and Recommendation

الـ `goto` statement هي أداة قوية في C#، لكنها زي السلاح ذو الحدين. ممكن تستخدمها عشان تحل مشاكل معينة زي الـ `code duplication` في الـ `switch` statement، لكن استخدامها المفرط أو غير المدروس بيؤدي لـ `spaghetti code` صعب الفهم والـ `maintenance`.

**الخلاصة:**

* **تجنب استخدام `goto` قدر الإمكان.** دايماً فيه بدائل أفضل وأكثر `readability` زي الـ `loops`، الـ `functions`، والـ `structured control flow statements`.
* **لو شفتها في كود، افهمها.** معرفتك بيها مهمة عشان تقدر تقرا وتفهم الأكواد القديمة أو الأكواد اللي كتبها غيرك.
* **استخدمها بحذر شديد وفي أضيق الحدود.** لو لقيت نفسك مضطر تستخدمها، فكر كويس جداً هل مفيش حل تاني أفضل.

**نصيحة إضافية:**

المحاضر نصح إننا نعمل `search` أكتر عن الـ `Jump Table` والـ `Hash Table` وإزاي الـ `switch` بتشتغل مع الـ `string`. دي نقط مهمة جداً عشان تفهم الـ `performance characteristics` بتاعة الـ `switch` statement في C#.

🤔 **Why is this important to know?**

فهمك للنقط دي بيخليك `developer` أفضل. مش بس بتعرف تكتب كود، لكن بتعرف تكتب كود `efficient` و `readable`، وده اللي بيميز الـ `professional developers`.

بالتوفيق في مذاكرتك! 🚀
