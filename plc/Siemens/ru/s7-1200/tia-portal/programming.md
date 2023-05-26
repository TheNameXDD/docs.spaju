# Программирование

## Принцип программирования контроллеров S7-1200

### Языки программирования <a href="#about-plc-programming" id="about-plc-programming"></a>

На момент 17 версии TIA portal поддерживает следующие языки программирования для контроллеров S7-1200:

**LAD** (Ladder diagram):

<figure><img src="../../../../../.gitbook/assets/TIA_LAD.png" alt=""><figcaption></figcaption></figure>

**FBD** (Functional block diagram):

<figure><img src="../../../../../.gitbook/assets/TIA_FBD.png" alt=""><figcaption></figcaption></figure>

**SCL** (Structured control language):IF "Button1" AND "Button2" THEN

```cpp
IF "Button1" AND "Button2" THEN
    "LED" := 1;
ELSE
    "LED" := 0;
END_IF;
```

**CEM** (Cause Effect Matrix)

<figure><img src="../../../../../.gitbook/assets/TIA_CEM.png" alt="" width="240"><figcaption></figcaption></figure>

### Логические операции

#### Логическая операция И

| ВХОД 1 | ВХОД 2 | РЕЗУЛЬТАТ |
| ------ | ------ | --------- |
| **1**  | **1**  | **1**     |
| 0      | 1      | 0         |
| 1      | 0      | 0         |
| 0      | 0      | 0         |

Реализация на языке LAD:

<figure><img src="../../../../../.gitbook/assets/TIA_AND.png" alt=""><figcaption></figcaption></figure>

Реализация на языке SCL:

```cpp
IF "Button1" AND "Button2" THEN 
    "LED" := 1; 
ELSE 
    "LED" := 0; 
END_IF;

//Второй способ
"LED" := "Button1" AND "Button2"
```

#### Логическая операция ИЛИ

| ВХОД 1 | ВХОД 2 | РЕЗУЛЬТАТ |
| ------ | ------ | --------- |
| 1      | 1      | 1         |
| 0      | 1      | 1         |
| 1      | 0      | 1         |
| 0      | 0      | 0         |

Реализация на языке LAD:

<figure><img src="../../../../../.gitbook/assets/TIA_OR.png" alt=""><figcaption></figcaption></figure>

Реализация на языке SCL

```cpp
IF "Button1" OR "Button2" THEN
    "LED" := 1;
ELSE
    "LED" := 0;
END_IF;

//Второй способ
"LED" := "Button1" OR "Button2"
```

#### **Логическая операция "Исключающее ИЛИ"**

| ВХОД 1 | ВХОД 2 | РЕЗУЛЬТАТ |
| ------ | ------ | --------- |
| 1      | 1      | 0         |
| 1      | 0      | 1         |
| 0      | 1      | 1         |
| 0      | 0      | 0         |

Реализация на языке LAD

<figure><img src="../../../../../.gitbook/assets/TIA_NOT-OR.png" alt=""><figcaption></figcaption></figure>

Реализация на языке SCL

```cpp
IF ("Button1" AND NOT "Button2") OR (NOT "Button1" AND "Button2") THEN
    "LED" := 1;
ELSE
    "LED" := 0;
END_IF;

//Второй способ
"LED" := ("Button1" AND NOT "Button2") OR (NOT "Button1" AND "Button2");
```

#### Инвертирование сигнала



<figure><img src="../../../../../.gitbook/assets/TIA_NOT.png" alt=""><figcaption></figcaption></figure>

```cpp
"LED" := NOT "Button1";
```

### Работа с памятью контроллера

У контроллера S7-1200 имеются различные виды памяти:&#x20;

M% / Q% - бит (0 или 1)

MB% - 8 бит

MW% - 16 бит

MD% - 32 бита

**Логика работы и обращение к памяти по адресу**

Битовая память (**M - memory**) имеет адрес M0.0, где первая цифра - это номер **байта**, а вторая - это номер **бита в байте**.&#x20;

> Обращаю внимание, что в ИТ счёт начинается с 0 (то есть 0 это для нас 1)

{% hint style="info" %}
Возьмем для примера 2 битовой памяти с адресами: M0.2 и M3.1

**M0.2** - это 3 бит памяти в 1 байте

**M3.1** - это 2 бит памяти в 4 байте
{% endhint %}



Следующий тип памяти - это байтовая память (**MB - memory byte**), которая вмещает в себя 8 бит (M). После байтовой памяти идет память слово (**MW - memory word**), которая вмещает в себя 16 бит (M) или просто 2 байта (MB). Последним типом памяти является память двойного слова (**MD - memory double**), которая вмещает в себя 32 бита (M), или 4 байте (MB), или 2 памяти слова (MW)

<figure><img src="../../../../../.gitbook/assets/TIA_memory" alt=""><figcaption></figcaption></figure>

