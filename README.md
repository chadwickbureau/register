This repository contains the Chadwick Baseball Bureau Register.
The Register provides an index of identities for baseball data.

Location
--------

The latest version of the data can always be found at
http://github.com/chadwickbureau/register

Updated versions are made available roughly once per week.  The repository contains a full
history of the Register from the start of 2016.

License
-------

This dataset is made available under the Open Data Commons Attribution License: 
http://opendatacommons.org/licenses/by/1.0 

Chadwick Bureau make this data available in the hopes it will be useful to the community.
All information is the best available at the time it is published, but may contain errors
and is subject to revision (in the case of some parts of the data, frequent and substantial
revision).

People
------

The index of people is in data/people.csv.  The scope of this register
includes all people whom the Bureau has confirmed to have been a player, 
manager, or umpire in a regulation professional game at any level.

* North American-based professional leagues, including those in the
National Association/Minor League Baseball and modern (post-1993) independent leagues.
* Fall and winter Leagues (Latin America and Australia) from 2005-present
* The top-level Japanese league (NPB), since 1936
* The top-level of the Korean Baseball Organization, 1982-present
* The Cuban National Series, 1997-present
* Negro Leagues including major Negro independent clubs (noting that records on Negro baseball are often sketchy, making this subset particularly likely to be revised substantially over time)

In addition, there are entries for most NCAA Division I players and many NCAA Division II
players active in the 2010s.  Coverage of this population is intended to improve over time.

The register also includes entries for some non-players, including all members of the 
National Baseball Hall of Fame, all people who have been the subjects of SABR BioProject essays, 
as well as other off-field personnel for Major League Baseball clubs.

The file contains basic name components and dates of birth and death (where known), as the minimal
amount of information useful to establish identities.  Also provided are year spans for playing, managing, 
and umpiring. These are given for professional leagues overall, and Major League Baseball specifically. 
Separate spans are reported for intercollegiate play.  Spans may be incomplete at the professional and
especially collegiate levels; they are intended to be helpful in disambiguation, especially for records
where first names are missing or there are multiple people with the same or similar names.

Cross-references are provided against several identifier systems:

* key_uuid: The primary key, providing the most stable reference to a person. Guaranteed not to be re-issued to a different person in the future.
* key_person: The first eight (hex) digits of the key_uuid. It is guaranteed that this is unique at any given time. However, should a person's record be withdrawn from the register, the same key_person may reappear referencing a different person in the future.
* key_retro: The person's Retrosheet identifier.
* key_mlbam: The person's identifier as used by MLBAM (for example, in Gameday).
* key_bbref: The person's identifier on Major League pages on baseball-reference.com.
* key_bbref_minors: The person's identifier on minor league and Negro League pages on baseball-reference.com.
* key_fangraphs: The person's identifier on fangraphs.com (Major Leaguers). As fangraphs uses BIS identifiers, this can also be used to match up people to BIS data.
* key_npb: The person’s identifier on the NPB official site, npb.or.jp.
* key_sr_nfl: The person's identifier on pro-football-reference.com
* key_sr_nba: The person's identifier on basketball-reference.com
* key_sr_nhl: The person's identifier on hockey-reference.com
* key_findagrave: The identifier of the person's memorial on findagrave.com

Names
-----

The table data/names.csv provides a list of alternate or variant names.  These may include aliases/assumed names, legal names,
birth names, or anglicizations/abbreviations of names.  This is a relatively new product and is at present known to be very
incomplete, even for people with MLB experience.



