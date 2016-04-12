#Computer Systems 2012
*Ananda didn't teach this year*
##Section A
###1 a.
2M X 16-bit memory made up from 256K x 4-bit chips.

2 x 2^20 = 2^1 x 2^20 = 2^21 rows.

16-bit = 2 bytes = 2 words per row.

256 x 2^10 = 2^8 x 2^10 = 2^18 rows per chip.

**(i.) 4 chips** per module are required (4-bit x N = 16-bit).  Since each module will have 512K, **4 modules** will be required to make up 2M.

**(ii.)** Bits required to access byte-addressable memory: 2^21 rows * 2^1 bytes per row = 2^22 bits.  Bits required to access word-addressable memory: **2^21 bits.**

**(iii.) Big Endian**

Integer #1 = 03F7 (hex) = 0000 0011 1111 0111 (binary) = 1+2+4+16+32+64+128+256+512 = 1015 (decimal)

Integer #2 = 8001 (hex) = 1000 0000 0000 0001 (binary) = -(2^N-1) - (2^0) = -2^15-1 = -32769 (decimal)

| Two's Complement | Binary              | Decimal |
|------------------|---------------------|---------|
| Integer #1       | 0000 0011 1111 0111 | 1015    |
| Integer #2       | 1000 0000 0000 0001 | -32769  |
| Sum              | 1000 0011 1111 1000 | -33784  |

**(iv.) Little Endian**

Integer #1 = F703 (hex) = 1111 0111 0000 0011 (binary) = -(2^N-1) - (2^0 + 2^1 + 2^8 + 2^9 + 2^10 + 2^12 + 2^13 + 2^14) = 2^15 - 30467 = 2301 (decimal)

Integer #2 = 0180 (hex) = 0000 0001 1000 0000 (binary) = 384 (decimal)

| Two's Complement | Binary              | Decimal |
|------------------|---------------------|---------|
| Integer #1       | 1111 0111 0000 0011 | -2301   |
| Integer #2       | 0000 0001 1000 0000 | 384     |
| Sum              | 1111 1000 1000 0011 |  -1917  |


###1 b.
