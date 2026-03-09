# STM32 OLED Slot Machine Game
![9a4cd127-2477-48c9-98c3-4055eaafb4df](https://github.com/user-attachments/assets/70d989a6-1912-4047-ad9a-f63e8a98ac63)
![b00a06ec-31ae-4fe5-b830-9cc9737a85c8](https://github.com/user-attachments/assets/9381269c-8e82-420e-a8ce-b1b6ae968bca)

A miniature slot machine game implemented on the **STM32L476RG** microcontroller using an OLED display. This project perfectly demonstrates the use of external interrupts (EXTI), hardware timers, and a state machine to control game logic.

## 🎮 How it works
1. A welcome screen greets the player.
2. Pressing the button (Blue push-button on the Nucleo board) starts the draw.
3. The screen displays spinning "question marks".
4. Three randomly drawn symbols are sequentially revealed: 💀 Skull, 🔫 Pistol, or 🗡️ Sword.
5. After all symbols are revealed, the system waits for another button press to play again.

## 🛠️ Features and Technical Details
* **State Machine:** Game logic is based on clear, defined states (`oczekiwanie`, `krecenie`, `odkrycie1`, `odkrycie2`, `odkrycie3`, `wynik`).
* **Hardware RNG Seed:** Uses a free-running hardware timer (`TIM3`) to seed the `srand()` function, ensuring unpredictable symbol generation.
* **Timer Interrupts (TIM2):** Animation state changes (revealing successive symbols) are controlled by timer interrupts at specific intervals, avoiding blocking `HAL_Delay()` functions.
* **External Interrupts (EXTI):** The button press reaction is handled instantly via a hardware interrupt.
* **Custom Graphics:** Uses custom icons as byte arrays (bitmaps) displayed on the OLED screen via the I2C bus.

## 📌 Hardware Setup (Pinout)

| Component | STM32 Pin | Function | Notes |
| :--- | :--- | :--- | :--- |
| **OLED Display** | **PB6** | I2C1 SCL | I2C Bus Clock |
| | **PB7** | I2C1 SDA | I2C Bus Data |
| **User Button**| **PC13** | EXTI13 | Built-in blue button (Nucleo) |
| **User LED** | **PA5** | GPIO Output | Built-in green LED (LD2) |

## 📚 Credits
This project uses an excellent open-source library for the OLED screen. Full credit goes to the original author:
* **SSD1306 OLED library for STM32:** [https://github.com/afiskon/stm32-ssd1306]
