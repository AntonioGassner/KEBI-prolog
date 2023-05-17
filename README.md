# KEBI-prolog
code in prolog for the KEBI exam 2022/2023

The code is divided in 2 parts: 
 - code: the logic behind the recommender
 - data: the information needed for the recommender

# To run the code
Go to: https://swish.swi-prolog.org/

Copy the contents of the data.txt file into swish, after that insert the contents of the code.txt file.

Queries are in the form:

recommender(A, B, C, D, E)

Where:
 - A is the Name of the wine recommended to you by the recommender. 
 
 - B is the food you want to pair the wine with
 - C is the color of the wine in question
 - D is the grape used to produce said wine
 - E is the region of provenience

The letters are in alphabetical order because this way the output is in alphabetical order, therefore the name of the wine is always in first positio for example.

A is the output of the recommender, while B,C,D,E are the inputs.

The way prolog and this program specifically work is that you can specify any number of inputs.

If you run the function:

recommender(A, B, C, D, E)

then you get all possible combinations as outputs.

If you want a wine made from barbera grapes:

recommender(A, B, C, barbera, E)

If you want to eat fish and drink an italian wine to it

recommender(A, fish, C, D, italy)

Some queries will not return any output, some queries will return more than strictly required.

This is because the output is any possible combination of data given the constraints imposed by the inputs. If the input is very generic (a french wine) then prolog will output each french wine it has with every possible food pairing it is recommended with.

This has the upside of also recommending you foods to your wine of choice, but has the downside of outputting the same wine for each possible food pairing it has.



