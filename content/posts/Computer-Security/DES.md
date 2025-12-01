---
date: "2025-12-01T18:23:22+05:30"
draft: false
title: "Computer Security: Data Encryption Standard (DES)"
categories: ['Computer Security']
---

DES is a symmetric-key block cipher that follows the Fiestal Cipher structure. 

### The steps involved in encryption are:

1. Apply an initial permutation to the 64-bit input block using a permutation matrix
2. Similar to the Fiestal Cipher structure, split the 64 bit output after permutation into 2 halves L<sub>0</sub> (32 bits) and R<sub>0</sub> (32 bits)
3. Compute F(R<sub>0</sub>, k<sub>0</sub>) using expansion, XOR, S-boxes, and permutation
4. Set L<sub>1</sub> = R<sub>0</sub> and R<sub>1</sub> = L<sub>0</sub> XOR F(R<sub>0</sub>, k<sub>0</sub>)
5. Now, this concludes the first round. Now, do steps 3-4 15 more times
6.  After round 16, Merge L<sub>16</sub> (32 bits) and R<sub>16</sub> (32 bits)
7. Undo the initial permutation to get the cipher text

### Now, let's look at some of the non-intuitive steps in detail:
**Initial Permutation** \
This step involves transposition of the 64-bit input block based on a IP matrix. The IP<sup>-1</sup> matrix is the reverse of the IP matrix which will be used in the last step will undo this transposition. This permutation plays no role in the cryptography aspect of the cipher. This step was introduced because of hardware considerations which were a major bottleneck during the 20th century.

**The Fiestal Function (F)** \
The heart of DES encryption lies in its Fiestal Function F, which takes two inputs: a 32-bit right half of data (R<sub>i</sub>), and a 48-bit round key (k<sub>i</sub>). The Fiestal Function provides DES the 2 key principles of encryption:
- **Diffusion** (The influence of 1 input bit should be spread across multiple output bits) 
- **Confusion** (The relationship between input and output is hidden)

There are 4 steps involved in the Fiestal Function:
1. Expansion (E-box) \
The expansion provides **Diffusion**. Expansion ensures diffusion by duplicating 16 of input bits in the output. Thus, the 32 bit R<sub>i</sub> input is expanded to a 48 bit output by duplicating 16 bits in the input.

> 32 bit -> E-box -> 48 bit 


This idea is illustrated below:
![E-box](/imgs/des/e-box.png)
In the above table, the first and the last column contain the repeated bits of the input.

2. XOR with subkey (k<sub>i</sub>)
This step is pretty straight forward.

> E-box output (48 bit) XOR Sub-key (k<sub>i</sub>)= 48 bit Output

3. Substition (S-box) \
The substitution provides **Confusion**. This is one of the crucial parts of the encryption process as this ensures that there is a complex relationship between the plain text and the cipher text. \
![S-box workflow](/imgs/des/substitution.png)
Steps involved:
    - The 48-bit result from the XOR operation is divided into eight 6-bit chunks
    - Each chunk is processed by its own S-box (4x16 matrix), which takes 6 bits as input, and outputs 4 bits
    - The first and last bits choose one of the 4 possible rows, and the middle 4 bits select one of the 16 possible columns
    - Using the row and column, choose the 4-bit entry from substitution lookup table
    - For each of the 8 chunks, you get a 4-bit entry. Therefore, the overall output will be 32 bits long.
    ![s-box](/imgs/des/s-box.png)
     
4. Permutation (P-box) \
The final step applies a permutation to the 32-bit output from the S-boxes. This permutation rearranges the bits further contributing to diffusion by ensuring the current output of the S-box affects multiple S-boxes in next rounds.

**Reverse Permutation** \
This step involves undoing the intitial permutation to get the final cipher text using IP<sup>-1</sup>

### Voilà! You have successfully nailed DES encryption.



