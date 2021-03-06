# Profiling and Analyzing the Yelp Dataset (Coursera Worksheet)

### Part 1: Yelp Dataset Profiling and Understanding
<br>
<br>
1. Profile the data, counting the records for each table:
<br>
<br>
SQL Code - Count records using the primary or foreign key.

	SELECT COUNT(key)
	FROM table

Results:  
	
	i. Attribute table = 10,000
	ii. Business table = 10,000
	iii. Category table = 10,000
	iv. Checkin table = 10,000
	v. elite_years table = 10,000
	vi. friend table = 10,000
	vii. hours table = 10,000
	viii. photo table = 10,000
	ix. review table = 10,000
	x. tip table = 10,000
	xi. user table = 10,000
<br>
<br>
2. Find the number of distinct records in each table:

SQL Code - Count distinct using the primary or foreign key.

    SELECT COUNT(DISTINCT(key))
    FROM table

Results:

	i. Business = 10,000
	ii. Hours = 1562
	iii. Category = 2643
	iv. Attribute = 1115
	v. Review = review: 10,000 | business_id: 8090 | user_id: 9581
	vi. Checkin = 493
	vii. Photo = id: 10,000 | business_id: 6493
	viii. Tip = user_id: 537 | business_id: 3979
	ix. User = 10,000
	x. Friend = 11
	xi. Elite_years = 2780
<br>
<br>
3. Search for NULL values in the users table.

SQL Code:
    
    SELECT COUNT(*)
    FROM user
    WHERE id IS NULL
    OR name IS NULL
    OR review_count IS NULL
    OR yelping_since IS NULL
    OR useful IS NULL
    OR funny IS NULL
    OR cool IS NULL
    OR fans IS NULL
    OR average_stars IS NULL
    OR compliment_hot IS NULL
    OR compliment_more IS NULL
    OR compliment_profile IS NULL
    OR compliment_cute IS NULL
    OR compliment_list IS NULL
    OR compliment_note IS NULL
    OR compliment_plain IS NULL
    OR compliment_cool IS NULL
    OR compliment_funny IS NULL
    OR compliment_writer IS NULL
    OR compliment_photos IS NULL;
    
Results:

    +----------+
    | COUNT(*) |
    +----------+
    |        0 |
    +----------+
<br>	
<br>	
4. Display the minimum, maximum, and mean for the following fields:

SQL Code - Use SQL functions to easily find results.

    SELECT MIN(column), MAX(column), AVG(column)
    FROM Table

Results:

	i. Table: Review, Column: Stars
	
		+------------+------------+------------+
    	| MIN(stars) | MAX(stars) | AVG(stars) |
    	+------------+------------+------------+
    	|          1 |          5 |     3.7082 |
    	+------------+------------+------------+
		
	ii. Table: Business, Column: Stars
	
		+------------+------------+------------+
    	| MIN(stars) | MAX(stars) | AVG(stars) |
    	+------------+------------+------------+
    	|        1.0 |        5.0 |     3.6549 |
   	 +------------+------------+------------+
		
	iii. Table: Tip, Column: Likes
	
		+------------+------------+------------+
   	 | MIN(likes) | MAX(likes) | AVG(likes) |
    	+------------+------------+------------+
    	|          0 |          2 |     0.0144 |
    	+------------+------------+------------+
		
	iv. Table: Checkin, Column: Count
	
		+------------+------------+------------+
    	| MIN(count) | MAX(count) | AVG(count) |
    	+------------+------------+------------+
    	|          1 |         53 |     1.9414 |
    	+------------+------------+------------+
		
	v. Table: User, Column: Review_count
	
		+-------------------+-------------------+-------------------+
    	| MIN(review_count) | MAX(review_count) | AVG(review_count) |
    	+-------------------+-------------------+-------------------+
    	|                 0 |              2000 |           24.2995 |
    	+-------------------+-------------------+-------------------+
<br>
<br>
5. Rank cities by number of reviews:

SQL code - List cities, add the reviews for each city by grouping by city.
    
	SELECT City, SUM(review_count) AS CityReviews
	FROM business
	GROUP BY city
	ORDER BY CityReviews DESC
	
