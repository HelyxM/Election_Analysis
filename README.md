# An Analysis of Election Data
### Election Results Data Worksheet
[election_results](Resources/election_results.csv)
### Election Analysis Python File
[PyPoll_Challenge](PyPoll_Challenge.py)


## **Overview of Election Audit**:
The purpose of this election audit analysis was to review the data collected from the election and determine the major conclusions from the results. By writing a script that would analyze the data presented in the worksheet, the most important conclusions of the election can be quickly and easily retrieved and presented in a text file from a single code file. The benefits from not having to count hundreds of thousands of individual values and calculate results based on them are numerous, the most notable being reduced labor and a reduced possibility for inaccuracy. In addition to these benefits, the code structure provided in this analysis can also be easily adapted for use in other elections of similar types.


### Election Analysis Text File of Conclusions
[election_analysis](analysis/election_analysis.txt)

## **Election-Audit Results**:
![Election_Analysis_Text_File](https://github.com/HelyxM/Election_Analysis/blob/7156fbd9997afcc3c4151b7a119c1d13f52eec5d/analysis/Election%20Analysis%20Text%20File.png)

There are several outcomes that this analysis has concluded about the congressional election in Colorado for the year in question. The major conclusions were:
1. The Total Number of Votes Cast: 369,711 votes
2. Number of Votes and Percentage of Votes Per County Involved: 
    - Jefferson: 10.5% with 38,855 votes
    - Denver: 82.8% with 306,055 votes
    - Arapahoe: 6.7% with 24,801 votes
3. The Candidates Involved and Their Respective Received Vote Totals and Percentages of the Total:
    - Charles Casper Stockham: 23.0% with 85,213 votes
    - Diana DeGette: 73.8% with 272,892 votes
    - Raymon Anthony Doane: 3.1% with 11,606 votes

        -These values were determined through use of a "for" logic loop and two "if" conditional loops nested inside of it to return the: total vote number value, county vote numbers, and candidate vote numbers as shown in the code below.


``` 
         for row in reader:
             total_votes = total_votes + 1
             candidate_name = row[2]        
             county_name = row[1]
            if candidate_name not in candidate_options:
                candidate_options.append(candidate_name)
                candidate_votes[candidate_name] = 0
            candidate_votes[candidate_name] += 1

            if county_name not in counties:            
               counties.append(county_name)
               county_votes[county_name] = 0
            county_votes[county_name] += 1
``` 

        -To determine the percentage of votes that each county contributed and each candidate received, code blocks were constructed with "for" logic loops that presented the votes per county as float objects and votes per candidate as float objects and divided them individually by the total number of votes. By multiplying them by 100 a percentage value was received as shown in the code below.

``` 
        for county_name in county_votes:
          vote_number = county_votes[county_name]
          county_vote_percentage = float(vote_number) / float (total_votes) * 100
        for candidate_name in candidate_votes:
          votes = candidate_votes.get(candidate_name)
          vote_percentage = float(votes) / float(total_votes) * 100
```

4. The County With the Largest Number of Votes: Denver
5. Winning Candidate in the Election: Diana DeGette at 73.8% of vote with 272,892 votes
        - These values were determined through "if" conditional loops inside of the for loops that determined their percentage values, which are presented above. Comparative logic statements were used that iterated through the vote numbers and vote percentages to determine the largest number in each of the two value types. Te winning candidate and largest county were then given as variables that were printed to the terminal and to a text file, as shown in the code below.

```
     if (vote_number > county_turnout):
       county_turnout = vote_number
       largest_county = county_name
     county_summary = (
       f"\n-------------------------\n"
       f"Largest County Turnout: {largest_county}\n"
       f"-------------------------\n")
     print(county_summary)
 txt_file.write(county_summary)

     if (votes > winning_count) and (vote_percentage > winning_percentage):
        winning_count = votes
        winning_candidate = candidate_name
        winning_percentage = vote_percentage
 winning_candidate_summary = (
    f"-------------------------\n"
    f"Winner: {winning_candidate}\n"
    f"Winning Vote Count: {winning_count:,}\n"
    f"Winning Percentage: {winning_percentage:.1f}%\n"
    f"-------------------------\n")
 print(winning_candidate_summary)
 txt_file.write(winning_candidate_summary)
```

## **Election-Audit Summary**:
This code file can be adapted for use in many different types of elections handled by the election commission while using a majority of the same structure and values defined already. So long as the election results are still recorded in a CSV file and the concluded categories presented in this analysis are still desired, only one change would need to be made to the code to run a different election analysis. The primary change that would need to be made for a different election analysis is the path to the CSV file for the data to be analyzed. For this path change, the given file path would need to be adjusted for where the new data is located with the current path being:

```
- file_to_load = os.path.join(dirname, "Resources", "election_results.csv")

and the new path would have to be adapted from a template of:

- file_to_load = os.path.join(dirname, "subfolder_inside_holding_folder_of_python_file", "CSV_file_to_be_analyzed.csv")
```

In addition to the data source changes, to adapt the code for use in different elections, such as a state-wide gubernatorial election, the focus on candidates and counties submitting ballots can be changed to simply focus on the candidates by removing the sections relating to counties. Alternatively to analyze the support for the different political parties, the county-related criteria can be changed to retrieve data from a column listing the candidates' party affiliations. With the existing code blocks, the returned analysis would also provide the number and percentage of votes each party received. The only needed changes for this adaptation would be to: open the python file and edit it with a program such as Visual Studio Code, select one instance of the words related to county or counties, right click the word, select "change all occurrences" and type in "party" or "parties" in the relevant cases to provide a usable analysis in the text file output.

  
