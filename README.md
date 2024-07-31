# Развёртывание Docsify на GitHub Pages
1. Создать стандартный, открытый репозиторий на GitHub
2. Перейти в корень проекта Docsify и добавить все файлы проекта в репозиторий
3. Перейти на вкладку репозитория Settings
4. На вкладке Settings открыть в боковом меню вкладку Pages
5. Выбрать ветку на которую был запушен проект или ветку с которой будет выполняться развёртывание (обычно main) и нажать кнопку save
6. Подождать некоторен время, периодически обновляя страницу
7. После появления кнопки "Vizit page" перейти по ней
#### __Парсинг markdown со страницы docsify__
* Создать и развурнуть страницу docsify по инструкции выше
* __Важно!__ Для удачного парсинга ссылка на страницу docsify должна иметь вид:
```
https://ссылка на развёрнутую docsify страницу/README.md
```
* Пример:
```
https://y0ungm0rris.github.io/docsify_page/README.md
```
#### __Код парсера:__
```dart
var link = Uri.tryParse('ссылка на документ');

FutureBuilder<http.Response>
                  (
                    future: http.get(link!),
                    builder: (context, snapshot) {
                      if (snapshot.hasData) {
                        String markdown = snapshot.data!.body;
                        return MarkdownBody(data: markdown);
                      } else if (snapshot.hasError) {
                        return Text('Ошибка: ${snapshot.error}');
                      }
                      return const CircularProgressIndicator();
                    }
                )
```
