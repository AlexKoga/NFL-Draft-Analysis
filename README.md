# NFL-Draft-Analysis

This came about from me looking at NFL draft data on the leadup to the 2024 NFL Draft. During the leadup coverage of the draft season I heard an analyst talk about how General Managers
place different amounts of weight on picks in different rounds which got me curious. The analyst said something to the effect of first round picks being 5 times as valuable as 
fourth round and later picks and second round picks being 3 times as valuable as fourth round and later picks. This statement made me want to investigate if the data backs up this style of thinking.
To approach this question I first had to find the data that could help. I ultimately found a page on Pro Football Reference that had each player sorted by what draft pick they were 
with a variety stats included. One of these stats was wAV or weighted approximate value. Created by PFR founder Doug Drinen, the Approximate Value (AV) method is an attempt to put a single number 
on the seasonal value of a player at any position from any year (since 1960). The stat obviously has its limitations as it is very difficult to quantify the impact of different positions
on the outcome of individual plays and games as a whole. With that being said I believed it was a sufficient enough stat for me to use as a general sense of the productivity of a players career.
The page I got my data from used weighted approximate value which is built on the AV framework. For each player, the following weighted sum of seasonal AV scores is calculated: 
100% of the player's best season, plus 95% of his 2nd-best season, plus 90% of his 3rd-best season, plus 85% of his 4th-best season, and so on...
I then downloaded the results from every draft class between 2010 and 2019 and combined them into one large data set. I could then manipulate this data set to investigate the results of a 
decades worth of drafts and at least 5 years worth of career perfromance. To counter the length of careers of different players varying I devided this wAV career value by the amount of seasons 
that had taken place since the player was drafted. Ex) A player drafted in 2010 had 14 seasons while a player in 2015 would only have 9 seasons. This does create some biases towards
younger players in the data set since almost all of the players from the 2010 draft never reached 14 seasons of playing and yet that is their normalizing value. 
This was done mainly because I did not want to go through every single players career and find out how many actual seasons they played in the NFL as there were 2,544 players drafted in the 2010's.

After importing the data set I first looked at each teams success at drafting throughout the decade. This chart shows a lot about how certain teams think about the draft. 
For example, the Seattle Seahawks have the second highest total but a rather low ranking amongst first round picks. This shows how good the Seahawks are at finding 
talent in later rounds in the draft compared to other teams. Contrasting the Seahawks with the New York Jets we see how poor the Jets are at finding value in the 3rd round or later.

