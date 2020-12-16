# Tiled to GBA export
This is a Tiled extension/export plugin that converts all tile layers to 4 byte aligned C arrays of hexadecimal values. Each tile is written out by its ID in hex, and blank tiles are defaulted to 0x0000.

This is a simple but easy to use format for Game Boy Advance development.

## Installation
To add this extension to your Tiled installation:
* Open Tiled and go to Edit > Preferences > Plugins and click the "Open" button to open the extensions directory.
* Download [tiled-to-gba-export.js](https://raw.githubusercontent.com/djedditt/tiled-to-gba-export/master/tiled-to-gba-export.js) in this repository and copy it to that location. The script can be placed either directly in the extensions directory or in a subdirectory.
* When using a version older than Tiled 1.3.3, restart Tiled.

## Output
The export plugin generates a .c source file and associated .h header file. Below you'll find example output for a very small 4x4 map with two tile layers.

**example.h**

```C
#ifndef EXAMPLE_H
#define EXAMPLE_H

#define EXAMPLE_WIDTH  (4)
#define EXAMPLE_HEIGHT (4)
#define EXAMPLE_LENGTH (16)

extern const unsigned short Tile_Layer_1[16];
extern const unsigned short Tile_Layer_2[16];

#endif

```

**example.c**

```C
#include "example.h"

const unsigned short Tile_Layer_1[16] __attribute__((aligned(4))) =
{
    0x0000, 0x0001, 0x0002, 0x0003, 
    0x001E, 0x001F, 0x0020, 0x0021, 
    0x003C, 0x003D, 0x003E, 0x003F, 
    0x005A, 0x005B, 0x005C, 0x005D
};

const unsigned short Tile_Layer_2[16] __attribute__((aligned(4))) =
{
    0x00F8, 0x00F9, 0x00FA, 0x00FB, 
    0x0116, 0x0117, 0x0118, 0x0119, 
    0x0134, 0x0135, 0x0136, 0x0137, 
    0x0152, 0x0153, 0x0154, 0x0155
};

```

## License
This work is licensed under the MIT License. See [LICENSE](https://raw.githubusercontent.com/djedditt/tiled-to-gba-export/master/LICENSE) for details.
