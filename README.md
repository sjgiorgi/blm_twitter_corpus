# Black Lives Matter Twitter Corpus


[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4056563.svg)](https://doi.org/10.5281/zenodo.4056563)


A data set of 41.8 million tweets from 10 million users which contain one of the following keywords: *BlackLivesMatter*, *AllLivesMatter* and *BlueLivesMatter*.

## Data

Data is available at [Zenodo](https://doi.org/10.5281/zenodo.4056563).

## Tweet Counter Per Day

Daily tweet counts are available in the `tweet_counts_per_day.csv` file. 


## Downloading Tweet Content

Due to Twitter's Terms of Service we are only able to distribute the numeric tweet id. Here we give brief instructions on how to populate the full tweet data from the list of ids. To do this we will use the Python command line tool [Twarc](https://github.com/DocNow/twarc). The following steps assume you have Twarc installed as well as a [Twitter Developer account](https://developer.twitter.com/en/apply-for-access). To install Twarc, please run

```
pip3 install twarc
```

Next, you must configure Twarc with your [Twitter API tokens](https://developer.twitter.com/en/apply-for-access). 

```
twarc configure
```

Next, download the data from Zenodo:

```
wget https://zenodo.org/record/4056563/files/blm_corpus.csv.gz
gunzip blm_corpus.csv.gz
```

This file contains the following fields: *message_id*, *user_id*, *blacklivesmatter*, *alllivesmatter*, *bluelivesmatter*. Next, we create a file containing only tweet ids (this also removes the header row):

```
cut -d, -f1 blm_corpus.csv | tail -n +2 > blm_tweet_ids.txt
``` 

### Using twarc from the command line

This command will produce a file where each line is a separate json file for each tweet ids. Note that only tweets which are publicly available at the time of your pull will be downloaded. Thus, our numbers might not match the numbers you see. 

```
twarc hydrate blm_tweet_ids.txt > blm.jsonl
```

### Using hydrate Python script

To run this script you must install the Python package tqdm:

```
pip3 install tqdm
```

Before running **hydrate.py** you must have the above file (**blm_tweet_ids.txt**) in the same directory as the Python script. Then run

```
python3 hydrate.py
```

This will produce the file **blm_tweet_ids.jsonl**.



### Other options 

Besides twarc, there are many other tools available for downloading Twitter data, such as [TwitterMySQL](https://github.com/dlatk/TwitterMySQL) and [hydrator](https://github.com/DocNow/hydrator).


## Citation

If you use this data in your work please cite the following [paper](https://arxiv.org/abs/2009.00596):

```
@misc{giorgi2020twitter,
    title={Twitter Corpus of the #BlackLivesMatter Movement And Counter Protests: 2013 to 2020},
    author={Salvatore Giorgi and Sharath Chandra Guntuku and Muhammad Rahman and McKenzie Himelein-Wachowiak and Amy Kwarteng and Brenda Curtis},
    year={2020},
    eprint={2009.00596},
    archivePrefix={arXiv},
    primaryClass={cs.SI}
}
```

## Contact

If you have any questions please contact Salvatore Giorgi at **sgiorgi[at]sas[dot]upenn[dot]edu**.

## License

Licensed under a [GNU General Public License v3 (GPLv3)](https://www.gnu.org/licenses/gpl-3.0.en.html).
