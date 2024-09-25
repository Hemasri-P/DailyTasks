## Tuesday(17/09/2024) : Task

- Display some data in grid format using Blazor and Add button functionality to a column to sort data , perform Bunit Testing
- Status : Display Employee data in grid format is completed ,sort the data accordingly and bUnit Testing is pending

## Wednesday(19/1/09/2024) :

- bunit , test cases for checking id should be unique
  add project solution to the existing project , install bunit package to new testing project , write code to test the scenarios

### test case in bunit task

```c#
using Bunit;
using BlazorTasks.Pages;
using BlazorTasks;

namespace TaskTesting
{
    public class UnitTest1: TestContext
    {
        [Fact]
        public void ToCheckTableExistance()
        {
            //arrange : set up we needed for the test
            var cut = RenderComponent<EmployeeData>();

            //act :action that we want to test
            var table =cut.Find("table");

            //assert :verifies the result of the action is what we expected
            Assert.NotNull(table);

        }
        [Fact]
        public void ButtonWorking()
        {
            var cut = RenderComponent<EmployeeData>();


            cut.Find("Button").Click();
            var RowsAfterClick = cut.FindAll("td");


            cut.Find("Button").Click();
            var rowsAfterSecondClick = cut.FindAll("td");
            Assert.Equal("Hemasri", rowsAfterSecondClick[1].TextContent);

        }
        [Fact]
        public void CheckRowsCount()
        {
            var cut= RenderComponent<EmployeeData>();
            var RowsCount = cut.FindAll("tbody tr");
            Assert.Equal(12,RowsCount.Count());

        }
        [Fact]
        public void CheckColumnsCount()
        {
            var cut = RenderComponent<EmployeeData>();
            var ColumnsCount = cut.FindAll("th");
            Assert.Equal(6, ColumnsCount.Count());

        }
        [Fact]
        public void CheckCellsCount()
        {
            var cut=RenderComponent<EmployeeData>();
            var ColumnsCount = cut.FindAll("th").Count();
            var RowsCount = cut.FindAll("td").Count();

            Assert.Equal(78,ColumnsCount + RowsCount);
        }
        [Fact]
        public void CheckHeaderData()
        {
            //arrange
            var cut = RenderComponent<EmployeeData>();

            //act
            var HeaderCount = cut.FindAll("th");

            //assert
            Assert.Contains("ID", HeaderCount[0].TextContent);
            Assert.Contains("Name",HeaderCount[1].TextContent);
            Assert.Contains("Domain",HeaderCount[2].TextContent);
            Assert.Contains("Email", HeaderCount[3].TextContent);
            Assert.Contains("Phone", HeaderCount[4].TextContent);
            Assert.Contains("Salary", HeaderCount[5].TextContent);
        }

    }

}
```

### AAA methodology

- The Arrange section of a unit test method initializes objects and sets the value of the data that is passed to the method under test.

- The Act section invokes the method under test with the arranged parameters.

- The Assert section verifies that the action of the method under test behaves as expected. For .NET, methods in the Assert class are often used for verification.

### Positive and Negative Test Cases

## CODE COVERAGE

- quantifies the extent to which the source code of a program is tested
- Statement Coverage : Measures whether each line of code is executed.
- Branch Coverage : Measures whether each possible branch (true/false) from each decision point is executed.
- Function Coverage : Measures whether each function or subroutine in the code is called.
- Condition Coverage : Measures whether each Boolean sub-expression is evaluated to both true and false.
- Path Coverage : Measures whether all possible paths through the code are executed.
- Line Coverage : Measures the number of executed lines divided by the total number of lines.
- Loop Coverage : Measures whether loops are executed and how many times.

## Thursday(19/092024)

## Tuesday(24/09/2024)

## DB First Approach :

- we are using a existing db for a application
- If we already have a designed database and you don't want to do extra effort then you can go with this approach.
- You can modify the database manually and update the model from the database.It creates model codes (classes, properties, DbContext etc.) from the database in the project and those classes become the link between the database and controller.

