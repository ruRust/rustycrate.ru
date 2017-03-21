---
title: "IDE для Rust"
categories: руководства
published: true
author: Олег В.
---

_Это вики-статья. Примем Pull Request с описанием настройки других
редакторов и IDE._

На сегодня не существует общепризнанного лидера в IDE для Rust. Мнения
расходятся, и это затрудняет быстрый старт для тех, кто начинает
знакомиться с Rust.

Это руководство для тех, кто хочет быстро начать работу с Rust в IDE с
подсветкой, автодополнением и прочими печеньями.

Ниже приведены способы настройки различных редакторов. Вам потребуется
меньше 10 минут!

<!--cut-->

{% spoiler Инструкция по настройке Sublime Text 3 %}

0. Rust
  * Ставим [Rust](https://www.rust-lang.org/)
  * Путь к _bin_ должен быть добавлен в переменную окружения PATH
1. Sublime Text 3
  * [Загружаем Sublime 3](http://www.sublimetext.com/3), именно 3 версии, т.к.
    некоторые пакеты поддержки Rust существуют только для неё
  * Ставим Package
    Control. [Simple intallation](https://packagecontrol.io/installation#st3)
    ясно и коротко описывает как это сделать
2. Плагины для поддержки Rust
  * Ставим все перечисленные [здесь](http://areweideyet.com/#sublime). Обратите
    внимание, _SublimeLinter_ необходимо установить перед
    _SublimeLinter-contrib-rustc_
  * Перезапускаем Sublime
3. Build and Run
  * В меню редактора _Tools -> Build System_ выбираем Rust
  * Создаём файл с расширением __*.rs__, тогда Sublime включит подсветку
    синтаксиса
  * Пишем код порабощения мира или можно
    взять [пример с главной страницы Rust](https://www.rust-lang.org/)
  * В меню редактора _Tools -> Build With..._ и выбираем _Rust_
  * В меню редактора _Tools -> Build With..._ и выбираем _Rust - Run_
4. Profit!

{% img '2015-12-04-ide-for-rust/sublime-3-rust.png' alt:'Sublime 3 with Rust' %}
{% endspoiler %}

{% spoiler Инструкция по настройке Visual Studio Code %}

_Проверено для Linux (ArchLinux) и для Mac OS X (El Capitan 10.11.2)_

0. Устанавливаем Rust и Cargo
  * [официальный сайт](https://www.rust-lang.org/)
1. Скачиваем исходный код Rust'a (необходим для racer'a)
  * Создаём директорию _.rust_ в домашней директории: _mkdir ~/.rust_
  * Заходим в созданную директорию: _cd ~/.rust_
  * Выполняем: _git_ _clone_ _https://github.com/rust-lang/rust.git_
2. Устанавливаем racer
   ([инструкция на github'e](https://github.com/phildawes/racer))
  * Выполняем: _git_ _clone_ _https://github.com/phildawes/racer.git_
  * Заходим в созданную директорию: _cd ./racer_
  * Собираем cargo: `cargo build --release`
  * Копируем исполняемый файл _.racer_ в _/usr/bin/_: _cp ./target/release/racer
    /usr/bin/_
3. Добавляем переменную окружения _RUST\_SRC\_PATH_
  * Н-р, для Linux выполняем: _export RUST\_SRC\_PATH=~/.rust/src_
  * Для Mac'a: добавляем строчку _export RUST\_SRC\_PATH=~/.rust/src_ в файл
    _.bash\_profile_
4. Устанавливаем [Visual Studio Code](https://code.visualstudio.com)
  * Для ArchLinux: _yaourt -Sy visual-studio-code_
5. Устанавливаем расширение rusty для Visual Studio Code
  * В редакторе нажимаем _Shift+Ctrl+P_ для Linux (для Mac'a - _Shift+Cmd+P_)
  * Набираем Install Extension
  * Затем: _ext install rusty_ (_ext install_ уже будет отображаться, осталось
    только набрать "rusty")
6. Настройка проекта в Visual Studio Code
  * Открываем директорию какого-либо проекта, созданного с помощью Cargo
  * В редакторе нажимаем _Shift+Ctrl+P_
  * Набираем Configure Task Runner
  * Закомментируем всё и вставляем
    следующее:
    [task.json](https://gist.github.com/kulinich/19ca430cffbad5caa551)
7. Назначаем сочетание клавиш для компиляции и запуска
  * В редакторе нажимаем _Shift+Ctrl+P_
  * Набираем Open Keyboard Shortcuts
  * Назначаем следующее сочетание:
  ```
  {"key": "shift+cmd+b",           "command": "workbench.action.tasks.runTask"}
  ```
8. Всё готово
  * По _Shift+Ctrl+B_ можно собирать и запускать проект
  * По _F12_ - Go to Definition
  * При наведении на символ с зажатой клавишей Ctrl (Cmd) определение появится в
    удобном окне (см. на изображении ниже)

{% img '2015-12-04-ide-for-rust/visual_studio_code_rust.png' alt:'Visual Studio Code with Rust' %}

{% endspoiler %}

{% spoiler Инструкция по настройке Emacs %}

_Проверено для Manjaro Linux 15.2 и Windows 10_

1. Устанавливаем Rust и Cargo (свежая версия есть в репозитории)
  * sudo pacman -S rust cargo
2. Скачиваем исходный код Rust'a (требуется для работы racer'a)
  * git clone https://github.com/rust-lang/rust.git ~/.rust
3. Устанавливаем racer
  * cargo install racer (_не забудьте добавить ~/.cargo/bin в переменную PATH_)
4. Добавляем переменную RUST\_SRC\_PATH
  * в файл .bash\_profile добавляем `export RUST_SRC_PATH=~/.rust/src`
  * После этого выполните `source ~/.bash_profile` в терминале, чтобы обновить
    пути
5. Устанавливаем Emacs
  * `pacman -S emacs`
6. Активируем репозиторий MELPA для Emacs
  * создаём файл ~/.emacs.d/init.el
  * добавляем в него следующие строки (активируем репозиторий и сразу же
    указываем необходимые пакеты):

        ```
        (require 'package)

        (add-to-list 'package-archives
                '("melpa" . "http://melpa.org/packages/") t)

        (package-initialize)
        (when (not package-archive-contents)
            (package-refresh-contents))

        ;; В этом месте мы указываем все необходимые пакеты для работы с Rust
        (defvar myPackages
            '(flycheck
            company
            company-racer
            racer
            flycheck-rust
            rust-mode))

        (mapc #'(lambda (package)
            (unless (package-installed-p package)
                (package-install package)))
                myPackages)
        ```

7. Добавляем сниппеты в свой init.el

        ;; Enable company globally for all mode
        (global-company-mode)

        ;; Reduce the time after which the company auto completion popup opens
        (setq company-idle-delay 0.2)

        ;; Reduce the number of characters before company kicks in
        (setq company-minimum-prefix-length 1)

        ;; Здесь указываем путь к бинарнику racer
        (setq racer-cmd "/usr/local/bin/racer")

        ;; Путь к исходникам Rust
        (setq racer-rust-src-path "/Users/YOURUSERNAME/.rust/src/")

        ;; Load rust-mode when you open `.rs` files
        (add-to-list 'auto-mode-alist '("\\.rs\\'" . rust-mode))

        ;; Setting up configurations when you load rust-mode
        (add-hook 'rust-mode-hook

            '(lambda ()
            ;; Enable racer
            (racer-activate)

            ;; Hook in racer with eldoc to provide documentation
            (racer-turn-on-eldoc)

            ;; Use flycheck-rust in rust-mode
            (add-hook 'flycheck-mode-hook #'flycheck-rust-setup)

            ;; Use company-racer in rust mode
            (set (make-local-variable 'company-backends) '(company-racer))

            ;; Key binding to jump to method definition
            (local-set-key (kbd "M-.") #'racer-find-definition)

            ;; Key binding to auto complete and indent
            (local-set-key (kbd "TAB") #'racer-complete-or-indent)))

8. Перезапускаем Emacs, дожидаемся установки пакетов.
9. Готово
  * _TAB_ - автодополнение
  * _M + ._ - go-to definition

{% img '2015-12-04-ide-for-rust/emacs_rust.png' alt:'Emacs with Rust' %}

{% endspoiler %}

{% spoiler Инструкция по настройке Vim %}

_Проверено для Fedora 23_

Простой способ начать работу с Rust в Vim - установить плагины [YouCompleteMe][]
с автодополнением на основе [racer][] и [rust.vim][] для подсветки кода.

## Возможности
Согласно документации YouCompleteMe, на данный момент поддерживается:

* Семантическое автодополнение
* Переход к определению (команды `GoTo`, `GoToDefinition`, `GoToDeclaration`
работают для Rust идентично)
* Управление экземпляром сервера `racer`.

## Настройка

1. Устанавливаем Rust и Cargo. Например, с помощью rustup:

        curl -sSf https://static.rust-lang.org/rustup.sh | sh

2. Скачиваем исходный код Rust'a (требуется для работы racer'a)

        git clone https://github.com/rust-lang/rust.git ~/.rust

3. Устанавливаем дополнения [YouCompleteMe][] и [rust.vim][]. К примеру, с
помощью [Vundle][]. Добавляем в `~/.vimrc`:

        Plugin 'Valloric/YouCompleteMe'
        Plugin 'rust-lang/rust.vim'
И устанавливаем дополнения:

        vim +PluginInstall +qall

4. Собираем плагин YouCompleteMe:

        cd ~/.vim/bundle/YouCompleteMe
        ./install.py --racer-completer

5. Указываем путь к исходному коду Rust в `~/.vimrc`:

        let g:ycm_rust_src_path = '~/.rust/src'
Или в `~/.bash_profile`:

        export RUST_SRC_PATH=~/.rust/src

6. (опционально) Добавляем в `~/.vimrc` сочетание клавиш для команды 'Goto':

        nmap <leader>j :YcmCompleter GoTo<CR>

7. Готово!

[YouCompleteMe]: https://github.com/valloric/YouCompleteMe
[racer]: https://github.com/phildawes/racer
[rust.vim]: https://github.com/rust-lang/rust.vim
[Vundle]: https://github.com/VundleVim/Vundle.vim

{% img '2015-12-04-ide-for-rust/vim_rust.gif' alt:'Vim with Rust' %}

{% endspoiler %}

# Ссылки
* [Прекрасная табличка со статусом поддержки возможностей для всех IDE (или почти всех), которые умеют работать с Rust](http://areweideyet.com/)
