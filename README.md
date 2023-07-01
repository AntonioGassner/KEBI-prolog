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

The letters used are in alphabetical order because the output gets ordered
by the names of the variables. This makes it so the output is always formatted
using the above layout. The way Prolog and this program specifically work
is that you can specify any number of inputs. 

Each argument can either be a variable(uppercase letter) or a constant (lowercase word). Prolog’s reasoner will
then try to match the variables to whatever you give it as constant.
In other words the variables are outputs, while the constants are inputs used
as a filter. We care only for one output, the wine name, but we still get the
other arguments as part of the output. To explain how this works let’s look at
some examples:

# Examples & how to test them

# Example 1
This query will output all wines in the knowledge base
recommender (A , B , C , D , E )

# Example 2 
If you want a wine made from barbera grapes
recommender (A , B , C , barbera , E )

A = nizza
B = red_meat
C = medium_red
E = france

# Example 3 
If you want to eat fish and drink an italian wine to it
recommender (A , fish , C , D , italy )

A = franciacorta
C = rich_white
D = chardonnay

# Example 4 Some queries will not return any output, some queries will returnmore than strictly required. 
Let’s take the following:
recommender (A , B , C , D , italy )

A = franciacorta
B = fish
C = rich_white
D = chardonnay

A = franciacorta
B = poultry
C = rich_white
D = chardonnay
A = franciacorta
B = lobster
C = rich_white
D = chardonnay

As we can see we have the same wine 3 times. This is because the output is
any possible combination of data given the constraints imposed by the inputs.
This does not pose a problem as long as we are filtering based on the properties
of the wine, which are 1 to 1 relations. Things change when we have a N to
N relation. The way we map a N to N relation like the one between foods and
wines is the following:
wine ( rosso_piceno ).
food ( fish ).
recommended ( rosso_piceno , fish )

the problem we encountered with representing this relation this way is that
if we query our knowledge base and don’t specify a food as an input we get
duplicate outputs. This is because Prolog outputs any possible combination of
elements which fit the input criteria. If a wine has multiple recommended food
associated then for each food that is a possible output match, and therefore we
get the same wine recommended one time for each food pairing.
This has the upside of also recommending foods which pair well with the
wine of choice, so we chose to classify this as a feature and not a bug.

# About negation
Filters allow us to exclude results when doing queries, but we found that given
the particular way Prolog works, adding this feature requires some workaround.
Prolog has a built-in predicate which provides negation as a failure to the rea-
soner. It’s syntax is the following:
legal ( X ) : - \+ illegal ( X ) .
The problem characterizing this form of negation as a proof is that it is sound as
long as it’s arguments are constants. Soundness is lost if the argument contains
variables, and in particular querying will not enumerate all true things. We
found out that passing arguments to exclude inside the function did not work
out well, since they cannot be used as variables, and therefore would break each
query where they are not specified.
# Example 5 
Say we want a wine which is light red, just to reduce the number of outputs
recommender (A , B , light_red , D , E )
A = rioja ,
B = cured_meat ,
D = carignan ,
E = china
A = rioja ,
 B = poultry ,
 D = carignan ,
 E = china
 A = carinena ,
 B = cured_meat ,
 D = carignan ,
 E = china
 A = carinena ,
 B = poultry ,
 D = carignan ,
 E = china
 A = gevrey_chambertin ,
 B = cured_meat ,
 D = pinot_noir ,
 E = france
 A = gevrey_chambertin ,
 B = poultry ,
 D = pinot_noir ,
 E = france
 A = nuits_saint_georges ,
 B = cured_meat ,
 D = pinot_noir ,
 E = france
 A = nuits_saint_georges ,
 B = poultry ,
 D = pinot_noir ,
 E = france
# Example 6
This leaves us with a chinese and a french wine. If we now want to exclude all french wines we change the query to:
1 recommender (A , B , light_red , D , E ) , \+ E = france
2
3 A = rioja ,
4 B = cured_meat ,
5 D = carignan ,
6 E = china
7 A = rioja ,
8 B = poultry ,
9 D = carignan ,
10 E = china
11 A = carinena ,
12 B = cured_meat ,
13 D = carignan ,
7
14 E = china
15 A = carinena ,
16 B = poultry ,
17 D = carignan ,
18 E = china
Example 7 Adding ”\+ E = france” excludes the french wines. We could
add multiple such exclusions by just separating them with a comma, as in
1 recommender (A , B , light_red , D , E ) , \+ E = france , \+ D = carignan
2
3 false
and by doing this we end up with no wines, as expected.
