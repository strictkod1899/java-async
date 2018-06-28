# Описание программы

Программа представляет пример запуска асинхронных методов.
Для сравнения, также запускаются обычные (последовательные) методы.

# Описание реализации
## Последовательность выполнения программы
Программа запускает методы в следующем порядке:
1. AsyncExecutionUsingGetMethod - задачи запустятся и выполнятся асинхронно, но вернут результат в последовательности вызова метода `get()` у объекта `FutureTask`;
2. AsyncExecution - задачи выполнятся асинхронно. Запуск задач произойдет последовательно, но они будут выполнены асинхронно;
3. SequentialExecution - задачи выполнятся последовательно.

## Процесс запуска задач асинхронно
Асинхронные методы описываются в методе `call` при реализации интерфейса `Callable`. В примере, этот интерфейс реализуют 3 класса `TaskShort`, `TaskMedium`, `TaskLong`, которые выводят информационные сообщения в консоль и в случае вызова у объекта `FutureTask` метода `get()`, будет возвращено сообщение, которое передается в их конструктор.
1. TaskShort выполняет задачу с задержкой в 2 секунды;
2. TaskMedium выполняет задачу с задержкой в 5 секунд;
3. TaskLong выполняет задачу с задержкой в 10 секунд.

В дальнейшем реализованные объекты `TaskXxx` должны быть переданны в конструктор класса `FutureTask`.

Непосредственно, для запуска задач (методов) асинхронно, используется пул потоков `ExecutorService`, который создается следующим способом:

`ExecutorService pool = Executors.newFixedThreadPool(3);`

В данном случае, создан пул потоков с ограничением на 3 выполняемые задачи.

Чтобы добавить задачу в пул потоков и начать ее выполнение, используется метод `submit`, в который передается объект класса `FutureTask`, после чего задачи начнут свое выполнение асинхронно.

Для того, чтобы заставить программу ожидать завершения какой-либо задачи, используется метод 'get()' у объекта `FutureTask`.


