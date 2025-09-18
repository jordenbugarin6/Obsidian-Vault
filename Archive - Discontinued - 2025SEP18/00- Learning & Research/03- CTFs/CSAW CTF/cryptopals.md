#### Converting Hex to base64
![[Pasted image 20240906231919.png]]

```bash
echo "49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d" | xxd -r -p | base64
```
-------------------
#### Fixed XOR
![[Pasted image 20240906232415.png]]
xor.py
```python
def xor_hex_strings(hex_str1, hex_str2):
    # Decode the hex strings to bytes
    buffer1 = bytes.fromhex(hex_str1)
    buffer2 = bytes.fromhex(hex_str2)

    if len(buffer1) != len(buffer2):
        raise ValueError("Buffers must be of equal length")

    # XOR each byte and convert back to hex
    result = bytes([b1 ^ b2 for b1, b2 in zip(buffer1, buffer2)])

    # Return the result as a hex string
    return result.hex()

# Example usage:
hex_str1 = "1c0111001f010100061a024b53535009181c"
hex_str2 = "686974207468652062756c6c277320657965"

result = xor_hex_strings(hex_str1, hex_str2)
print(result)  # Output should be: 746865206b696420646f6e277420706c6179
```
-----------------
#### Single-byte XOR cipher
XORcipher.py
```python
import binascii

# Define character frequencies for English letters, space, and common punctuation
english_freq = {
    'a': 0.0651738, 'b': 0.0124248, 'c': 0.0217339, 'd': 0.0349835,
    'e': 0.1041442, 'f': 0.0197881, 'g': 0.0158610, 'h': 0.0492888,
    'i': 0.0558094, 'j': 0.0009033, 'k': 0.0050529, 'l': 0.0331490,
    'm': 0.0202124, 'n': 0.0564513, 'o': 0.0596302, 'p': 0.0137645,
    'q': 0.0008606, 'r': 0.0497563, 's': 0.0515760, 't': 0.0729357,
    'u': 0.0225134, 'v': 0.0082903, 'w': 0.0171272, 'x': 0.0013692,
    'y': 0.0145984, 'z': 0.0007836, ' ': 0.1918182, '.': 0.002,
    ',': 0.002, '!': 0.001, '?': 0.001, "'": 0.002, '"': 0.002
}

# Function to score plaintext based on character frequencies
def score_text(text):
    return sum([english_freq.get(chr(byte), 0) for byte in text.lower()])

# Function to XOR a byte array with a single-byte key
def xor_with_key(data, key):
    return bytes([byte ^ key for byte in data])

# Hex string that was XOR'd with a single character
hex_string = '1b37373331363f78151b7f2b783431333d78397828372d363c78373e783a393b3736'

# Convert hex string to bytes
data = binascii.unhexlify(hex_string)

# Try XORing with every possible single-byte key (0-255)
best_score = 0
best_result = None
best_key = None

for key in range(256):
    result = xor_with_key(data, key)
    result_score = score_text(result)
    
    if result_score > best_score:
        best_score = result_score
        best_result = result
        best_key = key

# Print the best result
print(f"Best key: {chr(best_key)} (byte value: {best_key})")
print(f"Decrypted message: {best_result.decode('utf-8', errors='replace')}")
```