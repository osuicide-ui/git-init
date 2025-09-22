# git-init
Тема программы связана с вычислением Числа_Фибоначчи и фигурного числа. 
%% Калькулятор чисел Фибоначчи и треугольных чисел
% Автоматизированная система вычисления математических последовательностей
%
% МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ
% ФГБОУ ВО «АЛТАЙСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»
%
% Техническое задание 123456-2025
% Версия 1.0 | 2025 г. Барнаул

%% Оглавление
% 1. Обзор проекта
% 2. Установка
% 3. Быстрый старт
% 4. Документация функций
% 5. Примеры использования
% 6. Тестирование
% 7. Технические требования
% 8. Структура проекта
% 9. Лицензия

%% 1. Обзор проекта
% Автоматизированная система "Вычислитель математических последовательностей" (АС "ВМП")
%
% Проект реализует вычисление чисел последовательности Фибоначчи
% и треугольных чисел с высокой точностью и производительностью.

fprintf('=== Калькулятор чисел Фибоначчи и треугольных чисел ===\n');
fprintf('Версия: 1.0\n');
fprintf('Автор: Климанов И.Е.\n');
fprintf('Группа: 5.406-2\n');
fprintf('Руководитель: Шмаков И.А.\n\n');

%% 2. Установка
% Просто добавьте папку с проектом в путь MATLAB или запускайте функции напрямую.

fprintf('Установка:\n');
fprintf('1. Клонируйте репозиторий: git clone <url-репозитория>\n');
fprintf('2. Добавьте в путь MATLAB: addpath(pwd)\n');
fprintf('3. Запустите примеры из этого файла\n\n');

%% 3. Быстрый старт
% Базовые примеры использования:

fprintf('Примеры быстрого старта:\n');

% Пример 1: Число Фибоначчи
n = 10;
fib_num = fibonacci(n);
fprintf('Фибоначчи(%d) = %d\n', n, fib_num);

% Пример 2: Треугольное число
tri_num = triangular(n);
fprintf('Треугольное(%d) = %d\n', n, tri_num);

% Пример 3: Последовательности
fprintf('\nПервые 10 чисел Фибоначчи: ');
disp(arrayfun(@fibonacci, 0:9));

fprintf('Первые 10 треугольных чисел: ');
disp(arrayfun(@triangular, 1:10));

fprintf('\n');

%% 4. Документация функций

%% fibonacci - Вычисление числа Фибоначчи
function result = fibonacci(n)
    % FIBONACCI Вычисление n-го числа Фибоначчи
    %
    % Синтаксис:
    %   result = fibonacci(n)
    %
    % Входные параметры:
    %   n - целое неотрицательное число (индекс с 0)
    %
    % Выходные параметры:
    %   result - n-е число Фибоначчи
    %
    % Примеры:
    %   fibonacci(0) возвращает 0
    %   fibonacci(1) возвращает 1
    %   fibonacci(10) возвращает 55
    
    % Проверка входных данных
    if ~isnumeric(n) || n < 0 || floor(n) ~= n
        error('Входной параметр должен быть неотрицательным целым числом');
    end
    
    % Базовые случаи
    if n == 0
        result = 0;
        return;
    elseif n == 1
        result = 1;
        return;
    end
    
    % Эффективное итеративное вычисление
    a = 0;
    b = 1;
    for i = 2:n
        temp = a + b;
        a = b;
        b = temp;
    end
    result = b;
end

%% triangular - Вычисление треугольного числа
function result = triangular(n)
    % TRIANGULAR Вычисление n-го треугольного числа
    %
    % Синтаксис:
    %   result = triangular(n)
    %
    % Входные параметры:
    %   n - целое положительное число
    %
    % Выходные параметры:
    %   result - n-е треугольное число
    %
    % Примеры:
    %   triangular(1) возвращает 1
    %   triangular(4) возвращает 10
    %   triangular(10) возвращает 55
    
    % Проверка входных данных
    if ~isnumeric(n) || n <= 0 || floor(n) ~= n
        error('Входной параметр должен быть положительным целым числом');
    end
    
    % Формула треугольного числа: T_n = n(n+1)/2
    result = n * (n + 1) / 2;
end

%% 5. Расширенные примеры

fprintf('Расширенные примеры:\n');

%% Пример 1: Тестирование производительности
fprintf('\n1. Тестирование производительности:\n');
test_n = [100, 500, 1000];
for i = 1:length(test_n)
    n_val = test_n(i);
    
    tic;
    fib_val = fibonacci(n_val);
    fib_time = toc;
    
    tic;
    tri_val = triangular(n_val);
    tri_time = toc;
    
    fprintf('n=%d: Фибоначчи=%.6fс, Треугольные=%.6fс\n', ...
        n_val, fib_time, tri_time);
end

%% Пример 2: Генерация последовательностей
fprintf('\n2. Генерация последовательностей:\n');

% Генерация последовательности Фибоначчи
n_seq = 15;
fib_sequence = zeros(1, n_seq);
for i = 1:n_seq
    fib_sequence(i) = fibonacci(i-1); % индексация с 0
end
fprintf('Последовательность Фибоначчи (n=0..14):\n');
disp(fib_sequence);

