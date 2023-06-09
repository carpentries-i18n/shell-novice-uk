---
layout: page
title: "Примітки інструктора"
---
*   Навіщо ми вчимося користуватися терміналом?
    *   Дозволяє користувачам автоматизувати повторювані завдання
    *   І фіксує невеликі кроки маніпуляцій з даними, які зазвичай не записуються
        для того, щоб зробити дослідження відтворюваними
*   Проблема
    *   Запуск одного і того ж робочого процесу для декількох зразків може бути невиправдано трудомістким
    *   Ручна маніпуляція з файлами даних:
        *   часто не відображається в документації
        *   важко відтворити
        *   важко усунути несправності, переглянути або вдосконалити
*   Термінал
    *   Робочі процеси можна автоматизувати за допомогою скриптів терміналу
    *   Вбудовані команди дозволяють легко маніпулювати даними (наприклад, sort, grep тощо).
    *   Кожен крок може бути зафіксований у скрипті терміналу, що забезпечує відтворюваність та
        легке усунення несправностей

## Загальний підсумок

Багато хто ставить під сумнів, чи варто продовжувати вчити термінал.
Зрештою,
будь-хто, хто хоче перейменувати кілька тисяч файлів даних,
може легко зробити це інтерактивно в інтерпретаторі Python,
і будь-хто, хто займається серйозним аналізом даних
швидше за все, буде виконувати більшу частину своєї роботи в IPython Notebook або в R Studio.
Тож навіщо навчатися роботі в терміналі?

Перша відповідь така:
"Тому що від цього залежить так багато іншого".
Встановлення програмного забезпечення,
налаштування редактора за замовчуванням
та керування віддаленими комп'ютерами часто вимагають базового знайомства з командним терміналом
та пов'язаними з ним поняттями, такими як стандартний ввід та вивід.
Багато інструментів також використовують його термінологію
(наприклад, магічні команди `%ls` та `%cd` в IPython).

Друга відповідь така:
"Тому що це простий спосіб представити деякі фундаментальні ідеї про те, як користуватися комп'ютером".
Коли ми вчимо людей користуватися терміналом Unix,
ми вчимо їх, що вони повинні змусити комп'ютер повторювати дії
(за допомогою завершення клавішею табуляції,
знаком `!`, за яким йде номер команди,
та циклів "for").
замість того, щоб повторювати щось самому.
Ми також вчимо їх брати речі, які, як вони виявили, вони роблять часто,
і зберігати їх для подальшого використання
(за допомогою скриптів терміналу),
давати речам розумні назви
і писати невелику документацію
(наприклад, коментар у верхній частині скрипта терміналу)
щоб покращити життя своїх майбутніх поколінь.

Третя відповідь така:
"Тому що це дозволяє використовувати багато специфічних інструментів та обчислювальних ресурсів,
до яких дослідники не можуть отримати доступ інакше".
Знайомство з терміналом дуже корисне для віддаленого доступу до машин,
використання високопродуктивної обчислювальної інфраструктури
та запуску нових спеціалізованих інструментів у багатьох дисциплінах.
Ми не навчаємо навичкам роботи з високопродуктивними обчислювальними системами або роботі в конкретних галузях,
але закладаємо основу для подальшого розвитку цих навичок.
Зокрема,
розуміння синтаксису команд, прапорів та довідкових систем є корисним для роботи з специфічними інструментами,
а розуміння файлової системи (та способів навігації по ній) корисне для віддаленого доступу.

Нарешті,
і, можливо, найважливіше,
навчання людей терміналу дозволяє нам навчити їх
думати про програмування з точки зору композиції функцій.
У випадку з терміналом
це має форму конвеєрів, а не вкладених викликів функцій,
але основна ідея "маленьких шматочків, нещільно з'єднаних між собою" залишається тією ж самою.

Весь цей матеріал можна охопити за три години
за умови, що учні, які використовують Windows, не натраплять на такі перешкоди, як:

*   неможливысть з'ясувати, де знаходиться їхня домашня директорія
    (особливо якщо вони використовують Cygwin);
*   невміння запустити звичайний текстовий редактор;
    та
*   відмова терміналу виконувати скрипти, які містять закінчення рядків DOS.

## Підготовка до викладання

