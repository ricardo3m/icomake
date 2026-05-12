# icomake
Trivial tool that combines multiple ICO/PNGs into single .ICO file that keeps format of each sub-image.

## Usage
Command line:

    icomake.exe output.ico input1 [input2 [...]]

Input file formats supported:
* Any existing ICO containing either uncompressed bitmaps (BMPs) or PNGs
* 32-bit PNGs (with alpha channel) of any size.

Outputs single ICO file containing all input images.

* If multiple images of the same resolution and color depth are provided, the last (in order it appears on the command line) is used, i.e. you can use the tool to replace single sub-image within existing .ico file.

## PNG icons

Windows Vista and later supports ICO files that contain PNG sub-images. Most graphics applications (at least those that I use) will only save the 256×256 one as PNG, but all, even 16×16, can safely be PNGs too. Thus enter the purpose of this tool, as PNGs are by magnitudes smaller than uncompressed bitmaps.

**Note:** In order for ICOs to show on Windows XP and older, and perhaps other OSs, at least some icons should be stored as bitmaps. At least 32×32 icon, ideally also 16×16, 24×24, and 48×48. This tool does not and can not convert PNG to BMP ICO.

## Sub-image order optimization

Windows icon loader iterates over all icons in file, assessing difference between requested and available icons, stopping only on exact match. The assessment is in both resolution and color depth, preferring resolution over color depth; only to a certain degree though.

This tool orders sub-images from smallest to largest, with the highest quality image (256×256×32) placed last. Windows Photos (and WIC-based viewers) display the last frame of an ICO file by default, so this ensures the full-resolution image is shown when opening the file in Windows Photos.

If all resolutions were available, the order would be following (from first to last):

1. ?×?×1 (from smallest to largest)
1. ?×?×4 (from smallest to largest)
1. ?×?×8 (from smallest to largest)
1. ?×?×24 (from smallest to largest)
1. ?×?×32 (from smallest to largest, with 256×256×32 last)

*Of course, whether this is the best order is open for a debate.*
