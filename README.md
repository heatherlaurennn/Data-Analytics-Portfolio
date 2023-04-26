#Heather's Portfolio

#[Project 1:Pokemon_Gen_1](https://github.com/heatherlaurennn/Pokemon_Gen_1)

This is a project I completed once I finished the Google Data Analytics Course on Coursera.
I recently started learning about Generation One of Pokemon and wanted to learn different things by running analysis on these first 151 Pokemon.

* Data collected from:
  * (https://pokemondb.net/pokedex/stats/height-weight)
  * (https://pokemondb.net/pokedex/stats/gen1)
  
Data pieces then collected into a Google Sheet and uploaded to BigQuery in .csv format to run different analyses.

##SQL Code Chunks Used in BigQuery 

* Pokemon_Gen_1_AVG_SPEED_BY_TYPE

  `CREATE TABLE `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_AVG_SPEED_BY_TYPE`
    AS
    SELECT Pokemon_Type_1, Pokemon_Type_2, AVG(Speed) AS Avg_Speed
    FROM `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_Correct`
    GROUP BY Pokemon_Type_1, Pokemon_Type_2
    ORDER BY Avg_speed DESC`

* Pokemon_Gen_1_AVG_Weight_BY_Evolution

  `CREATE TABLE `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_AVG_Weight_BY_Evolution`
  AS 
  SELECT Evolution_Phase, AVG(Pokemon_Weight__lbs__) AS Avg_Weight
  FROM `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_Correct` 
  GROUP BY Evolution_Phase
  ORDER BY Evolution_Phase ASC`

* Pokemon_Gen_1_BY_TYPE

  `CREATE TABLE `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_BY_TYPE`
AS
SELECT Pokemon_Type_1, Pokemon_Type_2, COUNT(*) AS Num_Pokemon,
       (COUNT(*) / (SELECT COUNT(*) FROM `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_Correct`)) * 100 AS Percent_Pokemon
FROM `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_Correct`
GROUP BY Pokemon_Type_1, Pokemon_Type_2
ORDER BY Num_Pokemon DESC, Pokemon_Type_1, Pokemon_Type_2`
  
* Pokemon_Gen_1_Water_60_Attack

  `CREATE TABLE `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_Water_60_Attack`
  AS
  SELECT p.Name
  FROM `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_Correct` p
  JOIN (
  SELECT *
  FROM `pokemon-gen-1.Pokemon_Gen_1.Pokemon_Gen_1_Correct`
  WHERE Pokemon_Type_1 = 'Water' AND Attack >= 60
  ) f
  ON p.Name = f.Name`
  
  ##Findings
  
  * I found that the fastest average speed was produced by the Rock/Flying type of Pokemon. The slowest average speed was produced by the Bug/Grass type of Pokemon.
  * I found that the highest weight average was for the third evolution in a series and of course the lowest weight average was for the first evolution in a series.
  * I found that the highest percentage of Pokemon were a Water type and the lowest percentage of Pokemon were a number of different types of Pokemon including; Dragon/Flying
    Electric/Flying, Grass, Ice/Flying, Ice/Psychic, Psychic/Fairy, Rock/Flying, Water/Fighting, and Water/Flying.
  * In the last findings I wrote a JOIN function that would pull all of the Pokemon that are Water types and have at least an Attack of 60.



