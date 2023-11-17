# DevOps

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

added string