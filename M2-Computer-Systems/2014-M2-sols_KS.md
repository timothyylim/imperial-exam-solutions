#Computer Systems 2014
##Section A
###1 a.

Decimal | Binary
--------|-------
13 | 0000 1101
4 | 0000 0100
13 - 4 = 9 | 0000 1001

###1 b.

8G x 16-bit Main Memory. 8G = 8 x 2^30 rows.  16-bit = 2 bytes per row.

**(i.) Word-Addressable Main Memory:**
* word-addressable = address for every row (word = 1 row).
* bits required for addressing: 8 x 2^30 = 2^3 x 2^30 = 2^33.

**(ii.) Byte-Addressable Main Memory:**
* byte-addressable = address for every byte.
* bits required for addressing: 2 x 8 x 2^30 = 2^1 x 2^3 x 2^30 = 2^34.

###1 c.

Equation | Rule
------------ | -------------
E = A + (A' \* B) + (A + B)' | given
E = (A + A') \* (A + B) + (A + B)' | distributive
E = 1 \* (A + B) + (A + B)' | negation
E = (A + B) + (A + B)' | simplification
E = 1 | negation

###1 d.

C304 F000 ==> **1100 0011 0000 0100 1111 0000 0000 0000 (binary)**

Sign (1st bit): 1 --> negative number

Exponent (middle 8-bits): 1000 0110 = 134 --> E = 134 - 127 = 7

Significand + **hidden bit** (last 23-bits): **1**.000 0100 1111 0000 0000 0000

Now we put it all together... (significand + hidden bit) x (2^exponent) = a binary number.  Convert binary to decimal.  Add sign.

1.0000 1001 1110 0000 0000 000 x 2^7 = 1000 0100.1111 0000 0000 000 = 2^7 + 2^2 + 2^-1 + 2^-2 + 2^-3 + 2^-4 = 132.9375

add in the sign... -1.329375 x 2^2 = **-132.9375 (decimal)**

http://www.h-schmidt.net/FloatConverter/IEEE754.html

##Section B
###2 a.

**(i.)** Every machine instruction must have an **OPCODE** or operation code for selecting CPU instruction (4 bits).

For more information see [CPU Organization](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/3_Slides_CPUOrganisation.ppt) slides 6-8.
