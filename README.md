# Chadwick Baseball Bureau Persons Register

The Chadwick Register is the most comprehensive [authority file](https://en.wikipedia.org/wiki/Authority_control)
for identities of people involved in baseball.

## License

This dataset is made available under the Open Data Commons Attribution License: 
http://opendatacommons.org/licenses/by/1.0/

We offer much more detailed information and daily updates of this data for our clients.

## Location

The latest version of the data can always be found at
http://github.com/chadwickbureau/register

Updated versions are made available roughly once per week.  The repository contains a full
history of the Register from the start of 2016.

All information is the best available at the time it is published, but may contain errors
and is subject to revision (in the case of some parts of the data, frequent and substantial
revision).

## File details

### People

The index of people is contained in 16 files, `data/people-0.csv` through `data/people-f.csv`.
The file contains basic name components and dates of birth and death (where known), as the minimal
amount of information useful to establish identities.  Also provided are year spans for playing, managing, 
and umpiring. These are given for professional leagues overall, and Major League Baseball specifically. 
Separate spans are reported for intercollegiate play.  Spans may be incomplete at the professional and
especially collegiate levels; they are intended to be helpful in disambiguation, especially for records
where first names are missing or there are multiple people with the same or similar names.

For more information on how to interpret these records and how they may change over time, see
the [section on technical details](#technical-details) below.


Cross-references are provided against several identifier systems:

* `key_uuid`: The primary key.  This is guaranteed not to be re-used to label a different identity.
* `key_person`: The first eight (hex) digits of the `key_uuid`. It is guaranteed that this is unique at any given time.  However,
  over time the same short key may be re-used for a different identity.
* `key_retro`: The person's Retrosheet identifier
* `key_mlbam`: The person's identifier at MLBAM
* `key_bbref`: The person's identifier on Major League pages on baseball-reference.com
* `key_bbref_minors`: The person's identifier on minor league pages on baseball-reference.com
* `key_fangraphs`: The person's identifier on fangraphs.com
* `key_npb`: The person’s identifier on the NPB official site, npb.or.jp
* `key_sr_nfl`: The person's identifier on pro-football-reference.com
* `key_sr_nba`: The person's identifier on basketball-reference.com
* `key_sr_nhl`: The person's identifier on hockey-reference.com
* `key_wikidata`: The person's identifier on wikidata.org.  **NEW IN 2024**

### Links

We also provide a subset of some of the links used to produce the person identities in this file.
These are the source links currently made available in the public version:

* `tsncards`: The number of the Sporting News contract cards on the LA84 website.
* `findagrave`: A memorial ID on findagrave.com.


### Names

The table data/names.csv provides a list of alternate or variant names.  These may include aliases/assumed names, legal names,
birth names, or anglicizations/abbreviations of names.  This is a relatively new product and is at present known to be very
incomplete, even for people with MLB experience.


## Technical details

The Register is the product of record matching and linkage among tens of millions of mentions of people in electronic and
print source data.  Each entry in the Register is, internally, a cluster of records linked together by matching on one
or more data fields in the source records.  We refer to an entry as an *identity*, to distinguish it from a "person".
In the perfect world, there would be a one-to-one relationship between identities and people.  However, it is frequently
not possible to confirm a link between two mentions of a person in different sources; this is especially true when
the details in a source record are "sparse", consisting only of a person's name (or solely their surname), possibly not
spelled correctly or consistently.

We index and link new records daily, and in this process we are often able to link together records previously contained
in separate identities.  This creates a practical problem.  On the one hand, the contents of clusters change over time, 
and clusters coalesce (and sometimes split) based on new information.  On the other hand, it is desirable for cluster
identifiers to have some kind of stability properties.

In our approach, every identity cluster has a UUID.  We follow these principles in assigning UUIDs to clusters between
releases of the data.  Let $A$ and $B$ refer to two releases of the data, with $A$ being earlier than $B$.
Then the following will be true.
* If a cluster of records is exactly the same between $A$ and $B$, the UUID will be unchanged.
* If in $B$ there's a cluster of records which is the same as a cluster in $A$ with the addition of only *new*
  source records, then the UUID will be unchanged.
* If $B$ contains a cluster which is a merger of two or more clusters in $A$, the UUID of the merged cluster will
  be the UUID of the cluster in $A$ which had the "best" identifying information.  "Best" is determined heuristically
  on a case-by-case basis, along these lines:
  - A cluster with information on activity in Major League Baseball (playing, managing, umpiring, roles as executive,
    and so on) is always considered "best".
  - A cluster with more identifying details (e.g., more complete or correct name, date or place of birth or death
    information) is preferred.
  - A cluster with records as a professional player is preferred to one that does not have them; likewise a cluster
    with records as a professional manager or umpire is preferred.
  - A cluster with more source record entries is preferred.
  - Finally, when merging very small and sparse clusters, the cluster which references the earliest dates is
    preferred.
* If in $B$ there is a cluster which is a *superset* of one in $A$ - that is to say, there are source records which
  were previously linked and are no longer, we follow similar principles as above to determine which cluster keeps
  the same UUID.  Our linkage system tends to be conservative and links records only with a relatively high
  threshold of probability; the case of splitting clusters is therefore less frequent than coalescing them.
* If a cluster in $A$ is found to have records pertaining to more than one person *and* the identifying information in
  the cluster is sparse or confuses two or more people, we generally retire the previous UUID and issue new UUIDs
  in $B$ for the new clusters.

In any release of the data, we guarantee that the first eight hex digits of the UUID are unique within the dataset;
this "short" identifier is what is most commonly referred to as the Chadwick person identifier.

The result of the conventions above is that a person who is well-documented in source information will have a stable
Chadwick identity.  It is safe to say that Babe Ruth will always be `9dcdd01c-9ede-4aa0-8dd1-1cdb7fd5a9da`, and therefore
the short identifier `9dcdd01c` will always refer to him.  However, for less well-documented people, our system
provides a principled way of evolving the data that, in most cases, follows a principle of least surprise,
maximising the stability of identifiers while dealing with the reality that source information is always
incomplete and subject to inaccuracies.

We make only a subset of the source linkages available in the public version of the Register.  Greater detail
on links to source records is available for licensing.


