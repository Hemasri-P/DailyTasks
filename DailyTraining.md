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
