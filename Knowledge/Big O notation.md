---
tags:
  - Алгоритмы
---
**Биг О нотация** (Big O Notation) — это математический инструмент, используемый для описания временной и пространственной сложности алгоритмов. Она позволяет оценить, как время выполнения или потребление памяти алгоритма изменяется по мере увеличения размера входных данных.

## Основные принципы

- **Функция роста**: Биг О нотация фокусируется на самой высокой степени роста функции и игнорирует константы и низшие степени. Это позволяет сосредоточиться на наиболее значительном влиянии на производительность при больших входных данных.
  
- **Удобство выражения**: Она упрощает анализ алгоритмов, представляя сложность в виде стандартных классов, что помогает быстро сравнивать алгоритмы между собой.

## Основные категории Биг O нотации

### 1. **О(1) — Константная сложность**
Время выполнения не зависит от размера входных данных.

- **Пример**: Доступ к элементу массива по индексу.

### 2. **О(log n) — Логарифмическая сложность**
Время выполнения увеличивается логарифмически по мере увеличения размера входных данных.

- **Пример**: Бинарный поиск в отсортированном массиве.

### 3. **О(n) — Линейная сложность**
Время выполнения пропорционально размеру входных данных.

- **Пример**: Линейный поиск в массиве.

### 4. **О(n log n) — Линейно-логарифмическая сложность**
Сложность, характерная для многих эффективных алгоритмов сортировки, таких как слияние или быстрая сортировка.

- **Пример**: Быстрая сортировка (QuickSort) в среднем случае.

### 5. **О(n²) — Квадратичная сложность**
Время выполнения пропорционально квадрату размера входных данных.

- **Пример**: Алгоритм сортировки пузырьком.

### 6. **О(2^n) — Экспоненциальная сложность**
Время выполнения удваивается при каждом увеличении размера входных данных. Обычно встречается в задачах с высокой вычислительной сложностью, таких как генерация всех подмножеств.

- **Пример**: Решение задачи о рюкзаке методом перебора.

### 7. **О(n!) — Факториальная сложность**
Поскольку время выполнения пропорционально факториалу размера входных данных, считается одной из самых неэффективных сложностей.

- **Пример**: Полный перебор всех перестановок набора элементов.

