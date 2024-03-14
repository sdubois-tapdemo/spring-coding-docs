

## Create Table
```
CREATE TABLE student (
  id int NOT NULL AUTO_INCREMENT,
  first_name varchar(45) DEFAULT NULL,
  last_name varchar(45) DEFAULT NULL,
  email varchar(45) DEFAULT NULL,
  PRIMARY KEY (id)
)
```

# MySQL
## Adjust auto-increment to start at 3000

```
ALTER TABLE student_tracker.student AUTO_INCREMENT=3000    // djust auto-increment to start at 3000
TRUNCATE student_tracker.student                           // Delete all records from the table
```

