# To run the code
Go to: https://swish.swi-prolog.org/ 
Copy the contents of the code.txt file and you are ready to run some queries.

Queries are in the form:

# recommender (A , B , C , D , E )
The arguments for this function are currently the following:
A is the name of the recommended wine
B is the food you want to pair the wine with
C is the color of the wine in question
D is the grape used to produce said wine
E is the region of provenience

# Examples

This query will output all wines in the knowledge base
recommender(A, B, C, D, E)

If you want a wine made from barbera grapes
recommender(A, B, C, barbera, E)

If you want to eat fish and drink an italian wine to it
recommender(A, fish, C, D, italy)

Some queries will not return any output, some queries will return more than strictly required. Let's take the following:
recommender(A, B, C, D, italy)

The output is any possible combination of data given the constraints imposed by the inputs. This does not pose a problem as long as we are filtering based on the properties of the wine, which are 1 to 1 relations. Things change when we have a N to N relation, like the one between wines and foods.

# Negation

Say we want a wine which is light\_red, just to reduce the number of outputs
recommender(A, B, light_red, D, E)

This leaves us with a chinese and a french wine. If we now want to exclude all french wines we change the query to:
recommender(A, B, light_red, D, E), \+ E = france

Adding "\verb|\+ E = france|" excludes the french wines. We could add multiple such exclusions by just separating them with a comma, as in 
recommender(A, B, light_red, D, E), \+ E = france, \+ D = carignan

and by doing this we end up with no wines, as expected.
