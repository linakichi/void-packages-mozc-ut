# NOTICE

## Mozc

Mozc is developed by Google.

- Source: https://github.com/google/mozc
- License: BSD-3-Clause

Mozc dictionary data and source code have separate licensing terms. Refer to the original Mozc project for details.

## UT dictionaries

The UT dictionaries are provided by their respective authors.

- Source: https://github.com/utuhiro78
- Generated dictionary: `mozcdic-ut.txt`
- License information: Combined

The generated dictionary combines multiple dictionary sources. The original licensing terms of each source must be respected.

**Merge project:**
https://github.com/utuhiro78/merge-ut-dictionaries

**License information:**
https://github.com/utuhiro78/merge-ut-dictionaries/blob/main/LICENSE

The combined dictionary is generated locally during the package build.
Pre-generated combined dictionaries are not distributed by this project.

This follows the upstream project's distribution approach, in which
individual dictionaries are provided separately and users generate
the combined dictionary themselves.

## Dictionary processing

The dictionary merge process uses the following data:

| Source | License / terms | Usage |
|---|---|---|
| UT dictionary sources | Various; see individual projects | Dictionary entries |
| jawiki latest pages-articles multistream index | CC BY-SA | Word cost calculation |
| Mozc `dictionary*.txt` | Mixed | Duplicate word removal |
| Mozc `id.def` | BSD-3-Clause | Dictionary ID updates |

### jawiki index

Source:
https://dumps.wikimedia.org/jawiki/latest/

The index is used to calculate word costs during dictionary generation.

### Mozc dictionary data

Source:
https://github.com/google/mozc/tree/master/src/data/dictionary_oss

Mozc dictionary files are used for duplicate word removal and ID updates.

## Dictionary merge source code

The original dictionary merge source code is distributed under:

- Apache License, Version 2.0

Original copyright and license notices are retained in the source files.

The local implementation has been modified to support offline dictionary generation in the Void Linux package environment.

## License and attribution

This project combines software and dictionary data from multiple sources.

The license of each component remains governed by its respective original license and terms. This NOTICE does not replace or override those terms.

Please refer to the original projects and their license files for complete information.
