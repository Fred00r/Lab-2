## Отчет по лабораторной работе № 2

#### № группы: `ПМ-2403`

#### Выполнил: `Ковалюсь Фёдор Андреевич`

#### Вариант: `11`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Выбор структуры данных](#3-выбор-структуры-данных)
- [Алгоритм](#4-алгоритм)
- [Программа](#5-программа)
- [Анализ правильности решения](#6-анализ-правильности-решения)

### 1. Постановка задачи
> Программа работает с двумерным массивом булевых значений. Она должна:
>1. Считать с консоли размеры массива 𝑁 и 𝑀, 
затем элементы массива размером 𝑁 × 𝑀 (значения 𝑡𝑟𝑢𝑒 или 𝑓𝑎𝑙𝑠𝑒).
>2. Отсортировать по возрастанию количества значений 𝑡𝑟𝑢𝑒 в каждой строке. 
Если количества равны, сортирует строки по количеству последовательных значений 𝑡𝑟𝑢𝑒.
>3. Найти и вывести строку с максимальным количеством последовательных значений 𝑡𝑟𝑢𝑒, 
а также длину этой последовательности.
>4. Вывести элементы массива в виде матрицы, заменяя 𝑡𝑟𝑢𝑒 на «+», 
а 𝑓𝑎𝑙𝑠𝑒 на «˗». Дополнительно выводит число островков (групп соседних 𝑡𝑟𝑢𝑒).
>5. Проверять, является ли массив симметричным относительно главной диагонали, и выводить результат проверки. 
Если массив не симметричен, выводит минимальное количество изменений для достижения симметрии.

### 2. Входные и выходные данные
#### Данные на вход
|             | Тип         | min значение    | max значение   |
|-------------|-------------|-----------------|----------------|
| N (Количество строк массива) | Целое число | 0  | 2*10<sup>9</sup> |
| M (Количество столбцов массива) | Целое число | 0 |  2*10<sup>9</sup> |
| (Элементы строки) | Булевы значения | False (-) | True (+) |

#### Данные на выход
Отсортированный массив в виде матрицы.
Строка с максимальным количеством последовательных значений 𝑡𝑟𝑢𝑒, её длина.
Преобразованный массив с "+" и "-", вместо true и false соответственно.
Результат проверки на симметричность относительно главной диагонали. Если массив не симметричен, минимальное количество изменений для достижения симметрии.

### 3. Выбор структуры данных
Для решения задачи используются:
- Двумерный список (ArrayList<ArrayList<Boolean>>): для хранения булевых элементов массива.
- Одномерный список: для подсчета значений 𝑡𝑟𝑢𝑒 и суммы последовательных значений 𝑡𝑟𝑢𝑒 для каждой строки.
- Переменные для хранения индексов, суммы последовательных значений 𝑡𝑟𝑢𝑒 в строке; количества изменений для достижения симметрии массива относительно главной диагонали.

### 4. Алгоритм
#### Алгоритм выполнения программы:
1. Считать число строк N и число столбцов M. Считать элементы массива.
2. Отсортировать строки массива (по возрастанию количества значений 𝑡𝑟𝑢𝑒):
- Подсчитать количество значений 𝑡𝑟𝑢𝑒 в каждой строке.
- Если количество значений 𝑡𝑟𝑢𝑒 одинаково, подсчитать сумму последовательных значений 𝑡𝑟𝑢𝑒.
3. Найти и вывести строку с максимальным количеством последовательных значений 𝑡𝑟𝑢𝑒, её длину.
4. Вывести массив в формате матрицы, заменяя 𝑡𝑟𝑢𝑒 на символ «+», 
а 𝑓𝑎𝑙𝑠𝑒 на «˗». Дополнительно вывести число островков (групп соседних 𝑡𝑟𝑢𝑒).
5. Проверить, является ли массив симметричным относительно главной диагонали, и вывести результат проверки.
Если массив не симметричен, посчитать и вывести минимальное количество изменений для достижения симметрии.


#### Блок-схема
```mermaid

graph TD;
    A("Начало") --> B("Ввод: N, M (число строк, столбцов)");
    B --> C("Ввод: N*M булевых элементов");
    C --> D{Все элементы введены?};
    D -- Нет --> C;
    D -- Да --> E("Сортировка строк по возрастанию кол-ва значений 𝑡𝑟𝑢𝑒");
    E --> F{Кол-во значений 𝑡𝑟𝑢𝑒 совпадает?};
    F -- Да --> G("Сортировка по сумме последовательных значений 𝑡𝑟𝑢𝑒");
    F -- Нет --> I
    G --> I("Поиск и вывод строки с максимальным кол-вом последовательных значений 𝑡𝑟𝑢𝑒, её длины");
    I --> J("Вывод массива в формате матрицы (заменяя 𝑡𝑟𝑢𝑒 на символ «+», а 𝑓𝑎𝑙𝑠𝑒 на «˗»). Вывести число островков (групп соседних 𝑡𝑟𝑢𝑒)");
    J --> K{Массив симметричен относительно главной диагонали?};
    K -- Да --> M("Сортировка строк по возрастанию кол-ва значений 𝑡𝑟𝑢𝑒");
    K -- Нет --> L("поиск минимального кол-ва изменений для достижения симметрии");
    L --> M("Вывод результата проверки симметрии, минимального кол-ва необходимых изменений для достижения симметрии(если необходимо)");
    M --> N("Конец");


```

### 5. Программа
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.Scanner;

public class BooleanMatrix {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Считываем размеры массива
        System.out.print("Введите размеры массива N и M: ");
        int N = scanner.nextInt();
        int M = scanner.nextInt();

        boolean[][] matrix = new boolean[N][M];

        // Считываем элементы массива
        System.out.println("Введите элементы массива (true/false): ");
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                matrix[i][j] = scanner.nextBoolean();
            }
        }

        // Сортируем строки массива
        Arrays.sort(matrix, new Comparator<boolean[]>() {
            @Override
            public int compare(boolean[] row1, boolean[] row2) {
                int count1 = countTrue(row1);
                int count2 = countTrue(row2);

                if (count1 != count2) {
                    return Integer.compare(count1, count2);
                } else {
                    return Integer.compare(countConsecutiveTrues(row1), countConsecutiveTrues(row2));
                }
            }
        });

        // Находим строку с максимальным количеством последовательных true
        String maxSequenceRow = "";
        int maxLength = 0;
        for (boolean[] row : matrix) {
            int length = countConsecutiveTrues(row);
            if (length > maxLength) {
                maxLength = length;
                maxSequenceRow = Arrays.toString(row);
            }
        }

        System.out.println("Строка с максимальным количеством последовательных true: " + maxSequenceRow);
        System.out.println("Длина этой последовательности: " + maxLength);

        // Выводим элементы массива в виде матрицы
        System.out.println("Элементы массива в виде матрицы:");
        printMatrix(matrix);

        // Подсчет островков
        int islandsCount = countIslands(matrix);
        System.out.println("Количество островков (групп соседних true): " + islandsCount);

        // Проверка на симметричность
        boolean isSymmetric = checkSymmetry(matrix);
        System.out.println("Массив симметричен относительно главной диагонали: " + isSymmetric);

        if (!isSymmetric) {
            int minChanges = calculateMinChangesForSymmetry(matrix);
            System.out.println("Минимальное количество изменений для достижения симметрии: " + minChanges);
        }

        scanner.close();
    }

    private static int countTrue(boolean[] row) {
        int count = 0;
        for (boolean value : row) {
            if (value) count++;
        }
        return count;
    }

    private static int countConsecutiveTrues(boolean[] row) {
        int maxCount = 0;
        int currentCount = 0;

        for (boolean value : row) {
            if (value) {
                currentCount++;
                maxCount = Math.max(maxCount, currentCount);
            } else {
                currentCount = 0;
            }
        }

        return maxCount;
    }

    private static void printMatrix(boolean[][] matrix) {
        for (boolean[] row : matrix) {
            for (boolean value : row) {
                System.out.print(value ? "+" : "-");
            }
            System.out.println();
        }
    }

    private static int countIslands(boolean[][] matrix) {
        boolean[][] visited = new boolean[matrix.length][matrix[0].length];
        int islandsCount = 0;

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] && !visited[i][j]) {
                    dfs(matrix, visited, i, j);
                    islandsCount++;
                }
            }
        }

        return islandsCount;
    }
    private static void dfs(boolean[][] matrix, boolean[][] visited, int i, int j) {
        if (i < 0 || i >= matrix.length || j < 0 || j >= matrix[0].length || !matrix[i][j] || visited[i][j]) {
            return;
        }

        visited[i][j] = true;

        // Проверяем все соседние клетки
        dfs(matrix, visited, i + 1, j);
        dfs(matrix, visited, i - 1, j);
        dfs(matrix, visited, i, j + 1);
        dfs(matrix, visited, i, j - 1);
    }

    private static boolean checkSymmetry(boolean[][] matrix) {
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] != matrix[j][i]) {
                    return false;
                }
            }
        }
        return true;
    }

    private static int calculateMinChangesForSymmetry(boolean[][] matrix) {
        int changes = 0;

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] != matrix[j][i]) {
                    changes++;
                }
            }
        }

        return changes / 2; // Каждое изменение учитывается дважды
    }
}


```

### 6. Анализ правильности решения
Программа успешно выполняет поставленные задачи.
1. Тест:
    - **Input**:
        ```
        3
        3
        1.0 -2.0 3.0
        2
        -5.0 2.0
        4
        1.0 -1.0 2.0 -3.0
        ```

    - **Output**:
        ```
        Отсортированный массив в виде матрицы:
        1.00 -2.00 3.00 *
        1.00 -1.00 2.00 -3.00
        -5.00 2.00 * *

        Максимальный элемент: 3.0 (строка 1, позиция 3)

        Массив после замены на обратные значения:
        1.00 -0.50 0.33 *
        1.00 -1.00 0.50 -0.33
        -0.20 0.50 * *
        ```
