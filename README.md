# UniRTOS LVGL

UniRTOS external-library package for LVGL v8.3.11.

The library vendors the upstream LVGL source and the EG800Z RGB565 static-memory
profile in `include/lv_conf.h`. It contains no LCD controller, GPIO, LSPI, demo,
or application code.

Applications consume it through `env_config.json`:

```json
"libraries": {
  "list": [
    { "name": "unirtos-lvgl", "version": "8.3.11" }
  ]
}
```

Run `unirtos-cli env-setup` before `unirtos-cli build`. The SDK compiles this
library and links it only into applications that declare the dependency.

