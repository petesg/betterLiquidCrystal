# betterLiquidCrystal
non-blocking adaptation of Arduino LiquidCrystal library

This is adapted from the Arduino LiquidCrystal library, changes made to free up time when writing to display.  Warning, this means timing issues need to be avoided manually (maybe?)

This now works such that `print()` (which calls `send()`), now just queues up packets of 4 bits to be sent.  `upkeep()` must then be called at convenience in order to write packets to the display.  The buffer is 32 packets long, if there are issues in using this library the first thing to try should be to increase `BUFFER_SIZE`.

`print()` now takes ~80us to call (on a SAMD51, theoritically just scales with processor speed now), down from 2-3ms (hard coded delay) before.

Only 4-bit mode has been optimized as of now, 8-bit mode shouldn't be hard to fix but I don't use it (had other issues with it in the past) so didn't bother to change it.

Running most commands (other than `setCursor()`) still blocks, could try making them use `betterCommand()` instead of `command()` if needed.  Some of them had issues with that though (idk which ones).
