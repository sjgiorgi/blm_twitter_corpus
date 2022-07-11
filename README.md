# Black Lives Matter Twitter Corpus

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5835260.svg)](https://doi.org/10.5281/zenodo.5835260)

A data set of 63.9 million tweets from 13.0 million users from over 100 countries which contain one of the following keywords: *BlackLivesMatter*, *AllLivesMatter* and *BlueLivesMatter*.

## Data

Data is available at [Zenodo](https://doi.org/10.5281/zenodo.5835260).


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
wget https://zenodo.org/record/4897616/files/twitter.tar.gz
tar -xf twitter.tar.gz
```

This file contains separate folders for each year. Since the volume of tweets in 2020 was significantly larger than all previous years, all years except 2020 have a single file, while 2020 has separate files for each month. Each file contains the following fields: *message_id*, *blacklivesmatter*, *alllivesmatter*, *bluelivesmatter*. Next, we create a file containing only tweet ids. We extract data from June 2020 as an example:

```
cd twitter/2020
gunzip 2020-06.csv.gz
cut -d, -f1 2020-06.csv > 2020-06.txt
``` 

### Using twarc from the command line

This command will produce a file where each line is a separate json file for each tweet ids. Note that only tweets which are publicly available at the time of your pull will be downloaded. Thus, our numbers might not match the numbers you see. 

```
twarc hydrate 2020-06.txt > blm.jsonl
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

### Using Excel

Please be careful when opening these files in Excel. Excel might automatically convert the Tweet ids from an integer format to a decimal. 

## Citation

If you use this data in your work please cite the following [paper](https://arxiv.org/abs/2009.00596):

```
@misc{giorgi2022twitter,
  author       = {Salvatore Giorgi and
                  Sharath Chandra Guntuku and
                  McKenzie Himelein-Wachowiak and
                  Amy Kwarteng and
                  Sy Hwang and
                  Muhammad Rahman and
                  Brenda Curtis},
  title        = {Twitter Data of the \#BlackLivesMatter Movement And 
                   Counter Protests: 2013 to 2021},
  year         = {2022},
  journal      = {Proceedings of the International AAAI Conference on Web and Social Media}, 
}
```

## Contact

If you have any questions please contact Salvatore Giorgi at **sgiorgi[at]sas[dot]upenn[dot]edu**.

## License

Licensed under a [GNU General Public License v3 (GPLv3)](https://www.gnu.org/licenses/gpl-3.0.en.html).
