### Лабораторная работа 3 – GitHub Actions

# Task 1 — First GitHub Actions Workflow

![img_2.png](img_2.png)

```
Current runner version: '2.331.0'
Runner Image Provisioner
  Hosted Compute Agent
  Version: 20260123.484
  Commit: 6bd6555ca37d84114959e1c76d2c01448ff61c5d
  Build Date: 2026-01-23T19:41:17Z
  Worker ID: {9c51a0ac-13ce-4ab4-a58b-ca488afcabd6}
  Azure Region: northcentralus
Operating System
  Ubuntu
  24.04.3
  LTS
Runner Image
  Image: ubuntu-24.04
  Version: 20260209.23.1
  Included Software: https://github.com/actions/runner-images/blob/ubuntu24/20260209.23/images/ubuntu/Ubuntu2404-Readme.md
  Image Release: https://github.com/actions/runner-images/releases/tag/ubuntu24%2F20260209.23
GITHUB_TOKEN Permissions
  Actions: write
  ArtifactMetadata: write
  Attestations: write
  Checks: write
  Contents: write
  Deployments: write
  Discussions: write
  Issues: write
  Metadata: read
  Models: read
  Packages: write
  Pages: write
  PullRequests: write
  RepositoryProjects: write
  SecurityEvents: write
  Statuses: write
Secret source: Actions
Prepare workflow directory
Prepare all required actions
Complete job name: test
```



**Key concepts:**
- **Jobs** – набор шагов, выполняющихся на одном runner.
- **Steps** – отдельные команды или действия.
- **Runners** – виртуальные машины, предоставляемые GitHub.
- **Triggers** – событие `push` запускает workflow.

**Trigger reason:** pushed commit to branch `feature/lab3`.


**Link**
https://github.com/aliyalatipova/DevOps-Intro/actions/runs/22069562535/job/63770228391


## Task 2 — Manual Trigger + System Information


### Changes Made to the Workflow File
An additional step was added to collect detailed system information about the GitHub-hosted runner. This step runs standard Linux commands (`uname`, `lscpu`, `free`, `df`) to gather operating system details, hardware specifications, memory usage, and disk information.

### Gathered system information from runner
```
Run echo "=== OS Information ==="
=== OS Information ===
Linux runnervmjduv7 6.14.0-1017-azure #17~24.04.1-Ubuntu SMP Mon Dec  1 20:10:50 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
=== CPU cores ===
4
=== Memory ===
               total        used        free      shared  buff/cache   available
Mem:            15Gi       806Mi        13Gi        39Mi       1.8Gi        14Gi
Swap:          3.0Gi          0B       3.0Gi
=== Disk space ===
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       145G   53G   92G  37% /
tmpfs           7.9G   84K  7.9G   1% /dev/shm
tmpfs           3.2G 1000K  3.2G   1% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
efivarfs        128M   32K  128M   1% /sys/firmware/efi/efivars
/dev/sda16      881M   63M  757M   8% /boot
/dev/sda15      105M  6.2M   99M   6% /boot/efi
tmpfs           1.6G   12K  1.6G   1% /run/user/1001
=== Runner context ===
Runner OS: Linux
Runner temp directory: /home/runner/work/_temp
Runner workspace: /home/runner/work/DevOps-Intro
```


### Сравнение автоматического и ручного запуска
- **Автоматический запуск (push):** происходит при каждом пуше в репозиторий. Удобен для непрерывной интеграции – каждая новая версия кода сразу проверяется.
- **Ручной запуск (workflow_dispatch):** инициируется пользователем из интерфейса GitHub. Позволяет выполнить workflow в любое время без нового коммита, например, для диагностики, повторного запуска с теми же параметрами или выполнения задач по требованию.

**Основные различия:**
- Автоматический запуск обеспечивает быструю обратную связь, но происходит часто.
- Ручной запуск даёт контроль над моментом выполнения и может принимать входные параметры (хотя в данном случае они не использовались).

### Анализ окружения раннера
- **Операционная система:** Ubuntu 24.04.3 LTS (информация из секции Set up job).
- **Процессор:** 4 ядра (согласно выводу `nproc`).
- **Оперативная память:** 15 GiB (Mem total).
- **Дисковое пространство:** корневой раздел `/dev/root` имеет размер 145 ГБ, занято 53 ГБ, свободно 92 ГБ.
- **Тип окружения:** стандартный виртуальный раннер GitHub Actions (`ubuntu-latest`). Он предоставляется временно для каждого запуска и включает предустановленные инструменты разработки.