Results:	
	
    +-----------------+-------------+
    | city            | CityReviews |
    +-----------------+-------------+
    | Las Vegas       |       82854 |
    | Phoenix         |       34503 |
    | Toronto         |       24113 |
    | Scottsdale      |       20614 |
    | Charlotte       |       12523 |
    | Henderson       |       10871 |
    | Tempe           |       10504 |
    | Pittsburgh      |        9798 |
    | Montr??al        |        9448 |
    | Chandler        |        8112 |
    | Mesa            |        6875 |
    | Gilbert         |        6380 |
    | Cleveland       |        5593 |
    | Madison         |        5265 |
    | Glendale        |        4406 |
    | Mississauga     |        3814 |
    | Edinburgh       |        2792 |
    | Peoria          |        2624 |
    | North Las Vegas |        2438 |
    | Markham         |        2352 |
    | Champaign       |        2029 |
    | Stuttgart       |        1849 |
    | Surprise        |        1520 |
    | Lakewood        |        1465 |
    | Goodyear        |        1155 |
    +-----------------+-------------+
    (Output limit exceeded, 25 of 362 total rows shown)
<br>	
<br>
6. Find how stars are distributed to businesses in these cities:

SQL code - By grouping by stars, then the number of businesses with each rating can be counted in the specified city.

    SELECT stars,
    COUNT(*) AS count
    FROM business
    WHERE city = 'cityname'
    GROUP BY stars
    
i. Avon

Results:

    +-------+----------+
    | stars |  count   |
    +-------+----------+
    |   1.5 |        1 |
    |   2.5 |        2 |
    |   3.5 |        3 |
    |   4.0 |        2 |
    |   4.5 |        1 |
    |   5.0 |        1 |
    +-------+----------+

ii. Beachwood

Results:
	
    +-------+-------+
    | stars | count |
    +-------+-------+
    |   2.0 |     1 |
    |   2.5 |     1 |
    |   3.0 |     2 |
    |   3.5 |     2 |
    |   4.0 |     1 |
    |   4.5 |     2 |
    |   5.0 |     5 |
    +-------+-------+	


7. Find the three users with the most reviews:
	
SQL code:

    SELECT name,
    review_count
    FROM user
    ORDER BY review_count DESC
    LIMIT 3
	
Results:
	
    +--------+--------------+
    | name   | review_count |
    +--------+--------------+
    | Gerald |         2000 |
    | Sara   |         1629 |
    | Yuri   |         1339 |
    +--------+--------------+
<br>
<br>
8. Compare user reviews to their number of fans.

SQL Code - Users by review count descending    

    SELECT name,
    review_count,
    fans
    FROM user
    ORDER BY review_count DESC    

Sample result:

    +-----------+--------------+------+
    | name      | review_count | fans |
    +-----------+--------------+------+
    | Gerald    |         2000 |  253 |
    | Sara      |         1629 |   50 |
    | Yuri      |         1339 |   76 |
    | .Hon      |         1246 |  101 |
    | William   |         1215 |  126 |
    | Harald    |         1153 |  311 |
    | eric      |         1116 |   16 |
    | Roanna    |         1039 |  104 |
    | Mimi      |          968 |  497 |
    | Christine |          930 |  173 |
    +-----------+--------------+------+

SQL Code - Users by can count descending

    SELECT name,
    fans,
    review_count
    FROM user
    ORDER BY fans DESC    

Sample result:

    +-----------+------+--------------+
    | name      | fans | review_count |
    +-----------+------+--------------+
    | Amy       |  503 |          609 |
    | Mimi      |  497 |          968 |
    | Harald    |  311 |         1153 |
    | Gerald    |  253 |         2000 |
    | Christine |  173 |          930 |
    | Lisa      |  159 |          813 |
    | Cat       |  133 |          377 |
    | William   |  126 |         1215 |
    | Fran      |  124 |          862 |
    | Lissa     |  120 |          834 |
    +-----------+------+--------------+

Analysis:

    By querying users, their review count, and their number of fans, I found that the user with the highest number of reviews
    was Gerald, who had written 2000 reviews but only had 253 fans.  However, the user with the highest number of fans, Amy, 
    had only written 609 reviews.  The numbers of fans among the most prolific reviewers varies greatly.  At a glance, the two
    factors do not seem correlated.  But what do the numbers say?
    
