# DevOps

Ответы на ДЗ "Инструменты ГИТ":

В клонированном репозитории:
1.	Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.

> 		 Комманда: git show aefea

commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400
Update CHANGELOG.md



3.	Ответьте на вопросы.
2.1 Какому тегу соответствует коммит 85024d3?

> 		 (tag: v0.12.23)

> 		 Комманда: git log v0.12.23
2.2 	Сколько родителей у коммита b8d720? Напишите их хеши.

> 		 Комманда: git show --pretty=format:' %P' b8d720

> Два родителя с хешами 56cd7859e05c36c06b56d013b55a252d0bb7e158
> 9ea88f22fc6269854151c571162c5bcf958bee2b

2.3 Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.?

> 		 git log v0.12.23..v0.12.24 --oneline

    -	33ff1c03bb (tag: v0.12.24) v0.12.24
    -	b14b74c493 [Website] vmc provider links
    -	3f235065b9 Update CHANGELOG.md
    -	6ae64e247b registry: Fix panic when server is unreachable
    -	5c619ca1ba website: Remove links to the getting started guide's old location
    -	06275647e2 Update CHANGELOG.md
    -	d5f9411f51 command: Fix bug when using terraform login on Windows
    -	4b6d06cc5d Update CHANGELOG.md
    -	dd01a35078 Update CHANGELOG.md
    -	225466bc3e Cleanup after v0.12.23 release

2.4 	Найдите коммит, в котором была создана функция func providerSource, её определение в коде выглядит так: func providerSource(...) (вместо троеточия перечислены аргументы).

> 		 Комманда: git log -S'func providerSource('

> 	commit 8c928e83589d90a031f811fae52a81be7153e82f

2.5 	Найдите все коммиты, в которых была изменена функция globalPluginDirs.

> 		 Комманда: git log -L :"func globalPluginDirs":plugins.go --oneline

    8b1220558 Remove config.go and update things using its aliases
    52dbf94834 keep .terraform.d/plugins for discovery
    41ab0aef7a Add missing OS_ARCH dir to global plugin paths
    66ebff90cd move some more plugin search path logic to command

2.6 	Кто автор функции synchronizedWriters? 

> 		 Комманды: git log -S"func synchronizedWriters(" --pretty=format:"%h "
>         git show bdfea50cc8
>         git show 5ac311e2a9
    
    Martin Atkins
