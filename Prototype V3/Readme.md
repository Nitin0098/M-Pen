
Firmware (STM32) changes

1. Initial firmware written — 20-bit MMC5603, polling mode, 100 Hz, USB CDC format S1:x,y,z;S2:x,y,z
2. Fixed Error_Handler conflict with CubeMX weak stub
3. Fixed RCC_PERIPHCLK_CLK48 undefined — removed (F401 doesn't need it)
4. Fixed SystemClock_Config it shouldnot be static.
5. Fixed SystemCoreClock multiply defined — removed duplicate function
6. Fixed SystemInit undefined — kept one copy of system_stm32f4xx.c
7. Complete rewrite to 16-bit mode, DMA, 500 Hz — new main.c, mmc5603.h/c
8. Added MX_DMA_Init() before I2C init (required ordering)
9. Fixed AUTO_SR comment — it sends data every measurement(relative to magnetometer), not every 100
10. Removed AUTO_SR from trigger entirely, replaced with periodic manual SET/RESET cycle every 10 s
11. Bug fix: MMC5603_LSB_PER_UT was 102.4 (10× wrong) → corrected to 10.24 (Typo error)
12. Bug fix: Timing >= 2u → >= 3u to compensate for 1 ms HAL tick resolution (critical — was reading sensor before conversion complete)
13. Bug fix: cdc_send() was blocking up to 50 ms with retries → changed to single non-blocking call
14. Bug fix: MMC5603_Trigger() (blocking I2C) was called inside TIM2 ISR → moved to main loop, ISR now only sets do_trigger flag.

M-Pen algorithm evolution (25+ iterations)

1. V1: scipy.optimize L-BFGS-B dipole fit + cross-product rolling direction + LineCollection blit rendering
2. Fixed flicker — replaced blit/restore_region with PIL pixel buffer + imshow.set_data(), no blank intermediate frame.
3. Fixed over-filtering — EMA_ALPHA 0.25→0.55, POS_SMOOTH 0.55→0.92, NOISE_FLOOR_DEG 0.8→0.35
4. Fixed ink style — removed variable-width pooling effects, plain 3px dark blue line (simple virtual ink traces)
5. Fixed virtual paper size, changed to A4 dimensions — was 30×21 cm, corrected to 29.7×21 cm landscape.
6. Removed all filters — pure m_prev × m_curr cross product, no EMA, no dead-zone
7. Diagnosed zigzag root cause — cross products of nearly-parallel vectors are dominated by noise; also blind axis when both sensors on X axis
8. Added Option A (analytical φ direction from atan2(dm_y, dm_x)) + Option D (quaternion SLERP smoothing) combined
9. Hardware fix (Option B) — moved Sensor 2 from (4cm, 0, 0) to (0, 2cm, 0) — eliminated blind axis entirely. POS_S1=[0.02,0,0], POS_S2=[0,0.02,0]
10. Removed A+D pipeline — replaced with clean dm_xy direction mapping, no cross products, no SLERP
11. Removed scipy.optimize entirely — replaced with analytical dipole extraction:
   mx = B1x/2 - B2x
   my = B2y/2 - B1y
   mz = -(B1z+B2z)/2
   This was the real root cause of random motion — optimizer finding different local minima each frame.

13. witched to KDTree lookup (Approach 1) — pre-computed physics grid at 0.5° resolution, ~130k entries, ~0.1ms query
14. Added EMA smoothing on (θ, φ) outputs — circular EMA for φ via (sin φ, cos φ) to handle 0°/360° wrap
Added displacement accumulation gate — only draw stroke when accumulated displacement exceeds MIN_DRAW_MM = 0.15
Fixed COUNTS_PER_UT in Python — was 163.84 (20-bit), corrected to 10.24 (16-bit).

problems
1. Current algorithm still cannot predict and track dipole orientation accurately, Reason: I placed two magnetometers in opposite sides of a cube, which created a blind axis(Z axis) , rotation of magnetic sphere along Z axis was not tracked due to symmetry of magnetic field and current placement of magnetometers.

Solution:
1. place magnetometers in planes perpendicular to each other so solve the blind axis problem.
2. improve the dipole orientation tracking algorithm and x and y plot algorithm

