# Alyssa Johnson's JavaScript Midterm

- **Name**: Alyssa Johnson
- **Dataset**: meta-ads

## Overview

I decided to choose the meta-ads dataset because it strongly ties into two topics that interest me: one, advertising, and two, the use of media to incite political violence. I also thought it was really interesting that the data shows which ads were about Israel, since that connects to the ongoing conflict between Israel and Palestine. I also thought the variables (the currency used to purchase the ad, the amount spent on it, the number of impressions it received, etc.) would be fun to work with. 

```js
import {utcParse,utcFormat} from "d3-time-format";
```

## Attach the data


```js
const adData = FileAttachment("./../data/midterm-options/meta-ads/meta-ads-mentioning-israel-after-2015-09-11.csv").csv({typed: true})
```
```js
//The output is an array with 172,800 objects. I can see all the variables mentioned in the readme.md file, including the ad's id, creation time, currency, impressions, URL, and the amount of money spent. 
adData 
```

## Convert Dates

Convert the dates, which are strings, into Date() objects with your own custom
D3.js parser and any formatters. Discuss any particular choices to format the
date data in any new ways.

Again, be sure to output your newly transformed data in executable codeblocks
for easier verification and reviewing.

```js
const parseDateSlash = utcParse("%d/%m/%y")
```

```js
let adDateObjectNew = adData.map(
  (ad) => 
  {ad.ad_creation_time_obj = utcParse("%d/%m/%y")
    return ad
  }
)
```
```js
// This new field is showing up in the console for each object, but instead of a data, I'm seeing f(c), which means function. I'm unsure if this is okay or if I'm doing something wrong. I posted in the help forum. For now, I'll leave this as is unless I get a response or figure this out. 
adDateObjectNew
```

## Grouping #1 - adDataByCountryInternMap (Grouping By Currency)

1. Choose the field to group the data by (I chose 'currency_original' because I wanted to see the different countries the data came from and how much of it came from each place)
2. Declare an intern map to hold the newly grouped data (adDataByCountryInternMap) in an executable codeblock
3. Use d3.group to group the data by the 'currency_original' field
4. Declare the newly grouped data (adDataByCountryInternMap) in a second executable codeblock
5. Leave a multi-line comment in the second codeblock describing the new output

```js
const adDataByCountryInternMap = d3.group(
  adData, 
  (d) => d.currency_original
)
```
```js
// The output is a Map of 54 different Arrays of objects; each array represents a different type of currency, and each object is an item from the dataset (aka each item is an ad). According to this grouping, the most common currencies used were USD (with 99,057 objects) and ILS/Israeli Sheqels (with 23,980 objects), while the least common currency used was NIO/Nicaraguan Cordoba (With just 1 object). I plan to explore this one more in my own time; it's very fascinating to see which countries were most involved. 
adDataByCountryInternMap
```

## Grouping #2 - adDataRollUpMaxSpendAndID (Grouping By Max Spend and Ad Archive ID)

1. Decide which fields to use for grouping the data (I chose the ad_url and ad_archive_id fields because I felt that they would be very helpful fields for someone working with this dataset)
2. Introduce a new Array for grouping the data (adDataRollUpMaxSpendAndID)
3. Use d3.rollup to group and reduce the data with my chosen fields
4. Input my original Array of objects (adData)
5. Reduce the data with D.length
6. Use two arrow functions to group the data by my chosen fields
7. Declare the newly grouped data (adDataRollUpMaxSpendAndID) in a second executable codeblock
8. Describe the new output in the second codeblock with a multi-line comment

```js
let adDataRollUpMaxSpendAndID = d3.rollup(
  adData,
  (D) => D.length,
  (d) => d.ad_url,
    (d) => d.ad_archive_id
)
```

```js
// The output is a Map with 172,800 objects. Each object is an item (ad) from the dataset, and each item's Facebook URL and archive ID are shown. The URL is shown first, and then each URL has an arrow function pointing to the item's respective archive ID. It's worth noting that the archive IDs are each in Maps of their own, with the only object in these Maps being the archive ID. Presumably this is because both fields got a (d) => line and therefore each got their own Map. The fields I used for grouping here were less interesting than the first group, but the rollup method felt more convenient!
adDataRollUpMaxSpendAndID
```

## Reflection

Use the following prompt to guide your reflection about your data work:
"What 2-3 insights and 2-3 questions did you glean from your initial work
with the dataset?"

Use the PR-TEMPLATE prompts to reflect on the midterm experience.

```