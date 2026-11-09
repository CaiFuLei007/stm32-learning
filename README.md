# stm32-learning

STM32F103ZE（野火 F103 系列）HAL 库学习工程集，每个目录是一个独立的 STM32CubeMX + Keil MDK-ARM 工程，可直接用 Keil 打开各自 `MDK-ARM/*.uvprojx` 编译下载。

| 工程 | 说明 |
| --- | --- |
| `led_on/` | 点亮 LED：PF8 输出低电平（灌电流点亮），静态常亮 |
| `led-blink/` | LED 闪烁：PF8 每 500 ms 翻转一次电平 |
| `running-light/` | 跑马灯：PF8~PF11 四灯依次点亮再熄灭，每步 1 s |
| `key-toggle-led/` | 按键控制 LED：PG6/PG7/PG8/PG10 四键按下翻转对应 PF8~PF11 四灯，含 30 ms 软件消抖 |

## 硬件与外设

- MCU：STM32F103ZE，HSE 8 MHz 外部晶振
- LED：PF8、PF9、PF10、PF11，开漏输出（`GPIO_MODE_OUTPUT_OD`），低电平点亮
- 按键：PG6、PG7、PG8、PG10，上拉输入，低电平有效
- 调试：SWD（PA13/PA14）

## 目录约定

每个工程由 STM32CubeMX 生成，结构一致：

```
<project>/
├── <project>.ioc              CubeMX 工程配置
├── Core/Inc, Core/Src         main.c / 中断 / MSP 等用户代码
├── Drivers/                   HAL 库与 CMSIS（部分工程含完整的 CMSIS DSP/Lib，未参与链接）
└── MDK-ARM/                   Keil 工程文件与编译输出
```

编译产物（`*.o` `*.d` `*.axf` `*.hex` `*.map` 等）与 Keil 界面状态文件已通过 `.gitignore` 排除。
