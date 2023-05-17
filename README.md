# KEBI-prolog
code in prolog for the KEBI exam 2022/2023

The code is divided in 2 parts: 
 - code: the logic behind the recommender
 - data: the information needed for the recommender

# To run the code
Go to: https://swish.swi-prolog.org/
Copy the contents of the data.txt file into swish, after that insert the contents of the code.txt file.
Example queries:
p_recommender(poultry, Y). will output all values for Y, therefore returning names of wines as output
recommender(poultry, Y). will do the same, it’s just outputting the pairing instead of the perfect pairing above.
