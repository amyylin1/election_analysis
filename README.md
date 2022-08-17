# Election_Analysis

## 1.  Overview of Election Audit:

The overarching goal of this analysis is to determine the winning candidate from the election and the county with the most votes.  This analysis calculates the following:
  1.	the total number of votes
  2.	the list of candidates who received votes
  3.	total number of votes each candidate received
  4.	the percentage of votes each candidate won
  5.	the winner of the election based on the popular vote
  6.	total number of votes each county received and its percentage
  7.	the winning county

    
## 2.  Election-Audit Results:

  •	There were 369,711 votes cast in the election.

  •	The number of votes per county (percentage of the total vote):
  1.	Jefferson:   38,855 votes (10.5 %).
  2.	Denver:  306,055 votes (82.8 %).
  3.	Arapahoe:  24,801 votes (6.7%).  

  •	Denver had the largest number of votes.

  •	The number of votes received per candidate (percentage of the total vote:
  1.	Charles Casper Stockham received 23.0% of the vote and 82,213 votes. 
  2.	Diana DeGette received 73.8% of the vote and 272,892 votes.
  3.	Raymon Anthony Doane received 2.1% of the vote and 11,606 votes.

  •	Diane DeGette won the election with 272,892 votes, which accounts for 73.8 % of the total votes. 

### Election Summary  

<img width="365" alt="Screen Shot 2022-08-16 at 7 06 04 PM" src="https://user-images.githubusercontent.com/108419097/185000218-095c6381-fb7f-4d64-a096-640ba6e75f94.png">


## Methods and code used for the analysis:

### Load and save files
- csv module:  pulls in data from external CSV files
- os module:  opens file from an unknown path 
- os.path.join(“folder”, “file”):  joins the “Resources” folder with the “election_results.csv” file

      # Add our dependencies.
      import csv
      import os

      # Add a variable to load a file from a path.
      file_to_load = os.path.join( "Resources", "election_results.csv")

      # Add a variable to save the file to a path.
      file_to_save = os.path.join("analysis", "election_results.txt")

        
### create list and dictionary
- list:  declare an empty list before the for loop
- dictionary: declare an empty dictionary before the for loop

        # Initialize a total vote counter.
        total_votes = 0

        # Candidate Options and candidate votes.
        candidate_options = []
        candidate_votes = {}

        # 1: Create a county list and county votes dictionary.

        county_list = []
        county_votes = {}

        # Track the winning candidate, vote count and percentage
        winning_candidate = ""
        winning_count = 0
        winning_percentage = 0

        # 2: Track the largest county and county voter turnout.

        winning_county = ""
        winning_count_county = 0
        winning_percentage_county = 0
        
        # Read the csv and convert it into a list of dictionaries
        with open(file_to_load) as election_data:
        reader = csv.reader(election_data)
 
 
### for loops, conditional statements
- for loop: iterate through each row to get the name
- if statement with the not in membership:  adds the name that was not added previously

        # Read the header
        header = next(reader)

        # For each row in the CSV file.
        for row in reader:

            # Add to the total vote count
            total_votes = total_votes + 1

            # Get the candidate name from each row.
            candidate_name = row[2]

            # 3: Extract the county name from each row.
            county_name = row[1]

            # If the candidate does not match any existing candidate add it to
            # the candidate list
            if candidate_name not in candidate_options:

                # Add the candidate name to the candidate list.
                candidate_options.append(candidate_name)

                # And begin tracking that candidate's voter count.
                candidate_votes[candidate_name] = 0

            # Add a vote to that candidate's count
            candidate_votes[candidate_name] += 1

            # 4a: Write an if statement that checks that the
            # county does not match any existing county in the county list.
            if county_name not in county_list:

                # 4b: Add the existing county to the list of counties.
                county_list.append(county_name)

                # 4c: Begin tracking the county's vote count.
                county_votes[county_name] = 0

            # 5: Add a vote to that county's vote count.
            county_votes[county_name] += 1


## 3. Election-Audit Summary:

This script can be modified for national elections by changing the variable names.  
Original code: 

    # Create a county list and county votes dictionary
    county_list = []
    county_votes = {}
    
Modified code:

    Create a state list and state votes dictionary
    state_list = []
    state_votes = {}

This script can be modified for getting variables with different indexes on the datasheet: 
Original code:

        # Get the candidate name from each row.
        candidate_name = row[2]

        # Extract the county name from each row.
        county_name = row[1]

Modified code:

        # Get the candidate name from each row.
        candidate_name = row[index number]

        # 3: Extract the county name from each row.
        county_name = row[index number]

Also, since all variables have unique names, one can easily scale up the candidates and county numbers.  
