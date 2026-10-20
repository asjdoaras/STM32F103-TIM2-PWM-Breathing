# STM32F103 TIM2 定时器中断闪烁 + CH1 PWM 呼吸灯

基于 STM32F103C8T6 / HAL 库 / CubeMX / Keil MDK，CMSIS-DAP(SWD) 下载。

## 任务一：定时器更新中断 2s 亮灭
- TIM2 Internal Clock，PSC=7199，ARR=19999，72MHz → 2s 进一次更新中断
- 回调中 HAL_GPIO_TogglePin(PA0)，亮2s/灭2s

## 任务二：TIM2_CH1 PWM 呼吸灯（约2s）
- PSC=71，ARR=999 → 计数1MHz，PWM 1kHz，更新中断1ms
- 回调内比较值 duty 0→999→0 往返，渐亮1s、渐灭1s，全周期2s
- PA0 = TIM2_CH1 复用推挽，PWM1，高电平有效

## 接线
PA0 → 1kΩ → LED阳极，LED阴极 → GND；SWDIO=PA13，SWCLK=PA14，共地，3V3供电。

## 构建
Keil 打开 MDK-ARM/TIM2_Blink.uvprojx，编译 0 Error 0 Warning，CMSIS-DAP 下载 Verify OK。