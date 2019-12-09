# MEGS - Merged German Speech
This repository contains scripts to reproduce a merged version of multiple open-source german speech datasets.
For german there is no large speech corpus for automatic speech recognition tasks, as in english with for example
librispeech.
Therefore this repository combines multiple german speech corpora into a single one.
Check licenses in the list below or on the sites of the specific datasets, if you want use the data for any special
purposes.

## Recreate
In order to recreate the same corpus as in this repository,
execute the commands in the scripts ``recreate.sh``.
The scripts does the following steps.

1. Download all corpora to ``data/download``. Only the common-voice corpus has to be downloaded manually and placed
   inside ``data/download/common_voice``.

2. Merges all corpora into a single one. Furthermore creates specific subsets for train/dev/test.

3. Checks if the created corpus is equal to the given state of the repository.
   This is done by comparing hash values against the hash values in the file ``data/state.json``.

4. If needed the corpus can be converted to wave files only.
   This will make sure every utterance is in a separate wave file with a sampling rate of 16000.

## Corpus usage
The final corpus is stored in ``data/full``.
The format of the corpus is the default format of the [audiomate library](https://github.com/ynop/audiomate).
It is described in [audiomate default format](https://audiomate.readthedocs.io/en/latest/documentation/default_format.html).

Audiomate also can be used to read the corpus:
```python
import audiomate

corpus = audiomate.Corpus.load('data/full')
utt = corpus.utterances['utt-idx']
transcript = utt.label_lists[audiomate.corpus.LL_WORD_TRANSCRIPT].join()
samples = utt.read_samples(sr=16000)
```
Checkout [https://github.com/ynop/audiomate](https://github.com/ynop/audiomate) for more information.

## Corpus Statistics

| Part       | h      | Speakers                                            |
| -----------| -------| ----------------------------------------------------|
| unfiltered | 1021   | x (not known due to the absence of info in M-Ailabs |
| train      | 474    | x (not known due to the absence of info in M-Ailabs |
| dev        | 51     | 1251                                                |
| test       | 51     | 2112                                                |

## Corpus sources

| Name          | URL                                                                                                                                                                   | License       |
| --------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------|
| Common-Voice  | [https://voice.mozilla.org/en/datasets](https://voice.mozilla.org/en/datasets)                                                                                        | CC-0          |
| TuDa          | [https://www.inf.uni-hamburg.de/en/inst/ab/lt/resources/data/acoustic-models.html](https://www.inf.uni-hamburg.de/en/inst/ab/lt/resources/data/acoustic-models.html)  | CC-BY         |
| M-AILabs      | [https://www.caito.de/2019/01/the-m-ailabs-speech-dataset/](https://www.caito.de/2019/01/the-m-ailabs-speech-dataset/)                                                | See Page      |
| VoxForge      | [http://www.voxforge.org/de](http://www.voxforge.org/de)                                                                                                              | GPL           |
| SWC           | [https://nats.gitlab.io/swc/](https://nats.gitlab.io/swc/)                                                                                                            | CC BY-SA 4.0  |

## Create a new version
The scripts ``create.sh`` contains the commands to create a new version of the corpus.

## Changelog

| Version   | Changes                    |
| ----------|----------------------------|
| v1        | Initial version            |