SQL Code - Pearson Correlation Coefficient

    SELECT (SUM(a*b)*SUM(a*b))/(SUM(a*a)*SUM(b*b)) as r_square
    FROM(
        SELECT
        review_count-avg_review as a,
        fans-avg_fan as b
        FROM
            (SELECT
            review_count,
            fans,
            CASE
                WHEN review_count IS NOT NULL THEN 24.2995 
            END avg_review,
            CASE
                WHEN fans IS NOT NULL THEN 1.4896 
            END avg_fan
            FROM user))

Result:

    +----------------+
    |       r_square |
    +----------------+
    | 0.437136492915 |
    +----------------+  

    Therefore, r is 0.6611629851, which suggests some correlation, though not especially strong. 
<br>
<br>
9. Do reviews express love or hate more often?

SQL Code:

    SELECT COUNT(id) AS haters
    FROM review
    WHERE text LIKE "%hate%"
    
    SELECT COUNT(id) AS lovers
    FROM review
    WHERE text LIKE "%love%"

Results:

    +--------+
    | haters |
    +--------+
    |    232 |
    +--------+
    
    +--------+
    | lovers |
    +--------+
    |   1780 |
    +--------+

Answer:

    Love wins.  There are more reviews with the word "love" in them (1780) than the word "hate" (232).
<br>
<br>	
10. Which ten users have the most fans?

SQL code:
	
    SELECT name,
    fans,
    review_count
    FROM user
    ORDER BY fans DESC
    LIMIT 10

Result:

	+-----------+------+--------------+
    | name      | fans | review_count |
    +-----------+------+--------------+
    | Amy       |  503 |          609 |
    | Mimi      |  497 |          968 |
    | Harald    |  311 |         1153 |
    | Gerald    |  253 |         2000 |
    | Christine |  173 |          930 |
    | Lisa      |  159 |          813 |
    | Cat       |  133 |          377 |
    | William   |  126 |         1215 |
    | Fran      |  124 |          862 |
    | Lissa     |  120 |          834 |
    +-----------+------+--------------+
	
	

### Part 2: Inferences and Analysis

1. Choose a cateogy in any city and group those businesses by stars.
   Then, compare businesses with 4-5 stars to the 2-3 star businesses.
	
    i. Do the two groups have a different distribution of hours?
    
    	I chose the restaurants category in Phoenix, AZ.  Yes, the two groups had a slightly different distribution of hours; however, the distribution of hours within the two groups was far more varied.  The businesses with 4-5 stars both opened at 11:00 AM.  The top ranked restaurant closed at 6:00 PM where the other remained open until 11:00 PM.  The group with 2-3 stars had more variation, opening at 5:00 AM, 9:00 AM, and 10:00 AM and closed at midnight, 2:00 PM, and 11:00 PM respectively.  Hours of operation do not seem to correlate to stars.

