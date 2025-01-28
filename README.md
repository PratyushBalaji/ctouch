# Touch boilerplate C files (`ctouch`)

This is a simple Bash script that creates a basic prepopulated C (`.c`) file.  

---

## Features

- Automatically generates a `.c` file with boilerplate code:
  - Includes a default `main` function (can be skipped with the `--no-main` option).
  - Automatically adds the `#include` statements for standard headers like `<stdio.h>` and any additional headers specified by the user.
- Flexible handling of filenames and extensions:
  - Appends `.c` to filenames automatically unless the file already ends with `.c` or the `--keep-extension` (`-k`) option is used.
- Options to prevent accidental overwrites with the `--overwrite` (`-o`) flag.
- Customizable header inclusions using the `--header` option.
- Provides clear error messages and usage guidance for invalid inputs.

---

## Installation

### Step 1 : Clone or Copy the Script
Copy the script into a file named `ctouch` and make it executable :
```bash
chmod +x ctouch
```

### Step 2 : Add to Your `PATH`
If you are on a shared system or don’t have root access, you can add the directory containing the script to your `PATH`.

1. Move the script to a directory like `~/bin` :
   ```bash
   mv ctouch ~/bin
   ```
2. Add `~/bin` to your `PATH` if it's not already included. Edit your `~/.bashrc`, `~/.bash_profile` or `~/.profile` :
   ```bash
   nano ~/.bashrc
   ```
   Add the following line :
   ```bash
   export PATH="$HOME/bin :$PATH"
   ```

   Or do it in 1 step with :
   ```bash
   echo 'export PATH="$PATH :$HOME/bin"' >> ~/.bashrc
   ```
3. Reload the shell configuration :
   ```bash
   source ~/.bashrc
   ```

---

## Usage

### Basic Usage
Create a simple `.c` file with a `main` function and the default `#include <stdio.h>`:
```bash
ctouch myfile
```
This creates a file named `myfile.c` with the following content:
```c
#include <stdio.h>

int main() {
    // Your code here
    return 0;
}
```

### Specifying Additional Headers
Add custom headers using the `--header` option:
```bash
ctouch --header stdlib math myfile
```
This generates:
```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int main() {
    // Your code here
    return 0;
}
```

### Keep the Specified Extension
Use the `-k` or `--keep-extension` flag to prevent `.c` from being appended:
```bash
ctouch -k myprogram.cpp
```
This creates a file named `myprogram.cpp` instead of appending `.c`.

### Overwrite Existing Files
Use the `-o` or `--overwrite` flag to overwrite an existing file:
```bash
ctouch -o myfile
```

### Skip the Main Function
If you don't want the `main` function, use the `--no-main` option:
```bash
ctouch --no-main myfile
```
This generates:
```c
#include <stdio.h>

// Your code here
```

### Explicitly Specify the Filename
Use the `-f` or `--filename` option to specify the filename:
```bash
ctouch -f myprogram
```
This ensures the filename is treated correctly, even if other options might interfere.

### Combining Options
You can combine multiple options for more customization:
```bash
ctouch -o -k --no-main --header stdlib math -f myprogram.k
```
This creates a file named `myprogram` (with extension `.k`), overwrites if it exists, skips the `main` function, and includes `<stdio.h>`, `<stdlib.h>`, and `<math.h>`.

---

## Known issues and planned changes
Issues : 
- Since I'm using cases instead of `getopts`, stacking options like `-ko` to keep extension and overwrite is currently not supported. It must be separately specified as `-k -o` or similar.
- If the filename is the last argument following the `--header` option, it is treated as a header file to be included instead of as the filename. An error message is shown indicating that the filename was not detected and that the user should ideally specify the filename explicitly with `-f` or place it somewhere else in the command.

Improvements : 
- Plan on adding support for non-standard user-made headers (Potentially with custom extensions)
- Other basic boilerplates such as basic input reading or printing

## Purpose
This file isn't intended for professional development, but rather to aid my specific needs when it comes to learning C. Changes will be made as my demand from the program increases over time. All its really intended for is to avoid having to rewrite the main function and headers everytime I create a new .c file to learn something new / test something out.
