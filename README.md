# enwiktionary-english-pronunciation-ipa-data

This repo contains a dataset of English words and their pronunciations in [IPA](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet) notation parsed from [enwiktionary](https://en.wiktionary.org/wiki/Wiktionary:Main_Page).

Pronunciations for more than 72,000 unique English words are included. Many words have pronunciations for multiple accents, from American to British to Australian.

The source database dump was from [October 20, 2022](https://dumps.wikimedia.org/enwiktionary/20221020/) and the data was prepared on October 22, 2022 using the [wiktionary-english-pronunciations-to-mongo](TODO) Python app. See that project page for more details.

The data is provided in JSON and CSV formats. Both were exported from a MongoDB collection, so you could import them to Mongo and query or manipulate the data further from there.


## Content warning

There are many obscene and profane words defined on wiktionary which have ended up in this dataset. You may want to filter words out by using a package like [profanity-check](https://pypi.org/project/profanity-check/) that can detect profanity in a given string.

I take no responsibility for the words defined on wiktionary or included in the dataset.


## Data structure

There are often multiple rows in the dataset for any one English word. This is because:

- there might be multiple wiktionary pages with the same title
- there might be multiple words spelled the same way (homonyms)
- the word might have multiple parts of speech
- the word might have multiple accents for its listed pronunciations

```js
// each row in the dataset:
{
    _id <ObjectId>,      // MongoDB document id
    pageTitle <String>,  // the original page title
    pageIndex <Int32>,   // the page's index in the dumpfile
    pageId <Int32>,      // the actual page ID 
    title <String>,      // the normalized page title (lowercase)
    ipaLine <String>,    // the line of text containing one or more IPAs
    accents <String[]>,  // [optional] one or more accents parsed from the ipaLine
    ipas <String[]>      // one or more IPAs parsed from the ipaLine
}
```


## License

None, do what you will!
