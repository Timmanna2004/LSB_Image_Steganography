# 🔐 Steganography Using LSB in C

A **C-based Image Steganography** project that hides confidential text data inside a **BMP image** using the **Least Significant Bit (LSB)** technique. The project supports both **encoding** secret data into an image and **decoding** the hidden data from a stego image.

---

## 📌 Project Overview

Steganography is the technique of hiding secret information inside another medium in such a way that the existence of the information is not easily noticeable.

This project implements **image steganography using the LSB technique**. The secret text file is embedded into the pixel data of a BMP image by modifying the least significant bits of image bytes.

The project provides two operations:

* **Encoding (`-e`)** – Hide a secret text file inside a BMP image.
* **Decoding (`-d`)** – Extract the hidden text file from a stego BMP image.

---

## ✨ Features

* Hide text data inside a BMP image using **LSB encoding**.
* Extract hidden data from a stego image.
* Supports command-line arguments.
* Validates input and output file extensions.
* Checks whether the source image has sufficient capacity.
* Preserves the original BMP header.
* Stores the secret file extension and size along with the data.
* Uses a **magic string** to verify whether the image contains encoded data.
* Modular implementation using multiple `.c` and `.h` files.
* Handles file-opening and processing errors.

---

## 🛠️ Technologies Used

| Technology                 | Usage                                  |
| -------------------------- | -------------------------------------- |
| **C**                      | Core programming language              |
| **LSB Steganography**      | Data hiding technique                  |
| **BMP**                    | Cover image format                     |
| **File Handling**          | Reading/writing image and secret files |
| **Command Line Arguments** | User interaction                       |
| **GCC**                    | Compilation                            |

---

## 🧠 Concepts Demonstrated

This project helped strengthen the following concepts:

* C Programming
* Pointers
* Structures
* Enumerations
* File Handling
* Binary File Processing
* Bit Manipulation
* Bitwise Operators
* Command-Line Arguments
* Modular Programming
* Function Pointers and File Pointers
* Dynamic data processing
* Error Handling

---

## 🔄 Working Principle

### Encoding

The encoding process follows these major steps:

```text
        Cover BMP Image
               │
               ▼
        Read BMP Header
               │
               ▼
       Check Image Capacity
               │
               ▼
        Copy BMP Header
               │
               ▼
       Encode Magic String
               │
               ▼
    Encode Secret File Extension
               │
               ▼
       Encode Secret File Size
               │
               ▼
       Encode Secret File Data
               │
               ▼
          Stego Image
```

The secret information is stored by modifying the **LSB of image bytes**.

For example:

```text
Original byte : 10110100
Secret bit    :       1
Modified byte : 10110101
```

Only the least significant bit is modified, resulting in minimal visual changes to the image.

---

## 🔓 Decoding Process

The decoding process reverses the encoding operation:

```text
             Stego BMP Image
                    │
                    ▼
             Skip BMP Header
                    │
                    ▼
          Decode Magic String
                    │
                    ▼
       Decode Secret File Extension
                    │
                    ▼
          Decode Secret File Size
                    │
                    ▼
          Decode Secret File Data
                    │
                    ▼
            Extracted Text File
```

The program first verifies the **magic string** before extracting the hidden data.

---

## 📂 Project Structure

```text
Steganography/
│
├── main.c
├── encode.c
├── encode.h
├── decode.c
├── decode.h
├── common.h
├── types.h
│
├── beautiful.bmp
├── secret.txt
└── README.md
```

### File Description

| File            | Description                                                            |
| --------------- | ---------------------------------------------------------------------- |
| `main.c`        | Handles command-line arguments and selects encoding/decoding operation |
| `encode.c`      | Implements the complete encoding process                               |
| `encode.h`      | Encoding structures and function declarations                          |
| `decode.c`      | Implements the complete decoding process                               |
| `decode.h`      | Decoding structures and function declarations                          |
| `common.h`      | Contains common definitions such as the magic string                   |
| `types.h`       | Contains user-defined types and status enumerations                    |
| `beautiful.bmp` | Sample cover image                                                     |
| `secret.txt`    | Sample secret file                                                     |

---

## ⚙️ Compilation

Make sure GCC is installed on your system.

Compile the project using:

```bash
gcc main.c encode.c decode.c -o steganography
```

---

## 🚀 Usage

### Encode

```bash
./steganography -e <source.bmp> <secret.txt> [output.bmp]
```

Example:

```bash
./steganography -e beautiful.bmp secret.txt stego.bmp
```

This hides the contents of `secret.txt` inside `beautiful.bmp` and creates:

```text
stego.bmp
```

If an output filename is not provided, the program uses:

```text
default.bmp
```

---

### Decode

```bash
./steganography -d <stego.bmp> [output_file]
```

Example:

```bash
./steganography -d stego.bmp decoded
```

The hidden file is extracted using the original secret file extension.

If an output filename is not provided, the default output name is:

```text
Output
```

---

## 🧩 Encoding Data Format

The project stores information in the following order:

```text
BMP Header
    ↓
Magic String
    ↓
Secret File Extension Size
    ↓
Secret File Extension
    ↓
Secret File Size
    ↓
Secret File Data
    ↓
Remaining BMP Data
```

The project uses the magic string:

```text
#*
```

This is used during decoding to verify that the image contains data encoded by this application.

---

## 💻 Example

### Input

```text
Cover Image:
beautiful.bmp

Secret File:
secret.txt
```

Command:

```bash
./steganography -e beautiful.bmp secret.txt stego.bmp
```

Output:

```text
:::Encoding successfully:::
```

Then decode:

```bash
./steganography -d stego.bmp decoded
```

Output:

```text
:::Decoding successfully:::
```

The extracted file contains the original hidden message.

---

## 🔍 Important Functions

### Encoding

Some of the major functions implemented are:

```c
do_encoding()
open_encode_files()
check_capacity()
copy_bmp_header()
encode_magic_string()
encode_secret_file_extn_size()
encode_secret_file_extn()
encode_secret_file_size()
encode_secret_file_data()
encode_byte_to_lsb()
encode_size_to_lsb()
copy_remaining_img_data()
```

### Decoding

Major decoding functions include:

```c
do_decoding()
open_decode_files()
decode_magic_string()
decode_secret_file_extn_size()
decode_secret_file_extn()
decode_secret_file_size()
decode_secret_file_data()
decode_byte_from_lsb()
decode_size_from_lsb()
```

---

## 🧪 Error Handling

The application validates:

* Missing command-line arguments
* Unsupported operations
* Invalid image extensions
* Invalid secret file extensions
* Invalid output image extensions
* File opening failures
* Insufficient image capacity
* Invalid encoded data
* Failed read/write operations

---

## 🎯 Learning Outcomes

Through this project, I gained practical experience in:

* Implementing **LSB-based steganography**
* Working with **BMP image binary data**
* Performing bit-level data manipulation
* Handling files using `FILE *`
* Working with command-line arguments
* Designing modular C programs
* Implementing encoding and decoding algorithms
* Debugging file-processing applications
* Understanding how data can be embedded at the byte/bit level

---

## 🔮 Future Enhancements

Possible improvements include:

* Support for PNG/JPEG image formats
* Password-based encryption before embedding
* Support for hiding binary files
* Improved capacity calculation
* Improved command-line interface
* AES-based encryption of secret data
* Support for multiple secret files
* Improved validation and security

---

## 👨‍💻 Author

**Timmanna Kulagod**

Electronics & Communication Engineering
Embedded Systems | Embedded C | Linux | Data Structures

---

