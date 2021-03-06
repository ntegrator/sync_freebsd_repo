# sync_freebsd_repo
## Скрипт для синхронизации бинарных репозиториев FreeBSD.

В файле settings.ini необходимо указать следующие параметры:
- [repo] - Название репозитория. Например, *[repo11]*
- path - Путь к локальной копии репозитория. Например, *path = /tanker2/freebsd*
- mirror_url - Зеркало для синхронизации. Например, *mirror_url = http://pkg0.nyi.freebsd.org* (mirror_url = https://pkg.freebsd.org и т.д.)
- arch - Архитектура и версия FreeBSD (как в репозитории). Например, *arch = FreeBSD:11:amd64*
- release - Релиз FreeBSD (как в репозитории). Например, *release = latest* (*release = quarterly*, *release = release_0* и т.д.)
- tries - Количество попыток загрузки каждого файла в папке All/. Значение 0 соответствует бесконечному числу попыток (пока sha256sum не будет соответствовать заявленной). Не работает, если параметр *fast = yes*. Например, *tries = 0*.
- fast - Если *fast = yes*, репозиторий загружается без проверки shasum пакетов. Если *fast = no*, каждый файл в папке All/ проверяется на соответствие shasum. 

В файле settings.ini может быть указано любое количество репозиториев с различными параметрами. Например:

```
[repo11]
path = /tanker2/freebsd
mirror_url = http://pkg0.nyi.freebsd.org
arch = FreeBSD:11:amd64
release = latest
tries = 0
fast = no
[repka12]
path = /other_path/free12
mirror_url = http://pkg0.bme.freebsd.org
arch = FreeBSD:12:amd64
tries = 1
fast = yes
[repo11_arch386]
path = /other_path2/free12
mirror_url = http://pkg0.pkt.freebsd.org
arch = FreeBSD:11:i386
release = latest
tries = 2
```

Если существует локальная копия репозитория по заданному пути (*path*), скрипт проверит актуальность пакетов, удалит старые версии и скачает новые. 
Если локальной копии нет, скрипт полностью создаст её.
