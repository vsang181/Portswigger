# SQL injection

SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries an application makes to its database

## What is SQL injection?

- [What is SQL injection (SQLi)?](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/What%20is%20SQL%20injection%3F/What%20is%20SQL%20injection%20(SQLi)%3F.md)

## How to detect SQL injection vulnerabilities

- [How to detect SQL injection vulnerabilities](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/How%20to%20detect%20SQL%20injection%20vulnerabilities/How%20to%20detect%20SQL%20injection%20vulnerabilities.md)
- [SQL injection in different parts of the query](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/How%20to%20detect%20SQL%20injection%20vulnerabilities/SQL%20injection%20in%20different%20parts%20of%20the%20query.md) 

## Retrieving hidden data

- [Retrieving hidden data](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Retrieving%20hidden%20data/Retrieving%20hidden%20data.md)
- [Retrieving hidden data - Continued](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Retrieving%20hidden%20data/Retrieving%20hidden%20data%20-%20Continued.md)
- [Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Retrieving%20hidden%20data/Lab%3A%20SQL%20injection%20vulnerability%20in%20WHERE%20clause%20allowing%20retrieval%20of%20hidden%20data.md)

## Subverting application logic

- [Subverting application logic](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Subverting%20application%20logic/Subverting%20application%20logic.md)
- [Lab: SQL injection vulnerability allowing login bypass](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Subverting%20application%20logic/Lab%3A%20SQL%20injection%20vulnerability%20allowing%20login%20bypass.md)

## SQL injection UNION attacks

- [SQL injection UNION attacks](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/SQL%20injection%20UNION%20attacks/SQL%20injection%20UNION%20attacks.md)
- [SQL injection UNION attacks - Continued](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/SQL%20injection%20UNION%20attacks/SQL%20injection%20UNION%20attacks%20-%20Continued.md)
  
## Determining the number of columns required

- [Determining the number of columns required](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Determining%20the%20number%20of%20columns%20required/Determining%20the%20number%20of%20columns%20required.md)
- [Determining the number of columns required - Continued](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Determining%20the%20number%20of%20columns%20required/Determining%20the%20number%20of%20columns%20required%20-%20Continued.md)
- [Lab: SQL injection UNION attack, determining the number of columns returned by the query](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Determining%20the%20number%20of%20columns%20required/Lab%3A%20SQL%20injection%20UNION%20attack%2C%20determining%20the%20number%20of%20columns%20returned%20by%20the%20query.md)
- [Database-specific syntax](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Determining%20the%20number%20of%20columns%20required/Database-specific%20syntax.md)

## Finding columns with a useful data type

- [Finding columns with a useful data type](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Finding%20columns%20with%20a%20useful%20data%20type/Finding%20columns%20with%20a%20useful%20data%20type.md)
- [Lab: SQL injection UNION attack, finding a column containing text](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Finding%20columns%20with%20a%20useful%20data%20type/Lab%3A%20SQL%20injection%20UNION%20attack%2C%20finding%20a%20column%20containing%20text.md)

## Using a SQL injection UNION attack to retrieve interesting data

- [Using a SQL injection UNION attack to retrieve interesting data](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Using%20a%20SQL%20injection%20UNION%20attack%20to%20retrieve%20interesting%20data/Using%20a%20SQL%20injection%20UNION%20attack%20to%20retrieve%20interesting%20data.md)
- [Lab: SQL injection UNION attack, retrieving data from other tables](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Using%20a%20SQL%20injection%20UNION%20attack%20to%20retrieve%20interesting%20data/Lab%3A%20SQL%20injection%20UNION%20attack%2C%20retrieving%20data%20from%20other%20tables.md)
  
## Retrieving multiple values within a single column

- [Retrieving multiple values within a single column](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Retrieving%20multiple%20values%20within%20a%20single%20column/Retrieving%20multiple%20values%20within%20a%20single%20column.md)
- [Lab: SQL injection UNION attack, retrieving multiple values in a single column](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Retrieving%20multiple%20values%20within%20a%20single%20column/Lab%3A%20SQL%20injection%20UNION%20attack%2C%20retrieving%20multiple%20values%20in%20a%20single%20column.md)

## Examining the database

- [Examining the database in SQL injection attacks](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Examining%20the%20database/Examining%20the%20database%20in%20SQL%20injection%20attacks.md)
- [Querying the database type and version](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Examining%20the%20database/Querying%20the%20database%20type%20and%20version.md)
- [Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Examining%20the%20database/Lab%3A%20SQL%20injection%20attack%2C%20querying%20the%20database%20type%20and%20version%20on%20MySQL%20and%20Microsoft.md)
- [Listing the contents of the database](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Examining%20the%20database/Listing%20the%20contents%20of%20the%20database.md)
- [Lab: SQL injection attack, listing the database contents on non-Oracle databases](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Examining%20the%20database/Lab%3A%20SQL%20injection%20attack%2C%20listing%20the%20database%20contents%20on%20non-Oracle%20databases.md)

## Blind SQL injection

- [Blind SQL injection](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Blind%20SQL%20injection/Blind%20SQL%20injection.md)
- [What is blind SQL injection?](https://github.com/vsang181/Portswigger/blob/main/SQL%20injection/Blind%20SQL%20injection/What%20is%20blind%20SQL%20injection%3F.md)

## Exploiting blind SQL injection by triggering conditional responses

- Exploiting blind SQL injection by triggering conditional responses
- Exploiting blind SQL injection by triggering conditional responses - Continued
- Exploiting blind SQL injection by triggering conditional responses - Continued
- Lab: Blind SQL injection with conditional responses

## Error-based SQL injection

- Error-based SQL injection
- Exploiting blind SQL injection by triggering conditional errors
- Exploiting blind SQL injection by triggering conditional errors - Continued
- Lab: Blind SQL injection with conditional errors
- Extracting sensitive data via verbose SQL error messages
- Extracting sensitive data via verbose SQL error messages - Continued
- Lab: Visible error-based SQL injection

## Exploiting blind SQL injection by triggering time delays

- Exploiting blind SQL injection by triggering time delays
- Exploiting blind SQL injection by triggering time delays - Continued
- Lab: Blind SQL injection with time delays and information retrieval

## Exploiting blind SQL injection using out-of-band (OAST) techniques

- Exploiting blind SQL injection using out-of-band (OAST) techniques
- Exploiting blind SQL injection using out-of-band (OAST) techniques - Continued
- Lab: Blind SQL injection with out-of-band interaction
- Exploiting blind SQL injection using out-of-band (OAST) techniques - Continued
- Lab: Blind SQL injection with out-of-band data exfiltration

## SQL injection in different contexts

- SQL injection in different contexts
- Lab: SQL injection with filter bypass via XML encoding

## Second-order SQL injection

- Second-order SQL injection

## How to prevent SQL injection

- How to prevent SQL injection
- How to prevent SQL injection - Continued
