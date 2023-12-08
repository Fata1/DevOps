# DevOps

Ответы на ДЗ "Инструменты ГИТ":

В клонированном репозитории:
1.	Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.
commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400
Update CHANGELOG.md
2.	Ответьте на вопросы.
•	Какому тегу соответствует коммит 85024d3?
-	(tag: v0.12.23)
•	Сколько родителей у коммита b8d720? Напишите их хеши.
-	Два родителя с хешами 56cd7859e05c36c06b56d013b55a252d0bb7e158 9ea88f22fc6269854151c571162c5bcf958bee2b 
•	Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.?
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
•	Найдите коммит, в котором была создана функция func providerSource, её определение в коде выглядит так: func providerSource(...) (вместо троеточия перечислены аргументы).
-	commit 8c928e83589d90a031f811fae52a81be7153e82f
•	Найдите все коммиты, в которых была изменена функция globalPluginDirs.
78b1220558 Remove config.go and update things using its aliases

diff --git a/plugins.go b/plugins.go
--- a/plugins.go
+++ b/plugins.go
@@ -16,14 +18,14 @@
 func globalPluginDirs() []string {
        var ret []string
        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX
-       dir, err := ConfigDir()
+       dir, err := cliconfig.ConfigDir()
        if err != nil {
                log.Printf("[ERROR] Error finding global config directory: %s", err)
        } else {
                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)
                ret = append(ret, filepath.Join(dir, "plugins"))
                ret = append(ret, filepath.Join(dir, "plugins", machineDir))
        }

        return ret
 }
52dbf94834 keep .terraform.d/plugins for discovery

diff --git a/plugins.go b/plugins.go
--- a/plugins.go
+++ b/plugins.go
@@ -16,13 +16,14 @@
 func globalPluginDirs() []string {
        var ret []string
        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX
        dir, err := ConfigDir()
        if err != nil {
                log.Printf("[ERROR] Error finding global config directory: %s", err)
        } else {
                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)
+               ret = append(ret, filepath.Join(dir, "plugins"))
                ret = append(ret, filepath.Join(dir, "plugins", machineDir))
        }

        return ret
 }
41ab0aef7a Add missing OS_ARCH dir to global plugin paths

diff --git a/plugins.go b/plugins.go
--- a/plugins.go
+++ b/plugins.go
@@ -14,12 +16,13 @@
 func globalPluginDirs() []string {
        var ret []string
        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX
        dir, err := ConfigDir()
        if err != nil {
                log.Printf("[ERROR] Error finding global config directory: %s", err)
        } else {
-               ret = append(ret, filepath.Join(dir, "plugins"))
+               machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)
+               ret = append(ret, filepath.Join(dir, "plugins", machineDir))
        }

        return ret
 }
66ebff90cd move some more plugin search path logic to command

diff --git a/plugins.go b/plugins.go
--- a/plugins.go
+++ b/plugins.go
@@ -16,22 +14,12 @@
 func globalPluginDirs() []string {
        var ret []string
-
-       // Look in the same directory as the Terraform executable.
-       // If found, this replaces what we found in the config path.
-       exePath, err := osext.Executable()
-       if err != nil {
-               log.Printf("[ERROR] Error discovering exe directory: %s", err)
-       } else {
-               ret = append(ret, filepath.Dir(exePath))
-       }
-
        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX
        dir, err := ConfigDir()
        if err != nil {
                log.Printf("[ERROR] Error finding global config directory: %s", err)
        } else {
                ret = append(ret, filepath.Join(dir, "plugins"))
        }

        return ret
 }
•	Кто автор функции synchronizedWriters? 
Martin Atkins



Changes GIT

1. Change text


# Игнорировать Все файлы временного каталога .terraform , находящимся в любом другом каталоге (**) (почему не terraform хз, если же .terraform это временный файл почему дальше идет слэш со звездой намекающий, что .terraform это папка, значит .terrafrom это скрытый каталог)
# Требуются разьяснения  что значит эта комманда короче говоря
**/.terraform/*

# Файлы с расширением .tfstate и производные, например .tfstate.ar
*.tfstate
*.tfstate.*

# Крэш логи и производные, например crash.rar.log
crash.log
crash.*.log

# Исключить все файлы с расширением .tfvars и tfvars.json
# password, private keys, and other secrets. These should not be part of version 
# control as they are data points which are potentially sensitive and subject 
# to change depending on the environment.
*.tfvars
*.tfvars.json

# Исключить все файлы с расширением override.tf а также начинающихся на любой символ и заканчивающийся _override.tf и _override.tf.json
# are not checked in
override.tf
override.tf.json
*_override.tf
*_override.tf.json

# Include override files you do wish to add to version control using negated pattern
# !example_override.tf

# Include tfplan files to ignore the plan output of command: terraform plan -out=tfplan
# example: *tfplan*

# Ignore CLI configuration files
.terraformrc
terraform.rc
