# MD5 Implementation in Python

This project is a manual implementation of the MD5 hashing algorithm written in Python.

## What the Program Does

- Accepts a text message from the user
- Converts the message into UTF-8 bytes
- Saves the original message length in bits
- Applies MD5 padding
- Processes the padded message in 512-bit blocks
- Splits each block into sixteen 32-bit words
- Performs 64 MD5 operations across four rounds
- Updates the internal A, B, C, and D state values
- Produces a 128-bit MD5 digest
- Displays the result as a 32-character hexadecimal string

## Concepts Practiced

- Byte manipulation
- Bitwise operations
- Circular left rotation
- Little-endian byte order
- 32-bit arithmetic
- Message padding
- Block-based hashing

## Example

- Input: Hello
- Output: 8b1a9953c4611296a827abf8c47804d7

## Security Note

MD5 is no longer considered secure for modern cryptographic use because practical collision attacks exist. This implementation was created for educational purposes to understand how a cryptographic hash function processes data internally.
