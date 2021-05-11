# Задание

Написать Ansible playbook, который разворачивает 2 ноды в AWS EC2: сборочную и продовую. На сборочной ноде происходит сборка Java проекта, полученный артефакт передается на продовую ноду и на ней запускается.

# Выполнение

Страница с документацией как подружить [Ansible + ec2](https://docs.ansible.com/ansible/2.4/guide_aws.html)

Для авторизации в EC2 нужен ACCESS_KEY и SECRET_ACCESS_KEY. Получить их можно командой:
```bash 
aws ec2 create-key-pair --key-name my-key11 --query 'KeyMaterial' --output text > ~/.ssh/my-key.pem
```

Для Ansible нужны эти ключи, и я буду их задавать как переменные окружения на той ВМ, на которой запускаю сам скрипт. Делается так, чтобы случайно не опубликовать эти ключи в GitHub. Задать переменные окружения нужно командой
```bash
export AWS_ACCESS_KEY_ID=''
export AWS_SECRET_ACCESS_KEY=''
```

Далее на машину обязательно ставим `python3-pip` и библиотеку `boto`, это нужно чтобы Ansible мог выполнять действия с EC2

`pip3 install boto3`