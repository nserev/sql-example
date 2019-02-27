```
create database Cookbook; 
use Cookbook;
create table Recipe (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(25), time INT, people INT) ENGINE=InnoDB DEFAULT CHARSET=utf8;
create table Ingredient (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(50)) ENGINE=InnoDB DEFAULT CHARSET=utf8; 
create table Measure (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(30)) ENGINE=InnoDB DEFAULT CHARSET=utf8; 

create table RecipeIngredient (recipe_id INT NOT NULL, ingredient_id INT NOT NULL, measure_id INT, amount INT, 
	CONSTRAINT fk_recipe FOREIGN KEY(recipe_id) REFERENCES Recipe(id), 
	CONSTRAINT fk_ingredient FOREIGN KEY(ingredient_id) REFERENCES Ingredient(id), 
	CONSTRAINT fk_measure FOREIGN KEY(measure_id) REFERENCES Measure(id)) 
ENGINE=InnoDB DEFAULT CHARSET=utf8; 

INSERT INTO Measure (name) VALUES('CUP'), ('TEASPOON'), ('TABLESPOON');
INSERT INTO Ingredient (name) VALUES('egg'), ('salt'), ('sugar'), ('chocolate'), ('vanilla extract'), ('flour');
INSERT INTO Recipe (name, time, people) VALUES('Cake', 3000, 2);
INSERT INTO Recipe (name, time, people) VALUES('Wafle', 100, 1);
INSERT INTO Recipe (name, time, people) VALUES('Cookies', 1500, 5);
INSERT INTO RecipeIngredient (recipe_id, ingredient_id, measure_id, amount) VALUES (4, 1, NULL, 1);
INSERT INTO RecipeIngredient (recipe_id, ingredient_id, measure_id, amount) VALUES (4, 3, 1, 2);
INSERT INTO RecipeIngredient (recipe_id, ingredient_id, measure_id, amount) VALUES (4, 6, 2, 3);
INSERT INTO RecipeIngredient (recipe_id, ingredient_id, measure_id, amount) VALUES (3, 1, NULL, 3);
INSERT INTO RecipeIngredient (recipe_id, ingredient_id, measure_id, amount) VALUES (3, 3, 1, 2);
INSERT INTO RecipeIngredient (recipe_id, ingredient_id, measure_id, amount) VALUES (3, 6, 2, 1);


SELECT r.name AS 'Recipe', r.people, r.time AS 'Time', mu.name AS 'Unit of Measure', i.name AS 'Ingredient'  FROM Recipe r  JOIN RecipeIngredient ri on r.id = ri.recipe_id  JOIN Ingredient i on i.id = ri.ingredient_id  LEFT OUTER JOIN Measure mu on mu.id = measure_id where r.name = '?';

SELECT r.name AS 'Recipe', r.people, r.time AS 'Time', mu.name AS 'Unit of Measure', i.name AS 'Ingredient'  FROM Recipe r  JOIN RecipeIngredient ri on r.id = ri.recipe_id  JOIN Ingredient i on i.id = ri.ingredient_id  LEFT OUTER JOIN Measure mu on mu.id = measure_id where r.name = 'Cookies';

select i.name as "Ingredient", sum(r.time) as 'Time' from Ingredient  i JOIN RecipeIngredient ri on i.id = ri.ingredient_id JOIN Recipe r on r.id = ri.recipe_id where i.name = '?';

select i.name as "Ingredient", sum(r.time) as 'Time' from Ingredient  i JOIN RecipeIngredient ri on i.id = ri.ingredient_id JOIN Recipe r on r.id = ri.recipe_id where i.name = 'flour';
```