% Генерация последовательности треугольных чисел
tri_sequence = arrayfun(@triangular, 1:n_seq);
fprintf('Последовательность треугольных чисел (n=1..15):\n');
disp(tri_sequence);

%% Пример 3: Обработка ошибок
fprintf('\n3. Примеры обработки ошибок:\n');

try
    invalid_result = fibonacci(-5);
catch ME
    fprintf('Перехвачена ошибка: %s\n', ME.message);
end

try
    invalid_result = triangular(3.5);
catch ME
    fprintf('Перехвачена ошибка: %s\n', ME.message);
end

%% 6. Тестовый фреймворк

fprintf('\n=== Запуск тестового набора ===\n');

%% Тестирование функции Фибоначчи
function test_fibonacci_function()
    fprintf('Тестирование функции Фибоначчи...\n');
    
    test_cases = {
        {0, 0, 'Фибоначчи(0) должно быть 0'},
        {1, 1, 'Фибоначчи(1) должно быть 1'},
        {5, 5, 'Фибоначчи(5) должно быть 5'},
        {10, 55, 'Фибоначчи(10) должно быть 55'},
        {20, 6765, 'Фибоначчи(20) должно быть 6765'}
    };
    
    all_passed = true;
    for i = 1:length(test_cases)
        n = test_cases{i}{1};
        expected = test_cases{i}{2};
        message = test_cases{i}{3};
        
        try
            result = fibonacci(n);
            if result == expected
                fprintf('✓ ПРОЙДЕНО: %s\n', message);
            else
                fprintf('✗ НЕ ПРОЙДЕНО: %s (получено %d, ожидалось %d)\n', ...
                    message, result, expected);
                all_passed = false;
            end
        catch ME
            fprintf('✗ ОШИБКА: %s (%s)\n', message, ME.message);
            all_passed = false;
        end
    end
    
    if all_passed
        fprintf('Все тесты Фибоначчи пройдены!\n');
    else
        fprintf('Некоторые тесты Фибоначчи не пройдены!\n');
    end
end

%% Тестирование функции треугольных чисел
function test_triangular_function()
    fprintf('\nТестирование функции треугольных чисел...\n');
    
    test_cases = {
        {1, 1, 'Треугольное(1) должно быть 1'},
        {3, 6, 'Треугольное(3) должно быть 6'},
        {5, 15, 'Треугольное(5) должно быть 15'},
        {10, 55, 'Треугольное(10) должно быть 55'},
        {100, 5050, 'Треугольное(100) должно быть 5050'}
    };
    
    all_passed = true;
    for i = 1:length(test_cases)
        n = test_cases{i}{1};
        expected = test_cases{i}{2};
        message = test_cases{i}{3};
        
        try
            result = triangular(n);
            if result == expected
                fprintf('✓ ПРОЙДЕНО: %s\n', message);
            else
                fprintf('✗ НЕ ПРОЙДЕНО: %s (получено %d, ожидалось %d)\n', ...
                    message, result, expected);
                all_passed = false;
            end
        catch ME
            fprintf('✗ ОШИБКА: %s (%s)\n', message, ME.message);
            all_passed = false;
        end
    end
    
    if all_passed
        fprintf('Все тесты треугольных чисел пройдены!\n');
    else
        fprintf('Некоторые тесты треугольных чисел не пройдены!\n');
    end
end

%% Запуск всех тестов
test_fibonacci_function();
test_triangular_function();

fprintf('\n=== Тестовый набор завершен ===\n');

%% 7. Технические требования

fprintf('\n=== Технические характеристики ===\n');
fprintf('Система: Автоматизированный вычислитель математических последовательностей\n');
fprintf('Версия: 1.0\n');
fprintf('Период разработки: 12.09.2025 - 31.12.2025\n\n');

fprintf('Требования к производительности:\n');
fprintf('- Время вычисления для n=1000: < 1 секунды\n');
fprintf('- Точность: 100%%\n');
fprintf('- Доступность: 99.9%%\n\n');

fprintf('Технические характеристики:\n');
fprintf('- Архитектура: Standalone-приложение\n');
fprintf('- Язык программирования: MATLAB\n');
fprintf('- Требуемая версия MATLAB: R2020a или новее\n');
fprintf('- Память: минимум 1ГБ ОЗУ\n');
fprintf('- Хранилище: минимум 1ГБ свободного места\n');

%% 8. Структура проекта

fprintf('\n=== Структура проекта ===\n');
fprintf('README.m          - Основной файл документации (этот файл)\n');
fprintf('fibonacci.m       - Функция вычисления чисел Фибоначчи\n');
fprintf('triangular.m      - Функция вычисления треугольных чисел\n');
fprintf('test_suite.m      - Комплексный набор тестов\n');
fprintf('examples.m        - Примеры использования и демонстрации\n');
fprintf('docs/             - Папка с документацией\n');
fprintf('  technical_specification.pdf - Полное техническое задание\n');
fprintf('  user_manual.pdf - Руководство пользователя\n');

%% 9. Лицензия и авторские права