## Advantages :

- Good choice for working with an existing database and keeping everything in sync.
- Faster than code first: Quick setup when an existing database is available.Less time spent on designing the database schema.
- Reverse engineering: The database first approach allows you to reverse engineer a model from an existing database.

## Disadvantages:

- Offers less control and flexibility than other approaches.

## What is the use of Microsoft Entityframeworkcore tools?

The Entity Framework Core tools help with design-time development tasks. They're primarily used to manage Migrations and to scaffold a DbContext and entity types by reverse engineering the schema of a database.
If you need to change the database later, you can do it smoothly without losing data.

## Microsoft Entity Framework Core (EF Core)

- It is a tool that helps developers work with databases in their applications more easily.
- Data Access: It allows you to interact with your database using C# code instead of writing complex SQL queries.
- Object Mapping: EF Core maps your database tables to C# classes, so you can work with your data as objects.
- Database Management: It helps manage changes to your database structure over time, making it easier to update and maintain.
- Querying Data: You can easily retrieve, add, update, or delete data using straightforward C# methods.

## Microsoft Entity Framework Core SQL Server

- It is an extension of EF Core specifically designed to work with SQL Server databases.
- Connects to SQL Server: It allows your application to easily connect to and interact with SQL Server databases.
- Database Operations: You can perform operations like creating, reading, updating, and deleting data using simple C# code.
- Data Mapping: It maps your C# classes to SQL Server tables, making it easier to work with your data as objects.
- Efficient Queries: It helps you write efficient queries that run on SQL Server, optimising how data is retrieved.

## Code First Approach :

- Good for new applications where we want full control over the data models. Migrations are created and run to build/update the database.In this approach, we can do all the database operations from the code and manual changes to the database have been lost and everything is depending on the code.

## Advantages

- You can easily modify your data model in code and apply those changes to the database using migrations. 2. Strongly Typed: Using C# provides compile-time checking, reducing runtime errors related to database schema. 3. Developers can focus more on business logic rather than database management, speeding up development cycles. 4. Simplified Updates: Migrations can be automated, allowing you to apply changes without manually altering the database.

## Disadvantages

- Setting up the initial project structure and configurations can be time-consuming.

## Choose Code First if:

- You prefer to work primarily in code.
- You need flexibility to evolve your data model over time.
- You're starting a new project from scratch.

## Choose Database First if:

- You have an existing database that you need to work with.
- Your team has strong expertise in database design and management.
- You want to maintain a clear separation between the database and application logic.

## References :

- Entity Framework Tutorial (tutorialspoint.com) ., Entity Framework Code First v/s Database First Approach (c-sharpcorner.com) ,

## To use another schema in your system, especially when it contains the same tables, you can follow these steps:

- Create the Schema: First, create the new schema in your database. For example, in SQL Server, you can use the following command:

```sql
SQL
CREATE SCHEMA new_schema_name;
Transfer Tables: If you need to transfer tables from one schema to another, you can use the ALTER SCHEMA command. For example:
SQL
ALTER SCHEMA new_schema_name TRANSFER old_schema_name.table_name;


Access Tables: To access tables from the new schema, you need to fully qualify the table names with the schema name. For example:
SQL
SELECT * FROM new_schema_name.table_name;

Handle Conflicts: If the new schema contains tables with the same names as those in your current schema, you need to ensure that you are referencing the correct schema in your queries to avoid conflicts.
Permissions: Ensure that the necessary permissions are granted to users for accessing the new schema. You can use the GRANT statement to assign permissions:
SQL
GRANT SELECT, INSERT, UPDATE, DELETE ON SCHEMA::new_schema_name TO user_name;
```

- Testing: Before fully integrating the new schema, test your queries and operations to ensure that everything works as expected without conflicts.
  By following these steps, you can effectively use another schema in your system, even if it contains tables with the same names as those in your curreqnt schema

## Wednesday(25/09/2024)

-