![image](https://github.com/user-attachments/assets/484809f5-28d3-49db-a9a7-08bf1dda3021)
`ggplot(Full %>% arrange(Round), aes(fill = Round, y = wAV/Yr, x = Team)) + geom_bar(position = "stack", stat = "identity") + theme_classic() + ggtitle("Success By Team Per Round")`

Following this I took a year based approach and began looking at draft classes individually. Through this some patterns began to imerage in terms of diminishing values in later rounds of the draft.

![2010 Draft](https://github.com/user-attachments/assets/100a9a62-9302-4530-82fd-b86e77707d27)
![2011 Draft](https://github.com/user-attachments/assets/ba2f532e-75b1-44aa-a166-e6e017bf77da)
![2012 Draft](https://github.com/user-attachments/assets/5fe53a55-1499-41cd-8c64-09ad7e54c1b9)
![2013 Draft](https://github.com/user-attachments/assets/2c7b2700-cf23-493a-9087-952e25e894a3)
![2014 Draft](https://github.com/user-attachments/assets/7f4d9317-5a67-434f-8e44-8cb6b8222059)
![2015 Draft](https://github.com/user-attachments/assets/feb517f3-9f45-4367-bf29-a05b73dc6db9)
![2016 Draft](https://github.com/user-attachments/assets/30658ab1-7db9-46c9-8511-0c624e7191cf)
![2017 Draft](https://github.com/user-attachments/assets/d3871e18-0fc8-4bfa-8931-674ecbe18716)
![2018 Draft](https://github.com/user-attachments/assets/1cddffbd-1b73-4de9-ad0a-86f35c6b34fb)
![2019 Draft](https://github.com/user-attachments/assets/293ec6a6-a438-4f6b-a85c-2b3f22bd0652)
`ggplot(Full %>% filter(Year == '2019'),aes(x = Pick, y = wAV Career)) + geom_point() + ggtitle("2019 Draft") + geom_vline(xintercept = 33, linetype = "dotted", color = "red", linewidth = 1) + geom_vline(xintercept = 65, linetype = "dotted", color = "red", linewidth = 1) + geom_vline(xintercept = 97, linetype = "dotted", color = "red", linewidth = 1) + geom_vline(xintercept = 129, linetype = "dotted", color = "red", linewidth = 1) + geom_vline(xintercept = 161, linetype = "dotted", color = "red", linewidth
                                                                                                                                                                                                                                                                                                                                                                                                                                                                 = 1) + geom_vline(xintercept = 193, linetype = "dotted", color = "red", linewidth = 1) + geom_vline(xintercept = 224, linetype = "dotted", color = "red", linewidth = 1)`

The red dotted lines on these graphs are the deviding lines between rounds within each draft. The dependent variable on these graphs is not standardized because all players in the graph had equal career length opportunities.
Some key takeaways I found with these graphs is that the general trends seem to be consistent throughout the years.
The first round tends to be very valuable with a lot of high wAV players and then there is an exponentially decreasing curve for the following picks and rounds.
Each draft class tends to have between 2 and 10 diamonds in the rough where players drafted after the 4th round have incredibly productive seasons.
In terms of how GM's value picks in different round, I think the value is derived from the density of quality players in the first round relative to later rounds.
What I mean by this is that while there are incredibly valuable players to be found in the third or fourth rounds, in general, most of the players drafted do not work out whereas
in the first round, at least 25 of the 32 picks are going to have starter level career quality.

These general trends are summarized in these following bar charts:

![image](https://github.com/user-attachments/assets/3e83afca-a8dc-4d34-95d8-59f6cee81e19)
`ggplot(Full %>% arrange(Round), aes(x = Round, y = wAV/Yr)) + geom_col() + ggtitle("Success of Draft Picks by Round Drafted")`

![image](https://github.com/user-attachments/assets/98bf174b-05a4-4a5b-a832-c29be816c0b5)
`ggplot(Full %>% arrange(Pick), aes(x = Pick, y = wAV/Yr)) + geom_col() + ggtitle("Success of Draft Picks by Pick Selected")`

With these graphs I think I have enough data to answer my initial question. In general the thinking of diminishing returns to later round draft picks is correct. 
Me personally, I would probably value first round picks that arent the top 3 picks as 3-4 times more valuable than fourth round or later picks and second round picks as 2 times more valuable.
Top 3 picks, specifically the first overall pick, are pretty invaluable given my research as they often produced franchise level players for teams.

Additionally, positional value is something that certainly needs to be taken into account. To show this I made a bar chart of the value from draft picks in the second round or later sorted by position.

![image](https://github.com/user-attachments/assets/217e0744-8e62-4f14-9262-1cf46c62b9da)
`ggplot(Full %>% filter(Round > 1), aes(x = Position, y = wAV/Yr)) + geom_col() + ggtitle("Success By Position in Rounds 2 or Later")`

This graph is not perfect due to how the original dataset classified different players position but the general trends are still valuable. 
The main piece of evidence here is that it is very difficult to find value at the QB position outside of the first round. Intuitively, this makes sense to football fans as most later round QB's are often just career backups.
Another position that is difficult to find true talent outside of the first round is CB and edge rushers. While there is still some success for these positions they typically aren't franchise level guys outside of the first round.

I then investigated the bad side of draft classes. To do this I looked at a concpet I made up known as "duds". Duds are drafted players who had no impact in the NFL at all. 
This is not neccessarily an inditement on any players specifically but more a measure of the success of NFL scouting departments and GM's as a whole. 
A draft with a high amount of duds indicates a poor performance on the teams more so than the players in the draft.

![image](https://github.com/user-attachments/assets/63a32fc5-e53d-4d89-b5ed-19eca6a593f7)
`ggplot(Bad, aes(x=Round, y=count)) + geom_col() + ggtitle("# of Duds per Round for 2010s") + labs(x = "Round", y = "Duds")`
![image](https://github.com/user-attachments/assets/a1ec08da-2fcf-4f63-9581-01051935bb46)
`ggplot(Bad %>% group_by(Year) %>% summarise(across(count, sum)), aes(x = Year, y = count)) + geom_point() + ggtitle("Number of Duds by Year") + labs(x = "Year", y = "Duds")`
![image](https://github.com/user-attachments/assets/841786a1-c438-4f0e-8408-2f70fd1f0051)
`ggplot(Bad, aes(x=Round, y=count, fill = Year)) + geom_bar(position = "dodge", stat = "identity") + ggtitle("# of Duds by Round for Each Year") + labs(x = "Round", y = "Duds")`

As the charts show the amount of duds grows greatly the later the round. No 1st round draft pick has ever been classified as a dud but I assume that's in part due to the fact that
if a team spends a first round pick on a player then they will give them plenty of chances to play moreso than guys drafted later in the draft. On the year by year graph, 2016 and 2018
standout as big outliers with their lacking of duds. I'm not sure why this would happen because I doubt much changed from year to year. What these graphs show quite well is how
difficult it is to find good talent in the 6th and 7th round of the draft. As a result of this it is no suprise that GM's really dont value picks in these rounds at all.
Obviously though there are always exceptions such Tom Brady and Brock Purdy, but for the most part guys do not have much expectation on their production.

This was a project that I begun just for fun in my spare time and I ended up going down a rabbit hole with it. I definitely learned a lot about the proper expectations of 
players production following what position they are drafted. Overall it was a fun little project that gave me more ammo to argue with others about the draft.