*   Використовуйте каталог `data` для вправ на семинарах та прикладів кодування в реальному часі.
    Ви можете клонувати каталог shell-novice або використати *Завантажити ZIP*.
    кнопку праворуч, щоб отримати увесь
    [Git репозиторій](https://github.com/swcarpentry/shell-novice). Також тепер ми надаємо
    zip-файл каталогу `data`
    на [Сторінці налаштування]({{ page.root }}{% link setup.md %}).

*   Веб-сайт: використовувалися різні практики.
    *   Варіант 1: Ви можете дати учням посилання перед початком уроку, щоб вони могли слідувати за ним,
        надолужити пропущене
\tта переглянути вправи (особливо якщо ви дотримуєтесь змісту уроку без особливих змін).
    *   Варіант 2: Не показуйте веб-сайт учням під час уроку,
        оскільки це може відволікати:
        учні можуть читати замість того, щоб слухати, а відкрите вікно - це додаткове
        когнітивне навантаження.
\t*   У будь-якому випадку, не забудьте вказати на веб-сайт як на джерело інформації після воркшопу.

*   Зміст:
    Якщо ви не маєте справді щедрої кількості часу (4+ години),
    швидше за все, ви не зможете охопити весь матеріал цього уроку за один урок тривалістю у половину дня.
    Заздалегідь сплануйте, що ви можете пропустити, на чому хочете наголосити тощо.

*   Вправи:
    Заздалегідь продумайте, як ви будете працювати з вправами під час уроку.
    Як ви їх роздаєте (веб-сайт, слайд, роздатковий матеріал)?
    Ви хочете, щоб кожен спробував, а потім ви показали розв'язання?
    Чи попросити когось з учнів показати розв'язання?
    Доручити групам виконати різні вправи і презентувати свої рішення?

*   Сторінку [Посилання]({{ page.root }}{% link reference.md %}) можна роздрукувати
    і дати студентам для ознайомлення, на ваш вибір.

*   Інші приготування:
    Не соромтеся додавати власні приклади чи коментарі,
    але знайте, що це не обов'язково:
    теми і команди можна викладати так, як вони подані на сторінках уроків.
    Якщо ви вважаєте, що в уроці чогось не вистачає,
    не соромтеся повідомити про проблему або створити запит на зміну матеріалу.

## Викладацькі нотатки

*   Супер крутий онлайн-ресурс!
    <http://explainshell.com/> детально проаналізує будь-яку команду оболонки, яку ви введете,
    і покаже текст довідки для кожного фрагмента.
    Додатковим чудовим посібником може бути <http://tldr-pages.github.io/>
    з короткими дуже докладними інструкціями для команд командного рядка,
    особливо корисним у Windows під час використання Git Bash, де `man` не може працювати.

*   Ще один супер крутий онлайн-ресурс - це <http://www.shellcheck.net>,
    який перевірить скрипти оболонки (як завантажені, так і введені) на наявність типових помилок.

*   Ресурси для "розщеплення" вашої терміналу так, щоб нещодавні команди
    залишалися в полі зору: <https://github.com/rgaiacs/swc-shell-split-window>.

*   Іноді учні можуть потрапити в пастку в текстових редакторах командного рядка, таких як
    Vim, Emacs або Nano.
    Закриття емулятора терміналу та відкриття нового може викликати розчарування
    оскільки учням доведеться знову переходити до потрібної папки.
    Для пом'якшення цієї проблеми ми радимо викладачам використовувати
    той самий текстовий редактор, що й учні під час семінарів (у більшості випадків Nano).

*   Знайомство з файловою системою в терміналі та навігація нею (розглянуто в
    секції [Навігація файлами та каталогами]({{ page.root }}{% link _episodes/02-filedir.md %}))
    можуть плутати.
    Ви можете мати відкриті термінал і графічний провідник файлів поруч, щоб учні могли бачити
    вміст і структуру файлів, коли вони використовують термінал для навігації системою.

*   Завершення клавішею табуляції звучить як дрібниця: це не так.
    Повторний запуск старих команд за допомогою `!123` або `!wc`
    теж не дрібниця,
    і також дрібницями не є розгортання підстановочних символів та цикли `for`.
    Кожен із них — це можливість повторити одну з великих ідей Software Carpentry:
    якщо комп'ютер *може* це повторити,
    якийсь програміст десь майже напевно створить
    якийсь спосіб для комп’ютера *повторити* це.

*   Побудова конвеєру з чотирма або п'ятьма ступенями,
    з подальшим розміщенням його в скрипт терміналу для повторного використання
    і виклик цього сценарію всередині циклу `for`,
    це чудова можливість показати, як
    "сім плюс-мінус два"
    пов'язано з програмуванням.
    Коли ми з’ясували, як зробити щось помірно складне,
    ми робимо його придатним для повторного використання та даємо йому назву
    так що він займає лише один слот у робочій пам’яті,
    а не кілька
    Це також гарна можливість поговорити про пошукове програмування:
    замість того, щоб розробляти програму заздалегідь,
    ми можемо зробити кілька корисних речей
    а потім заднім числом вирішити, які варті інкапсуляції
    для майбутнього повторного використання.

*   Якщо все йде добре, ви можете переконати, що розширення файлів
    по суті існують, щоб допомогти комп’ютерам (і людям-
    читачам) зрозуміти вміст файлів, і не є вимогою для файлів
    (коротко висвітлено в секції
    [Навігація файлами та каталогами]({{ page.root }}{% link _episodes/02-filedir.md %})).
    Це можна зробити в
    секції [Канали та фільтри]({{ page.root }}{% link _episodes/04-pipefilter.md %}) шляхом демонстрації
    що ви можете перенаправити стандартний вихід у файл без розширення .txt
    (наприклад, lengths), і що отриманий файл все ще є цілком придатним для використання текстовим файлом.
    Зауважте, що у разі подвійного кліку в графічному інтерфейсі комп’ютер буде,
    напевно, запитувати вас, що ви хочете зробити.

*   Через брак часу нам доводиться пропускати багато важливих речей,
    включаючи дозволи на файли, керування завданнями та SSH.
    Якщо учні вже розуміють базовий матеріал,
    цей матеріал можна розглянути, використовуючи онлайн-уроки як орієнтири.
    Ці обмеження також мають подальші наслідки:

*   Важко обговорювати `#!` (шебанг), не обговоривши попередньо
    дозволів, чого ми не робимо. `#!` також [доволі
    складний][shebang], тож навіть якби ми обговорювали дозволи,
    ми, мабуть, все одно б не захотіли обговорювати `#!`.

*   Встановлення Bash та доцільного набору команд Unix на Windows
    завжди пов'язане з деякими клопотами та розчаруваннями.
    Будь ласка, зверніться до останнього набору інструкцій щодо встановлення для отримання порад,
    і спробуйте самі, перш ніж викладати у класі.

*   На машинах Windows
    якщо `nano` не було належним чином встановлено за допомогою
    [Software Carpentry Windows Installer][windows-installer]
    можна скористатися `notepad` як альтернативою. У цьому випадку буде використано графічний інтерфейс
    і закінчення рядків обробляються по-різному, але для
    цілей цього уроку `notepad` і `nano` можна використовувати майже як взаємозамінні.

*   На машинах Windows, виявляється, наступні команди:

    ~~~
    $ cd
    $ cd Desktop
    ~~~
    {: .language-bash}

    завжди відправлять когось у каталог свого робочого столу
    (якщо на їхньому комп'ютері не створено резервну копію за допомогою корпоративного OneDrive, див. наступний пункт).
    Попросіть їх створити там каталог прикладів для вправ у командному рядку
    щоб вони могли легко його знайти
    і спостерігати за його розвитком.

*   Якщо на комп'ютері з Windows створено резервну копію корпоративного OneDrive, його робочий стіл із графічним інтерфейсом може
    буде відображено з каталогу у OneDrive, який не збігатиметься із вмістом `~/Desktop`.
    Доступ до робочого столу OneDrive має бути забезпечено за допомогою однієї з наведених нижче команд
    (якщо назва підприємства незрозуміла, перегляньте виведення `ls`, щоб знайти
    потрібний каталог):

    ~~~
    $ cd "~/OneDrive - Name Of Enterprise/Desktop"
    $ cd "C:/Users/Username/OneDrive - Name Of Enterprise/Desktop"
    ~~~
    {: .language-bash}

    Один із способів визначити, чи використовує комп'ютер таку конфігурацію, - це переглянути файли,
    каталоги або посилання на робочому столі. Зазвичай піктограма містить символ ярлика/стрілки, якщо це
    посилання, або просто піктограму, якщо файл просто збережено в папці "Робочий стіл".
    Файли, синхронізовані зі службою OneDrive, містять додатковий символ, що вказує на стан синхронізації
    (зазвичай сині стрілки для "очікує синхронізації" або зелена галочка для "синхронізовано").

*  Дотримуйтесь POSIX-сумісних команд, як і в усіх навчальних матеріалах.
   Ваша конкретна оболонка може мати розширення за межами POSIX, які недоступні
   на інших машинах, особливо у типових емуляторах bash для macOS і bash для Windows.
   Наприклад, POSIX `ls` не має опції `--ignore=` або `-I`, а POSIX
   `head` приймає `-n 10` або `-10`, але не довгу форму `--lines=10`.

## Windows

Встановлення Bash та доцільного набору команд Unix на Windows
завжди пов'язане з деякими клопотами та розчаруваннями.
Будь ласка, зверніться до останнього набору інструкцій щодо встановлення для отримання порад,
і спробуйте самі, перш ніж викладати у класі.
Ми розглянули такі варіанти:

1.  [msysGit](http://msysgit.github.io/) (також відомий як "Git Bash"),
2.  [Cygwin](http://www.cygwin.com/),
3.  використання віртуальної машини, та
4.  підключення учнів до віддаленої Unix-машини (як правило, віртуальної машини в хмарі).

Cygwin був найкращим варіантом до середини 2013 року,
але як тільки ми почали викладати Git,
msysGit виявився кращим.
Настільні віртуальні машини та хмарні віртуальні машини добре підходять для технічно-підкованих учнів
і можуть скоротити час на встановлення та налаштування на початку семінару,
але:

1.  вони погано працюють на малопотужних машинах,
2.  вони збивають з пантелику новачків (тому що такі прості речі, як копіювання та вставка, працюють по-різному),
3.  учні залишають семінар без робочого середовища на обраній ними операційній системі,
    та
4.  учні можуть з'явитися, не завантаживши віртуальну машину, або бездротовий зв'язок зникне
    (або стане перевантаженим) під час уроку.
    

Що б ви не використовували,
будь ласка, *протестуйте його власноруч* на комп'ютері з Windows *до* початку семінару:
з часу вашого останнього семінару все могло змінитися за вашою спиною.
І, будь ласка, також скористайтеся нашим
[Software Carpentry Windows Installer][windows-installer].

[shebang]: http://www.in-ulm.de/~mascheck/various/shebang/
[windows-installer]: {{ site.swc_github }}/windows-installer

