---
title: "Цикли"
teaching: 40
exercises: 10
questions:
- "Як виконати одні й ті ж дії над різними файлами?"
objectives:
- "Написати цикл, який застосовує одну або декілька команд окремо до кожного файлу в наборі файлів".
- "Простежити, яких значень набуває змінна циклу під час виконання циклу".
- "Пояснити різницю між ім'ям змінної та її значенням".
- "Пояснити, чому в іменах файлів не можна використовувати пробіли та деякі розділові знаки".
- "Продемонструвати, як побачити, які команди були виконані останнім часом".
- "Повторно запустити нещодавно виконані команди без повторного введення".
keypoints:
- "Цикл `for` повторює команди один раз для кожного елемента списку."
- "Кожному циклу `for` потрібна змінна для посилання на об'єкт, над яким він зараз працює."
- "Використовуйте `$name` для розкриття змінної (тобто отримання її значення). Також можна використовувати `${name}`."
- "Не використовуйте у назвах файлів пробіли, лапки або символи підстановки, такі як '*' або '?', оскільки це ускладнює розширення змінних."
- "Надавайте файлам однакові імена, які легко співпадають із шаблонами підстановок, щоб полегшити їх вибір для циклів".
- "Використовуйте клавішу зі стрілкою вгору для прокрутки попередніх команд, щоб редагувати та повторювати їх."
- "Використовуйте <kbd>Ctrl</kbd>+<kbd>R</kbd> для пошуку попередньо введених команд."
- "Використовуйте `history` для відображення останніх команд і `![номер]` для повторення команди за номером."
---

**Цикли** - це конструкція програмування, яка дозволяє повторювати команду або набір команд
для кожного елемента у списку.
Таким чином, вони є ключем до підвищення продуктивності за рахунок автоматизації.
Подібно до підстановочних символів і завершення клавішею табуляції, використання циклів також зменшує
кількість необхідного набору тексту (а отже, зменшує кількість помилок).

Припустимо, у нас є кілька сотень файлів геномних даних з іменами `basilisk.dat`, `minotaur.dat` та
`unicorn.dat`.
Для цього прикладу ми використаємо каталог `exercise-data/creatures`, який містить лише три
файли з прикладами,
але ці принципи можна застосувати до набагато більшої кількості файлів одночасно.

Структура цих файлів однакова: загальна назва, класифікація та дата оновлення
у перших трьох рядках, а в наступних - послідовності ДНК.
Давайте подивимось на файли:

```
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```
{: .language-bash}

Ми хотіли б роздрукувати класифікацію для кожного виду, яка наведена у другому
рядку кожного файлу.
Для кожного файлу нам потрібно виконати команду `head -n 2` і з'єднати її каналом з командою `tail -n 1`.
Для вирішення цієї задачі ми скористаємося циклом, але спочатку розглянемо загальну форму циклу,
використовуючи псевдокод нижче:

```
for thing in list_of_things
do
    operation_using $thing    # Відступ усередині циклу не є обов'язковим, але полегшує читабельність
done
```
{: .language-bash}

і ми можемо застосувати це до нашого прикладу наступним чином:

```
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $filename | tail -n 1
> done
```
{: .language-bash}

```
CLASSIFICATION: basiliscus vulgaris
CLASSIFICATION: bos hominus
CLASSIFICATION: equus monoceros
```
{: .output}


> ## Слідкуйте за підказкою
>
> Запрошення до введення в терміналі змінюється з `$` на `>` і назад, коли ми
> вводили команди всередині нашого циклу. Друге запрошення до введення, `>`, відрізняється, щоб нагадати
> нам, що ми ще не закінчили введення повної команди. Крапка з комою `;`
> використовується для розділення двох команд, написаних в одному рядку.
{: .callout}

