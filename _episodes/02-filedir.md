---
title: "Навігація файлами та каталогами"
teaching: 30
exercises: 10
questions:
- "Як я можу переміщатися на моєму комп'ютері?"
- "Як я можу побачити, які файли та каталоги у мене є?"
- "Як вказати місцезнаходження файлу або каталогу на комп'ютері?"
objectives:
- "Пояснити подібності та відмінності між файлом і каталогом".
- "Перетворити абсолютний шлях у відносний і навпаки".
- "Створити абсолютні та відносні шляхи, які ідентифікують певні файли та каталоги".
- "Використати опції та аргументи для зміни поведінки команди оболонки".
- "Продемонструвати використання завершення вкладки та пояснити його переваги".
keypoints:
- "Файлова система відповідає за керування інформацією на диску".
- "Інформація зберігається у файлах, які зберігаються в каталогах (папках)".
- "У каталогах також можуть зберігатися інші каталоги, які потім утворюють дерево каталогів".
- "Команда `pwd` виводить поточний робочий каталог користувача."
- "Команда `ls [шлях]` виводить список певного файлу або каталогу; Команда `ls` сама по собі виводить список поточного робочого каталогу."
- "Команда `cd [шлях]` змінює поточний робочий каталог."
- "Більшість команд приймають параметри, які починаються з одного символу `-`."
- "Назви каталогів у шляху розділяються символами `/` у Unix, але `\\` у Windows."
- "Символ `/` сам по собі є кореневим каталогом усієї файлової системи."
- "Абсолютний шлях вказує на розташування від кореня файлової системи."
- "Відносний шлях вказує на розташування, починаючи з поточного розташування."
- "Символ `.` сам по собі означає "поточний каталог"; `..` означає "каталог вище поточного", "батьківський каталог".
---

Частина операційної системи, яка відповідає за роботу з файлами та директоріями,
називається **файлова система**.
Вона організує наші дані у вигляді файлів,
які містять інформацію,
та директорій (їх ще називають 'каталогами'),
які містять файли або інші директорії.

Декілька команд часто використовуються для створення, перевірки, перейменування та видалення файлів та директорій.
Для початку їх огляду, перейдемо до нашого відкритого вікна терміналу.

По-перше, давайте дізнаємося, де ми знаходимося, шляхом виконання команди `pwd`
(англ. 'print working directory' - надрукувати робочу директорію). Директорії — це немов *місця* — будь-коли
під час використання терміналу ми знаходимось в якомусь одному конкретному місці, яке називається
нашою **поточною робочою директорією**. Команди здебільшого читають вміст файлів та пишуть до них в
поточній робочій директорії, тобто 'тут', отже розуміння того, де ви знаходитесь, перед запуском
команди є важливим. Команда `pwd` покаже вам, де ви знаходитесь:

~~~
$ pwd
~~~
{: .language-bash}

~~~
/Users/nelle
~~~
{: .output}

У наведеному прикладі
комп'ютер відповів `/Users/nelle`,
що є **домашньою директорією** Неллі:

