# Лабораторная работа №7

## Ход работы

### 1. Установка и подготовка среды
Работа выполнялась в среде Fedora 14.0. Установлены следующие инструменты:
  
  ● clang — компилятор языка C/C++;
  
  ● llvm — инструменты анализа и оптимизации кода;
  
  ● opt — инструмент для работы с LLVM IR и применения оптимизаций;
  
  ● Graphviz — инструмент для визуализации кода.
  
Команда установки: ```sudo dnf install clang llvm```
  
![image_2025-05-14_12-18-53](https://github.com/user-attachments/assets/92a2aaa1-bcf0-427f-b19c-c89379ed6108)

![image](https://github.com/user-attachments/assets/fd2a4876-5c04-4426-ad64-9434b93f254d)

### 2. Исходный код
``` C
#include <stdio.h>
int main(void) {
  printf("Hello, LLVM!\n");
  return 0;
}
```
Сохранена в файл hello.c

![image](https://github.com/user-attachments/assets/86a8feb6-b977-4173-8ce2-057a56be896f)

### 3. Получение AST
Команда: ```clang -Xclang -ast-dump -fsyntax-only hello.c```
   
![image](https://github.com/user-attachments/assets/3b1c13b6-7a13-41ea-be65-53f9eaf1c254)

### 4. Генерация LLVM IR
Команда: ```clang -S -emit-llvm hello.c -o hello.ll```

![image](https://github.com/user-attachments/assets/c554f9ef-b14f-46f5-bb83-21e7738c6f31)

### 5. Оптимизация IR
Команда: ```opt -O2 hello.ll -S -o hello_opt.ll```

![image](https://github.com/user-attachments/assets/3c84552e-276e-480f-8c21-b9c359666c20)

Команда: ```diff -u hello.ll hello_opt.ll```
  
Сравнение двух файлов:

![image](https://github.com/user-attachments/assets/59f57d8a-c917-40d6-9838-be51a83f79aa)

Стоит отметить, что после оптимизации произошли следующие изменения:

  ● Переменные типа alloca были удалены;
  
  ● Код переведён в SSA-форму;
  
  ● Оптимизация улучшила читаемость и упростила поток управления.

### 6. Граф потока управления программы
Команда для генерации оптимизированного LLVM IR: ```opt -passes=dot-cfg -disable-output hello_opt.bc```

![image](https://github.com/user-attachments/assets/ac20eb93-d9c7-45e4-9579-d77e931a3bf5)

Команда для генерации .dot-файлов CFG для функций: ```dot -Tpng cfg.main.dot -o cfg_main.png```

![image](https://github.com/user-attachments/assets/26e81a1f-c704-4a95-a626-a3612df11e09)

## Команды терминала
```bash
sudo dnf install clang llvm
clang -Xclang -ast-dump -fsyntax-only hello.c
clang -S -emit-llvm hello.c -o hello.ll
opt -O2 hello.ll -S -o hello_opt.ll
diff -u hello.ll hello_opt.ll
```

## Скриншоты работы
![image_2025-05-14_12-18-53](https://github.com/user-attachments/assets/878fd8df-5c83-4d9b-ba02-b1b7b3eaf723)

![image](https://github.com/user-attachments/assets/2eadaa81-e871-4755-a906-88e88c861054)

![image](https://github.com/user-attachments/assets/a9ba7ad0-1953-4434-9c4b-16daf58ad8e3)

![image](https://github.com/user-attachments/assets/6d54772b-b1c3-42de-b979-e01878ee77ac)

![image](https://github.com/user-attachments/assets/b58f740d-9bf9-4f10-8690-9cdba7f76c92)

![image](https://github.com/user-attachments/assets/a57b2a09-71d8-440f-9076-6b6cb1779ba2)

![image](https://github.com/user-attachments/assets/db718cc0-306a-4b03-bb19-7725113b52de)

![image](https://github.com/user-attachments/assets/a82b6cfd-0380-4b99-bbc7-fcd2f52b18f9)

![image](https://github.com/user-attachments/assets/98ae4cc6-7ec8-4bcc-b7d7-d95451277c5c)

![image](https://github.com/user-attachments/assets/81901c24-19ff-484f-a30c-b72962bc3243)

![image](https://github.com/user-attachments/assets/1053b3ee-ee5a-4b92-8c09-ce3ac8a3247c)

![image](https://github.com/user-attachments/assets/58805fe9-75f6-4786-828f-9a6a315dd8ab)

![image](https://github.com/user-attachments/assets/2632be1f-d203-4908-b795-7d28c68a3d6f)

![image](https://github.com/user-attachments/assets/f86a5226-a726-4810-8a68-39b9c917ba00)

![image](https://github.com/user-attachments/assets/59352041-f58f-420a-b353-e8277b5f86ee)

![image](https://github.com/user-attachments/assets/23a76d3b-1e02-4e8f-b8cf-00a659ce1661)

![image](https://github.com/user-attachments/assets/092d9abd-fb3a-4d66-a237-e69078151721)

![image](https://github.com/user-attachments/assets/8c7f747a-6adf-4a77-846c-eb87d90e5136)

![image](https://github.com/user-attachments/assets/f327eee1-aa64-4ff8-a2e2-593180bd8a37)

![image](https://github.com/user-attachments/assets/57cfde4f-5e63-47ee-ba31-12caabe52d9d)

![image](https://github.com/user-attachments/assets/b624bef8-2719-4d16-a6a7-5167a821a31c)

## Промежуточные выводы по каждому заданию
1. **Установка Clang/LLVM на Fedora**  
   **Вывод:** Установлены все необходимые пакеты (`clang`, `llvm`, `llvm-tools-extra`, `lld`, `lldb`, `graphviz`), команды `clang`, `opt`, `llvm-dis` и `dot` доступны в PATH.

2. **Создание простого C-файла**  
   **Вывод:** Файл `hello.c` с корректным примером «Hello, LLVM!» создан; синтаксис проверен без ошибок.

3. **Генерация AST**  
   **Вывод:** AST успешно выгружено в `hello_ast.txt`. Структура дерева соответствует исходному коду (узел `FunctionDecl main`, внутри — `CallExpr printf` и др.).

4. **Генерация LLVM IR**  
   - **Текстовый IR (`hello.ll`):**  
     **Вывод:** Читаемая текстовая версия IR содержит определение функции `@main` и глобальные данные.  
   - **Биткод (`hello.bc`):**  
     **Вывод:** Файл `hello.bc` распознаётся командой `file` как «LLVM IR bitcode».

5. **Оптимизация IR с помощью `opt -O2`**  
   **Вывод:** Оптимизированный биткод `hello_opt.bc` и текстовый IR `hello_opt.ll` созданы. В `hello_opt.ll` удалены неиспользуемые блоки и константы, код упрощён.

6. **Построение графа потока управления (CFG)**  
   **Вывод:** Сгенерирован файл `cfg.main.dot` и успешно преобразован в изображение `cfg_main.png`. Граф отображает основные базовые блоки и переходы внутри `main`.

## Выводы
● С помощью Clang можно получить полную структуру AST и IR, а также CGF;

● LLVM предоставляет гибкие инструменты анализа и оптимизации;

● Промежуточное представление кода удобно для написания компиляторных трансформаций.

## Ответы на контрольные вопросы
1. **Что такое Clang, и какова его роль в процессе компиляции программ?**  
   Clang — это фронтенд компилятора для языков C, C++ и Objective-C, который разбирает исходный код, проверяет его на ошибки и строит абстрактное синтаксическое дерево (AST). Затем он переводит AST в представление LLVM IR, передавая его в бэкенд LLVM для оптимизации и генерации машинного кода.

2. **Что представляет собой LLVM и как он используется в современных компиляторах?**  
   LLVM — это модульная инфраструктура для компиляторов, включающая среду исполнения, оптимизаторы и бэкенды для разных архитектур. Фронтенды (например, Clang) транслируют исходный код в LLVM IR, после чего LLVM выполняет анализ, оптимизацию и генерацию машинного кода.

3. **Чем отличается абстрактное синтаксическое дерево (AST) от промежуточного представления LLVM IR?**  
   – AST отражает исходную структуру программы: имена переменных, синтаксические конструкции, вложенность выражений.  
   – LLVM IR — более низкоуровневое, трёадресное представление, близкое к ассемблеру, с операциями над виртуальными регистрами и простыми базовыми блоками.

4. **Для чего необходимо промежуточное представление (IR) в процессе компиляции?**  
   IR служит единым языком между фронтендом и бэкендом: на нём проводят разнообразные оптимизации, независимые от синтаксиса исходного языка и целевой архитектуры, а затем генерируют машинный код.

5. **Что делает инструкция `alloca` в LLVM IR, и зачем она используется в функциях?**  
   `alloca` выделяет область в стеке текущей функции для локальных переменных. Она генерирует динамическое смещение от указателя стека, позволяя использовать локальные буферы и хранить временные значения в памяти.

6. **Зачем нужна оптимизация кода в компиляторе, и какие основные цели она преследует?**  
   Основные цели оптимизации — сократить объём и время выполнения кода, уменьшить потребление памяти и энергопотребление. Это достигается удалением неиспользуемых переменных, упрощением арифметики, инлайнингом функций и улучшением расположения инструкций.

7. **Что такое SSA-форма и почему она важна при оптимизации программ?**  
   SSA (Static Single Assignment) — форма представления, в которой каждая переменная присваивается ровно один раз. Это упрощает анализ зависимостей и позволяет легко выполнять преобразования, такие как распространение констант и устранение мёртвого кода.

8. **Что такое граф потока управления (CFG) и как он помогает анализировать поведение программы?**  
   CFG — это ориентированный граф, вершины которого соответствуют базовым блокам кода, а рёбра — возможным переходам управления. CFG необходим для анализа путей выполнения, обнаружения циклов, точек входа и оптимизации, связанной с перемещением и переупорядочиванием кода.

9. **Как устроено представление арифметических операций в LLVM IR (например, умножение, сложение)?**  
   Арифметические операции в IR — это одноинструкционные команды вида `add`, `sub`, `mul`, `udiv`, `sdiv` и др. Они принимают два операнда (регистры или константы) и возвращают новый виртуальный регистр с результатом.

10. **Почему функции в LLVM IR обычно представляют собой отдельные единицы анализа и оптимизации?**  
    Функции инкапсулируют области видимости и контрольные потоки; разделение на функции позволяет локально выполнять оптимизации (инлайнинг, устранение мёртвого кода) и упрощает многопоточную компиляцию и кеширование результатов.

11. **Что происходит с функцией в LLVM IR, если она вызывается один раз и очень короткая?**  
    При оптимизации на уровне O2 и выше LLVM обычно инлайнит такие функции в их единственное место вызова, устраняя накладные расходы на переход и упрощая общий CFG.

12. **Какие преимущества даёт использование IR и CFG для автоматических оптимизаций по сравнению с анализом исходного текста на C?**  
    – IR абстрагирует платформу и синтаксис, что упрощает разработку универсальных оптимизаций.  
    – CFG обеспечивает явную модель переходов управления, необходимую для сложных оптимизаций (распараллеливание, ветвления, устранение ветвей).  
    – Анализ на уровне IR быстрее и надёжнее, чем попытки переанализировать исходный код с учётом всех синтаксических особенностей.  


Вариант 7. Объявление массива символов с инициализацией строковой константой

Тема: char msg[] = "Hello"; и вывод msg[1].

Исходный код (variant7.c):

#include <stdio.h>

int main(void) {
    char msg[] = "Hello";
    printf("%c\n", msg[1]);  // ожидаемый вывод: 'e'
    return 0;
}


## Дополнительное задание Вариант 7

![image](https://github.com/user-attachments/assets/554b53da-436e-4b34-ab51-5dba198b5f53)

IR без оптимизаций (`-O0`):

```clang -S -emit-llvm -O0 variant7.c -o variant7_O0.ll```

![image](https://github.com/user-attachments/assets/3e7fe4e0-108b-444c-b03a-efb09d1f4076)

Фрагмент IR (`variant7_O0.ll`):

```@.str = private unnamed_addr constant [6 x i8] c"Hello\00", align 1```
```
define i32 @main() {
entry:
  %ptr = getelementptr inbounds [6 x i8], [6 x i8]* @.str, i64 0, i64 1
  %ch  = load i8, i8* %ptr, align 1
  %ext = sext i8 %ch to i32
  call i32 (i8*, ...) @printf(i8* getelementptr inbounds ([4 x i8], [4 x i8]* @.str.printf, i32 0, i32 0), i32 %ext)
  ret i32 0
}
```

![image](https://github.com/user-attachments/assets/fd1eff18-5bf5-445f-9efe-8e06598743a6)


**Вывод:** Строка хранится в глобальной константе `@.str`. Доступ к `msg[1]` реализован через `getelementptr` и `load`.

IR с оптимизацией (`-O2`):

```clang -S -emit-llvm -O2 variant7.c -o variant7_O2.ll```

![image](https://github.com/user-attachments/assets/49b090b7-4ad9-4a6d-906c-0f7131f5997e)

Фрагмент IR (`variant7_O2.ll`):

```@.str = private unnamed_addr constant [6 x i8] c"Hello\00", align 1```
```
define i32 @main() #0 {
entry:
  %0 = getelementptr inbounds [6 x i8], [6 x i8]* @.str, i64 0, i64 1
  %1 = load i8, i8* %0, align 1
  %2 = sext i8 %1 to i32
  call i32 (i8*, ...) @printf(i8* getelementptr inbounds ([4 x i8], [4 x i8]* @.str.printf, i32 0, i32 0), i32 %2)
  ret i32 0
}
```

![image](https://github.com/user-attachments/assets/38e0aacf-4a5b-4d32-b4e8-25048b1d7c59)

**Вывод:** Оптимизация не меняет структуру доступа: используется всё та же пара `getelementptr` + `load`, так как вычисление индекса выполняется во время выполнения.
