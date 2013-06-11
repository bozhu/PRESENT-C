PRESENT is an ultra-lightweight block cipher well suitable for extremely constrained environments such as RFID tags and sensor networks [1]. Here we give a fast and compact software implementation of PRESENT. The program is written in plain C, which is easy to be changed to work on various platforms.

Lookup tables (1040 bytes in total) are used to speed up the permutation layer (also merged with S-boxes). Our implementation costs 1.83 ms on MICAz wireless sensor node to perform a full-round (31 rounds) encryption of PRESENT. Compared with the software implementation of AES in [2], which needs 1.46 ms and 1915 bytes to perform a full-round encryption, our software implementation of PRESENT is a competitive alternative to traditional ways based on AES. This result has also been included in our paper [3].

## License

BSD license

## Usage

There are two interfaces:

1. The full-round encryption function:
```c
    void present(uint8_t *plain, uint8_t *key, uint8_t *cipher)
```
Before using this function, the plaintext should have already been placed in the array `plain`, and the 80-bit secret key should also be arranged at `key`. After the encryption is done, the ciphertext will be computed and copied into `cipher`. Please note that the areas identified by `plain` and `cipher` can overlap with each other (also key and cipher).

2. We also provide an interface in which the rounds of encryption can be specified:
```c
    void present_rounds(uint8_t *plain, uint8_t *key, uint8_t rounds, uint8_t *cipher)
```
Especially, if `rounds` is equal to 31, it will be a full-round encryption, same as present().

## References

1. A. Bogdanov, L. R. Knudsen, G. Leander, C. Paar, A. Poschmann, M. J. B. Robshaw, Y. Seurin and C. Vikkelsoe. PRESENT: An Ultra-Lightweight Block Cipher. CHES 2007.
2. Michael Healy, Thomas Newe and Elfed Lewis. Analysis of Hardware Encryption Versus Software Encryption on Wireless Sensor Network Motes. Smart Sensors and Sensing Technology 2008.
3. Zheng Gong, Pieter Hartel, Svetla Nikova and Bo Zhu. Towards Secure and Practical MACs for Body Sensor Networks. Indocrypt 2009.
