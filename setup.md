---
layout: page
title: Встановлення
root: .
---

## Завантаження файлів
Для перегляду цього уроку вам потрібно завантажити деякі файли.

1. Завантажте [shell-lesson-data.zip][zip-file] і перемістіть файл на робочий стіл.
2. Розархівуйте файл.
   **Повідомте інструктора, якщо вам потрібна допомога на цьому етапі**.
   У вас має з'явитися новий каталог з назвою **`shell-lesson-data`** на робочому столі.

## Встановлення програмного забезпечення
Якщо у вас ще не встановлено програму-термінал, вам потрібно
[завантажити і встановити] [install_shell] її.

## Відкрити новий термінал
Після встановлення програмного забезпечення
3. Відкрити термінал.
   Якщо ви не знаєте, як відкрити термінал у вашій операційній системі, див. інструкції нижче.
4. У терміналі введіть `cd` і натисніть клавішу <kbd>Return</kbd>.
   Цей крок гарантує, що ви почнете з вашого домашнього каталогу як робочого каталогу.

У цьому уроці ви дізнаєтеся, як отримати доступ до файлів даних у цій папці.

> ## Де вводити команди: Як відкрити новий термінал
>
> Термінал - це програма, за допомогою якої ми можемо надсилати команди комп'ютеру та отримувати результати.
> Її також називають оболонкою або командним рядком.
>
> На деяких комп'ютерах за замовчуванням встановлено програму Unix Shell.
> Нижче описано деякі способи визначення та відкриття
> програми Unix Shell, якщо її вже встановлено.
> Також існують способи визначення та завантаження програми Unix Shell,
> емулятора Linux/UNIX або програми для доступу до оболонки Unix на сервері.
>
> Якщо жоден із наведених нижче варіантів не відповідає вашим обставинам,
> спробуйте скористатися пошуком в Інтернеті: Unix shell [модель вашого комп'ютера] [ваша операційна система].
{: .callout}

{::options parse_block_html="true" /}
<div>
<ul class="nav nav-tabs nav-justified" role="tablist">
<li role="presentation" class="active"><a data-os="windows" href="#windows" aria-controls="Windows"
role="tab" data-toggle="tab">Windows</a></li>
<li role="presentation"><a data-os="macos" href="#macos" aria-controls="macOS" role="tab"
data-toggle="tab">macOS</a></li>
<li role="presentation"><a data-os="linux" href="#linux" aria-controls="Linux" role="tab"
data-toggle="tab">Linux</a></li>
</ul>

<div class="tab-content">
<article role="tabpanel" class="tab-pane active" id="windows">
На комп'ютерах з операційною системою Windows автоматично не встановлюється програма Unix Shell
У цьому уроці ми рекомендуємо вам скористатися емулятором, що входить до складу [Git for Windows][install_shell],
який надає доступ як до команд оболонки Bash, так і до Git'у.

Після встановлення ви можете відкрити термінал, запустивши програму Git Bash зі стартового
меню Windows.

**Для досвідчених користувачів:**

Як альтернативу Git'у для Windows ви можете [Встановити підсистему Windows для Linux][wsl]
яка надає доступ до інструменту командного рядка Bash у Windows 10.

Зверніть увагу, що команди у підсистемі Windows для Linux (WSL) можуть дещо відрізнятися
від тих, що показані в уроці або представлені на семінарі.
</article>

<article role="tabpanel" class="tab-pane" id="macos">
На комп'ютерах Mac з macOS Mojave або більш ранніми версіями за замовчуванням використовується Unix-термінал Bash.
На комп'ютерах Mac з macOS Catalina або пізніших версій стандартним терміналом Unix є Zsh.
Ваша стандартний термінал доступний за допомогою програми Terminal у каталозі Utilities.

Щоб відкрити Термінал, спробуйте один або обидва з наведених нижче способів:
* У Finder виберіть меню "Перехід", а потім виберіть "Утиліти".
Знайдіть програму Terminal у папці Utilities і відкрийте її.
* Використовуйте функцію пошуку на комп'ютері Mac 'Spotlight'.
Знайдіть `Термінал` і натисніть <kbd>Return</kbd>.

Щоб перевірити, чи налаштовано на вашому комп'ютері використання чогось іншого, окрім Bash,
введіть `echo $SHELL` у вікні вашого терміналу.

Щоб перевірити, чи налаштовано ваш комп'ютер на використання чогось іншого, окрім Bash,
введіть `echo $SHELL` у вікні вашого терміналу.

[Як користуватися терміналом на Mac][mac-terminal]
</article>

<article role="tabpanel" class="tab-pane" id="linux">
Терміналом Unix для операційних систем Linux за замовчуванням зазвичай є Bash.
У більшості версій Linux він доступний за допомогою команд
[Gnome Terminal][gnome-terminal], [KDE Konsole][kde-konsole] або [xterm][xterm],
які можна знайти за допомогою меню програм або рядка пошуку.
Якщо на вашому комп'ютері налаштовано використання інших програм, окрім Bash,
ви можете запустити її, відкривши термінал і набравши `bash`.
</div>
</div>

[zip-file]: {{ page.root }}/data/shell-lesson-data.zip
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/install-win10
[mac-terminal]: http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/
[gnome-terminal]: https://help.gnome.org/users/gnome-terminal/stable/
[kde-konsole]: https://konsole.kde.org/
[xterm]: https://en.wikipedia.org/wiki/Xterm
[install_shell]: https://carpentries.github.io/workshop-template/#shell

