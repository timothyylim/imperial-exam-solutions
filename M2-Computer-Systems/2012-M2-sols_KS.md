#Computer Systems 2012
*Ananda didn't teach this year*
##Section A
###1 a.
2M X 16-bit memory made up from 256K x 4-bit chips.

2 x 2^20 = 2^1 x 2^20 = 2^21 rows.

16-bit = 2 bytes = 2 words per row.

256 x 2^10 = 2^8 x 2^10 = 2^18 rows per chip.

Memory Size = 2M x 2 Bytes = 4MB

**(i.) 4 chips** per module are required (4-bit x N = 16-bit).  Since each module will have 512KB (256K x 2 Bytes) and the total memory size required is 4MB, then we will need **8 modules**.

**(ii.)** Bits required to access byte-addressable memory: 2^21 rows * 2^1 bytes per row = 2^22 so 22 bits.  Bits required to access word-addressable memory: **21 bits.**

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
