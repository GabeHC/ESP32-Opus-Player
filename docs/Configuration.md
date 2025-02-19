# ESP32 Opus Player Configuration Guide

## Current Working Configuration

### Platform Settings (platformio.ini)
\\\ini
[env:waveshare_esp32_one]
platform = espressif32
board = waveshare_esp32_one
framework = arduino
upload_speed = 921600
monitor_speed = 115200

build_flags = 
    -DCORE_DEBUG_LEVEL=3
    -DCONFIG_FREERTOS_HZ=1000
    -DCONFIG_I2S_ISR_IRAM_SAFE=1
    -DAUDIO_BUFFER_SIZE=8192    ; Critical for smooth playback
    -DI2S_BUFFER_COUNT=8        ; Prevents buffer underruns
    -DCONFIG_FREERTOS_OPTIMIZATION_LEVEL=3
    -DCONFIG_ESP_SYSTEM_EVENT_TASK_STACK_SIZE=8192
    -DCONFIG_FREERTOS_UNICORE=n
    -DCONFIG_ESP_INT_WDT=n      ; Disable interrupt watchdog
    -DCONFIG_ESP_TASK_WDT=n     ; Disable task watchdog

lib_deps = 
    sparkfun/SparkFun WM8960 Arduino Library @ ^1.0.3
\\\

## Quick Troubleshooting Guide

✅ **Working Audio Checklist**
- [ ] AUDIO_BUFFER_SIZE = 8192
- [ ] I2S_BUFFER_COUNT = 8
- [ ] Watchdog timers disabled
- [ ] Task stack size ≥ 8192
- [ ] FreeRTOS optimization level = 3

🔄 **Recovery Steps**
1. Reset to these settings
2. \pio run -t clean\
3. \pio run -t upload\
4. \pio device monitor\

⚠️ **Common Issues**
- Audio stuttering  Check buffer sizes
- System crashes  Verify watchdog settings
- Stack overflow  Increase task stack size
