Добавляет пункт вычисления хеш суммы файла в контекстное меню Windows 
(в моем случае 11, но должно работать и на 10).

По сути просто выполняет Powershell команду над выбранным файлом и вставляет результат в буфер обмена в формате:
$название алгоритма$=$хеш сумма$

Пример:
SHA512=8996E74DFE96EE845BDD25E2FC5EC73A73073B2B7945693A6058182A19FD8486C4D7F03DE87A3369FB73A912411B8F9061A93F0FEF77C4D729157DE2F31E96BE

![image](https://github.com/user-attachments/assets/f8413458-cdf8-4d43-ab5d-3605f576d54f)
![image](https://github.com/user-attachments/assets/8da5d787-8c03-481a-801b-343f13ca6787)


В самой команде несколько популярных хешей:
(1-MD5, 2-SHA256, 3-SHA1, 4-SHA384, 5-SHA512)
Но вы можете добавить свои модифицировав команду:
```
powershell.exe -Command "& { $algorithms = @{1='MD5'; 2='SHA256'; 3='SHA1'; 4='SHA384'; 5='SHA512'}; $choice = [int](Read-Host 'Введите номер алгоритма (1-MD5, 2-SHA256, 3-SHA1, 4-SHA384, 5-SHA512)'); $algorithm = $algorithms[$choice]; if (-not $algorithm) { $algorithm = 'SHA256'; Write-Host 'Неверный выбор, используется SHA256' -ForegroundColor Yellow }; $hash = Get-FileHash '%1' -Algorithm $algorithm; Write-Output ($hash.Algorithm + '=' + $hash.Hash) | clip; Write-Host ('Скопировано: ' + $hash.Algorithm + '=' + $hash.Hash) }"
```

Файл реестра просто добавляет несколько значений:
![image](https://github.com/user-attachments/assets/7c139fac-aeae-4bee-8841-b532bd384c51)
![image](https://github.com/user-attachments/assets/fb6c3de6-2737-45b2-b190-5cb8dc7f20bb)

