# gherkin
Gherkin keyboard keymap

https://www.40percent.club/2016/11/gherkin.html

 - Added KC_DOT, KC_SLSH, and KC_ENT to layer 1
 - Added KC_ENT to layer 2


In QMK MSYS:
```
$ qmk setup
y

$ qmk new-keymap
Keyboard Name: 40percentclub/gherkin
Keymap Name: feralpacket
```
After editing the keymap.c file:
```
make 40percentclub/gherkin:feralpacket
```
The first time the controller is flashed, the pins GND and RST need to be shorted on the controller.  QMK Toolbox will not even see the keyboard until it has been reset.  The keyboard can then be flashed.

```
*** Caterina device connected (usbser): Microsoft USB Serial Device (COM4) (2341:0036:0001) [COM4]
*** Attempting to flash, please don't remove device
>>> avrdude.exe -p atmega32u4 -c avr109 -U flash:w:"C:\Users\feralpacket\qmk_firmware\40percentclub_gherkin_feralpacket.hex":i -P COM4

    Connecting to programmer: .
    Found programmer: Id = "CATERIN"; type = S
        Software Version = 1.0; No Hardware Version given.
    Programmer supports auto addr increment.
    Programmer supports buffered memory access with buffersize=128 bytes.
    
    Programmer supports the following devices:
        Device code: 0x44
    
    avrdude.exe: AVR device initialized and ready to accept instructions
    
    Reading | ################################################## | 100% 0.00s
    
    avrdude.exe: Device signature = 0x1e9587 (probably m32u4)
    avrdude.exe: NOTE: "flash" memory has been specified, an erase cycle will be performed
                 To disable this feature, specify the -D option.
    avrdude.exe: erasing chip
    avrdude.exe: reading input file "C:\Users\feralpacket\qmk_firmware\40percentclub_gherkin_feralpacket.hex"
    avrdude.exe: writing flash (18020 bytes):
    
    Writing | ################################################## | 100% 1.38s
    
    avrdude.exe: 18020 bytes of flash written
    avrdude.exe: verifying flash memory against C:\Users\feralpacket\qmk_firmware\40percentclub_gherkin_feralpacket.hex:
    avrdude.exe: load data flash data from input file C:\Users\feralpacket\qmk_firmware\40percentclub_gherkin_feralpacket.hex:
    avrdude.exe: input file C:\Users\feralpacket\qmk_firmware\40percentclub_gherkin_feralpacket.hex contains 18020 bytes
    avrdude.exe: reading on-chip flash data:
    
    Reading | ################################################## | 100% 0.15s
    
    avrdude.exe: verifying ...
    avrdude.exe: 18020 bytes of flash verified
    
    avrdude.exe done.  Thank you.
    
*** Caterina device disconnected (usbser): Microsoft USB Serial Device (COM4) (2341:0036:0001)
```
To reset the keyboard after the controller has the firmware installed, hold the LT(5) key and hit the key configured for RESET.

The keymap:
```
#define FN1_SPC     LT(1, KC_SPC)
#define FN2_BSPC    LT(2, KC_BSPC)
#define FN3_C       LT(3, KC_C)
#define FN4_V       LT(4, KC_V)
#define FN5_B       LT(5, KC_B)
#define CTL_Z       CTL_T(KC_Z)
#define ALT_X       ALT_T(KC_X)
#define ALT_N       ALGR_T(KC_N)
#define CTL_M       RCTL_T(KC_M)
#define SFT_ENT     RSFT_T(KC_ENT)

/* Layer 0
 * ,-------------------------------------------------------------------------------.
 * |   Q   |   W   |   E   |   R   |   T   |   Y   |   U   |   I   |   O   |   P   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |   A   |   S   |   D   |   F   |   G   |   H   |   J   |   K   |   L   |  Esc  |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |CTRL(Z)| ALT(X)| L3(C) | L4(V) |L2(BSPC)|L1(SPC)| L5(B)| ALT(N)|CTRL(M)| SftEnt|
 * `-------------------------------------------------------------------------------'
 */

 [0] = LAYOUT_ortho_3x10(
    KC_Q,    KC_W,    KC_E,    KC_R,    KC_T,    KC_Y,    KC_U,    KC_I,    KC_O,    KC_P,
    KC_A,    KC_S,    KC_D,    KC_F,    KC_G,    KC_H,    KC_J,    KC_K,    KC_L,    KC_ESC,
    CTL_Z,   ALT_X,   FN3_C,   FN4_V,   FN2_BSPC,FN1_SPC, FN5_B,   ALT_N,   CTL_M,   SFT_ENT
  ),

