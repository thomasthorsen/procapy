procapy
=======

Programmer's Calculator in Python

Installation
------------

Place proca.py in your executable path (for example ~/bin). For ease of access it is recommended to add a short alias to bash:

    alias c='procapy.py'

This will allow the calculator to be invoked simply as:

    c "5+5"

Usage
-----

Procapy supports any valid Python, and will reduce the result of any expression to a number and print it as floating point (if applicable), integer, hex and binary.

In addition to the built-in functions in Python the following functions have been added:

 * u(w,x): truncate x to an unsigned integer of width w.
 * u8(x), u16(x), u32(x), u64(x): truncate x to an unsigned integer of the indicated width.
 * i(w,x): truncate x to a signed integer of width w.
 * i8(x), i16(x), i32(x), i64(x): truncate x to a signed integer of the indicated width.

These are similar to the built-in function int(x) which will truncate to an integer of unlimited width.

Examples
--------

Difference between two hex numbers:

    > c "0x0003 - 0xFFFE"
    -65531 0xffff0005 0b11111111111111110000000000000101

Same but truncated to 16bit unsigned range:

    > c "u16(0x0003 - 0xfffe)"
    u16(-65531) => 5
    5 0x5 0b101

Division and addition:

    > c "800 / 33 + 500 / 42"
    36.14718614718615 36 0x24 0b100100

Same but showing effects of truncation to 8bit unsigned of intermediate results:

    > c "u8(800 / 33) + u8(500 / 42)"
    u8(24.242424242424242) => 24
    u8(11.904761904761905) => 11
    35 0x23 0b100011

Interpretation of a hex number as unsigned integer:

    > c "0xfffffffe"
    4294967294 0xfffffffe 0b11111111111111111111111111111110

Same but showing truncation to 32bit signed integer:

    > c "i32(0xfffffffe)"
    i32(4294967294) => -2
    -2 0xfe 0b11111110

Comparisons operators return True/False:

    > c "0x0003 - 0xffff > 50"
    False 0x0 0b0

Same but with truncation of intermediate result to 32bit unsigned integer:

    > c "u32(0x0003 - 0xffff) > 50"
    u32(-65532) => 4294901764
    True 0x1 0b1

Mixed radix numbers:

    > c "0b1011 + 0x5 + 5"
    21 0x15 0b10101

Bitwise operators (AND, NOT, OR, XOR):

    > c "0b1011 | ~0x5 & 5 ^ 0b101"
    15 0xf 0b1111

Shift operators:

    > c "(1 << 7) >> 3"
    16 0x10 0b10000

Boolean operators and (in)equality:

    > c "45 > 5 and 6 < 7 or 5 == 3 and 4 != 4"
    True 0x1 0b1

Rounding:

    > c "round(4.49)"
    4 0x4 0b100
