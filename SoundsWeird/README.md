# Sounds Weird

## Chalenge Description

Police caught a man high on **LS*** who is suspected to be the part of the kidney selling organization. Police recovered nothing suspicious from him except an audio file. Police is trying to interogate him but he is to high to answer anything. He says he is the least significant  member of the organization and his work is to **blow** ballons and look after **fishes** in the fish tank.
Anakin01 knows that perseverance is the key to success in cracking such codes.Help find investigate the file.

## Solution

The decription suggests that LSB stegnography may have been used to encrypt some hidden messae in the wav file.We then write a simple pythn LSB decryption Script

```

import wave

# Extract data from audio file using LSB steganography
def extract_data(audio_file):
    # Open audio file
    with wave.open(audio_file, "rb") as wav:
        # Get audio file parameters
        params = wav.getparams()
        nframes = params[3]
        sampwidth = params[1]
        frames = wav.readframes(nframes)

        # Extract data from audio file
        data_bin = ""
        for i in range(0, len(frames), sampwidth):
            for j in range(sampwidth):
                # Convert byte to binary string
                byte_bin = int_to_bin(frames[i + j])
                # Extract least significant bit
                data_bin += byte_bin[-1]

        # Convert binary data to ASCII string
        data = ""
        for i in range(0, len(data_bin), 8):
            byte = bin_to_int(data_bin[i:i+8])
            data += chr(byte)

        return data

# Convert integer to binary string
def int_to_bin(n):
    return bin(n)[2:].zfill(8)

# Convert binary string to integer
def bin_to_int(b):
    return int(b, 2)

# Test the function
audio_file = "chall.wav"
extracted_data = extract_data(audio_file)
print("Extracted data:", extracted_data)

```
The Extracted data gives us 

