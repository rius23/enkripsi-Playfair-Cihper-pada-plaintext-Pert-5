# enkripsi-Playfair-Cihper-pada-plaintext-Pert-5

Nama    : Serius Ndruru

NIM     : 312210508

Kelas   :TI.22.A.5

#prompt: Lakukan enkripsi Playfair Cihper pada plaintext:

#GOOD BROOM SWEEP CLEAN

#REDWOOD NATIONAL STATE PARK

#JUNK FOOD AND HEALTH PROBLEMS

#Dengan kunci “TEKNIK INFORMATIKA” dekripnya

def prepare_key(key):
    key = key.upper().replace("J", "I")
    matrix = [[None for _ in range(5)] for _ in range(5)]
    letters_used = set()
    row = 0
    col = 0

    for char in key:
        if 'A' <= char <= 'Z' and char not in letters_used:
            matrix[row][col] = char
            letters_used.add(char)
            col += 1
            if col == 5:
                col = 0
                row += 1

    for char_code in range(ord('A'), ord('Z') + 1):
        char = chr(char_code)
        if char == 'J':
            continue
        if char not in letters_used:
            matrix[row][col] = char
            letters_used.add(char)
            col += 1
            if col == 5:
                col = 0
                row += 1

    return matrix

def find_char_coordinates(matrix, char):
    for row in range(5):
        for col in range(5):
            if matrix[row][col] == char:
                return row, col
    return None

def encrypt_playfair(plaintext, key):
    matrix = prepare_key(key)
    plaintext = plaintext.upper().replace("J", "I")
    plaintext = "".join(filter(str.isalpha, plaintext))
    if len(plaintext) % 2 != 0:
        plaintext += "X"

    ciphertext = ""
    for i in range(0, len(plaintext), 2):
        char1 = plaintext[i]
        char2 = plaintext[i + 1]
        row1, col1 = find_char_coordinates(matrix, char1)
        row2, col2 = find_char_coordinates(matrix, char2)

        if row1 == row2:
            ciphertext += matrix[row1][(col1 + 1) % 5]
            ciphertext += matrix[row2][(col2 + 1) % 5]
        elif col1 == col2:
            ciphertext += matrix[(row1 + 1) % 5][col1]
            ciphertext += matrix[(row2 + 1) % 5][col2]
        else:
            ciphertext += matrix[row1][col2]
            ciphertext += matrix[row2][col1]

    return ciphertext

def decrypt_playfair(ciphertext, key):
    matrix = prepare_key(key)
    ciphertext = ciphertext.upper()
    plaintext = ""

    for i in range(0, len(ciphertext), 2):
        char1 = ciphertext[i]
        char2 = ciphertext[i + 1]
        row1, col1 = find_char_coordinates(matrix, char1)
        row2, col2 = find_char_coordinates(matrix, char2)

        if row1 == row2:
            plaintext += matrix[row1][(col1 - 1) % 5]
            plaintext += matrix[row2][(col2 - 1) % 5]
        elif col1 == col2:
            plaintext += matrix[(row1 - 1) % 5][col1]
            plaintext += matrix[(row2 - 1) % 5][col2]
        else:
            plaintext += matrix[row1][col2]
            plaintext += matrix[row2][col1]

    return plaintext


key = "TEKNIK INFORMATIKA"
plaintext1 = "GOOD BROOM SWEEP CLEAN"
plaintext2 = "REDWOOD NATIONAL STATE PARK"
plaintext3 = "JUNK FOOD AND HEALTH PROBLEMS"


ciphertext1 = encrypt_playfair(plaintext1, key)
ciphertext2 = encrypt_playfair(plaintext2, key)
ciphertext3 = encrypt_playfair(plaintext3, key)

decrypted1 = decrypt_playfair(ciphertext1, key)
decrypted2 = decrypt_playfair(ciphertext2, key)
decrypted3 = decrypt_playfair(ciphertext3, key)


print(f"Plaintext 1: {plaintext1}, Ciphertext: {ciphertext1}, Decrypted: {decrypted1}")
print(f"Plaintext 2: {plaintext2}, Ciphertext: {ciphertext2}, Decrypted: {decrypted2}")
print(f"Plaintext 3: {plaintext3}, Ciphertext: {ciphertext3}, Decrypted: {decrypted3}")


![Screenshot 2024-10-16 141508](https://github.com/user-attachments/assets/dbfe5cbf-89b8-43e9-a60d-51253fbf5622)
