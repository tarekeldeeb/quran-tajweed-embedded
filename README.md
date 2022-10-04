### NOTE: This project is not actively maintained
Please consider using the [Quran.com API](https://quran.api-docs.io/v4/quran/get-uthmani-script-of-ayah) instead.

# quran-tajweed

<img src="https://i.imgur.com/uwp35yJ.png" width="500"/>


Tajweed annotations for the Qur'an (riwayat hafs). The data is available as a JSON file with exact character indices for each rule, and as individual decision trees for each rule.

You can use this data to display the Qur'an with tajweed highlighting, refine models for Qur'anic speech recognition, or - if you enjoy decision trees - improve your own recitation.

The following tajweed rules are supported:

* Ghunnah (`ghunnah`)
* Idghaam...
  * With Ghunnah (`idghaam_ghunnah`)
  * Without Ghunnah (`idghaam_no_ghunnah`)
  * Mutajaanisain (`idghaam_mutajaanisain`)
  * Mutaqaaribain (`idghaam_mutaqaaribain`)
  * Shafawi (`idghaam_shafawi`)
* Ikhfa...
  * Ikhfa (`ikhfa`)
  * Ikhfa Shafawi (`ikhfa_shafawi`)
* Iqlab (`iqlab`)
* Madd...
  * Regular: 2 harakat (`madd_2`)
  * al-Aarid/al-Leen: 2, 4, 6 harakat (`madd_246`)
  * al-Muttasil: 4, 5 harakat (`madd_muttasil`)
  * al-Munfasil: 4, 5 harakat (`madd_munfasil`)
  * Laazim: 6 harakat (`madd_6`)
* Qalqalah (`qalqalah`)
* Hamzat al-Wasl (`hamzat_wasl`)
* Lam al-Shamsiyyah (`lam_shamsiyyah`)
* Silent (`silent`)

This project was built using information from [ReciteQuran.com](http://recitequran.com), the [Dar al-Maarifah](http://tajweedquran.com) tajweed masaahif, and others.

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