/* Layer 1
 * ,-------------------------------------------------------------------------------.
 * |   1   |   2   |   3   |   4   |   5   |   6   |   7   |   8   |   9   |   0   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |   F1  |   F2  |   F3  |   F4  |   F5  |   F6  |   F7  |   F8  |   F9  |  F10  |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |       |       |       |       |  DEL  |       |       |   .   |   /   | Enter |
 * `-------------------------------------------------------------------------------'
 */

  [1] = LAYOUT_ortho_3x10(
    KC_1,    KC_2,    KC_3,    KC_4,    KC_5,    KC_6,    KC_7,    KC_8,    KC_9,    KC_0,
    KC_F1,   KC_F2,   KC_F3,   KC_F4,   KC_F5,   KC_F6,   KC_F7,   KC_F8,   KC_F9,   KC_F10,
    _______, _______, _______, _______, KC_DEL,  _______, _______, KC_SLSH, KC_DOT , KC_ENT
  ),

/* Layer 2
 * ,-------------------------------------------------------------------------------.
 * |   !   |   @   |   #   |   $   |   %   |   ^   |   &   |   *   |   (   |   )   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |  F11  |  F12  |       |       |       |       |       |       |       |   `   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |       |       |       |       |       |       |       |       |       | Enter |
 * `-------------------------------------------------------------------------------'
 */

  [2] = LAYOUT_ortho_3x10(
    KC_EXLM, KC_AT,   KC_HASH, KC_DLR,  KC_PERC, KC_CIRC, KC_AMPR, KC_ASTR, KC_LPRN, KC_RPRN,
    KC_F11,  KC_F12,  _______, _______, _______, _______, _______, _______, _______, KC_GRV,
    _______, _______, _______, _______, _______, _______, _______, _______, _______, KC_ENT
  ),

/* Layer 3
 * ,-------------------------------------------------------------------------------.
 * |       |       |       |       |       |   -   |   =   |   [   |   ]   |   \   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |  TAB  |       |       |       |       |   ,   |   .   |   /   |   ;   |   '   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |       |       |       |       |       |       |  Left |  Down |   Up  | Right |
 * `-------------------------------------------------------------------------------'
 */

  [3] = LAYOUT_ortho_3x10(
    _______, _______, _______, _______, _______, KC_MINS, KC_EQL,  KC_LBRC, KC_RBRC, KC_BSLS,
    KC_TAB,  _______, _______, _______, _______, KC_COMM, KC_DOT,  KC_SLSH, KC_SCLN, KC_QUOT,
    _______, _______, _______, _______, _______, _______, KC_LEFT, KC_DOWN, KC_UP,   KC_RGHT
  ),

/* Layer 4
 * ,-------------------------------------------------------------------------------.
 * |       |       |       |       |       |   _   |   +   |   {   |   }   |   |   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |  TAB  |       |       |       |       |   <   |   >   |   ?   |   :   |   "   |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |       |       |       |       |       |       |  Home |  PGDN |  PGUP |  End  |
 * `-------------------------------------------------------------------------------'
 */

  [4] = LAYOUT_ortho_3x10(
    _______, _______, _______, _______, _______, KC_UNDS, KC_PLUS, KC_LCBR, KC_RCBR, KC_PIPE,
    KC_TAB,  _______, _______, _______, _______, KC_LABK, KC_RABK, KC_QUES, KC_COLN, KC_DQUO,
    _______, _______, _______, _______, _______, _______, KC_HOME, KC_PGDN, KC_PGUP, KC_END
  ),

/* Layer 5
 * ,-------------------------------------------------------------------------------.
 * |  Calc |Brwsr H|  Mail | MyComp|       |       |       |       |       | PSCR  |
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |       |       |       |       |       |       |       |       | BL_DEC| BL_INC|
 * |-------+-------+-------+-------+-------+-------+-------+-------+-------+-------|
 * |       |       |       |       | RESET |       |       |       |       |       |
 * `-------------------------------------------------------------------------------'
 */

  [5] = LAYOUT_ortho_3x10(
    KC_CALC, KC_WHOM, KC_MAIL, KC_MYCM, _______, _______, _______, _______, _______, KC_PSCR,
    _______, _______, _______, _______, _______, _______, _______, _______, BL_DEC,  BL_INC,
    _______, _______, _______, _______, RESET,   _______, _______, _______, _______, _______
  )
```
