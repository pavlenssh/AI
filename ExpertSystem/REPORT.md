# Отчет по лабораторной работе
## по курсу "Искусственный интеллект"

### Студенты: 

| ФИО       | Роль в проекте                     | Оценка       |
|-----------|------------------------------------|--------------|
| Жуков М.А. | Реализовал оболочку ЭС на Прологе, заполнил базу данных |          |
| Шорников П.С. | Тестирование, написал отчет и проделал всю остальную работу | |

## Результат проверки

| Преподаватель     | Дата         |  Оценка       |
|-------------------|--------------|---------------|
| Сошников Д.В. |              |               |

> *Комментарии проверяющих (обратите внимание, что более подробные комментарии возможны непосредственно в репозитории по тексту программы)*

## Тема работы

В качестве темы было решено  выбрать подбор автомобилей. Сегодня молодые водители, которые только хотят приобрести себе автомобиль, не могут определиться с выбором и в итоге выбирают не то, что хотели бы на самом деле. Некоторые обращаются к авто экспертам, которые пользуясь смоим опытом и знаниями проделывают всю работу за них. Данная экспертная система нацелена именно на это. Водитель отвечает на  вопросы , и в результате, экспертная система рекомендует пользователю автомобиль.

## Концептуализация предметной области

Результаты концептуализации предметной области:
 - выделенные понятия (тип, бюджет, страна, тип топлива, КПП)
 - тип получившейся онтологии - иерархия 
 - статические - тип, бюджет, страна, тип топлива, КПП
 - всей базой знания занимался один человек, но основе своих личных знаний


## Принцип реализации системы

Для решения поставленной задачи используется система программирования SWI Prolog. У нас есть небольшая база данных салатов. Пользователю рекомендуется автомобиль исходя из его предпочтений, которые мы узнаём путем ответа пользователя на некоторые вопросы. Например, какой тип автомобиля хочет выбрать пользователь (Седан, хетчбэк, универсал, минивен или кроссовер), какой бюджет у пользователя, из какой страны должен быть автомобиль, тип потребляемого топлива, и на какой КПП. Ответы обрабатываются, и в результате отсекаются некоторые ветки решения.

## Механизм вывода

Механизм вывода вопросов:
```
answers([], _).
answers([First|Rest], Index):-
    write(Index), write(' '), answer(First), nl,
    NextIndex is Index + 1,
    answers(Rest, NextIndex).
```
Механизм запоминания ответа пользователя:
```
ask(Question, Answer, Choices) :-
    question(Question),
    answers(Choices, 0),
    read(Index),
    parse(Index, Choices, Response),
    asserta(progress(Question, Response)),
    Response = Answer.а}
```

Пользователю задаются вопросы, в базу знаний с помощью предиката asserta подгружаются новые ответы, когда какое-либо решение было найдено система отвечает на вопрос.

## Извлечение знаний и база знаний

В коде за извлечение знаний отвечает данный фрагмент:
```
parse(0, [First|_], First).
parse(Index, [First|Rest], Response) :-
    Index > 0,
    NextIndex is Index - 1,
    parse(NextIndex, Rest, Response).
```
## Протокол работы системы
```
?- main.
Какой тип автомобиля вы ищете?
0 Седан
1 Универсал
2 Хэтчбэк
3 Минивен
4 Кроссовер
|: 0
|: .
В каком бюджете?
0 От трехсот  до шестисот тысяч
1 От шестясот тысяч до миллиона рублей
2 От миллиона до полутра миллиона рублей
3 От полутра миллиона до двух c половиной миллиона рублей
4 От двух c половиной миллиона до четырех миллионов рублей
|: 2.
Какая страна-производитель?
0 Германия
1 Россия
2 Америка
3 Китай
4 Корея
5 Япония
|: 2.
Дизель или бензин?
0 Бензин
1 Дизель
|: 0.
Автомат или механика?
0 Механика
1 Автомат
|: 1.
Вам подойдет Форд Фокус.
```
## Выводы

Экспертная система - это компьютерная программа, которая в некоторой области проявляет степень познаний равнозначную степени познания человека-эксперта (что очень удобно, ведь всем нам не нравится разговаривать с консультантами). Данная лабораторная работа помогла освежить знания курса Логическое программирование. К сожалению, мне не удалось  состоять в команде при написании лабораторной, так как данная работа была выполнена слишком поздно. С другой стороны, мне легче улавливать концепцию темы одному, в этом случае информация выстраивается в голове по полочкам. 