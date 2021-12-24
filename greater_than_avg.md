```sql
Create Table country(
  id int Primary Key,
  country_name varchar(128)
);

Insert Into country
    (id, country_name) 
Values
    (1,"America"),
    (2,"China"),
    (3,"Britain");
    
Create Table city(
  id int Primary Key,
  city_name varchar(128),
  postal_code varchar(128),
  country_id int
);
Insert Into city
    (id, city_name, postal_code, country_id)
Values
    (1, "NY", "10027", 1),
    (2, "LD", "00000", 3),
    (3, "SH", "200086", 2);
    
Create Table customer(
  id int Primary Key,
  customer_name varchar(255),
  city_id int);

Insert Into customer
    (id, customer_name, city_id)
Values
    (1, "Alice", 1),
    (2, "Bob", 1),
    (3, "B", 2),
    (4, "xiao ming", 3),
    (5, "xiao hong", 3);
```



```sql
/*country_name, city_name, number_of_customers*/
Select country_name, city_name, count(*) cnt From
city
Left Join country on city.country_id=country.id
Left Join customer on city.id = customer.city_id
Group By city.id
Having cnt >
  (Select (count(customer.id)/count(city.id)) From city, customer)
Order By country_name ASC;

```

