Webdav-client
===========

Пакет webdav-client обеспечивает легкую и удобную работу с такими webdav-серверами, как Yandex.Disk, DropBox, Google Drive, One Drive.
В данный пакет включены следующие компоненты: webdav API, resource API и webdav tool.

Установка
===========
* через pypi
* через easy_install

Webdav API - представляет из себя набор webdav-методов работы с облачными хранилищами. В этот набор входят следующие методы: check, free, list, mkdir, clean, copy, move, download, upload, publish, unpublish, published.

Примеры
===========

Настройка клиента
=======
```python
import webdav-client as webdav
options = {
    'webdav_hostname': "https://webdav.yandex.ru",
    'webdav_login': "login",
    'webdav_paassword': "password"
}
client = webdav.Client(options)
```

Синхронные методы
=========

Проверка существования ресурса
=======
```python
client.check("dir1/file1")
client.check("dir1/")
```

Проверка свободного места
=======
```python
free_size = client.free()
```

Получение списка ресурсов
=======
```python
files1 = client.list()
files2 = client.list("dir1")
```

Создание директории
=======
```python
client.mkdir("dir1/dir2")
```

Удаление ресурса
=======
```python
client.clean("dir1/dir2/")
```

Копирование ресурса
=======
```python
client.copy(remote_path_from="dir1/file1", remote_path_to="dir2/file1")
```

Перемещения ресурса
=======
```python
client.move(remote_path_from="dir1/file1", remote_path_to="dir2/file1")
```

Загрузка ресурса
=======
```python
client.download_sync(remote_path="dir1/file1", local_path="~/Downloads/file1")
client.download_sync(remote_path="dir1/dir2/", local_path="~/Downloads/dir2/")
```

Выгрузки ресурса
=======
```python
client.upload_sync(remote_path="dir1/file1", local_path="~/Documents/file1")
client.upload_sync(remote_path="dir1/dir2/", local_path="~/Documents/dir2/")
```

Публикация ресурса
=======
```python
link = client.publish("dir1/file1")
```

Публикация ресурса
=======
```python
link = client.publish("dir1/file1")
```

Отмена публикации ресурса
=======
```python
client.unpublish("dir1/file1")
```

Обработка исключений
=======
```python
try:
    ...
except WebDavException as e:
    loggin_except(e)
```

Ассинхронные методы
=========
Загрузка ресурса
=======
```python
client.download_async(remote_path="dir1/file1", local_path="~/Downloads/file1", callback=callback)
client.download_async(remote_path="dir1/dir2/", local_path="~/Downloads/dir2/", callback=callback)
```

Выгрузки ресурса
=======
```python
client.upload_async(remote_path="dir1/file1", local_path="~/Documents/file1", callback=callback)
client.upload_async(remote_path="dir1/dir2/", local_path="~/Documents/dir2/", callback=callback)
```

Resource API
===========

Resource API - используя концепцию ООП, обеспечивает работу с облачными хранилищами на уровне ресурсов.

Получение ресурса
=======

```python
res1 = client.resource("dir1/file1")
```

Работа с ресурсом
=======

```python
res1.rename("file2")

res1.move("dir1/file2")

res1.copy("dir2/file1")

info = res1.info()

res1.read_from(buffer)

res1.read(local_path="~/Documents/file1")

res1.read_async(local_path="~/Documents/file1", callback)

res1.write_to(buffer)

res1.write(local_path="~/Downloads/file1")

res1.write_async(local_path="~/Downloads/file1", callback)
```

Webdav tool
===========

Webdav tool - кросплатформенная утилита, обеспечивающая удобную работы с webdav-серверами прямо из Вашей консоли. Помимо полной реализации методов из webdav API, также добавлены методы синхронизации содержимого локальной и удаленной директории.

Аутентификация:
=======

```bash
$ webdav login https://wedbav.yandex.ru -p http://127.0.0.1:8080
webdav_login: w_login
webdav_password: w_password
proxy_login: p_login
proxy_password: p_password
```

Работа с утилитой
=======
```bash
$ webdav -h
$ webdav check file1
$ webdav free
245234120344
$ webdav ls dir1
file1
...
fileN
$ webdav mkdir dir2
$ webdav copy dir1/file1 -t dir2/file1
$ webdav mode dir2/file1 -t dir2/file2
$ webdav download dir1/file1 -t ~/Downloads/file1
$ webdav upload dir2/file2 -f ~/Documents/file1
$ webdav publish di2/file2
https://yadi.sk/i/vWtTUcBucAc6k
$ webdav unpublish di2/file2
```

TODO:
* adding cert
* adding sync
* adding progress bar for download and upload