Коли термінал бачить ключове слово `for`,
він знає, що потрібно повторити команду (або групу команд) один раз для кожного елемента списку.
Кожного разу, коли вміст циклу виконується (одне виконання команд всередині циклу називається ітерацією), елемент списку послідовно присвоюється
**змінній**, і команди всередині циклу виконуються, перш ніж перейти
до наступного елементу списку.
Усередині циклу
ми звертаємося до значення змінної, ставлячи `$` перед ї іменем.
Символ `$` вказує інтерпретатору командного рядка розглядати
змінну як ім'я змінної і підставити замість неї її значення,
замість того, щоб розглядати її як текст або зовнішню команду.

У цьому прикладі список складається з трьох файлів: `basilisk.dat`, `minotaur.dat` та `unicorn.dat`.
Кожного разу, коли виконанується цикл, він присвоює чергове ім'я файлу змінній `filename`
і виконає команду `head`.
При першому проходженні циклу
`$filename` дорівнює `basilisk.dat`.
Інтерпретатор виконує команду `head` на `basilisk.dat`
і передає перші два рядки команді `tail`,
яка виводить другий рядок файлу `basilisk.dat`.
Для другої ітерації `$filename` стає
`minotaur.dat`. Цього разу термінал виконує команду `head` на `minotaur.dat`
і передає перші два рядки команді `tail`,
яка виводить другий рядок `minotaur.dat`.
На третій ітерації `$filename` стає
`unicorn.dat`, тому термінал виконує команду `head` для цього файлу,
і `tail` на виході цього.
Оскільки у списку було лише три елементи, термінал вийде з циклу `for`.

> ## Однакові символи, різні значення
>
> Тут ми бачимо, що символ `>` використовується як запрошення командного рядка, тоді як `>` також
> використовується для перенаправлення виводу.
> Аналогічно, символ `$` використовується як запрошення до командного рядка, але, як ми бачили раніше,
> він також використовується для запиту до оболонки про значення змінної.
>
> Якщо *термінал* виводить `>` або `$`, то він очікує, що ви щось введете,
> і цей символ є підказкою.
>
> Якщо *ви* вводите `>` або `$` самостійно, це є вашою вказівкою про те, що
> оболонці перенаправити вивід або отримати значення змінної.
{: .callout}

При використанні змінних також
можна брати імена у фігурні дужки, щоб чітко розмежувати імена змінних:
`$filename` еквівалентно `${filename}`, але відрізняється від
`${file}name`. Ви можете зустріти таку форму запису у програмах інших людей.

