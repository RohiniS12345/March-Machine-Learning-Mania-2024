# March-Machine-Learning-Mania-2024
# Dataset Description


Each season there are thousands of NCAA basketball games played between Division I college basketball teams, culminating in March Madness®, the 68-team national championship that starts in the middle of March. We have provided a large amount of historical data about college basketball games and teams, going back many years. Armed with this historical data, you can explore it and develop your own distinctive ways of predicting March Madness® game outcomes. You can even evaluate and compare different approaches by seeing which of them would have done best at predicting tournament games from the past.

If you are unfamiliar with the format and intricacies of the NCAA® tournament, we encourage reading the wikipedia pages for the men's and women's tournaments before before diving into the data.  The data description and schema may seem daunting at first, but is not as complicated as it appears.

Please note that in previous years, there were separate competitions for predicting the men's tournament games or the women's tournament games. That changed last year. Once again, you will be submitting combined prediction files that include predictions for both the men's tournament and the women's tournament. Thus the data files incorporate both men's data and women's data. The files that pertain only to men's data will start with the letter prefix M, and the files that pertain only to women's data will start with the letter prefix W. Some files span both men's and women's data, such as Cities and Conferences, and these files do not start with an M prefix or a W prefix.

As a reminder, you are encouraged to incorporate your own sources of data. We have provided extensive historical data to jump-start the modeling process, and this data is self-consistent (for instance, dates and team ID's are always treated the same way). Nevertheless, you may also be able to make productive use of external data. If you head down this path, please be forewarned that many sources have their own distinctive way of identifying the names of teams, and this can make it challenging to link up with our data. The MTeamSpellings and WTeamSpellings files, which are listed in the bottom section below, may help you map external team references into our own Team ID structure, and you may also need to understand exactly how dates work in our data.

We extend our gratitude to Kenneth Massey for providing much of the historical data.

Special Acknowledgment to Jeff Sonas of Sonas Consulting for his support in assembling the dataset for this competition.

# Code Requirements
Please note that this is a Code Competition. You will submit a notebook that produces a portfolio of bracket predictions for both the Men's and Women's tournaments.

During the submission phase of the competition, we provide a 2024_tourney_seeds.csv file that actually contains the seeds from 2023 and will score your submissions against the 2023 tournament results. After Selection Sunday, when the competition has closed, we will replace this file with the actual 2024 tournament selections and rescore your submissions against the 2024 results.

You may find details of the submission format and evaluation metric on the Evaluation page.

# File descriptions
Below we describe the format and fields of the competition data files. All of the files are complete through February 14th of the current season. As we get closer to the tournament, we will periodically provide updates to these files to incorporate data from the remaining weeks of the current season.

# Data Section 1 - The Basics
This section provides everything you need to build a simple prediction model and submit predictions.

# Team ID's and Team Names
Tournament seeds since 1984-85 season

Final scores of all regular season, conference tournament, and NCAA® tournament games since 1984-85 season
Season-level details including dates and region names

# Example submission file for stage 1
Special note about "Season" numbers: the college basketball season lasts from early November until the national championship tournament that starts in the middle of March. For instance, this year the first regular season games were played in November 2023 and the national championship games will be played in April 2024. Because a basketball season spans two calendar years like this, it can be confusing to refer to the year of the season. By convention, when we identify a particular season, we will reference the year that the season ends in, not the year that it starts in. So for instance, the current season will be identified in our data as the 2024 season, not the 2023 season or the 2023-24 season or the 2023-2024 season, though you may see any of these in everyday use outside of our data.

# Data Section 1 file: MTeams.csv and WTeams.csv

These files identify the different college teams present in the dataset (MTeams is for the men's teams and WTeams is for the women's teams). Each school is uniquely identified by a 4 digit id number. Men's team id's start with a 1 and women's team id's start with a 3, and typically there is exactly a difference of 2000 between the men's and women's team id's for a given school. For example, the men's Arizona State team id is 1113 and the women's Arizona State team id is 3113. You will not see games present for all teams in all seasons, because the games listing is only for matchups where both teams are Division-I teams. There are 362 teams currently in Men's Division-I and 360 teams currently in Women's Division-I. Each year, some teams might start being Division-I programs, and others might stop being Division-I programs. For example, this year there is one new Division-I program (Le Moyne) and two programs that have stopped being Division-I programs (Hartford and St Francis NY). So there will be some teams listed in the data only for historical seasons and not for the current season, and thus there are more than 362 men's teams and more than 360 women's teams listed.

**TeamID** - a 4 digit id number, uniquely identifying each NCAA® men's or women's team. A school's TeamID does not change from one year to the next, so for instance the Duke men's TeamID is 1181 for all seasons. To avoid possible confusion between the men's data and the women's data, all of the men's team ID's range from 1000-1999, whereas all of the women's team ID's range from 3000-3999.
**TeamName** - a compact spelling of the team's college name, 16 characters or fewer. There are no commas or double-quotes in the team names, but you will see some characters that are not letters or spaces, e.g., Texas A&M, St Mary's CA, TAM C. Christi, and Bethune-Cookman.
**FirstD1Season** - the first season in our dataset that the school was a Division-I school. For instance, FL Gulf Coast (famously) was not a Division-I school until the 2008 season, despite their two wins just five years later in the men's 2013 NCAA® tourney. Of course, many schools were Division-I far earlier than 1985, but since we don't have any data included prior to 1985, all such teams are listed with a FirstD1Season of 1985. This column is only present in the men's data, so it is not found in WTeams.csv.
**LastD1Season** - the last season in our dataset that the school was a Division-I school. For any teams that are currently Division-I, they will be listed with LastD1Season=2024. Again, this column is only present in the men's data, so it is not found in WTeams.csv.
## Data Section 1 file: MSeasons.csv and WSeasons.csv

These files identify the different seasons included in the historical data, along with certain season-level properties. There are separate files for men's data (MSeasons) and women's data (WSeasons).

**Season** - indicates the year in which the tournament was played. Remember that the current season counts as 2024.


**DayZero** - tells you the date corresponding to DayNum=0 during that season. All game dates have been aligned upon a common scale so that (each year) the Monday championship game of the men's tournament is on DayNum=154. Working backward, the men's national semifinals are always on DayNum=152, the "play-in" games are on days 134-135, men's Selection Sunday is on day 132, the final day of the regular season is also day 132, and so on. All game data includes the day number in order to make it easier to perform date calculations. If you need to know the exact date a game was played on, you can combine the game's "DayNum" with the season's "DayZero". For instance, since day zero during the 2011-2012 season was 10/31/2011, if we know that the earliest regular season games that year were played on DayNum=7, they were therefore played on 11/07/2011. Also note that the men's and women's data share the same DayZero each season, although the women's championship game is not necessarily played on DayNum=154
**RegionW, RegionX, Region Y, Region Z** - by our competitions' convention, each of the four regions in the final tournament is assigned a letter of W, X, Y, or Z. Whichever region's name comes first alphabetically, that region will be Region W. And whichever Region plays against Region W in the national semifinals, that will be Region X. For the other two regions, whichever region's name comes first alphabetically, that region will be Region Y, and the other will be Region Z. This allows us to identify the regions and brackets in a standardized way in other files, even if the region names change from year to year. For instance, during the 2012 men's tournament, the four regions were East, Midwest, South, and West. Being the first alphabetically, East becomes W. Since the East regional champion (Ohio State) played against the Midwest regional champion (Kansas) in the national semifinals, that makes Midwest be region X. For the other two (South and West), since South comes first alphabetically, that makes South Y and therefore West is Z. So for that season, the W/X/Y/Z are East,Midwest,South,West. And so for instance, Ohio State, the #2 seed in the East, is listed in the MNCAATourneySeeds file that year with a seed of W02, meaning they were the #2 seed in the W region (the East region). We will not know the final W/X/Y/Z designations until the brackets are announced on Selection Sunday, because the national semifinal pairings in the Final Four will depend upon the overall ranks of the four #1 seeds.


# Data Section 1 file: MNCAATourneySeeds.csv and WNCAATourneySeeds.csv

These files identify the seeds for all teams in each NCAA® tournament, for all seasons of historical data. Thus, there are between 64-68 rows for each year, depending on whether there were any play-in games and how many there were. In recent years the structure has settled at 68 total teams, with four "play-in" games leading to the final field of 64 teams entering Round 1 on Thursday/Friday of the first week (by definition, that is DayNum=136/137 each season). We will not know the seeds of the respective tournament teams, or even exactly which 68 teams it will be, until Selection Sunday on March 17, 2024 (DayNum=132).

**Season** - the year that the tournament was played in
**Seed** - this is a 3/4-character identifier of the seed, where the first character is either W, X, Y, or Z (identifying the region the team was in) and the next two digits (either 01, 02, ..., 15, or 16) tell you the seed within the region. For play-in teams, there is a fourth character (a or b) to further distinguish the seeds, since teams that face each other in the play-in games will have seeds with the same first three characters. The "a" and "b" are assigned based on which Team ID is lower numerically. As an example of the format of the seed, the first record in the MNCAATourneySeeds file is seed W01 from 1985, which means we are looking at the #1 seed in the W region (which we can see from the "MSeasons.csv" file was the East region).
**TeamID** - this identifies the id number of the team, as specified in the MTeams.csv or WTeams.csv file
# Data Section 1 file: MRegularSeasonCompactResults.csv and WRegularSeasonCompactResults.csv

These files identify the game-by-game results for many seasons of historical data, starting with the 1985 season for men (the first year the NCAA® had a 64-team men's tournament) and the 1998 season for women. For each season, the file includes all games played from DayNum 0 through 132. It is important to realize that the "Regular Season" games are simply defined to be all games played on DayNum=132 or earlier (DayNum=132 is Selection Sunday, and there are always a few conference tournament finals actually played early in the day on Selection Sunday itself). Thus a game played on or before Selection Sunday will show up here whether it was a pre-season tournament, a non-conference game, a regular conference game, a conference tournament game, or whatever.

**Season** - this is the year of the associated entry in MSeasons.csv or WSeasons.csv, namely the year in which the final tournament occurs. For example, during the 2016 season, there were regular season games played between November 2015 and March 2016, and all of those games will show up with a Season of 2016.
**DayNum** - this integer always ranges from 0 to 132, and tells you what day the game was played on. It represents an offset from the "DayZero" date in the "MSeasons.csv" or "WSeasons.csv" file. For example, the first game in the "MRegularSeasonCompactResults.csv" file was DayNum=20. Combined with the fact from the "MSeasons.csv" file that day zero was 10/29/1984 that year, this means the first game was played 20 days later, or 11/18/1984. There are no teams that ever played more than one game on a given date, so you can use this fact if you need a unique key (combining Season and DayNum and WTeamID). In order to accomplish this uniqueness, we had to adjust one game's date. In March 2008, the men's SEC postseason tournament had to reschedule one game (Georgia-Kentucky) to a subsequent day because of a tornado, so Georgia had to actually play two games on the same day. In order to enforce this uniqueness, we moved the game date for the Georgia-Kentucky game back to its original scheduled date.
**WTeamID** - this identifies the id number of the team that won the game, as listed in the "MTeams.csv" or "WTeams.csv" file. No matter whether the game was won by the home team or visiting team, or if it was a neutral-site game, the "WTeamID" always identifies the winning team. Please note that in this case the "W" in "WTeamID does not refer to women's data; the "W" is for "winning". Both the men's data and women's data will identify the winning team id by this WTeamID column. The same note applies to WScore and WLoc below - these are "W" for "winning" and not for "women's".
**WScore** - this identifies the number of points scored by the winning team.
**LTeamID** - this identifies the id number of the team that lost the game.
**LScore** - this identifies the number of points scored by the losing team. Thus you can be confident that WScore will be greater than LScore for all games listed.
**WLoc** - this identifies the "location" of the winning team. If the winning team was the home team, this value will be "H". If the winning team was the visiting (or "away") team, this value will be "A". If it was played on a neutral court, then this value will be "N". Sometimes it is unclear whether the site should be considered neutral, since it is near one team's home court, or even on their court during a tournament, but for this determination we have simply used the Kenneth Massey data in its current state, where the "@" sign is either listed with the winning team, the losing team, or neither team. If you would like to investigate this factor more closely, we invite you to explore Data Section 3, which provides the city that each game was played in, irrespective of whether it was considered to be a neutral site.
**NumOT** - this indicates the number of overtime periods in the game, an integer 0 or higher.
# Data Section 1 file: MNCAATourneyCompactResults.csv and WNCAATourneyCompactResults.csv

These files identify the game-by-game NCAA® tournament results for all seasons of historical data. The data is formatted exactly like the corresponding RegularSeasonCompactResults data. All men's games will show up as neutral site (so WLoc is always N) and some women's games will show up as neutral site, depending on the specifics. Note that this tournament game data also includes the play-in games for those years that had play-in games. Thus each season you will see between 63 and 67 games listed, depending on how many play-in games there were.

Because of the consistent structure of the NCAA® tournament schedule, you can generally tell what round a game was, depending on the exact DayNum. However, the men's 2021 tournament scheduling was slightly different, and the women's scheduling has varied a lot. Nevertheless, in general the men's schedule will be:

DayNum=134 or 135 (Tue/Wed) - play-in games to get the tournament field down to the final 64 teams
DayNum=136 or 137 (Thu/Fri) - Round 1, to bring the tournament field from 64 teams to 32 teams
DayNum=138 or 139 (Sat/Sun) - Round 2, to bring the tournament field from 32 teams to 16 teams
DayNum=143 or 144 (Thu/Fri) - Round 3, otherwise known as "Sweet Sixteen", to bring the tournament field from 16 teams to 8 teams
DayNum=145 or 146 (Sat/Sun) - Round 4, otherwise known as "Elite Eight" or "regional finals", to bring the tournament field from 8 teams to 4 teams
DayNum=152 (Sat) - Round 5, otherwise known as "Final Four" or "national semifinals", to bring the tournament field from 4 teams to 2 teams
DayNum=154 (Mon) - Round 6, otherwise known as "national final" or "national championship", to bring the tournament field from 2 teams to 1 champion team
**Special note:** Each year, there are also going to be other games that happened after Selection Sunday, which are not part of the NCAA® Tournament. This includes tournaments like the postseason NIT, the CBI, the CIT, and the Vegas 16. Such games are not listed in the Regular Season or the NCAA® Tourney files; they can be found in the "Secondary Tourney" data files (only for men's data) within Data Section 6. Although they would not be games you would ever be predicting directly for the NCAA® tournament, and they would not be games you would have data from at the time of predicting NCAA® tournament outcomes, you may nevertheless wish to make use of these games for model optimization, depending on your methodology. The more games that you can test your predictions against, the better your optimized model might eventually become, depending on how applicable all those games are. A similar argument might be advanced in favor of optimizing your predictions against conference tournament games, which might be viewed as reasonable proxies for NCAA® tournament games.

# Data Section 2 - Team Box Scores
This section provides game-by-game stats at a team level (free throws attempted, defensive rebounds, turnovers, etc.) for all regular season, conference tournament, and NCAA® tournament games since the 2002-03 season (men) or since the 2009-10 season (women).

Team Box Scores are provided in "Detailed Results" files rather than "Compact Results" files. However, the two files are strongly related.

In a Detailed Results file, the first eight columns (Season, DayNum, WTeamID, WScore, LTeamID, LScore, WLoc, and NumOT) are exactly the same as a Compact Results file. However, in a Detailed Results file, there are many additional columns. The column names should be self-explanatory to basketball fans (as above, "W" or "L" refers to the winning or losing team):

WFGM - field goals made (by the winning team)
WFGA - field goals attempted (by the winning team)
WFGM3 - three pointers made (by the winning team)
WFGA3 - three pointers attempted (by the winning team)
WFTM - free throws made (by the winning team)
WFTA - free throws attempted (by the winning team)
WOR - offensive rebounds (pulled by the winning team)
WDR - defensive rebounds (pulled by the winning team)
WAst - assists (by the winning team)
WTO - turnovers committed (by the winning team)
WStl - steals (accomplished by the winning team)
WBlk - blocks (accomplished by the winning team)
WPF - personal fouls committed (by the winning team)
(and then the same set of stats from the perspective of the losing team: LFGM is the number of field goals made by the losing team, and so on up to LPF).

Note: by convention, "field goals made" (either WFGM or LFGM) refers to the total number of fields goals made by a team, a combination of both two-point field goals and three-point field goals. And "three point field goals made" (either WFGM3 or LFGM3) is just the three-point fields goals made, of course. So if you want to know specifically about two-point field goals, you have to subtract one from the other (e.g., WFGM - WFGM3). And the total number of points scored is most simply expressed as 2*FGM + FGM3 + FTM.

# Data Section 2 file: MRegularSeasonDetailedResults.csv and WRegularSeasonDetailedResults.csv

These files provide team-level box scores for many regular seasons of historical data, starting with the 2003 season (men) or starting with the 2010 season (women). All games listed in the MRegularSeasonCompactResults file since the 2003 season should exactly be present in the MRegularSeasonDetailedResults file, and similarly, all games listed in the WRegularSeasonCompactResults file since the 2010 season should exactly be present in the WRegularSeasonDetailedResults file.

# Data Section 2 file: MNCAATourneyDetailedResults.csv and WNCAATourneyDetailedResults.csv

These files provide team-level box scores for many NCAA® tournaments, starting with the 2003 season (men) or starting with the 2010 season (women). Similarly, all games listed in the MNCAATourneyCompactResults or MNCAATourneyCompactResults file for those seasons should exactly be present in the corresponding MNCAATourneyDetailedResults or WNCAATourneyDetailedResults file.

# Data Section 3 - Geography
This section provides city locations of all regular season, conference tournament, and NCAA® tournament games since the 2009-10 season

# Data Section 3 file: Cities.csv

This file provides a master list of cities that have been locations for games played. Please notice that the Cities and Conferences files are the only two that don't start with an M; this is because the data files are identical between men's and women's data, so you don't need to maintain separate listings of cities or conferences across the two datasets. Also note that if you created any supplemental data in previous years on cities (latitude/longitude, altitude, city-to-city distances, etc.), the CityID's match between previous years and this year, so you should be able to re-use that information.

**CityID** - a four-digit ID number uniquely identifying a city.
**City** - the text name of the city.
**State** - the state abbreviation of the state that the city is in. In a few rare cases, the game location is not inside one of the 50 U.S. states and so other abbreviations are used. For instance Cancun, Mexico has a state abbreviation of MX.

# Data Section 3 file: MGameCities.csv and WGameCities.csv

This file identifies all games, starting with the 2010 season, along with the city that the game was played in. Games from the regular season, the NCAA® tourney, and other post-season tournaments (men's data only), are all listed together. There should be no games since the 2010 season where the CityID is not known. Games from the 2009 season and before are not listed in this file.

**Season, DayNum, WTeamID, LTeamID** - these four columns are sufficient to uniquely identify each game. Additional data, such as the score of the game and other stats, can be found in the corresponding Compact Results and/or Detailed Results file.
**CRType** - this can be either Regular or NCAA or Secondary. If it is Regular, you can find more about the game in the corresponding Regular Season Compact Results and Regular Season Detailed Results files. If it is NCAA, you can find more about the game in the corresponding NCAA Tourney Compact Results and NCAA Tourney Detailed Results files. If it is Secondary, you can find more about the game in the MSecondaryTourneyCompactResults file.
**CityID** - the ID of the city where the game was played, as specified by the CityID column in the Cities.csv file.

# Data Section 4 - Public Rankings
This section provides weekly team rankings (men's teams only) for dozens of top rating systems - Pomeroy, Sagarin, RPI, ESPN, etc., since the 2002-2003 season

# Data Section 4 file: MMasseyOrdinals.csv

This file lists out rankings (e.g. #1, #2, #3, ..., #N) of men's teams going back to the 2002-2003 season, under a large number of different ranking system methodologies. The information was gathered by Kenneth Massey and provided on his College Basketball Ranking Composite page. The format has been changed this year on this website.

Note that a rating system is more precise than a ranking system, because a rating system can provide insight about the strength gap between two adjacently-ranked teams. A ranking system will just tell you who is #1 or who is #2, but a rating system might tell you whether the gap between #1 and #2 is large or small. Nevertheless, it can be hard to compare two different rating systems that are expressed in different scales, so it can be very useful to express all the systems in terms of their ordinal ranking (1, 2, 3, ..., N) of teams.

**Season** - this is the year of the associated entry in MSeasons.csv (the year in which the final tournament occurs)
RankingDayNum - this integer always ranges from 0 to 133, and is expressed in the same terms as a game's DayNum (where DayZero is found in the MSeasons.csv file). The RankingDayNum is intended to tell you the first day that it is appropriate to use the rankings for predicting games. For example, if RankingDayNum is 110, then the rankings ought to be based upon game outcomes up through DayNum=109, and so you can use the rankings to make predictions of games on DayNum=110 or later. The final pre-tournament rankings each year have a RankingDayNum of 133, and can thus be used to make predictions of the games from the NCAA® tournament, which generally start on DayNum=134 (the Tuesday after Selection Sunday).
**SystemName** - this is the (usually) 3-letter abbreviation for each distinct ranking system. These systems may evolve from year to year, but as a general rule they retain their meaning across the years. Near the top of the Massey composite page, you can find slightly longer labels describing each system, along with links to the underlying pages where the latest rankings are provided (and sometimes the calculation is described).
**TeamID** - this is the ID of the team being ranked, as described in MTeams.csv.
**OrdinalRank** - this is the overall ranking of the team in the underlying system. Most systems from recent seasons provide a complete ranking from #1 through #351, but more recently they go higher because additional teams were added to Division I in recent years.
**Disclaimer**: you ought to be careful about your methodology when using or evaluating these ranking systems. They are presented on a weekly basis, and given a consistent date on the Massey Composite page that typically is a Sunday; that is how the ranking systems can be compared against each other on this page. However, these systems each follow their own timeline and some systems may be released on a Sunday and others on a Saturday or Monday or even Tuesday. You should remember that if a ranking is released on a Tuesday, and was calculated based on games played through Monday, it will make the system look unusually good at predicting if you use that system to forecast the very games played on Monday that already inform the rankings. To avoid this methodological trap, we have typically used a conservative RankingDayNum of Wednesday to represent the rankings that were released at approximately the end of the weekend, a few days before, even though those rankings are represented on the composite page as being on a Sunday. For some of the older years, a more precise timestamp was known for each ranking system that allowed a more precise assignment of a RankingDayNum. By convention, the final pre-tournament rankings are always expressed as RankingDayNum=133, even though sometimes the rankings for individual systems are not released until Tuesday (DayNum=134) or even Wednesday or Thursday. If you decide to use some rankings from these Massey Ordinals to inform your predictions, be forewarned that we have no control over when they are released, and not all systems may turn out to be available in time to make pre-tournament predictions by our submission deadline. In such a situation, you may wish to use the rankings from DayNum=128 or you may need to dig into the details of the actual source of the rankings, by following the respective links on the Massey Composite Page. We may also be able to provide partial releases of the final pre-tournament Massey Ordinals on the forums, so that as systems come in on Monday or Tuesday you can use them right away.

# Data Section 5 - Supplements
This section contains additional supporting information, including coaches, conference affiliations, alternative team name spellings, bracket structure, and game results for NIT and other postseason tournaments.

# Data Section 5 file: MTeamCoaches.csv

This file indicates the head coach for each team in each season, including a start/finish range of DayNum's to indicate a mid-season coaching change. For scenarios where a team had the same head coach the entire season, they will be listed with a DayNum range of 0 to 154 for that season. For head coaches whose term lasted many seasons, there will be many rows listed, most of which have a DayNum range of 0 to 154 for the corresponding season.

**Season** - this is the year of the associated entry in MSeasons.csv (the calendar year in which the final tournament occurs)
**TeamID** - this is the TeamID of the team that was coached, as described in MTeams.csv.
**FirstDayNum, LastDayNum** - this defines a continuous range of days within the season, during which the indicated coach was the head coach of the team. In most cases, a data row will either have FirstDayNum=0 (meaning they started the year as head coach) and/or LastDayNum=154 (meaning they ended the year as head coach), but in some cases there were multiple new coaches during a team's season, or a head coach who went on leave and then returned (in which case there would be multiple records in that season for that coach, indicating the continuous ranges of days when they were the head coach).
**CoachName** - this is a text representation of the coach's full name, in the format first_last, with underscores substituted in for spaces.

# Data Section 5 file: Conferences.csv

This file indicates the Division I conferences that have existed over the years since 1985. Each conference is listed with an abbreviation and a longer name. There has been no attempt to link up conferences who merged with other conferences, or whose names changed over time. Thus you will see, for instance, a "Pacific-10" conference up through the 2011 season, and then a "Pacific-12" conference starting in the 2012 season, and these look like different conferences in the data, even though it was still mostly the same teams. Please notice that the Cities and Conferences files are the only two that don't start with an M; this is because the data files are identical between men's and women's data, so you don't need to maintain separate listings of cities or conferences across the two datasets. However, the Team Conferences data differs slightly between men's and women's, so those files do have the prefixes. That's because there's two programs (VMI and The Citadel) that only have men's teams and not women's teams.

**ConfAbbrev** - this is a short abbreviation for each conference; the abbreviation is used in some other files to indicate the parent conference of a team or of a conference tournament.
**Description** - this is a longer text name for the conference.

# Data Section 5 files: MTeamConferences.csv and WTeamConferences.csv

These files indicate the conference affiliations for each team during each season. Some conferences have changed their names from year to year, and/or changed which teams are part of the conference. These files tracks this information historically, for men's and women's teams separately.

**Season** - this is the year of the associated entry in MSeasons.csv or WSeasons.csv (the year in which the final tournament occurs)
**TeamID** - this identifies the TeamID (as described in MTeams.csv or WTeams.csv).
**ConfAbbrev** - this identifies the conference (as described in Conferences.csv).

# Data Section 5 file: MConferenceTourneyGames.csv

This file indicates which games were part of each year's post-season men's conference tournaments (all of which finished on Selection Sunday or earlier), starting from the 2001 season. Many of these conference tournament games are held on neutral sites, and many of the games are played by tournament-caliber teams just a few days before the NCAA® tournament. Thus these games could be considered as very similar to NCAA® tournament games, and (depending on your methodology) may be of use in optimizing your predictions. However, this is NOT a new listing of games; these games are already present within the MRegularSeasonCompactResults and MRegularSeasonDetailedResults files. So this file simply helps you to identify which of the "regular season" games since the 2001 season were actually conference tournament games, in case that is useful information.

**ConfAbbrev** - this identifies the conference (as described in Conferences.csv) that the tournament was for.
Season, DayNum, WTeamID, LTeamID - these four columns are sufficient to uniquely identify each game. Further details about the game, such as the final score and other stats, can be found in the associated data row of the MRegularSeasonCompactResults and/or MRegularSeasonDetailedResults files.

# Data Section 5 file: MSecondaryTourneyTeams.csv

This file identifies the teams that participated in post-season men's tournaments other than the NCAA® Tournament (such events would run in parallel with the NCAA® Tournament). These are teams that were not invited to the NCAA® Tournament and instead were invited to some other tournament, of which the NIT is the most prominent tournament, but there have also been the CBI, CIT, Vegas 16 (V16), and The Basketball Classic (TBC) at various points in recent years. Depending on your methodology, you might find it useful to have these additional game results, above and beyond what is available from the NCAA® Tournament results. Many of these teams, especially in the NIT, were "bubble" teams of comparable strength to several NCAA® Tournament invitees, and so these games may be of use in model optimization for predicting NCAA® Tournament results. Also note that this information could be determined just from inspecting the MSecondaryTourneyCompactResults file, but is presented in this file as well, for your convenience.

**Season** - this is the year of the associated entry in MSeasons.csv (the year in which the post-season tournament was played)
SecondaryTourney - this is the abbreviation of the tournament, either NIT, CBI, CIT, V16 (which stands for Vegas 16), or TBC (which stands for The Basketball Classic).
**TeamID** - this identifies the TeamID that participated in the tournament (as described in MTeams.csv).

# Data Section 5 file: MSecondaryTourneyCompactResults.csv

This file indicates the final scores for the tournament games of "secondary" post-season tournaments: the NIT, CBI, CIT, and Vegas 16. The detailed results (team box scores) have not been assembled for these games. For the most part, this file is exactly like other Compact Results listings, although it also has a column for Secondary Tourney. Also note that because these games are played after DayNum=132, they are NOT listed in the MRegularSeasonCompactResults file.

**SecondaryTourney** - this is the abbreviation of the tournament, either NIT, CBI, CIT, V16 (which stands for Vegas 16), or TBC (which stands for The Basketball Classic).

# Data Section 5 files: MTeamSpellings.csv and WTeamSpellings.csv

These files indicate alternative spellings of many team names. They are intended for use in associating external spellings against our own TeamID numbers, thereby helping to relate the external data properly with our datasets. Over the years we have identified various external spellings of different team names (as an example, for Ball State we have seen "ball st", and "ball st.", and "ball state", and "ball-st", and "ball-state"). Other teams have had more significant changes to their names over the years; for example, "Texas Pan-American" and "Texas-Rio Grande Valley" are actually the same school. The current list is obviously not exhaustive, and we encourage participants to identify additional mappings and upload extended versions of this file to the forums.

**TeamNameSpelling** - this is the spelling of the team name. It is always expressed in all lowercase letters - e.g. "ball state" rather than "Ball State" - in order to emphasize that any comparisons should be case-insensitive when matching.
**TeamID** - this identifies the TeamID for the team that has the alternative spelling (as described in MTeams.csv or WTeams.csv).

# Data Section 5 files: MNCAATourneySlots and WNCAATourneySlots

These files identify the mechanism by which teams are paired against each other, depending upon their seeds, as the tournament proceeds through its rounds. They can be of use in identifying, for a given historical game, what round it occurred in, and what the seeds/slots were for the two teams (the meaning of "slots" is described below). Because of the existence of play-in games for particular seed numbers, the pairings have small differences from year to year. You may need to know these specifics if you are trying to represent/simulate the exact workings of the tournament bracket.

**Season** - this is the year of the associated entry in MSeasons.csv or WSeasons.csv (the year in which the final tournament occurs). Please note that in recent years, the women's tournament has expanded from 64 to 68 teams, which means this Tourney Slots information is no longer the same every year. Previously there was an WNCAATourneySlots file without a Season column, but starting this year we have switched over to making the WNCAATourneySlots file match the format of the men's file, so now it will have a Season column and there is a complete set of Tourney Slots data in the file for each season listed. The 2022 women's tournament was the first one with play-in games, and we expect they may be distributed differently this season, and so there is a need for season-specific Tourney Slots data rather than just one global set that could always be used for the 64-team brackets.
**Slot** - this uniquely identifies one of the tournament games. For play-in games, it is a three-character string identifying the seed fulfilled by the winning team, such as W16 or Z13. For regular tournament games, it is a four-character string, where the first two characters tell you which round the game is (R1, R2, R3, R4, R5, or R6) and the second two characters tell you the expected seed of the favored team. Thus the first row is R1W1, identifying the Round 1 game played in the W bracket, where the favored team is the 1 seed. As a further example, the R2W1 slot indicates the Round 2 game that would have the 1 seed from the W bracket, assuming that all favored teams have won up to that point. Even if that R2W1 slot were actually a game between the W09 and W16 teams, it is still considered to be the R2W1 slot. The slot names are different for the final two rounds, where R5WX identifies the national semifinal game between the winners of regions W and X, and R5YZ identifies the national semifinal game between the winners of regions Y and Z, and R6CH identifies the championship game. The "slot" value is used in other columns in order to represent the advancement and pairings of winners of previous games.
**StrongSeed** - this indicates the expected stronger-seeded team that plays in this game. For Round 1 games, a team seed is identified in this column (as listed in the "Seed" column in the MNCAATourneySeeds.csv or WNCAATourneySeeds.csv file), whereas for subsequent games, a slot is identified in this column. In the first record of the men's file (slot R1W1), we see that seed W01 is the "StrongSeed", which during the 1985 tournament would have been Georgetown. Whereas for games from Round 2 or later, rather than a team seed, we will see a "slot" referenced in this column. So in the 33rd record of this file (slot R2W1), it tells us that the winners of slots R1W1 and R1W8 will face each other in Round 2. Of course, in the last few games of the tournament - the national semifinals and finals - it's not really meaningful to talk about a "strong seed" or "weak seed", since you would have #1 seeds favored to face each other, but those games are nevertheless represented in the same format for the sake of consistency.
**WeakSeed** - this indicates the expected weaker-seeded team that plays in this game, assuming all favored teams have won so far. For Round 1 games, a team seed is identified in this column (as listed in the "Seed" column in the MNCAATourneySeeds.csv or WNCAATourneySeeds.csv file), whereas for subsequent games, a slot is identified in this column.

# Data Section 5 file: MNCAATourneySeedRoundSlots.csv

This file helps to represent the men's bracket structure in any given year. No matter where the play-in seeds are located, we can always know, for a given tournament seed, exactly what bracket slot they would be playing in, on each possible game round, and what the possible DayNum values would be for that round. Thus, if we know when a historical game was played, and what the team's seed was, we can identify the slot for that game. This can be useful in representing or simulating the tournament bracket structure. The women's scheduling has varied a lot more and does not lend itself to this common structure and so there is not a corresponding file for the women's data. Also note that the 2021 men's tournament had unusual scheduling and did not follow the traditional assignment of DayNums for each round.

**Seed** - this is the tournament seed of the team.
**GameRound** - this is the round during the tournament that the game would occur in, where Round 0 (zero) is for the play-in games, Rounds 1/2 are for the first weekend, Rounds 3/4 are for the second weekend, and Rounds 5/6 are the national semifinals and finals.
**GameSlot** - this is the game slot that the team would be playing in, during the given GameRound. The naming convention for slots is described above, in the definition of the MNCAATourneySlots file.
**EarlyDayNum, LateDayNum** - these fields describe the earliest possible, and latest possible, DayNums that the game might be played on.
