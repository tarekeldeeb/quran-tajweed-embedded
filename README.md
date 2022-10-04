# Quran Tajweed Embedded

<img src="https://i.imgur.com/uwp35yJ.png" width="500"/>


Tajweed annotations for the Qur'an (riwayat hafs). The data is available as an string file with embedded rules. Additionally, a JSON file with exact character indices for each rule, and as individual decision trees for each rule.

You can use this data to display the Qur'an with tajweed highlighting, refine models for Qur'anic speech recognition, or - if you enjoy decision trees - improve your own recitation.

The following tajweed rules are supported. Note that in case of embedded output (default), the single character is the embedding to be added within the Quran text. The JSON contains the longer text rule name.

* Ghunnah (`ghunnah`) (`g`)
* Idghaam...
  * With Ghunnah (`idghaam_ghunnah`) (`d`)
  * Without Ghunnah (`idghaam_no_ghunnah`) (`n`) 
  * Mutajaanisain (`idghaam_mutajaanisain`) (`j`)
  * Mutaqaaribain (`idghaam_mutaqaaribain`) (`b`)
  * Shafawi (`idghaam_shafawi`) (`f`)
* Ikhfa...
  * Ikhfa (`ikhfa`) (`k`)
  * Ikhfa Shafawi (`ikhfa_shafawi`) (`w`)
* Iqlab (`iqlab`) (`i`)
* Madd...
  * Regular: 2 harakat (`madd_2`) (`o`)
  * al-Aarid/al-Leen: 2, 4, 6 harakat (`madd_246`) (`m`)
  * al-Muttasil: 4, 5 harakat (`madd_muttasil`) (`t`)
  * al-Munfasil: 4, 5 harakat (`madd_munfasil`) (`f`)
  * Laazim: 6 harakat (`madd_6`) (`x`)
* Qalqalah (`qalqalah`) (`q`)
* Hamzat al-Wasl (`hamzat_wasl`) (`h`)
* Lam al-Shamsiyyah (`lam_shamsiyyah`) (`l`)
* Silent (`silent`) (`e`)

This project was built using information from [ReciteQuran.com](http://recitequran.com), the [Dar al-Maarifah](http://tajweedquran.com) tajweed masaahif, and others.

## Using the tajweed embedded file

To display the Quran text, just filter out all [a-z] characters, those are the embedded tajweed rule. Each char maps a rule in place. To highlight the tajweed rules, the embedded rules should be smartly used forward.

## Using the tajweed JSON file

All the data you probably need is in `output/tajweed.hafs.uthmani-pause-sajdah.json`. It has the following schema:

    [
        {
            "surah": 1,
            "ayah": 1,
            "annotations": [
                {
                    "rule": "madd_6",
                    "start": 245,
                    "end": 247
                },
                ...
            ]
        },
        ...
    ]

The `start` and `end` indices of each annotation refer to the Unicode codepoint (not byte!) offset within the [Tanzil.net](http://tanzil.net/download) Uthmani Qur'an text.

This data file is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/), while the original Tanzil.net text file linked above is made available under the [Tanzil.net terms of use](https://tanzil.net/download/).

## Using the decision trees

`tajweed_classifier.py` is a script that takes [Tanzil.net](http://tanzil.net/download) "Text (with aya numbers)"-style input via STDIN, and produces the tajweed JSON file (as described above) via STDOUT. It reads the decision trees from `rule_trees/*.json`. Note that the trees have been built to function best with the Madani text; they rely on the prescence of pronunciation markers (e.g. maddah) that may not be present in other texts.