ii. Do the two groups you chose to analyze have a different number of reviews?
         
    Yes, there was a major difference in number of reviews between the two groups.  The group with 4-5 stars had a total of 438 reviews.  
    Interestingly, the restaurant with the higher rating only had 7 of those 438 reviews. The group with 2-3 stars had 131 reviews.  The bottom ranked restaurant (McDonald's) only had 8 of those reviews.
    
    +-------------+----------------------------------------+---------+--------------+-------+----------------------+
    | category    | name                                   | city    | review_count | stars | hours                |
    +-------------+----------------------------------------+---------+--------------+-------+----------------------+
    | Restaurants | Charlie D's Catfish & Chicken          | Phoenix |            7 |   4.5 | Saturday|11:00-18:00 |
    | Restaurants | Bootleggers Modern American Smokehouse | Phoenix |          431 |   4.0 | Saturday|11:00-22:00 |
    | Restaurants | Five Guys                              | Phoenix |           63 |   3.5 | Saturday|10:00-22:00 |
    | Restaurants | Gallagher's                            | Phoenix |           60 |   3.0 | Saturday|9:00-2:00   |
    | Restaurants | McDonald's                             | Phoenix |            8 |   2.0 | Saturday|5:00-0:00   |
    +-------------+----------------------------------------+---------+--------------+-------+----------------------+
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.

  	No, at this point I am not able to infer anything from the location data between these two groups.  While McDonald's appears to be in a less affluent part of the city, Charlie D's Catfish & Chicken is only two miles away and seems to be in a better taken care of part of the city.  The second and fourth ranked businesses are over 20 miles north of the first and last ranked restaurants. Without neighborhood data, it would be difficult to infer that location is playing a true role in the ratings.

SQL code used for analysis:

	SELECT c.category, b.name, b.city, b.review_count, b.stars, b.address
    FROM category c JOIN business b 
    ON c.business_id = b.id
    JOIN hours h 
    ON b.id = h.business_id
    WHERE category = "Restaurants" AND city = "Phoenix"
    GROUP BY b.stars
    ORDER BY stars DESC	
    
	+-------------+----------------------------------------+---------+--------------+-------+-------------------------+
	| category    | name                                   | city    | review_count | stars | address                 |
	+-------------+----------------------------------------+---------+--------------+-------+-------------------------+
	| Restaurants | Charlie D's Catfish & Chicken          | Phoenix |            7 |   4.5 | 1153 E Jefferson St     |
	| Restaurants | Bootleggers Modern American Smokehouse | Phoenix |          431 |   4.0 | 3375 E Shea Blvd        |
	| Restaurants | Five Guys                              | Phoenix |           63 |   3.5 | 2641 N 44th St, Ste 100 |
	| Restaurants | Gallagher's                            | Phoenix |           60 |   3.0 | 751 E Union Hls Dr      |
	| Restaurants | McDonald's                             | Phoenix |            8 |   2.0 | 1850 S 7th St           |
	+-------------+----------------------------------------+---------+--------------+-------+-------------------------+
<br>
<br>
<br>
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? 
		
i. Difference 1:

	While reviews are obviously not going to be evenly distributed between businesses, there is a large difference between the average number of reviews for closed businesses versus open businesses. Averaged, closed businesses only had 129 reviews per business, where open businesses have 311.  
    
    
ii. Difference 2:
         
    Proportionally, the closed business have more reviews that were rated as useful than open businesses.  
    Only 0.2% of the open businesses's reviews were marked as useful, as opposed to 0.7% of closed businesses' reviews.   
         
SQL code used for analysis:

	SELECT COUNT(b.is_open) AS "Closed/Open", 
	AVG(b.stars) AS "Avg. Stars", 
	SUM(b.review_count) AS "Total Reviews", 
	(SUM(b.review_count))/(COUNT(b.is_open)) AS "Avg. Reviews/Biz",
	SUM(r.useful) AS "Useful Reviews"
	FROM business b JOIN review r 
	ON b.id = r.business_id
	GROUP BY b.is_open

	+-------------+---------------+---------------+------------------+----------------+
	| Closed/Open |    Avg. Stars | Total Reviews | Avg. Reviews/Biz | Useful Reviews |
	+-------------+---------------+---------------+------------------+----------------+
	|          71 | 3.54225352113 |          9217 |              129 |             69 |
	|         565 |  3.7610619469 |        175821 |              311 |            484 |
	+-------------+---------------+---------------+------------------+----------------+
	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.
	
i. Indicate the type of analysis you chose to do:
    
    I decided to analyze whether the number of fans a Yelp user has any bearing on whether a Yelp user is "Elite" and vice versa.
    
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
    
    Originally, I was simply going to try to analyze the number of fans a user has and see whether there was a correlation with the types of compliments they recieved from other users.  The data I chose were the name, yelping_since, fans, review_count, and all of the compliment columns from the user table.  From there, I decided to investigate style versus substance by comparing the number of compliments based on style elements, i.e. cool, funny, cute, or a good profile, to the number of compliments based on the user's writing.
    
    As I was doing that, I decided to include whether the user was an Elite Yelper, as Yelp has identified those members as writing high-quality reviews that are worth reading. When I joined the user and elite_years tables and ran the same query, I realized that the names had changed and only one of the original top 10 users was in the result.
    
    I decided to leave in the counts of compliments so I could see how they are distributed between both sets of users
    
iii. Output of your finished dataset:

Table 1: This is the top 10 users based on number of fans. 

	+-----------+---------------+------+---------+------+---------+------+-------+-------+--------+
	| name      | Yelping Since | fans | Reviews |  hot | profile | cute | funny |  cool | writer |
	+-----------+---------------+------+---------+------+---------+------+-------+-------+--------+
	| Amy       | 2007-07-19    |  503 |     609 | 2370 |     145 |  281 |  2950 |  2950 |    709 |
	| Mimi      | 2011-03-30    |  497 |     968 |  983 |      54 |  137 |   725 |   725 |    326 |
	| Harald    | 2012-11-27    |  311 |    1153 | 7246 |    2367 | 1176 | 12008 | 12008 |   5772 |
	| Gerald    | 2012-12-16    |  253 |    2000 |  206 |      19 |    1 |   704 |   704 |    430 |
	| Christine | 2009-07-08    |  173 |     930 |  168 |      39 |    8 |   242 |   242 |    202 |
	| Lisa      | 2009-10-05    |  159 |     813 |   85 |       6 |    4 |   104 |   104 |    127 |
	| Cat       | 2009-02-05    |  133 |     377 |  660 |      53 |   79 |   612 |   612 |    207 |
	| William   | 2015-02-19    |  126 |    1215 |  100 |      12 |    0 |   375 |   375 |     95 |
	| Fran      | 2012-04-05    |  124 |     862 | 2334 |      94 |   43 |  4285 |  4285 |    748 |
	| Lissa     | 2007-08-14    |  120 |     834 |  417 |      57 |   17 |   482 |   482 |    346 |
	+-----------+---------------+------+---------+------+---------+------+-------+-------+--------+
<br>
Table 2: This is the top 10 users based on number of fans once being an Elite Yelper becomes part of the criteria.

	+---------+---------------+------+---------+-------------+-----+---------+------+-------+------+--------+
	| name    | Yelping Since | fans | Reviews | Years Elite | hot | profile | cute | funny | cool | writer |
	+---------+---------------+------+---------+-------------+-----+---------+------+-------+------+--------+
	| Lissa   | 2007-08-14    |  120 |     834 |           9 | 417 |      57 |   17 |   482 |  482 |    346 |
	| Nieves  | 2013-07-08    |   80 |     178 |           4 | 159 |       3 |   13 |   183 |  183 |     77 |
	| Dixie   | 2011-01-19    |   41 |     503 |           6 |  32 |       2 |    4 |    67 |   67 |     34 |
	| Ed      | 2009-08-10    |   38 |     904 |           8 |  14 |       1 |    1 |    13 |   13 |      5 |
	| Dominic | 2011-02-06    |   37 |     836 |           7 |  16 |       1 |    0 |    36 |   36 |     17 |
	| Lalena  | 2014-02-20    |   25 |     224 |           3 |  12 |       0 |    1 |    26 |   26 |     13 |
	| Elaine  | 2010-04-21    |   18 |     332 |           7 |   4 |       0 |    0 |    22 |   22 |      9 |
	| Kristen | 2015-12-23    |   15 |     428 |           2 |   2 |       0 |    0 |     8 |    8 |      5 |
	| Matt    | 2006-10-11    |   14 |     476 |           6 |   4 |       0 |    1 |    16 |   16 |      4 |
	| Justin  | 2012-10-07    |   13 |     177 |           4 |   6 |       1 |    1 |    15 |   15 |      9 |
	+---------+---------------+------+---------+-------------+-----+---------+------+-------+------+--------+

Table 3: This is the top 25 uers based on number of fans, without the Elite Yelper criteria.  Notice only Lissa and Nieves from Table 2 make the list.

	+-----------+---------------+------+---------+------+---------+------+-------+-------+--------+
	| name      | Yelping Since | fans | Reviews |  hot | profile | cute | funny |  cool | writer |
	+-----------+---------------+------+---------+------+---------+------+-------+-------+--------+
	| Amy       | 2007-07-19    |  503 |     609 | 2370 |     145 |  281 |  2950 |  2950 |    709 |
	| Mimi      | 2011-03-30    |  497 |     968 |  983 |      54 |  137 |   725 |   725 |    326 |
	| Harald    | 2012-11-27    |  311 |    1153 | 7246 |    2367 | 1176 | 12008 | 12008 |   5772 |
	| Gerald    | 2012-12-16    |  253 |    2000 |  206 |      19 |    1 |   704 |   704 |    430 |
	| Christine | 2009-07-08    |  173 |     930 |  168 |      39 |    8 |   242 |   242 |    202 |
	| Lisa      | 2009-10-05    |  159 |     813 |   85 |       6 |    4 |   104 |   104 |    127 |
	| Cat       | 2009-02-05    |  133 |     377 |  660 |      53 |   79 |   612 |   612 |    207 |
	| William   | 2015-02-19    |  126 |    1215 |  100 |      12 |    0 |   375 |   375 |     95 |
	| Fran      | 2012-04-05    |  124 |     862 | 2334 |      94 |   43 |  4285 |  4285 |    748 |
	| Lissa     | 2007-08-14    |  120 |     834 |  417 |      57 |   17 |   482 |   482 |    346 |
	| Mark      | 2009-05-31    |  115 |     861 |  109 |       2 |    2 |   181 |   181 |     62 |
	| Tiffany   | 2008-10-28    |  111 |     408 |  197 |      17 |    2 |   415 |   415 |    175 |
	| bernice   | 2007-08-29    |  105 |     255 |  175 |      18 |   26 |   235 |   235 |     49 |
	| Roanna    | 2006-03-28    |  104 |    1039 |  235 |       7 |   13 |   415 |   415 |     92 |
	| Angela    | 2010-10-01    |  101 |     694 |  141 |       7 |    3 |   159 |   159 |     49 |
	| .Hon      | 2006-07-19    |  101 |    1246 |  226 |      20 |   48 |   569 |   569 |     99 |
	| Ben       | 2007-03-10    |   96 |     307 |  434 |      46 |   56 |   726 |   726 |    162 |
	| Linda     | 2005-08-07    |   89 |     584 |  574 |      34 |   92 |   796 |   796 |    227 |
	| Christina | 2012-10-08    |   85 |     842 |   24 |       2 |    1 |    62 |    62 |     35 |
	| Jessica   | 2009-01-12    |   84 |     220 |  143 |      36 |   10 |   175 |   175 |     86 |
	| Greg      | 2008-02-16    |   81 |     408 | 1004 |      72 |   80 |  1209 |  1209 |    333 |
	| Nieves    | 2013-07-08    |   80 |     178 |  159 |       3 |   13 |   183 |   183 |     77 |
	| Sui       | 2009-09-07    |   78 |     754 |   41 |       5 |    6 |    38 |    38 |     32 |
	| Yuri      | 2008-01-03    |   76 |    1339 |  109 |       6 |    3 |    91 |    91 |     41 |
	| Nicole    | 2009-04-30    |   73 |     161 |   79 |       5 |    9 |    58 |    58 |     83 |
	+-----------+---------------+------+---------+------+---------+------+-------+-------+--------+

	Clearly, Yelp and Yelp users have different standards by which they judge whether a Yelper is especially worth paying attention to!

iv. Provide the SQL code you used to create your final dataset:

Table 1:

	SELECT u.name, 
	DATE(u.yelping_since) AS "Yelping Since",
	u.fans,
	u.review_count AS "Reviews", 
	u.compliment_hot AS hot,
	u.compliment_profile AS profile,
	u.compliment_cute AS cute,
	u.compliment_funny AS funny,
	u.compliment_cool AS cool,
	u.compliment_writer AS writer
	FROM user u
	ORDER BY u.fans DESC
	LIMIT 10

Table 2:

	SELECT u.name, 
	DATE(u.yelping_since) AS "Yelping Since",
	u.fans,
	u.review_count AS "Reviews", 
	COUNT(e.year) AS "Years Elite",
	u.compliment_hot AS hot,
	u.compliment_profile AS profile,
	u.compliment_cute AS cute,
	u.compliment_funny AS funny,
	u.compliment_cool AS cool,
	u.compliment_writer AS writer
	FROM user u JOIN elite_years e
	ON u.id = e.user_id
	GROUP BY name
	ORDER BY u.fans DESC
	LIMIT 10

Table 3:

	SELECT u.name, 
	DATE(u.yelping_since) AS "Yelping Since",
	u.fans,
	u.review_count AS "Reviews", 
	u.compliment_hot AS hot,
	u.compliment_profile AS profile,
	u.compliment_cute AS cute,
	u.compliment_funny AS funny,
	u.compliment_cool AS cool,
	u.compliment_writer AS writer
	FROM user u
	ORDER BY u.fans DESC
	LIMIT 25
