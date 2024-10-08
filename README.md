1. **Откройте настройки шаблонов:**  File > Settings > Editor > Live Templates.

2. **Найдите/создайте шаблон `rsc`:**  Убедитесь, что у вас есть шаблон `rsc` в разделе `React`.

3. **Измените шаблон:** В поле "Template text" используйте следующий код:

```javascript
import { FC } from 'react';

interface $TM_FILENAME_BASE$Props {
  
}

export const $TM_FILENAME_BASE$:FC<$TM_FILENAME_BASE$Props> = ({}) => {
 return (
  <div>
   $END$
  </div>
 );
};
```

4. **Настройте переменную `TM_FILENAME_BASE`:** Нажмите "Edit variables". Для переменной `TM_FILENAME_BASE` выберите  "Expression" и вставьте следующий Groovy скрипт:

```groovy
groovyScript("def file = new File(_editor.virtualFile.path); def parent = file.parentFile; return parent.name")
```

5. **Сохраните изменения:** Нажмите "OK" в окне редактирования переменных и "OK" в окне настроек Live Templates.

**Объяснение:**

Этот Groovy скрипт непосредственно обращается к объекту файла в WebStorm и извлекает имя родительской папки. Это более надежный способ, чем манипуляции со строками пути, так как он учитывает особенности файловой системы и WebStorm API.

**Если это *все еще* не работает:**

* **Проверьте наличие ошибок:** После применения шаблона, если имя компонента все еще генерируется неправильно, проверьте вкладку "Event Log" в WebStorm на наличие ошибок, связанных с Live Templates. Это может дать подсказки о причине проблемы.
* **Упрощенный вариант (для проверки):**  Создайте временную переменную с простым Groovy скриптом, например: `groovyScript("return 'Test'")`. Если этот скрипт работает и подставляет `Test` в шаблон, значит, проблема не в Groovy, а в самом скрипте для получения имени папки.
* **Абсолютный путь:** Для отладки можно временно использовать вывод абсолютного пути родительской папки:  `groovyScript("def file = new File(_editor.virtualFile.path); def parent = file.parentFile; return parent.absolutePath")`. Это поможет понять, правильно ли WebStorm определяет родительскую папку.

Если ни один из этих вариантов не помог, пожалуйста, предоставьте следующую информацию для дальнейшей диагностики:

* **Скриншот настроек Live Template для `rsc`.**
* **Скриншот структуры проекта, показывающий расположение папки и файла компонента.**
* **Логи из Event Log (если есть ошибки).**

С этой информацией я смогу лучше понять контекст и предложить более точное решение.