Ми назвали змінну у цьому циклі `filename` (ім'я файлу)
для того, щоб зробити її призначення більш зрозумілим для читачів-людей.
Самій оболонці байдуже, як називається змінна;
якщо ми напишемо цей цикл наступним чином:

~~~
$ for x in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $x | tail -n 1
> done
~~~
{: .language-bash}

чи:

~~~
$ for temperature in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $temperature | tail -n 1
> done
~~~
{: .language-bash}

це спрацювало б точно так само.
*Не роби цього.*
Програми корисні лише тоді, коли люди можуть їх розуміти,
тому беззмістовні назви (наприклад, `x`) або назви, що вводять в оману (наприклад, `temperature`)
збільшують ймовірність того, що програма не буде робити те, що читачі думають, що вона робить.

У наведених вище прикладах змінним (`thing`, `filename`, `x` та `temperature`)
можна було б назвати будь-якою іншою назвою, аби вона була зрозумілою як для того,
хто пише код, так і для того, хто його читає.

Зауважте також, що цикли можна використовувати для інших речей, окрім імен файлів, наприклад, для списку чисел
або підмножини даних.

> ## Напишіть власний цикл
>
> Як би ви написали цикл, який виводить всі 10 чисел від 0 до 9?
>
> > ## Розв'язання
> >
> > ~~~
> > $ for loop_variable in 0 1 2 3 4 5 6 7 8 9
> > > do
> > >     echo $loop_variable
> > > done
> > ~~~
> > {: .language-bash}
> >
> > ```
> > 0
> > 1
> > 2
> > 3
> > 4
> > 5
> > 6
> > 7
> > 8
> > 9
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

> ## Змінні в циклах
>
> Ця вправа звертається до каталогу `shell-lesson-data/exercise-data/proteins`.
> `ls *.pdb` видає наступний результат:
>
> ~~~
> cubane.pdb ethane.pdb methane.pdb octane.pdb pentane.pdb propane.pdb
> ~~~
> {: .output}
>
> Що виводить наступний код?
>
> ~~~
> $ for datafile in *.pdb
> > do
> >     ls *.pdb
> > done
> ~~~
> {: .language-bash}
>
> Тепер, що виводить наступний код?
>
> ~~~
> $ for datafile in *.pdb
> > do
> >     ls $datafile
> > done
> ~~~
> {: .language-bash}
>
> Чому ці два цикли дають різні результати?
>
> > ## Розв'язання
> > Перший блок коду дає однаковий результат на кожній ітерації
> > циклу.
> > Bash розширює шаблон `*.pdb` в тілі циклу (а також
> > перед початком циклу), щоб знайти всі файли, що закінчуються на `.pdb`.
> > а потім перераховує їх за допомогою `ls`.
> > Розширений цикл матиме такий вигляд:
> > ```
> > $ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > > do
> > >     ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > > done
> > ```
> > {: .language-bash}
> >
> > ```
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > ```
> > {: .output}
> >
> > Другий блок коду перераховує різні файли на кожній ітерації циклу.
> > Значення змінної `datafile` обчислюється за допомогою `$datafile`,
> > а потім перераховується за допомогою `ls`.
> >
> > ```
> > cubane.pdb
> > ethane.pdb
> > methane.pdb
> > octane.pdb
> > pentane.pdb
> > propane.pdb
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

> ## Обмеження набору файлів
>
> Що буде виведено у результаті виконання наступного циклу в каталозі
> `shell-lesson-data/exercise-data/proteins`?>
> ~~~
> $ for filename in c*
> > do
> >     ls $filename
> > done
> ~~~
> {: .language-bash}
>
> 1. Жодної назви файлу не буде виведено.
> 2. Будуть перелічені всі файли.
> 3. Будуть перелічені лише `cubane.pdb`, `octane.pdb` та `pentane.pdb`.
> 4. Буде виведено лише `cubane.pdb`.
>
> > ## Розв'язання
> > 4 - правильна відповідь. Підстановочний символ `*` відповідає нулю або більшій кількості символів, тому будь-яке ім'я файлу, що починається з
> > літери 'c', за якою йдуть нуль або більша кількість символів, підійде.
> {: .solution}
>
> Як зміниться результат, якщо замість неї використати цю команду?
>
> ~~~
> $ for filename in *c*
> > do
> >     ls $filename
> > done
> ~~~
> {: .language-bash}
>
> 1. Будуть перераховані ті ж файли.
> 2. Цього разу перераховані всі файли.
> 3. Цього разу не виведено жодного файла.
> 4. Будуть перераховані файли `cubane.pdb` і `octane.pdb`.
> 5. Буде перераховано лише файл `octane.pdb`.
>
> > ## Розв'язання
> > 4 - правильна відповідь. Підстановочний символ `*` відповідає нулю або більшій кількості символів, тому всі імена файлів з нулем або більшою кількістю
> > символів перед літерою 'c' і нулем або більшою кількістю символів після літери 'c' підійдуть.
> {: .solution}
{: .challenge}

> ## Збереження у файл в циклі - Частина перша
>
> В каталозі `shell-lesson-data/exercise-data/proteins`, який результат роботи цього циклу?
>
> ~~~
> for alkanes in *.pdb
> do
>     echo $alkanes
>     cat $alkanes > alkanes.pdb
> done
> ~~~
> {: .language-bash}
>
> 1. Буде виведено `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` і
> `propane.pdb`, а текст з `propane.pdb` буде збережено у файлі з назвою `alkanes.pdb`.
> 2. Буде виведено `cubane.pdb`, `ethane.pdb` і `methane.pdb`, і текст з усіх трьох файлів
> буде об'єднано і збережено у файл з назвою `alkanes.pdb`.
> 3. Буде виведено `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb` і `pentane.pdb`,
> а текст з `propane.pdb` буде збережено до файлу з назвою `alkanes.pdb`.
> 4. Нічого з перерахованого вище.
>
> > ## Розв'язання
> > 1. Текст з кожного файлу по черзі записується у файл `alkanes.pdb`.
> Однак, файл перезаписується на кожній ітерації циклу, тому кінцевий вміст
> > `alkanes.pdb'
> > буде дорівнювати тексту з файлу `propane.pdb`.
> {: .solution}
{: .challenge}

> ## Збереження у файл в циклі - Частина друга
>
> Також у каталозі `shell-lesson-data/exercise-data/proteins`,
> що буде виведено у наступному циклі?>
> ~~~
> for datafile in *.pdb
> do
>     cat $datafile >> all.pdb
> done
> ~~~
> {: .language-bash}
>
> 1. Весь текст з файлів `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb` та
> `pentane.pdb` буде об'єднано і збережено у файлі з назвою `all.pdb`.
> 2. Текст з файлу `ethane.pdb` буде збережено до файлу з назвою `all.pdb`.
> 3. Весь текст з файлів `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb`
> та `propane.pdb` буде об'єднано та збережено у файл з назвою `all.pdb`.
> 4. Весь текст з файлів `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb`
> і `propane.pdb` буде виведено на екран і збережено у файлі з назвою `all.pdb`.
>
> > ## Розв'язання
> > 3 - правильна відповідь. Оператор `>>` додає вміст до файлу, а не перезаписує його перенаправленим
> > виводом команди.
> > Оскільки вивід команди `cat` було перенаправлено, на екран нічого не буде виведено.
> {: .solution}
{: .challenge}

Давайте продовжимо наш приклад у каталозі `shell-lesson-data/exercise-data/creatures`.
Тут цикл трохи складніший:

~~~
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
~~~
{: .language-bash}

Термінал розпочинає роботу з розгортання `*.dat` для створення списку файлів, які він буде обробляти.
**Тіло циклу**
виконує дві команди для кожного з цих файлів.
Перша команда, `echo`, виводить аргументи командного рядка у стандартний вивід.
Наприклад:

~~~
$ echo hello there
~~~
{: .language-bash}

виводить:

~~~
hello there
~~~
{: .output}

У цьому випадку,
оскільки термінал розширює `$filename` до імені файлу,
`echo $filename` виводить ім'я файлу.
Зауважте, що ми не можемо написати це як:

~~~
$ for filename in *.dat
> do
>     $filename
>     head -n 100 $filename | tail -n 20
> done
~~~
{: .language-bash}

тому що при першому проходженні через цикл,
коли `$filename` розшириться до `basilisk.dat`, оболонка спробує запустити `basilisk.dat`
як програму.
Нарешті,
комбінація `head` і `tail` виділить рядки 81-100
з будь-якого файлу, який обробляється
(за умови, що у відповідному файлі є принаймні 100 рядків).

> ## Пробіли в іменах
>
> Пробіли використовуються для відокремлення елементів списку
> які ми будемо перебирати у циклі. Якщо один з цих елементів
> містить пробіл, нам потрібно взяти його в
> лапки і зробити те ж саме зі змінною циклу.
> Припустимо, що наші файли даних мають імена:
>
> ~~~
> red dragon.dat
> purple unicorn.dat
> ~~~
> {: .source}
>
> Щоб виконати цикл над цими файлами, нам потрібно додати подвійні лапки, ось так:
>
> ~~~
> $ for filename in "red dragon.dat" "purple unicorn.dat"
> > do
> >     head -n 100 "$filename" | tail -n 20
> > done
> ~~~
> {: .language-bash}
>
> Простіше уникати використання пробілів (або інших спеціальних символів) у назвах файлів.
>
> Вищевказані файли не існують, тому якщо ми виконаємо вищенаведений код, команда `head` не зможе
> знайти їх, однак у повідомленні про помилку буде показано назви цих файлів,
> що очікувалися:
>
> ~~~
> head: cannot open ‘red dragon.dat’ for reading: No such file or directory
> head: cannot open ‘purple unicorn.dat’ for reading: No such file or directory
> ~~~
> {: .error}
>
> Спробуйте видалити лапки навколо `$filename` у наведеному вище циклі, щоб побачити ефект лапок
> позначки на пробілах. Зверніть увагу, що ми отримуємо результат команди циклу для unicorn.dat
> коли ми запускаємо цей код у каталозі `creatures`:
>
> ~~~
> head: cannot open ‘red’ for reading: No such file or directory
> head: cannot open ‘dragon.dat’ for reading: No such file or directory
> head: cannot open ‘purple’ for reading: No such file or directory
> CGGTACCGAA
> AAGGGTCGCG
> CAAGTGTTCC
> ...
> ~~~
> {: .output}
{: .callout}

Ми б хотіли змінити кожен з файлів у `shell-lesson-data/exercise-data/creatures`,
але також зберегти версію
оригінальних файлів, назвавши копії `original-basilisk.dat` і `original-unicorn.dat`.
Ми не можемо використовувати:

~~~
$ cp *.dat original-*.dat
~~~
{: .language-bash}

тому що це буде розширено до:

~~~
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
~~~
{: .language-bash}

Це не створить резервну копію наших файлів, натомість ми отримаємо помилку:

~~~
cp: target `original-*.dat' is not a directory
~~~
{: .error}

Ця проблема виникає, коли команда `cp` отримує більше двох входів. Коли це відбувається, вона
очікує, що останнім вхідним параметром буде каталог, куди вона зможе скопіювати всі файли, які їй було передано.
Оскільки у каталозі `creatures` немає каталогу з назвою `original-*.dat`, ми отримаємо
помилку.

Замість цього ми можемо використати цикл:
~~~
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
~~~
{: .language-bash}

Цей цикл виконує команду `cp` один раз для кожного імені файлу.
Перший раз,
коли змінна `$filename` має значення до `basilisk.dat`,
термінал виконає:

~~~
cp basilisk.dat original-basilisk.dat
~~~
{: .language-bash}

У другий раз команда наступна:

~~~
cp minotaur.dat original-minotaur.dat
~~~
{: .language-bash}

В третій, останній раз, команда буде такою:

~~~
cp unicorn.dat original-unicorn.dat
~~~
{: .language-bash}

Оскільки команда `cp` зазвичай не виводить нічого, важко перевірити
що цикл працює правильно.
Однак раніше ми дізналися, як виводити рядки за допомогою `echo`, і ми можемо модифікувати цикл
щоб використовувати `echo` для виведення наших команд без їхнього виконання.
Таким чином, ми можемо перевірити, які команди виконувалися *би* у немодифікованому циклі.

Наступна діаграма
показує, що відбувається при виконанні модифікованого циклу, і демонструє, як
розумне використання `echo` є гарною технікою зневадження.

![Цикл for "for filename in *.dat; do echo cp $filename original-$filename;
done" послідовно присвоїть змінній "$filename" імена всіх "*.dat" файлів у вашому поточному
каталозі змінній "$filename" та після цього виконає команду. Для
файлів "basilisk.dat", "minotaur.dat" та "unicorn.dat" в поточному каталозі
цикл тричі послідовно викличе команду echo і виведе три
рядки: "cp basislisk.dat original-basilisk.dat", потім "cp minotaur.dat
original-minotaur.dat" та нарешті "cp unicorn.dat
original-unicorn.dat"](../fig/shell_script_for_loop_flow_chart.svg)

## Конвеєр Неллі: Обробка файлів

Тепер Неллі готова обробити свої файли даних за допомогою `goostats.sh` ---
скрипта терміналу, написаного її керівником.
Він обчислює деякі статистичні дані з файлу зразка білка і приймає два аргументи:

1. вхідний файл (що містить вихідні дані)
2. вихідний файл (для збереження розрахованої статистики)

Оскільки вона все ще вчиться користуватися терміналом,
вона вирішує створювати необхідні команди поетапно.
Першим кроком буде переконатися, що вона може вибирати правильні вхідні файли - запам'ятайте,
це ті, назви яких закінчуються на 'A' або 'B', а не на 'Z'.
Починаючи з домашнього каталогу, Неллі набирає:

~~~
$ cd north-pacific-gyre
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile
> done
~~~
{: .language-bash}

~~~
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
NENE02043A.txt
NENE02043B.txt
~~~
{: .output}

Наступним кроком буде вирішити
як назвати файли, які створить програма аналізу `goostats.sh`.
Додавання до імені кожного вхідного файлу префікса "stats" здається простим,
тому вона модифікує свій цикл для цього:

~~~
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile stats-$datafile
> done
~~~
{: .language-bash}

~~~
NENE01729A.txt stats-NENE01729A.txt
NENE01729B.txt stats-NENE01729B.txt
NENE01736A.txt stats-NENE01736A.txt
...
NENE02043A.txt stats-NENE02043A.txt
NENE02043B.txt stats-NENE02043B.txt
~~~
{: .output}

Насправді, вона ще не запускала `goostats.sh`,
але тепер вона впевнена, що може вибрати правильні файли і згенерувати правильні назви вихідних файлів.

Введення команд знову і знову стає нудним,
і Неллі хвилюється через можливі помилки,
тож замість того, щоб перенабирати свій цикл,
вона натискає <kbd>↑</kbd>.
У відповідь
оболонка відобразить весь цикл в одному рядку
(використовуючи крапку з комою для розділення частин):

~~~
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile stats-$datafile; done
~~~
{: .language-bash}

За допомогою клавіші зі стрілкою ліворуч,
Неллі створює резервну копію і змінює команду `echo` на `bash goostats.sh`:

~~~
$ for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
~~~
{: .language-bash}

Коли вона натискає <kbd>Enter</kbd>,
термінал виконає змінену команду.
Однак, здається, нічого не відбувається - немає ніякого виводу.
За мить Неллі розуміє, що оскільки її скрипт більше нічого не виводить на екран,
вона не має жодного уявлення про те, чи виконується він, а тим паче, як швидко.
Вона перериває команду виконання, набравши <kbd>Ctrl</kbd>+<kbd>C</kbd>,
використовує <kbd>↑</kbd> для повтору команди,
і редагує її, щоб читати:

~~~
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile;
bash goostats.sh $datafile stats-$datafile; done
~~~
{: .language-bash}

> ## Початок і кінець
>
> Перехід на початок рядка в оболонці здійснюється за допомогою комбінації клавіш <kbd>Ctrl</kbd>+<kbd>A</kbd>
> і в кінець рядка - за допомогою <kbd>Ctrl</kbd>+<kbd>E</kbd>.
{: .callout}

Коли вона запускає свою програму зараз,
програма виводить один рядок кожні п'ять секунд або близько того:

~~~
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
~~~
{: .output}

Значення 1518, помножене на 5 секунд,
поділене на 60,
каже їй, що її сценарій буде виконуватися близько двох годин.
Для остаточної перевірки
вона відкриває інше вікно терміналу,
переходить в `north-pacific-gyre`,
і використовує `cat stats-NENE01729B.txt`.
для перевірки одного з вихідних файлів.
Виглядає добре,
тож вона вирішує випити кави і продовжити читання.

> ## Хто знає історію, той може її повторити
>
> Інший спосіб повторити попередню роботу - скористатися командою `history`, щоб
> отримати список останніх кількох сотень команд, які було виконано, і
> потім скористатися командою `!123` (де "123" замінено на номер команди), щоб
> повторити одну з цих команд. Наприклад, якщо Неллі набере наступне:
>
> ~~~
> $ history | tail -n 5
> ~~~
> {: .language-bash}
> ~~~
>   456  ls -l NENE0*.txt
>   457  rm stats-NENE01729B.txt.txt
>   458  bash goostats.sh NENE01729B.txt stats-NENE01729B.txt
>   459  ls -l NENE0*.txt
>   460  history
> ~~~
> {: .output}
>
> тоді вона може перезапустити `goostats.sh` на `NENE01729B.txt`, просто набравши
> `!458`.
{: .callout}

> ## Інші команди історії
>
> Існує ряд інших команд швидкого доступу до історії.
>
> - <kbd>Ctrl</kbd>+<kbd>R</kbd> переходить у режим "зворотного пошуку" в історіїі і знаходить
> останню команду у вашому журналі, яка відповідає тексту, що ви введете далі.
> Натисніть<kbd>Ctrl</kbd>+<kbd>R</kbd> ще один або кілька додаткових разів для пошуку більш ранніх збігів.
> За допомогою клавіш зі стрілками вліво і вправо виберіть цей рядок і відредагуйте
> його, потім натисніть <kbd>Return</kbd> щоб виконати команду.
> - `!!` повертає безпосередньо попередню команду
> (ви можете знайти це більш зручним, ніж використання <kbd>↑</kbd>)
> - `!$` повертає останнє слово останньої команди.
> Це корисно частіше, ніж ви можете собі уявити: після
> `bash goostats.sh NENE01729B.txt stats-NENE01729B.txt`, ви можете ввести
> `less !$` для перегляду файлу `stats-NENE01729B.txt`, що
> швидше, ніж набирати <kbd>↑</kbd> і редагувати командний рядок.
{: .callout}

> ## Виконання пробного запуску
>
> Цикл - це спосіб зробити багато речей одночасно --- або зробити багато помилок
> одночасно, якщо він робить неправильні речі. Один зі способів перевірити, що *робив би* цикл
> це за допомогою `echo` виводити команди, які він виконуватиме, замість того, щоб виконувати їх насправді.
>
> Припустимо, ми хочемо переглянути команди, які виконає наступний цикл
> без виконання цих команд:
>
> ~~~
> $ for datafile in *.pdb
> > do
> >     cat $datafile >> all.pdb
> > done
> ~~~
> {: .language-bash}
>
> У чому різниця між двома наведеними нижче циклами, і який з них ми
> хочемо запустити?
>
> ~~~
> # Варіант 1
> $ for datafile in *.pdb
> > do
> >     echo cat $datafile >> all.pdb
> > done
> ~~~
> {: .language-bash}
>
> ~~~
> # Варіант 2
> $ for datafile in *.pdb
> > do
> >     echo "cat $datafile >> all.pdb"
> > done
> ~~~
> {: .language-bash}
>
> > ## Розв'язання
> > Друга версія - це та, яку ми хочемо запустити.
> > Вона виводить на екран усе, що укладено у лапки, розширюючи
> > назву змінної циклу, оскільки ми додали до неї знак долара.
> > Він також *не* змінює і не створює файл `all.pdb`, оскільки оператор `>>`
> > розглядається буквально як частина рядка, а не як
> > інструкція перенаправлення.
> >
> > Перша версія додає вивід команди `echo cat $datafile`
> > до файлу `all.pdb`. Цей файл міститиме лише список
> > `cat cubane.pdb`, `cat ethane.pdb`, `cat methane.pdb` тощо.
> >
> > Спробуйте обидві версії, щоб побачити результат! Обов'язково відкрийте
> > файл `all.pdb`, щоб переглянути його вміст.
> {: .solution}
{: .challenge}

> ## Вкладені цикли
>
> Припустімо, що ми хочемо створити структуру каталогів для організації
> певних експериментів з вимірювання констант швидкості реакції з різними сполуками
> *та* різними температурами. Яким буде
> результат виконання наступного коду:
>
> ~~~
> $ for species in cubane ethane methane
> > do
> >     for temperature in 25 30 37 40
> >     do
> >         mkdir $species-$temperature
> >     done
> > done
> ~~~
> {: .language-bash}
>
> > ## Розв'язання
> > Ми маємо вкладений цикл, тобто такий, що міститься в іншому циклі, тому для кожного значення змінної species
> > у зовнішньому циклі внутрішній цикл (вкладений цикл) перебирає список
> > температур і створює новий каталог для кожної комбінації.
> >
> > Спробуйте запустити код самостійно, щоб побачити, які каталоги буде створено!
> {: .solution}
{: .challenge}

{% include links.md %}
