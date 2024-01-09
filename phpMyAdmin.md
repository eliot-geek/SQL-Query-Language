phpMyAdmin Requests

>- Selects all columns from the 'good' table
```sql
SELECT * FROM `good`;
```

>- Selects all columns from the 'good_category' table
```sql
SELECT * FROM `good_category`;
```

>- Selects all columns from the 'order' table
```sql
SELECT * FROM `order`;
```

>- Selects all columns from the 'order2good' table
```sql
SELECT * FROM `order2good`;
```

>- Selects all columns from the 'order_status' table
```sql
SELECT * FROM `order_status`;
```

>- Selects all columns from the 'order_status_change' table
```sql
SELECT * FROM `order_status_change`;
```

>- Selects all columns from the 'user' table
```sql
SELECT * FROM `user`;
```

>- Selects all columns from the 'good' table
```sql
SELECT * FROM `good`;
```

>- Selects all columns from the 'good' table and orders by the 'count' column in ascending order
```sql
SELECT * FROM `good` ORDER BY `good`.`count` ASC;
```

>- Updates the 'name' column to 'Сироп Прана «Харизма»' for the row with 'id' equal to 1009 in the 'good' table
```sql
UPDATE `good` SET `name` = 'Сироп Прана «Харизма»' WHERE `good`.`id` = 1009;
```

>- Deletes the row with 'id' equal to 844 from the 'good' table
```sql
DELETE FROM `good` WHERE `good`.`id` = 844;
```

>- Inserts a new row into the 'good' table with specific values for 'category_id', 'name', 'count', and 'price'
```sql
INSERT INTO `good` (`id`, `category_id`, `name`, `count`, `price`) VALUES (NULL, '38', 'Mokka', '678', '900');
```

>- Selects all columns from the 'good' table
```sql
SELECT * FROM `good`;
```

>- Selects all columns from the 'good' table and orders by the 'id' column in ascending order
```sql
SELECT * FROM `good` ORDER BY `good`.`id` ASC;
```

>- Selects all columns from the 'good' table and orders by the 'id' column in descending order
```sql
SELECT * FROM `good` ORDER BY `good`.`id` DESC;
```

>- Drops the 'count' column from the 'good' table
```sql
ALTER TABLE `good` DROP `count`;
```

>- Adds a new 'count' column to the 'good' table after the 'price' column
```sql
ALTER TABLE `good` ADD `count` INT NOT NULL AFTER `price`;
```

>- Selects all columns from the 'good' table
```sql
SELECT * FROM `good`;
```
