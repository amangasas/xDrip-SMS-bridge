# xDrip SMS Bridge

A small Android app that reads the current glucose value from **xDrip+'s local HTTP API** and sends it to another phone via SMS.

Designed for situations where the receiving phone is too old to comfortably run xDrip+, WhatsApp, Messenger, etc.

![xDrip SMS Bridge](images/1.png)

## Example SMS

The bridge sends a deliberately simple SMS format so it remains readable on older phones and does not depend on emoji support.

### Flat

```text
142 mg/dL
- (?1.2)
```

### Rising

```text
156 mg/dL
^ (?2.4)
```

### Falling

```text
128 mg/dL
V (?−3.1)
```

The format is:

```text
<glucose> mg/dL
<direction> (?<delta>)
```

Direction symbols:

| Symbol | Meaning |
| ------ | ------- |
| `^`    | Rising  |
| `-`    | Flat    |
| `V`    | Falling |

The glucose value is taken directly from xDrip+'s `sgv` value. **No mmol/L conversion is performed.**


## How it works

```text
Libre sensor
     ↓
  Juggluco
     ↓
   xDrip+
     ↓
127.0.0.1:17580/sgv.json
     ↓
xDrip SMS Bridge
     ↓
   SMS
     ↓
Receiving phone
```
