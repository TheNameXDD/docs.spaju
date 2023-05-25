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

