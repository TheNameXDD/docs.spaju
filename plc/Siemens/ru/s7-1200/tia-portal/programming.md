# Программирование

## Принцип программирования контроллеров S7-1200

#### Языки программирования <a href="#about-plc-programming" id="about-plc-programming"></a>

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

<figure><img src="../../../../../.gitbook/assets/TIA_CEM.png" alt=""><figcaption></figcaption></figure>
