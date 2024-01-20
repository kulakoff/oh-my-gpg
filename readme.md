# GnuPG todo
# Создать ключ
упрощенная версия диалога
```
gpg --gen-key
```
полный диалог при создании ключа
```
gpg --full-generate-key
```
# Список имеющихся ключей
```
gpg --list-keys --keyid-format long
```
```
anton@localhost:~> gpg --list-keys --keyid-format long
/home/anton/.gnupg/pubring.kbx
------------------------------
pub   ed25519/506AA485B568B8A4 2024-01-20 [SC] [   годен до: 2027-01-19]
      C9F9D91EABBD9749BC7B66C9506AA485B568B8A4
uid               [  абсолютно ] Василий Пупкин <vpupkin@example.com>
sub   cv25519/D1667A1286F719A2 2024-01-20 [E] [   годен до: 2027-01-19]

pub   ed25519/F3B5B016B821946A 2024-01-20 [SC]
      A5A15E988F7F8210BF75D257F3B5B016B821946A
uid               [  абсолютно ] Семен Семенович <semenich@example.com>
sub   cv25519/FB99554F5EA45E31 2024-01-20 [E]
```
# Вывод отпечатка ключа
```
gpg --fingerprint
```
```
anton@localhost:~> gpg --fingerprint  FB99554F5EA45E31
pub   ed25519 2024-01-20 [SC]
      A5A1 5E98 8F7F 8210 BF75  D257 F3B5 B016 B821 946A
uid         [ неизвестно ] Семен Семенович <semenich@example.com>
sub   cv25519 2024-01-20 [E]

```

# Экспорт
### Экспорт публичного ключа
Опция --armor сокращенный вариант -a  
для вывода содержимого ключа в Radix 64 (base 64)
```
gpg --export --armor username@example.com
```
экспорт в файл
```
gpg --export --armor username@example.com > public_key.asc
```
### Экспорт приватного ключа
Потребуется пароль который был указан при создании ключа
```
gpg --export-secret-key -a username@example.com
```
экспорт в файл
```
gpg --export-secret-key -a username@example.com > private_key.asc
```

# Импорт
### Импорт публичного ключа
расширение файла не имеет значение
```
gpg --import public_key.asc
```
### Импорт приватного ключа
При импорте потребуется пороль который был указан при создании ключа
```
gpg --import private_key.asc
```

# Удалить ключ
Если есть приватный ключ, то gpg сперва потребует удалить его.
### Удаление приватного ключа
```
gpg --delete-secret-keys FB99554F5EA45E31
```
### Удаление публичного ключа
```
gpg --delete-keys FB99554F5EA45E31
```
----
# Распространение ключей
Отправка на серверпубличных ключей
```
gpg --send-keys FB99554F5EA45E31
```
Указать собственный серер
```
gpg --keyserver keyring.debian.org --recv-keys FB99554F5EA45E31
```

# Обновить срок действия ключа
```
gpg --edit-key D1667A1286F719A2
expire
```