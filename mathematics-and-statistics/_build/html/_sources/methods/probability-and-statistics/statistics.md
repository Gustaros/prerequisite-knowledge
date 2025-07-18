# Математическая статистика

Если теория вероятностей — это игра по известным правилам, то статистика — это попытка понять правила игры, наблюдая за ее ходом. У нас есть данные, и мы хотим использовать их, чтобы узнать что-то о мире.

## Случайная выборка из генеральной совокупности

*   **Генеральная совокупность (Population):** Это *все* объекты, которые нас интересуют. Например, *все* жители города, *все* произведенные на заводе детали. Изучить генеральную совокупность целиком почти всегда невозможно — это слишком дорого или долго.

*   **Выборка (Sample):** Это небольшая, случайно отобранная часть генеральной совокупности, которую мы непосредственно изучаем.

**Главная задача статистики** — по характеристикам выборки сделать обоснованные выводы о характеристиках всей генеральной совокупности. Чтобы эти выводы были верными, выборка должна быть **репрезентативной**, то есть хорошо отражать структуру всей совокупности. Лучший способ этого добиться — случайный отбор.

## Описательные статистики

Это первый шаг в любом анализе данных. Мы считаем простые показатели, которые описывают нашу **выборку**.

*   **Меры центральной тенденции (где "центр" данных?):**
    *   **Среднее (Mean):** Сумма всех значений, деленная на их количество. Очень чувствительно к выбросам.
    *   **Медиана (Median):** Значение, которое находится ровно посередине отсортированного набора данных. 50% данных меньше медианы, 50% — больше. Не чувствительна к выбросам.
    *   **Мода (Mode):** Самое часто встречающееся значение в наборе данных.

*   **Меры изменчивости (насколько данные "разбросаны"?):**
    *   **Дисперсия (Variance, $\sigma^2$):** Средний квадрат отклонений значений от их среднего. Показывает, насколько данные в среднем "далеки" от центра.
    *   **Стандартное отклонение (Standard Deviation, $\sigma$):** Корень из дисперсии. Удобнее, так как измеряется в тех же единицах, что и сами данные.

*   **Меры формы распределения:**
    *   **Асимметрия (Skewness):** Показывает, "скошен" ли график распределения данных в одну из сторон.
    - **Эксцесс (Kurtosis):** Показывает, насколько "остроконечным" или "плоским" является пик распределения по сравнению с нормальным.

## Математическое ожидание и моменты

Эти понятия тесно связаны с описательными статистиками, но относятся к теоретическим **случайным величинам** и их распределениям, а не к конкретным выборкам.

*   **Математическое ожидание (Expectation, $E[X]$):** Это теоретический аналог среднего значения. Это среднее значение, которое мы *ожидаем* получить, если будем проводить наш случайный эксперимент бесконечное число раз. Для дискретной величины это сумма произведений каждого значения на его вероятность.

*   **Моменты:** Это обобщенное понятие.
    *   **Первый начальный момент** — это и есть математическое ожидание.
    *   **Второй центральный момент** (момент относительно среднего) — это и есть дисперсия.
    *   Третий и четвертый моменты связаны с асимметрией и эксцессом.

## Выборочное распределение и Центральная предельная теорема

Это одна из самых волшебных и фундаментальных идей в статистике.

Представьте, что мы берем из генеральной совокупности много-много выборок одинакового размера (например, 1000 выборок по 30 человек в каждой). Для каждой выборки мы считаем ее среднее значение. В итоге мы получим 1000 выборочных средних.

**Центральная предельная теорема (ЦПТ) утверждает:**

> Распределение этих выборочных средних будет стремиться к **нормальному распределению**, независимо от того, какое распределение было у исходной генеральной совокупности.

И еще два бонуса:
1.  Среднее этого распределения выборочных средних будет равно среднему самой генеральной совокупности.
2.  Стандартное отклонение этого распределения (называемое **стандартной ошибкой среднего**) будет меньше, чем у исходной совокупности, и равно $\frac{\sigma}{\sqrt{n}}$, где $n$ — размер выборки.

**Почему это так важно?** ЦПТ позволяет нам использовать свойства нормального распределения для того, чтобы делать выводы о среднем генеральной совокупности, даже если мы ничего не знаем о ее форме!

## Построение доверительных интервалов

Так как мы работаем с выборкой, мы никогда не можем узнать *точное* значение параметра генеральной совокупности (например, точное среднее). Но мы можем построить **доверительный интервал**.

**Доверительный интервал** — это диапазон значений, который с высокой вероятностью (например, 95%) содержит истинное значение параметра генеральной совокупности.

**Как это работает (упрощенно):**
1.  Берем нашу выборку и считаем выборочное среднее.
2.  Используя ЦПТ и стандартную ошибку, мы строим "сеть" вокруг нашего выборочного среднего.
3.  Ширина этой "сети" зависит от двух вещей:
    *   Размера выборки $n$ (чем больше выборка, тем уже интервал).
    *   Выбранного уровня доверия (для 99% интервал будет шире, чем для 95%).

**Интерпретация:** Если мы построим 100 таких 95% доверительных интервалов по 100 разным выборкам, то примерно 95 из них "поймают" истинное среднее генеральной совокупности.

## Проверка гипотез и ошибки I и II рода

Это формальная процедура для принятия решений на основе данных.

**Процесс:**
1.  **Формулируем нулевую гипотезу ($H_0$):** Это утверждение "по умолчанию", статус-кво. Например, "новое лекарство не эффективнее плацебо" или "средний рост мужчин в двух городах одинаков".
2.  **Формулируем альтернативную гипотезу ($H_1$):** Это то, что мы хотим доказать. Например, "новое лекарство эффективнее плацебо".
3.  **Собираем данные** и считаем тестовую статистику.
4.  **Вычисляем p-value.**

**P-value** — это вероятность получить такие же (или еще более экстремальные) данные, которые мы получили, *при условии, что нулевая гипотеза верна*.

*   **Если p-value очень маленькое** (обычно < 0.05), это означает, что наши данные очень маловероятны при условии $H_0$. У нас есть веские основания **отвергнуть нулевую гипотезу** в пользу альтернативной.
*   **Если p-value большое**, у нас нет оснований отвергать $H_0$. Мы говорим, что "не смогли отвергнуть нулевую гипотезу" (но это не значит, что мы ее доказали!).

**Ошибки при принятии решения:**
*   **Ошибка I рода (False Positive):** Мы отвергаем верную нулевую гипотезу. (Например, объявляем лекарство эффективным, хотя это не так). Вероятность этой ошибки — это наш уровень значимости $\alpha$ (обычно 0.05).
*   **Ошибка II рода (False Negative):** Мы не отвергаем неверную нулевую гипотезу. (Например, объявляем лекарство неэффективным, хотя на самом деле оно работает).