> ## Варіації домашнього каталогу
> 
> Розташування домашньої директорії виглядає по-різному в різних операційних системах.
> В Linux воно може виглядати як `/home/nelle`,
> а у Windows воно буде схоже на `C:\Documents and Settings\
elle` чи
> `C:\Users\
elle`.
> (Зауважте, що воно може виглядати дещо інакше для різних версій Windows.)
> У майбутніх прикладах ми використовували формат виводу Mac як стандартний – формати виводу Linux та Windows
> можуть дещо відрізнятися, але загалом мають бути подібними.
> Ми також припустимо, що ваша команда `pwd` повертає вашу домашню директорію користувача.
> Якщо команда `pwd` повертає щось інше, вам може знадобитися перейти туди за допомогою команди `cd`,
> інакше деякі команди в цьому уроці не будуть працювати як описано.
> Дивись [Огляд інших каталогів](#exploring-other-directories), щоб дізнатися більше
> про команду `cd`.{: .callout}

Для того, щоб зрозуміти, що таке 'домашній каталог',
давайте подивимось, як організована файлова система в цілому. Для
цього прикладу ми
проілюструємо файлову систему на комп’ютері нашої вченої Неллі. Після цієї
ілюстрації ви вивчатимете команди для дослідження власної файлової системи,
яка буде побудовані подібним чином, але не буде абсолютно ідентичною.

На комп’ютері Неллі файлова система виглядає так:

![Файлова система складається з кореневого каталогу, який містить підкаталоги
під назвами bin, data, users та tmp](../fig/filesystem.svg)

У верхній частині знаходиться **кореневий каталог**,
який містить усе інше.
Ми виконуємо посилання на нього за допомогою символу косої риски, `/`;
цей символ - це перший (лівий) символ у рядку `/Users/nelle`.

Усередині цього каталогу є кілька інших каталогів:
`bin` (в якому зберігаються певні вбудовані програми),
`data` (для різноманітних файлів даних),
`Users` (де знаходяться особисті директорії користувачів),
`tmp` (для файлів тимчасового зберігання)
та інші.

Ми знаємо, що наш поточний робочий каталог `/Users/nelle` зберігається всередині каталогу `/Users`,
тому що `/Users` є першою частиною його імені.
Відповідно,
ми знаємо, що каталог `/Users` зберігається всередині кореневої директорії `/`,
бо його ім'я розпочинається з `/`.

> ## Символи скісної риски
> 
> Зверніть увагу, що символ `/` має два значення.
> Коли він з’являється на початку назви файлу чи каталогу,
> це посилання на кореневу директорію. Коли він використовується *всередині* шляху,
> це лише роздільник.
{: .callout}

Під `/Users`
ми знайдемо по одній директорії для кожного користувача на машині Неллі:
її колег *imhotep* та *larry*.

![Як і інші каталоги, домашні каталоги є підкаталогами
"/Users", наприклад "/Users/imhotep", "/Users/larry" або
"/Users/nelle"](../fig/home-directories.svg)

Файли користувача *imhotep* зберігаються в директорії `/Users/imhotep`,
користувача *larry* - в `/Users/larry`,
і Неллі - в `/Users/nelle`. Оскільки саме Неллі є користувачем у наших
прикладах, тому ми отримуємо `/Users/nelle` як наш домашній каталог.
Як правило, коли ви відкриваєте новий командний рядок, ви опиняєтесь в
вашому домашньому каталозі.

Тепер давайте вивчимо команду, яка дозволить нам бачити вміст нашої
власної файлової системи. Ми можемо побачити, що знаходиться в нашому домашньому каталозі, запустивши `ls`:

~~~
$ ls
~~~
{: .language-bash}

~~~
Applications Documents    Library      Music        Public
Desktop      Downloads    Movies       Pictures
~~~
{: .output}

(Знову ж таки, ваші результати можуть дещо відрізнятися залежно від вашої операційної
системи та того, як ви налаштували свою файлову систему.)

`ls` друкує назви файлів і каталогів у поточному каталозі.
Ми можемо зробити його вивід більш зрозумілим, використовуючи **опцію** `-F`
який повідомляє `ls` про необхідність класифікації виводу
шляхом додавання маркера до імен файлів і каталогів, щоб вказати, що вони собою представляють:
- символ `/` наприкінці назви вказує на те, що це каталог
- `@` вказує на посилання
- `*` вказує на виконуваний файл

Залежно від налаштувань терміналу за замовчуванням,
в терміналі також можуть бути використані кольори, щоб вказати, чи є кожен елемент файлом або
каталогом.

~~~
$ ls -F
~~~
{: .language-bash}

~~~
Applications/ Documents/    Library/      Music/        Public/
Desktop/      Downloads/    Movies/       Pictures/
~~~
{: .output}

В наведеному прикладі
ми бачимо, що наш домашній каталог містить лише **підкаталоги**.
Будь-які імена в наших результатах, які не мають символу класифікації
відповідають звичайним старим **файлам**.

> ## Очищення терміналу
>
> Якщо екран стає занадто захаращеним, ви можете очистити термінал за допомогою
> команди `clear`. Ви все ще можете отримати доступ до попередніх команд за допомогою клавіш <kbd>↑</kbd>
> та <kbd>↓</kbd> щоб переміщатися рядок за рядком, або за допомогою прокрутки у вашому терміналі.
{: .callout}

### Отримання допомоги

У `ls` є багато інших **опцій**. Існує два поширених способи дізнатися, як
використовувати команду і які параметри вона приймає ---
**залежно від вашого середовища, ви можете виявити, що працює лише один із цих способів:**.

1. Ми можемо передати команді опцію `--help` (доступну в Linux і Git Bash), наприклад:
    ~~~
    $ ls --help
    ~~~
    {: .language-bash}

2. Ми можемо прочитати інструкцію до використання команди за допомогою `man` (доступно на Linux і macOS), наприклад:
    ~~~
    $ man ls
    ~~~
    {: .language-bash}

Далі ми опишемо обидва способи.

#### Опція `--help'

Більшість команд bash і програм, які люди написали для того, щоб їх можна було
запускати з bash, підтримують опцію `--help`, яка виводить додаткову
інформацію про те, як користуватися відповідною командою або програмою.

~~~
$ ls --help
~~~
{: .language-bash}

~~~
Використання: ls [ПАРАМЕТР]... [ФАЙЛ]...
Виводить дані щодо ФАЙЛів (типово у поточному каталозі).
Впорядковує у алфавітному порядку, якщо не вказано ні --sort, ні один з
параметрів -cftuSUX.

Обов'язкові аргументи для довгих форм запису параметрів є обов'язковими і для ск орочених форм.
  -a, --all                  не ігнорувати записи, що починаються з .
  A, --almost-all           не виводити неявні . і ..
      --author               разом з -l, виводити автора кожного файла
  -b, --escape               виводити вісімкові керівні послідовності
                             замість неграфічних знаків
      --block-size=РОЗМІР    якщо вкзаано -l, використовувати блоки розміром РОЗМІР.

                               Наприклад, «--block-size=M». Формат РОЗМІРу наведено
                               нижче.
  -B, --ignore-backups       не виводити файли, що закінчуються на ~
  -c                         з -lt: сортувати за часом зміни; з -l:
                              виводити час зміни та впорядкувати за назвою,
                              у іншому випадку впорядкувати за часом зміни,
                              найновіші — перші
  -C                     виводити список у декілька колонок
      --color[=КОЛИ]                     вказує, чи позначати типи файлів кольором.
                               КОЛИ може бути «never», «auto» або
                               «always» (типовий, якщо не вказано)
  -d, --directory            виводити назви каталогів, а не їх зміст, а
                              також не слідувати за символічним посиланням
  -D, --dired                 створити виведені дані у режимі Emacs dired
  -f                         не сортувати, вмикає -aU, вимикає -lst
  -F, --classify             додавати до назви індикатор (один з */=>@|)...        ...        ...
~~~
{: .output}

> ## Непідтримувані параметри командного рядка
> Якщо ви спробуєте використати параметр, який не підтримується, `ls` та інші команди
> зазвичай виводитимуть повідомлення про помилку, схоже на:
>
> ~~~
> $ ls -j
> ~~~
> {: .language-bash}
>
> ~~~
> ls: invalid option -- 'j'
> Try 'ls --help' for more information.
> ~~~
> {: .error}
{: .callout}

#### Команда `man`

Інший спосіб дізнатися про `ls` -- це ввести
~~~
$ man ls
~~~
{: .language-bash}

Ця команда перетворить ваш термінал на сторінку з описом
команди `ls` та її параметрів.

Для навігації по сторінках `man`,
ви можете використовувати <kbd>↑</kbd> і <kbd>↓</kbd> для переміщення рядок за рядком,
або клавіші <kbd>B</kbd> та <kbd>Пробіл</kbd> для переходу вгору і вниз на цілу сторінку.
Для пошуку символу або слова на сторінках `man`,
використовуйте клавішу <kbd>/</kbd>, за фкою введіть символ або слово, яке ви шукаєте.
Іноді пошук може призвести до кількох результатів.
У такому випадку ви можете переміщатися між результатами за допомогою клавіш <kbd>N</kbd> (для переміщення вперед) та
<kbd>Shift</kbd>+<kbd>N</kbd> (для переходу назад).

Для **виходу** зі сторінок `man` натисніть <kbd>Q</kbd>.

## Сторінки з інструкціями в Інтернеті
>
> Звісно, є й третій спосіб отримати доступ до довідки до команд:
> пошук в інтернеті за допомогою веб-браузера.
> Якщо ви скористаєтеся пошуком у Інтернеті, додання до запиту фрази `unix man page`
> дозволить отримати більш відповідні результати.
>
GNU надає посилання на свої
> [посібники].(http://www.gnu.org/manual/manual.html), в тому числі на
> [основні утиліти GNU](http://www.gnu.org/software/coreutils/manual/coreutils.html),
> які охоплюють багато команд, представлених у цьому уроці.
{: .callout}

> ## Вивчення більше `ls` опцій
>
> Ви також можете використовувати декілька опцій одночасно. Що робить команда `ls` при використанні
> з опцією `-l`? А якщо ви використовуєте і `-l`, і `-h`?
>
> Деякі з результатів виконання команди стосуються властивостей, які ми не розглядаємо у цьому уроці (наприклад,
> права доступу до файлів і права власності), але решта має бути корисною
> тим не менш.
>
> > ## Розв'язання
> > Опція `-l` змушує `ls` використовувати довгий (англ. **l**ong) формат лістингу, показуючи не лише
> > назви файлів/директорій, але й додаткову інформацію, таку як розмір файлу
> > і час його останньої модифікації. Якщо ви використовуєте як `-h`, так і `-l`,
> > це зробить виведення розміру файлу у більш зрозумілому людині вигляді ("**h**uman readable"), тобто покаже щось на кшталт `5.3K`.
> > замість `5369`.
> {: .solution}
{: .challenge}

> ## Виведення у зворотному хронологічному порядку
>
> За замовчуванням `ls` виводить вміст каталогу в алфавітному
> порядку за іменами елементів. Команда `ls -t` перелічує елементи за часом останньої
> зміни, а не за алфавітом. Команда `ls -r` виводить
> вміст каталогу у зворотному порядку.
> Який файл буде показано останнім при комбінації команд `-t` і `-r`?
> Підказка: Вам може знадобитися скористатися опцією `-l`, щоб переглянути
> дати останніх змін.
>
> > ## Рішення
> > При використанні `-rt` останній змінений файл відображається останнім у списку. Це
> > може бути дуже корисним для пошуку ваших останніх редагувань або перевірки
> > чи було створено новий вихідний файл.
> {: .solution}
{: .challenge}

### Огляд інших каталогів

Ми можемо використовувати `ls` не лише у поточному робочому каталозі,
але ми також можемо використовувати його для виведення вмісту іншого каталогу.
Давайте подивимося на наш каталог `Desktop` (робочий стіл), виконавши `ls -F Desktop`,
тобто,
команду `ls` з `-F` **опцією** і [**аргументом**] [Arguments] `Desktop`.
Аргумент `Desktop` повідомляє `ls`, що
ми хочемо отримати список чогось іншого, ніж наш поточний робочий каталог:

~~~
$ ls -F Desktop
~~~
{: .language-bash}

~~~
shell-lesson-data/
~~~
{: .output}

Зауважте, що якщо у вашому поточному робочому каталозі не існує каталогу з назвою `Desktop`,
ця команда поверне помилку. Зазвичай, каталог `Desktop` існує у вашому
домашньому каталозі, який ми вважаємо поточним робочим каталогом вашого терміналу bash.

На виході ви маєте отримати список усіх файлів і підкаталогів у вашому
каталозі Desktop, включно з каталогом `shell-lesson-data`, який ви завантажили за посиланням
під час [налаштування цього уроку]({{ page.root }}{% link setup.md %}).
У багатьох системах
каталог Desktop командного рядка збігається з каталогом Desktop вашого графічного інтерфейсу.
Подивіться на свій робочий стіл, щоб переконатися у правильності виведених даних.

Як ви тепер бачите, використання терміналу bash сильно залежить від того, що
ваші файли організовано в ієрархічній файловій системі.
Ієрархічна організація речей таким чином допомагає нам відстежувати нашу роботу:
у нашому домашньому каталозі можуть бути сотні файлів,
так само, як можна скласти сотні роздрукованих паперів на столі,
але це самогубна стратегія.

Тепер, коли ми знаємо, що каталог `shell-lesson-data` розташовано у каталозі Desktop, ми
можемо зробити дві речі.

По-перше, ми можемо переглянути його вміст, використовуючи ту ж стратегію, що і раніше, передавши
ім'я каталогу в `ls`:

~~~
$ ls -F Desktop/shell-lesson-data
~~~
{: .language-bash}

~~~
exercise-data/  north-pacific-gyre/
~~~
{: .output}

По-друге, ми можемо фактично змінити наше місцезнаходження на інший каталог, щоб
ми більше не знаходилися в
в нашому домашньому каталозі.

Команда зміни розташування в файловій системі має вигляд `cd`, за якою зазначається
ім'я каталогу, на який треба змінити наш робочий каталог.
`cd` означає 'змінити каталог' (англ. 'change directory'),
що трохи вводить в оману:
команда не змінює каталог;
вона змінює поточний робочий каталог терміналу.
Іншими словами, вона змінює уявлення терміналу про те, у якому каталозі ми перебуваємо.
Команда `cd` подібна до подвійного кліку на каталозі у графічному інтерфейсі, щоб потрапити до нього.

Припустимо, ми хочемо перейти до каталогу `exercise-data`, який ми бачили вище. Ми можемо
скористатися наступною серією команд, щоб дістатися туди:

~~~
$ cd Desktop
$ cd shell-lesson-data
$ cd exercise-data
~~~
{: .language-bash}

Ці команди перемістять нас з домашнього каталогу до каталогу Desktop, потім до
каталогу `shell-lesson-data`, а потім до каталогу `exercise-data`.
Ви помітите, що команда `cd` нічого не виводить. Це нормально.
Багато команд терміналу нічого не виводять на екран у разі успішного виконання.
Але якщо ми виконаємо `pwd` після неї, то побачимо, що зараз ми знаходимося
у `/Users/nelle/Desktop/shell-lesson-data/exercise-data`.

Якщо ми зараз виконаємо команду `ls -F` без аргументів,
вона виведе вміст `/Users/nelle/Desktop/shell-lesson-data/exercise-data`,
тому що саме там ми зараз знаходимося:

~~~
$ pwd
~~~
{: .language-bash}

~~~
/Users/nelle/Desktop/shell-lesson-data/exercise-data
~~~
{: .output}

~~~
$ ls -F
~~~
{: .language-bash}

~~~
animal-counts/  creatures/  numbers.txt  proteins/  writing/
~~~
{: .output}

Тепер ми знаємо, як спускатися вниз по дереву каталогів (тобто, як увійти до підкаталогу),
але як піднятися вгору (тобто як вийти з каталогу і перейти до його батьківського каталогу)?
Ми можемо спробувати наступне:

~~~
$ cd shell-lesson-data
~~~
{: .language-bash}

~~~
-bash: cd: shell-lesson-data: No such file or directory
~~~
{: .error}

Але ми отримуємо помилку! Чому?

За допомогою наших методів, використовуваних до цього,
`cd` може бачити лише підкаталоги у вашому поточному каталозі. Існують
різні способи перегляду каталогів над вашим поточним розташуванням; ми почнемо
з найпростішого.

В терміналі є скорочення для переходу на один рівень каталогу вгору,
який виглядає так:

~~~
$ cd ..
~~~
{: .language-bash}

`..` -- це спеціальне ім'я каталогу, що означає
"каталог, що містить цей",
або більш стисло,
**батько** поточного каталогу.
Звичайно,
якщо ми запустимо `pwd` після виконання `cd ..`, ми знову у `/Users/nelle/Desktop/shell-lesson-data`:

~~~
$ pwd
~~~
{: .language-bash}

~~~
/Users/nelle/Desktop/shell-lesson-data
~~~
{: .output}

Спеціальний каталог `..` зазвичай не з'являється, коли ми запускаємо `ls`. Якщо ми хочемо
відобразити його, ми можемо додати опцію `-a` до `ls -F`:

~~~
$ ls -F -a
~~~
{: .language-bash}

~~~
./  ../  exercise-data/  north-pacific-gyre/
~~~
{: .output}

`-a` означає 'показати все' (англ. show all) (включно з прихованими файлами);
опція змушує `ls` показувати нам імена файлів і каталогів, які починаються з `.`,
наприклад, `..` (яке, якщо ми знаходимося у `/Users/nelle`, вказує на каталог `/Users`).
Як ви можете бачити,
команда також показує ще один спеціальний каталог, який називається `.`,
що означає 'поточний робочий каталог'.
Може здатися, що це дещо надлишково - мати для нього ім'я,
але незабаром ми побачимо, як воно може бути використано.

Зауважте, що у більшості інструментів командного рядка можна комбінувати декілька параметрів
за допомогою одного `-` і без пробілів між параметрами: `ls -F -a` є
еквівалентним до `ls -Fa`.

> ## Інші приховані файли
>
> Крім прихованих каталогів `..` і `.`, ви також можете побачити файл
> який називається `.bash_profile`. Цей файл зазвичай містить конфігурацію терміналу
> Ви також можете побачити інші файли і каталоги, що починаються
> з `.`. Зазвичай це файли і каталоги, які використовуються для налаштування
> різних програм на вашому комп'ютері. Префікс `.` використовується для того, щоб ці
> конфігураційні файли не захаращували термінал, коли використовується стандартна команда `ls`.
{: .callout}

Ці три команди є основними командами для навігації по файловій системі на вашому комп'ютері:
`pwd`, `ls` і `cd`. Давайте розглянемо деякі варіації цих команд. Що станеться
якщо ви введете команду `cd` саму по собі, без зазначення
каталогу?

~~~
$ cd
~~~
{: .language-bash}

Як ви можете перевірити, що сталося? Команда `pwd` дає нам відповідь!

~~~
$ pwd
~~~
{: .language-bash}

~~~
/Users/nelle
~~~
{: .output}

Виявляється, `cd` без аргументу поверне вас до домашнього каталогу,
що дуже зручно, якщо ви загубилися у власній файловій системі.

Спробуємо повернутися до каталогу `exercise-data` з попереднього. Минулого разу ми використовували
три команди, але насправді ми можемо поєднати перелік каталогів
для переходу до каталогу `exercise-data` за один крок:

~~~
$ cd Desktop/shell-lesson-data/exercise-data
~~~
{: .language-bash}

Переконайтеся, що ми перемістилися в потрібне місце, виконавши `pwd` і `ls -F`.

Якщо ми хочемо перейти на один рівень вище від каталогу даних, ми можемо використати `cd ..`. Але
існує інший спосіб переміщення до будь-якого каталогу, незалежно від вашого
поточного розташування.

Дотепер, коли ми вказували імена каталогів або навіть шлях до каталогів (як описано вище),
ми використовували **відносні шляхи**. Коли ви використовуєте відносний шлях за допомогою команди
на кшталт `ls` або `cd`, вона намагається знайти це місце з того місця, де ми перебуваємо,
а не з кореня файлової системи.

Втім, можна зазначити **абсолютний шлях** до каталогу за допомогою
включивши до нього повний шлях від кореневого каталогу, який позначається символом
скісної риски (слешу). Символ `/` на початку абсолютного шляху вказує комп'ютеру йти за шляхом від
кореня файлової системи, тому він завжди вказує лише на один і той самий каталог,
незалежно від того, де ми знаходимося під час виконання команди.

Це дає змогу перейти до каталогу `shell-lesson-data` з будь-якого місця у файловій системі
файлової системи (у тому числі з каталогу `exercise-data`). Щоб знайти абсолютний шлях
ми можемо скористатися `pwd`, а потім витягти потрібний нам фрагмент,
шоб перейти до `shell-lesson-data`.

~~~
$ pwd
~~~
{: .language-bash}

~~~
/Users/nelle/Desktop/shell-lesson-data/exercise-data
~~~
{: .output}

~~~
$ cd /Users/nelle/Desktop/shell-lesson-data
~~~
{: .language-bash}

Виконайте `pwd` і `ls -F`, щоб переконатися, що ми знаходимося в потрібному каталозі.

> ## Ще два скорочення
>
> Термінал інтерпретує символ тильди (`~`) на початку шляху як
> "домашній каталог поточного користувача". Наприклад, якщо домашнім каталогом користувача Неллі
> є каталог `/Users/nelle`, то `~/data` еквівалентно
> `/Users/nelle/data`. Це працює лише у випадку, якщо це перший символ у
> шляху: `here/there/~/elsewhere` *не* дорівнює `here/there/Users/nelle/elsewhere`.
>
> Іншим скороченням є символ `-` (тире). `cd` транслює `-` у
> *попередній каталог, у якому я був*, що швидше, ніж запам'ятовувати,
> а потім набирати повний шлях. Це *дуже* ефективний спосіб переміщення
> *вперед і назад між двома каталогами* - тобто, якщо ви виконаєте `cd -` двічі,
> ви повернетесь до початкового каталогу.
>
> Різниця між `cd ..` і `cd -` полягає в тому,
> що перший повертає вас *вгору*, тоді як другий повертає вас *назад*.
>
> ----
> Спробуйте!
> Спочатку перейдіть до `~/Desktop/shell-lesson-data` (ви вже маєте бути там).
> ~~~
> $ cd ~/Desktop/shell-lesson-data
> ~~~
> {: .language-bash}
>
> Потім `cd` у каталог `exercise-data/creatures`.
> ~~~
> $ cd exercise-data/creatures
> ~~~
> {: .language-bash}
>
> Тепер, якщо ви виконаєте
> ~~~
> $ cd -
> ~~~
> {: .language-bash}
> ви побачите, що повернулися до `~/Desktop/shell-lesson-data`.
> Запустіть `cd -` ще раз і ви повернетесь до `~/Desktop/shell-lesson-data/exercise-data/creatures`.
{: .callout}

> ## Абсолютні та відносні шляхи
>
> Починаючи з `/Users/amanda/data`,
> яку з наведених нижче команд Аманда може використати для переходу до свого домашнього каталогу,
> тобто `/Users/amanda`?
>
> 1. `cd .`
> 2. `cd /`
> 3. `cd /home/amanda`.
> 4. `cd ../..`
> 5. `cd ~`
> 6. `cd home`
> 7. `cd ~/data/..`
> 8. `cd`
> 9. `cd ..`
>
> > ## Розв'язання
> > 1. Ні: скорочення `.` означає поточний каталог.
> > 2. Ні: скорочення `/` означає кореневий каталог.
> > 3. Ні: домашнім каталогом Аманди є `/Users/amanda`.
> > 4. Ні: ця команда піднімається на два рівні, тобто закінчується на `/Users`.
> > 5. Так: скорочення `~` позначає домашній каталог користувача, у цьому випадку `/Users/amanda`.
> > 6. Ні: ця команда виконає перехід до каталогу `home` у поточному каталозі
> > якщо він існує.
> > 7. Так: надмірно складна, але правильна.
> > 8. Так: комбінація клавіш для повернення до домашнього каталогу користувача.
> > 9. Так: піднімається на один рівень.
> {: .solution}
{: .challenge}

> ## Розв'язання відносного шляху
>
> Використовуючи наведену нижче схему файлової системи, якщо `pwd` показує `/Users/thing`,
> що покаже команда `ls -F ../backup`?
>
> 1. `../backup: Не існує такого файлу або каталогу`
> 2. `2012-12-01 2013-01-08 2013-01-27`
> 3. `2012-12-01/ 2013-01-08/ 2013-01-27/`
> 4. `original/ pnas_final/ pnas_sub/`
>
> ![Дерево каталогів під каталогом Users, де "/Users" містить
каталоги "backup" і "thing"; "/Users/backup" містить "original",
"pnas_final" та "pnas_sub"; "/Users/thing" містить "backup"; та
"/Users/thing/backup" містить "2012-12-01", "2013-01-08" та
"2013-01-27"](../fig/filesystem-challenge.svg)
>
> > Розв'язання
> > 1. Ні: у каталозі `/Users` існує каталог `backup`.
> > 2. Ні: це вміст каталогу `Users/thing/backup`,
> > але за допомогою `..` ми просили піднятися на один рівень вище.
> > 3. Ні: див. попереднє пояснення.
> > 4. Так: `../backup/` вказує на `/Users/backup/`.
> {: .solution}
{: .challenge}

> ## Розуміння прочитаного про команду `ls`
>
> Використовуючи схему файлової системи, наведену нижче,
> якщо `pwd` показує `/Users/backup`,
> а `-r` каже `ls` виводити все у зворотному порядку,
> яка команда (команди) призведе до наступного виводу:
>
> ~~~
> pnas_sub/ pnas_final/ original/
> ~~~
> {: .output}
>
> ![Дерево каталогів під каталогом Users, де "/Users" містить
каталоги "backup" та "thing"; "/Users/backup" містить "original",
"pnas_final" та "pnas_sub"; "/Users/thing" містить "backup"; та
"/Users/thing/backup" містить "2012-12-01", "2013-01-08" та
"2013-01-27"](../fig/filesystem-challenge.svg)
>
> 1. `ls pwd`
> 2. `ls -r -F`
> 3. `ls -r -F /Users/backup`
>
> > ## Рішення
> > 1. Ні: `pwd` не є назвою каталогу.
> > 2. Так: команда `ls` без аргументу каталогу перелічує файли і каталоги
> >      у поточному каталозі.
> > 3. Так: явно використовує абсолютний шлях.
> {: .solution}
{: .challenge}


## Загальний синтаксис команди терміналу
Ми вже познайомилися з командами, опціями та аргументами,
але, можливо, буде корисно формалізувати деяку термінологію.

Розглянемо команду нижче як загальний приклад команди,
яку ми розберемо на складові частини:

~~~
$ ls -F /
~~~
{: .language-bash}

![Загальний синтаксис команди терміналу](../fig/shell_command_syntax.svg)

`ls` - це **команда**, з **опцією** `-F` та
**аргументом** `/`.
Ми вже зустрічалися з опціями, які
починаються з одного тире (`-`) або двох тире (`--`),
і вони змінюють поведінку команди.
[Аргументи] вказують команді, з чим працювати (наприклад, з файлами і каталогами).
Іноді опції та аргументи називають **параметрами**.
Команду можна викликати з більш ніж одним параметром і більш ніж одним аргументом, але команда
не завжди вимагає наявності аргументу або параметра.

Іноді ви можете побачити, що опції називають **перемикачами** або **прапорами**,
особливо для параметрів, які не потребують аргументації. У цьому уроці ми будемо дотримуватися
терміну *опція*.

Кожна частина відокремлюється пробілами: якщо ви пропустите пробіл
між `ls` і `-F`, термінал шукатиме команду з назвою `ls-F`, якої
не існує. Також може бути важливим написання великої літери.
Наприклад, `ls -s` покаже розмір файлів і каталогів поряд з назвами,
а `ls -S` відсортує файли і каталоги за розміром, як показано нижче:

~~~
$ cd ~/Desktop/shell-lesson-data
$ ls -s exercise-data
~~~
{: .language-bash}

~~~
total 28
 4 animal-counts   4 creatures  12 numbers.txt   4 proteins   4 writing
~~~
{: .output}

Зверніть увагу, що розміри, які повертає команда `ls -s`, подано у *блоках*. 
Оскільки вони визначаються по-різному для різних операційних систем,
ви можете отримати не такі значення, як у прикладі.

~~~
$ ls -S exercise-data
~~~
{: .language-bash}

~~~
animal-counts  creatures  proteins  writing  numbers.txt
~~~
{: .output}

Зібравши все це разом, наша команда вище дасть нам список
файлів і каталогів у кореневому каталозі `/`.
Приклад результату, який ви можете отримати за допомогою наведеної вище команди, наведено нижче:

~~~
$ ls -F /
~~~
{: .language-bash}

~~~
Applications/         System/
Library/              Users/
Network/              Volumes/
~~~
{: .output}


### Конвеєр Неллі: Організація файлів

Знаючи так багато про файли та каталоги,
Неллі готова впорядкувати файли, які створить машина для аналізу білків.

Вона створює каталог під назвою `north-pacific-gyre`.
(щоб нагадати собі, звідки взялися дані),
яка міститиме файли даних з аналітичної машини,
та її скрипти для обробки даних.


Кожен її фізичний зразок маркується згідно з прийнятими в лабораторії правилами
з унікальним десятисимвольним ідентифікатором,
наприклад, "NENE01729A".
Цей ідентифікатор вона використовує у своєму журналі збору зразків
для запису місця, часу, глибини та інших характеристик зразка,
тому вона вирішила використовувати його як частину імені кожного файлу даних.
Оскільки результат роботи аналізатора є звичайним текстом,
вона назве свої файли `NENE01729A.txt`, `NENE01812A.txt` і так далі.
Усі 1520 файлів буде збережено в одному каталозі.


Тепер у її поточному каталозі `shell-lesson-data`,
Нелл може побачити, які файли вона має за допомогою цієї команди:

~~~
$ ls north-pacific-gyre/
~~~
{: .language-bash}

Для введення цієї команди потрібно багато набирати на клавіатурі,
але вона може дозволити терміналу виконати більшу частину роботи за допомогою так званого **завершення табуляції**.
Якщо вона небере:

~~~
$ ls nor
~~~
{: .language-bash}

а потім натискає клавішу <kbd>Tab</kbd> (клавішу табуляції на її клавіатурі),
оболонка автоматично доповнить назву каталогу для неї:

~~~
$ ls north-pacific-gyre/
~~~
{: .language-bash}

Повторне натискання клавіші <kbd>Tab</kbd> нічого не дасть,
оскільки існує декілька варіантів;
якщо натиснути <kbd>Tab</kbd> двічі, буде показано список усіх файлів.

Якщо Неллі додасть <kbd>G</kbd> і знову натисне <kbd>Tab</kbd>,
оболонка додасть 'goo', оскільки всі файли, що починаються з 'g', мають спільні
перші три символи 'goo'.

~~~
$ ls north-pacific-gyre/goo
~~~
{: .language-bash}

Щоб побачити всі ці файли, вона може натиснути клавішу <kbd>Tab</kbd> ще двічі.
~~~
ls north-pacific-gyre/goo
goodiff.sh goostats.sh
~~~
{: .language-bash}

Це називається **завершення табуляції**,
і ми побачимо його у багатьох інших інструментах.

[Аргументи]: https://swcarpentry.github.io/shell-novice/reference.html#argument

{% include links.md %}
