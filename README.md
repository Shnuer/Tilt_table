# Tilt_table

Проект шарика на плоскости. Стенд реализован как в реальной среде, так и в симуляторе.

# Содержание

- `Hardware` - прошивка контроллера для варианта "Стол-Компьютер-МК". В этом варианте компьютер считывает положение шарика на столе с помощью USB преобразователя, формирует управление и передает на МК через UART
- `Software` - программы на Desktop для варианта "Стол-Компьютер-МК". Основная программа (на С++) реализует считывание данных с сенсорного стола, формирует управляющее воздействие и передает данные на МК для отработки
- `Simulation` - вариант симулятора с некоторыми скриптами для исследования работы нейроэволюционных алгоритмов для реализации СУ. Симуляция разработана на основе фреймворка `pybullet`. Основной скрипт, содержащий поведение объекта расположен в `objects.py`
- `plane_control_2019b.slx` - матлаб схема, в которой реализована вся схема управления столом
- `servo_test_2019b.slx` - часть схемы управления столом для теста работы сервоприводов
- `table_test_2019b.slx` - часть схемы управления столов для тестирования установки конкретного угла стола

# Физический стенд

Реализован стенд на основе микроконтроллера STM32F767ZI, а также двух сервоприводов ???. Сервоприводы разобраны и ДПТ внутри подключен отдельно к драйверам ???, а потенциометры считываются напрямую микроконтроллером. Таким образом система управления столом представлена в виде следующих уровней:
- СУ по положению сервопривода;
- СУ по положению угла наклона стола;
- СУ по положению шарика на столе.

Система протестирована как в варианте "Стол-Компьютер-МК", так и при прошивке МК через MALTAB с дальнейшей автономной работой.

# Проблемы
Наблюдались следующие проблемы:
- Стол имеет что-то похожее на дрифт, при котором напряжение, выдаваемое сенсором, нелинейно менялось. Вероятнее всего, дело в принципе считывания, но может дело и в самом сенсоре. Симптом - в одном и том же месте со временем меняется выдаваемый аналоговый сигнал, шарик не стоит на месте.
- MATLAB часто сбоил в плане соединения, что раздражало и в некоторых случаях не давало держать постоянное соединение с контроллером для наблюдения.
