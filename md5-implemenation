def main(): 
    # get the message from the user
    message = input("Enter a message: ")

    # send the message to my md5 function 
    compute_md5(message)

def left_rotate(x, s):
    return ((x << s) | (x >> (32 - s))) & 0xffffffff

# md5 rotation amounts for all rounds
shifts = [
    # round 1
    7, 12, 17, 22,
    7, 12, 17, 22,
    7, 12, 17, 22,
    7, 12, 17, 22,

    # round 2
    5, 9, 14, 20,
    5, 9, 14, 20,
    5, 9, 14, 20,
    5, 9, 14, 20,

    # round 3
    4, 11, 16, 23,
    4, 11, 16, 23,
    4, 11, 16, 23,
    4, 11, 16, 23, 

    # round 4
    6, 10, 15, 21,
    6, 10, 15, 21,
    6, 10, 15, 21,
    6, 10, 15, 21
]

constants = [
    0xd76aa478, 0xe8c7b756, 0x242070db, 0xc1bdceee,
    0xf57c0faf, 0x4787c62a, 0xa8304613, 0xfd469501,
    0x698098d8, 0x8b44f7af, 0xffff5bb1, 0x895cd7be,
    0x6b901122, 0xfd987193, 0xa679438e, 0x49b40821, 
    0xf61e2562, 0xc040b340, 0x265e5a51, 0xe9b6c7aa, 
    0xd62f105d, 0x02441453, 0xd8a1e681, 0xe7d3fbc8,
    0x21e1cde6, 0xc33707d6, 0xf4d50d87, 0x455a14ed,
    0xa9e3e905, 0xfcefa3f8, 0x676f02d9, 0x8d2a4c8a,
    0xfffa3942, 0x8771f681, 0x6d9d6122, 0xfde5380c,
    0xa4beea44, 0x4bdecfa9, 0xf6bb4b60, 0xbebfbc70,
    0x289b7ec6, 0xeaa127fa, 0xd4ef3085, 0x04881d05,
    0xd9d4d039, 0xe6db99e5, 0x1fa27cf8, 0xc4ac5665,
    0xf4292244, 0x432aff97, 0xab9423a7, 0xfc93a039,
    0x655b59c3, 0x8f0ccc92, 0xffeff47d, 0x85845dd1,
    0x6fa87e4f, 0xfe2ce6e0, 0xa3014314, 0x4e0811a1,
    0xf7537e82, 0xbd3af235, 0x2ad7d2bb, 0xeb86d391
]

def compute_md5(message):
    # convert the message from a string to bytes
    message_bytes = message.encode('utf-8')

    # save the original bit length
    bit_length = len(message_bytes) * 8

    # make the message bytes changeable
    padded_message = bytearray(message_bytes)

    # add the first md5 padding byte
    padded_message.append(0x80)

    # keep adding zero bytes until the message reaches 56 bytes in the block
    while len(padded_message) % 64 != 56:
        padded_message.append(0x00)

    # convert original bit length into 8 bytes using little endian order 
    bit_length_bytes = bit_length.to_bytes(8, byteorder='little')
    padded_message.extend(bit_length_bytes)

    # initialize the four md5 state values
    A = 0x67452301
    B = 0xefcdab89
    C = 0x98badcfe
    D = 0x10325476

    for block_start in range(0, len(padded_message), 64):
        block = padded_message[block_start:block_start + 64]
        words = []
            
        for i in range(0, 64, 4):
            word = int.from_bytes(block[i:i+4], byteorder='little')
            words.append(word)

        a = A
        b = B
        c = C
        d = D

        for i in range(64):

            if i < 16:
                f = ((b & c) | ((~b) & d)) & 0xffffffff
                g = i

            elif i < 32:
                f = ((b & d) | (c & (~d))) & 0xffffffff
                g = (5 * i + 1) % 16

            elif i < 48:
                f = (b ^ c ^ d) & 0xffffffff
                g = (3 * i + 5) % 16

            else:
                f = (c ^ (b | (~d))) & 0xffffffff
                g = (7 * i) % 16

            temp = (a + f + constants[i] + words[g]) & 0xffffffff
            temp = left_rotate(temp, shifts[i])
            temp = (temp + b) & 0xffffffff

            a = d
            d = c
            c = b
            b = temp

        # after the 64 steps, update the main md5 state
        A = (A + a) & 0xffffffff
        B = (B + b) & 0xffffffff
        C = (C + c) & 0xffffffff
        D = (D + d) & 0xffffffff
    A_bytes = A.to_bytes(4, byteorder='little')
    B_bytes = B.to_bytes(4, byteorder='little')
    C_bytes = C.to_bytes(4, byteorder='little')
    D_bytes = D.to_bytes(4, byteorder='little')

    digest = A_bytes + B_bytes + C_bytes + D_bytes

    # converting to hexadecimal
    hash_result = digest.hex()

    print("MD5 Hash:", hash_result)

if __name__ == "__main__":
    main()
