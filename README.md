# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
def encryptRailFence(text, key):
    rail = [['\n' for i in range(len(text))] for j in range(key)]
    dir_down = False
    row, col = 0, 0
    for i in range(len(text)):
        if row == 0 or row == key - 1:
            dir_down = not dir_down
        rail[row][col] = text[i]
        col += 1
        row += 1 if dir_down else -1
    result = []
    for i in range(key):
        for j in range(len(text)):
            if rail[i][j] != '\n':
                result.append(rail[i][j])
    return "".join(result)

def decryptRailFence(cipher, key):
    rail = [['\n' for i in range(len(cipher))] for j in range(key)]
    dir_down, row, col = None, 0, 0
    for i in range(len(cipher)):
        if row == 0: dir_down = True
        if row == key - 1: dir_down = False
        rail[row][col] = '*'
        col += 1
        row += 1 if dir_down else -1
    index = 0
    for i in range(key):
        for j in range(len(cipher)):
            if rail[i][j] == '*' and index < len(cipher):
                rail[i][j] = cipher[index]
                index += 1
    result, row, col = [], 0, 0
    for i in range(len(cipher)):
        if row == 0: dir_down = True
        if row == key - 1: dir_down = False
        if rail[row][col] != '*':
            result.append(rail[row][col])
            col += 1
        row += 1 if dir_down else -1
    return "".join(result)

text = input("Enter text: ")
key = int(input("Enter key: "))

encrypted = encryptRailFence(text, key)
decrypted = decryptRailFence(encrypted, key)

print("Plaintext:", text)
print("Ciphertext:", encrypted)
print("Decrypted:", decrypted)

```
# OUTPUT
<img width="349" height="161" alt="image" src="https://github.com/user-attachments/assets/5042b91d-9591-47b4-93b9-6d88aa8f1690" />

# RESULT
Thus the rail fence transposition technique has been implemented successfully.
