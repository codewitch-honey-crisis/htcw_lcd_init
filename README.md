# LCD Init

This is a header to drive many kinds of display using an ESP32

It can drive RGB displays, I2C, SPI, I8080, and well, anything the ESP LCD Panel API can drive.

It has the necessary magic to make RGB work, some of which I ripped from LovyanGFX.

```cpp
// declare in exactly one source file
#define LCD_IMPLEMENTATION
#include "lcd_init.h"
// only needed if DMA enabled
static bool lcd_flush_ready(esp_lcd_panel_io_handle_t panel_io, 
                            esp_lcd_panel_io_event_data_t* edata, 
                            void* user_ctx) {
    // TODO: notify flush complete
    return true;
}
// initializes the driver
lcd_panel_init(); // no DMA
// or 
lcd_panel_init(lcd_buffer_size,lcd_flush_ready); // DMA w/ callback
// draws a bitmap to the display
lcd_panel_draw_bitmap(x1,y1,x2,y2,(void*)bmp);
```
There are configurations for many different devices in lcd_config.h
Note that some require an external driver.