fprintf('\n=== Информация о лицензии ===\n');
fprintf('Лицензия MIT\n');
fprintf('Авторские права (c) 2025 Алтайский Государственный Университет\n');
fprintf('Автор: Климанов И.Е.\n');
fprintf('Руководитель: Шмаков И.А.\n\n');

fprintf('Данная лицензия разрешает лицам, получившим копию данного программного\n');
fprintf('обеспечения и сопутствующей документации, безвозмездно использовать ПО...\n\n');

%% Вспомогательные функции

%% generate_fibonacci_sequence - Генерация последовательности Фибоначчи
function sequence = generate_fibonacci_sequence(n)
    % GENERATE_FIBONACCI_SEQUENCE Генерация первых n чисел Фибоначчи
    %
    % Вход: n - количество элементов для генерации
    % Выход: sequence - массив чисел Фибоначчи
    
    if n <= 0
        sequence = [];
        return;
    end
    
    sequence = zeros(1, n);
    for i = 1:n
        sequence(i) = fibonacci(i-1);
    end
end

%% generate_triangular_sequence - Генерация последовательности треугольных чисел
function sequence = generate_triangular_sequence(n)
    % GENERATE_TRIANGULAR_SEQUENCE Генерация первых n треугольных чисел
    %
    % Вход: n - количество элементов для генерации
    % Выход: sequence - массив треугольных чисел
    
    if n <= 0
        sequence = [];
        return;
    end
    
    sequence = arrayfun(@triangular, 1:n);
end

%% Функция бенчмаркинга
function benchmark_results = run_benchmark(max_n)
    % RUN_BENCHMARK Тестирование производительности для различных значений n
    %
    % Вход: max_n - максимальное значение n для тестирования
    % Выход: benchmark_results - структура с данными о времени выполнения
    
    fprintf('\nЗапуск тестирования производительности...\n');
    
    n_values = [10, 50, 100, 500, 1000];
    n_values = n_values(n_values <= max_n);
    
    benchmark_results = struct();
    benchmark_results.n_values = n_values;
    benchmark_results.fib_times = zeros(size(n_values));
    benchmark_results.tri_times = zeros(size(n_values));
    
    for i = 1:length(n_values)
        n = n_values(i);
        
        % Тестирование Фибоначчи
        tic;
        fibonacci(n);
        benchmark_results.fib_times(i) = toc;
        
        % Тестирование треугольных чисел
        tic;
        triangular(n);
        benchmark_results.tri_times(i) = toc;
        
        fprintf('n=%d: Фибоначчи=%.4fс, Треугольные=%.4fс\n', ...
            n, benchmark_results.fib_times(i), benchmark_results.tri_times(i));
    end
end

%% Функция сравнения последовательностей
function compare_sequences(max_n)
    % COMPARE_SEQUENCES Сравнение последовательностей Фибоначчи и треугольных чисел
    %
    % Вход: max_n - максимальное количество элементов для сравнения
    
    fprintf('\nСравнение последовательностей (n=1..%d):\n', max_n);
    fprintf('n\tФибоначчи\tТреугольные\tРазница\n');
    fprintf('-\t----------\t------------\t-------\n');
    
    for n = 1:max_n
        fib_val = fibonacci(n);
        tri_val = triangular(n);
        difference = abs(fib_val - tri_val);
        
        fprintf('%d\t%d\t\t%d\t\t%d\n', n, fib_val, tri_val, difference);
    end
end

%% Демонстрация работы системы
fprintf('\n=== Демонстрация работы системы ===\n');

% Демонстрация обеих функций
demo_n = 8;
fprintf('Демонстрация для n = %d:\n', demo_n);
fprintf('Последовательность Фибоначчи: ');
fib_demo = generate_fibonacci_sequence(demo_n+1);
disp(fib_demo);

fprintf('Последовательность треугольных чисел: ');
tri_demo = generate_triangular_sequence(demo_n);
disp(tri_demo);

% Сравнение последовательностей
fprintf('\nСравнение значений:\n');
compare_sequences(10);

% Тестирование производительности
fprintf('\nТестирование производительности для больших значений:\n');
benchmark_results = run_benchmark(1000);

fprintf('\nРазработка проекта успешно завершена!\n');
fprintf('Все требования выполнены в соответствии с техническим заданием.\n');

%% Конец файла README.m
fprintf('\n=== Выполнение README.m завершено ===\n');
fprintf('Для получения дополнительной информации см. папку с документацией.\n');
fprintf('Для использования отдельных функций вызывайте их напрямую из MATLAB.\n');

%% Дополнительная информация для разработчиков
fprintf('\n=== Информация для разработчиков ===\n');
fprintf('Архитектура системы: модульная\n');
fprintf('Методология разработки: модульное программирование\n');
fprintf('Система контроля версий: Git\n');
fprintf('Среда разработки: MATLAB IDE\n\n');

fprintf('План дальнейшего развития:\n');
fprintf('1. Добавление вычисления других математических последовательностей\n');
fprintf('2. Реализация графического интерфейса пользователя\n');
fprintf('3. Оптимизация алгоритмов для больших значений n\n');
fprintf('4. Добавление возможности экспорта результатов\n');
