Данное дз сделано на основе прошлого использовался терраформ для создания виртуалок.
Файл hosts собирается автоматически
Переделан playbook "svc.yml" на "playbook_roles.yaml" c использование roles

Вывод команды "ansible-playbook playbooks/playbook_roles.yaml"
```
PLAY [Install ClickHouse] ********************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************
ok: [clickhouse]

TASK [clickhouse-role : Download and add Clickhouse GPG key] *********************************************************************************************
changed: [clickhouse]

TASK [clickhouse-role : Add Clickhouse repository] *******************************************************************************************************
changed: [clickhouse]

TASK [clickhouse-role : Update apt cache] ****************************************************************************************************************
ok: [clickhouse]

TASK [clickhouse-role : Install ClickHouse packages] *****************************************************************************************************
changed: [clickhouse]

TASK [clickhouse-role : Create ClickHouse database] ******************************************************************************************************
FAILED - RETRYING: [clickhouse]: Create ClickHouse database (10 retries left).
FAILED - RETRYING: [clickhouse]: Create ClickHouse database (9 retries left).
changed: [clickhouse]

RUNNING HANDLER [clickhouse-role : Start clickhouse service] *********************************************************************************************
changed: [clickhouse]

PLAY [Install Vector] ************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************
ok: [vector]

TASK [vector-role : Download Vector deb package] *********************************************************************************************************
changed: [vector]

TASK [vector-role : Install Vector] **********************************************************************************************************************
changed: [vector]

TASK [vector-role : Deploy Vector configuration] *********************************************************************************************************
changed: [vector]

RUNNING HANDLER [vector-role : Restart Vector] ***********************************************************************************************************
changed: [vector]

PLAY [Install LightHouse] ********************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************
ok: [lighthouse]

TASK [lihghouse-role : Install dependencies] *************************************************************************************************************
changed: [lighthouse]

TASK [lihghouse-role : Clone the Lighthouse repository] **************************************************************************************************
changed: [lighthouse]

PLAY RECAP ***********************************************************************************************************************************************
clickhouse                 : ok=7    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
lighthouse                 : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
vector                     : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

# Описание ролей

# Vector Role

Ansible role for installing and configuring [Vector](https://vector.dev/), a high-performance observability data pipeline.

## Requirements

- Ansible 2.9 or higher
- Ubuntu/Debian based OS (other systems may require modifications)
- `vector` package repository is set up.

## Role Variables

| Variable                | Default                 | Description                                                                 |
|-------------------------|-------------------------|-----------------------------------------------------------------------------|
| `vector_version`         | `0.42.0`                | The version of Vector to be installed.                                      |
| `vector_config_file`     | `/etc/vector/vector.yaml`| Path to the Vector configuration file.                                      |
| `vector_config_template` | `vector_config.j2`      | The Jinja2 template file for configuring Vector.                            |
| `vector_install_source`  | `https://github.com/vectordotdev/vector`| The source repository to fetch the Vector package from.                    |

## Dependencies

None.

## Example Playbook

```yaml
- hosts: vector
  become: true
  roles:
    - vector-role
```

## Использование
Клонируйте этот репозиторий и перейдите в директорию роли.
Включите роль vector-role в ваш плейбук.
При необходимости измените переменные vector_config_file и vector_version в вашем плейбуке или в файле roles/vector-role/defaults/main.yml.
Запустите плейбук.

## Задачи
Эта роль выполняет следующие задачи:

Устанавливает Vector из указанного репозитория пакетов.
Разворачивает конфигурационный файл Vector на основе предоставленного шаблона.
Запускает сервис Vector с помощью systemd.
Обработчики
Эта роль включает обработчики для перезапуска сервиса Vector, если в конфигурации были внесены изменения.

Заметки
Шаблон vector_config.j2 можно настроить. Вы можете добавить дополнительные параметры конфигурации в соответствии с вашими потребностями.

### 2. `README.md` для **Lighhouse** роли

# Lighthouse Role

Ansible role for installing and configuring [Lighthouse](https://github.com/VKCOM/lighthouse.git), an open-source observability and monitoring tool.

## Requirements

- Ansible 2.9 or higher

## Role Variables

| Variable                | Default                   | Description                                                                  |
|-------------------------|---------------------------|------------------------------------------------------------------------------|
| `lighthouse_repo_url` | `https://github.com/VKCOM/lighthouse.git` | The source repository to fetch the Lighthouse package from.                   |

## Dependencies

None.

## Example Playbook

```yaml
- hosts: lighhouse
  become: true
  roles:
    - lighhouse-role
```

## Использование
Клонируйте этот репозиторий и перейдите в директорию роли.
Включите роль lighthouse-role в ваш плейбук.
При необходимости измените переменные lighthouse_install_path в вашем плейбуке или в файле roles/lighhouse-role/defaults/main.yml.
Запустите плейбук.

## Задачи
Эта роль выполняет следующие задачи:

Устанавливает Lighthouse из указанного репозитория пакетов.
Запустите index.html bp rfnfkjuf ecnfyjdrb
