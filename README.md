testing main page

## Документация

*   [Страница 1](page1.md)
*   [Страница 2](page2.md)


В частности, в рассмотренных трёх задачах компоненты выглядят
таким образом:


```text
компонент   TwoSum                   дубликаты                    ищем цикл
тип         навстречу                разделение                   быстрый/медленный
указатели   left=0, right=n-1        k=1, i=1                     slow=head, fast=head
условие     sum < target ->left++    nums[i] != nums[k-1] ->k++   slow = slow.next
            sum > target ->right--   i++ всегда                   fast = fast.next.next
остановка   left <= right            i < nums.length              fast == null / next == null

```
Связь паттерна с реальным кодом задач (разметка в коде компонентов)
---
так как компонентов слишком мало и они слишком очевидны, показать их в коде
не составит для нас труда, однако на другом типе задач этот паттерн к сожалению
воспроизвести не выйдет, но в целом он вот такой:

```java
public int[] findPair(int[] prices, int target) {

    // <- указатели
    int left = 0;
    int right = prices.length - 1;

    // <- цикл перемещения + критерий установки
    while (left < right) {
        int currentSum = prices[left] + prices[right];

        // <- условие перемещения
        if (currentSum == target)       return new int[]{prices[left], prices[right]};
        else if (currentSum < target)   left++;
        else                            right--;
    }

    // <- ничего не нашли
    return null;
}
```
Всё понятно, но стоит добавить, что часто путают: вместо (left++) делают (right--)
в этой ветке - и наоборот. Поэтому прежде чем кодировать, лучше накидать небольшую
схемку - как я показывал в начале главы
