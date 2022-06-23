# Test-Driven Development

---

<section>

# Test Strategy
</section>

<section>

![Agile Testing Quadrants](images/quadrants.jpeg)
</section>

<section>

## Types of Tests

* **Unit**\
  Fast, run in isolation.

* **Integration**\
  Slow, use parts of the real system.

* **End-to-End**\
  Even more slow and brittle, use the real system.

* **Manual and Exploratory**\
  Involves humans.

</section>

<section>

## Test Pyramid

![Test Pyramid](images/test-pyramid-1.svg)
</section>

<section>

| Unit Tests  | Tests using mocks to test integration | Integration Tests |
| ----------- | ------------------------------------- | ----------------- |
| Trustworthy | ~~Trustworthy~~                       | Trustworthy       |
| Cheap       | Cheap                                 | ~~Cheap~~         |
| Fast        | Fast                                  | ~~Fast~~          |
| Reliable    | Reliable                              | ~~Reliable~~      |
| Targeted    | Targeted                              | ~~Targeted~~      |

</section>

<section>

![Test Pyramid](images/test-pyramid-2.svg)
</section>

<section>

![Test Pyramid](images/test-pyramid-3.svg)
</section>

<section>

![Test Pyramid](images/test-pyramid-4.svg)
</section>

<section>

![Test Pyramid](images/test-pyramid-5.svg)
</section>

<section>

## Onion Architecture

A.K.A.

* Hexagonal Architecture
* Ports & Adapters
* The Clean Architecture
</section>

<section>

![Onion Architecture](images/onion-architecture-1.svg)
</section>

<section>

![Onion Architecture](images/onion-architecture-2-detail.svg)
</section>

<section>

![Onion Architecture](images/onion-architecture-3-tests.svg)
</section>

<section>

![Onion Architecture](images/onion-architecture-4-detail-test.svg)
</section>

<section>

![Onion Architecture](images/onion-architecture-5-outside.svg)
</section>

<section>

## Contract Tests

An alternative approach to end-to-end testing.

</section>

<section>

### Specification-First Design

![Contract Tests](images/contract-tests/spec-first-1.svg)
</section>

<section>

### Specification-First Design

![Contract Tests](images/contract-tests/spec-first-2.svg)
</section>

<section>

### Consumer-Driven Contracts

![Contract Tests](images/contract-tests/consumer-driven-1.svg)
</section>

<section>

### End-To-End-Testing

![Contract Tests](images/contract-tests/app-1.svg)
</section>

<section>

### End-To-End-Testing

![Contract Tests](images/contract-tests/app-2-e2e.svg)
</section>

<section>

### Contract-Based Testing

![Contract Tests](images/contract-tests/app-3-seams.svg)
</section>

<section>

### Contract-Based Testing

* **Simple**\
  Targets a single integration point at a time. No need to deploy.

* **No special environments**\
  Runs on a developer machine.

* **Fast**\
  Behaves more like a Unit Test with reliable feedback. Scales linearly.

* **Independent**\
  Deploy services one at a time with preserved compatibility.

* **Documents**\
  Consumer's expectations from providers.

</section>

<section>

### Contract-Based Testing

![Contract Tests](images/contract-tests/producer-consumer-1.svg)

</section>

<section>

### What An Integration Test Would Look Like

![Contract Tests](images/contract-tests/producer-consumer-2.svg)

</section>

<section>

### Contract-Based Testing

![Contract Tests](images/contract-tests/producer-consumer-3.svg)

</section>

<section>

### Contract-Based Testing

![Contract Tests](images/contract-tests/producer-consumer-4.svg)

</section>

<section>

### Contract-Based Testing

![Contract Tests](images/contract-tests/producer-consumer-5.svg)

</section>

<section>

| Unit Tests  | Contract-Based Tests | Integration Tests |
| ----------- | -------------------- | ----------------- |
| Trustworthy | Trustworthy          | Trustworthy       |
| Cheap       | Cheap                | ~~Cheap~~         |
| Fast        | Fast                 | ~~Fast~~          |
| Reliable    | Reliable             | ~~Reliable~~      |
| Targeted    | Targeted             | ~~Targeted~~      |

</section>


<section>

### *Do Use* Contract-Based Testing

* You own the provider and the consumer
* Both are actively developed
* The provider can control the data it returns
* The consumer's requirements drive the development of the provider
* The provider team can manage the (small enough number of) relationships with
  its consumers

</section>

<section>

### *Do Not Use* Contract-Based Testing

* The team maintaining the provider does not use Contract-Based Testing
* There a no communication channels between consumers and providers
* Public APIs with many consumers that you do not know about
* The data returned by providers cannot be controlled
* Functional testing of the provider - that is the provider's responsibility

</section>

---

<section>

# Workflow
</section>

<section>

![Red-Green-Refactor](images/red-green-refactor-1.svg)
</section>

<section>

![Red-Green-Refactor](images/red-green-refactor-2.svg)
</section>

<section>

![Red-Green-Refactor](images/red-green-refactor-3.svg)
</section>

<section>

1. Write a failing test
1. Do the minimum amount of work to make it pass
1. Remove duplication and refactor your solution

Commit to source control after you reach a working state.

> Make it work, make it right, make it fast.
</section>

<section>

## FIRST Properties of Unit Tests

* **Fast**\
  Unit tests should take very little time to run.
* **Isolated**\
  Unit tests are standalone and have no dependencies on any outside factors such
  as a file system or database.
* **Repeatable**\
  Running a unit test should be consistent with its results.
* **Self-Checking**\
  The test should automatically detect if it passed or failed.
* **Timely**\
  A unit test should not take a disproportionately long time to write compared
  to the code being tested.

</section>

<section>

## System Under Test

The thing that we want to exercise. Could be a method, a class instance, a
composition of instances, an API or the whole system.
</section>

<section>

## Given, When, Then, Cleanup

== Arrange, Act, Assert, Teardown
</section>

<section>

```cs
Given = () => {
  // Prepare for the scenario to be executed, e.g.
  // launch browser, log in, prepare database,
  // create classes.
}

When = () => {
  // Exercise System under Test.
}

Then = () => {
  // Check if the expected happened.
}

Cleanup = () => {
  // Dispose of resources.
}
```

</section>

<section>

```cs
[TestFixture]
public class Calculation
{
  [Test]
  public void Should_yield_42_when_adding_40_and_2()
  {
    // Arrange

    // Act

    // Assert
  }
}
```

</section>

<section>

```cs
[TestFixture]
public class Calculation
{
  [SetUp]
  public void Create_calculation()
  {
  }

  [TearDown]
  public void Dispose_of_system_under_test()
  {
  }

  [Test]
  public void Should_yield_42_when_adding_40_and_2()
  {
    // Act

    // Assert
  }
}
```

</section>

---

<section>

# Assertions
</section>

<section>

## Asserting State

```csharp
// Built-in to the .NET Framework.
Trace.Assert(42 == 42);

// Included in your testing framework.
Assert.AreEqual(expected, actual);

// Separate library: fluentassertions.com
actual.Should().Be(expected);
```

</section>

<section>

## Asserting State

```csharp
[TestFixture]
public class Asserting_with_Verify
{
  [Test]
  public Task Sample()
  {
    var person = SystemUnderTest.FindPerson();
    return Verify(person);
  }
}
```

[Extensions](https://github.com/VerifyTests/Verify#extensions) available for
various data types.

</section>

<section>

## Asserting Interactions

Using state and "hand-rolled" mocks.

```csharp
class FakeNotifications : ISendNotifications {
  public WasSent = false;

  public void Send(string message) {
    WasSent = true;
  }
}

var notification = new FakeNotifications();
notification.Send("hello, world");
Assert.IsTrue(notification.WasSent);
```

</section>

<section>

## Asserting Interactions

Using specialized mock/stub/dummy/spy/fake libraries.

```csharp
var notifications = A.Fake<ISendNotifications>();

A.CallTo(() => notifications.Send(A<string>.Ignored))
 .MustHaveHappened();
```

Above: [FakeItEasy](https://fakeiteasy.github.io/)

</section>

<section>

## Providing Canned Answers

```csharp
var notifications = A.Fake<ISendNotifications>();

A.CallTo(() => notifications.Send(A<string>.Ignored))
 .Throws(new NetworkUnavailableException());
```

</section>

---

<section>

# Test Styles

[Examples](https://github.com/agross/test-styles)
</section>

---

<section>

# Behavior-Driven

Focus on the *What*, not on the *How*.
</section>

<section>

## Specifications

1. Are written from the perspective of an external user of the system.
1. Evaluate the system in life-like scenarios.
1. Are evaluated in [production-like test environments](https://github.com/mariotoffia/FluentDocker).
1. Interact with the System under Test (SUT) through public interfacess.
1. Focus on the *What*, not on the *How*.
1. Work best with other forms of test automation.

</section>

<section>

Write specifications from the perspective of the user. Try to invert your
specification structure, putting the business case first.

```gherkin
As a call-center employee
I want to see the most recent purchases
such that I can help the customer if they have problems.
```

```text
In order to support customers
call-center employees need to see the most recent purchases.
```

A least technical person that is proficient in the problem domain should be able
to understand these.
</section>

<section>

1. Build a domain-specific language describing your scenarios.
1. Make them executable.
1. Guide your development from these user needs.

</section>

<section>

```gherkin
Given I am a user in the "business controller" role
And I am not logged in
When I  visit the dashboard
Then I am redirected to the login page
```

vs.

```text
In order to do useful business controlling work
When I view the dashboard while not being logged in
I am given the chance to log in
```

</section>

<section>

```csharp
[Test]
public void Should_be_able_to_log_in_to_see_the_dashboard()
{
  authorization.LogOut();
  controlling.VisitTheDashboard();

  authentication.FillInCredentialsAndLogIn();

  controlling.AssertViewsDashboard();
}
```

</section>

<section>

![4 layers from test to SUT](images/four-layered-approach.svg)

[Screenplay Pattern](https://www.infoq.com/articles/Beyond-Page-Objects-Test-Automation-Serenity-Screenplay/),
[Boa Constrictor](https://q2ebanking.github.io/boa-constrictor/)
</section>

<section>

## Pitfalls

</section>

<section>

### UI Interaction != Specification

```gherkin
Given I am an authorized user
When I enter "scott" into the username field
And I enter "tiger" into the password field
And I click login
Then the home page should open
```

</section>

<section>

### UI Interaction != Specification

Would the specification need to change if:

* We need to support fingerprint authentication, voice activation or thought control,
* The login UI becomes a 2-step process (extra button click)?

</section>

<section>

### UI Interaction != Specification

```gherkin
Given authorized user "scott"
When "scott" logs in with valid credentials
Then "scott" can access their accounts
```

</section>

<section>

### Long-Running Specifications

```gherkin
Scenario: Bus Edit Saving a bus should have attributes
          saved and return to bus list
Given I am logged in as "bmfs-admin"
And I verify data exists for testing
Then I should see "BMFS Homepage"

When I select the "Buses" menu
Then I should see "Buses"
And I should see a list of buses

When I click "Edit"
Then I should see "Contract Details"
And I should see "Registration Details"

When I type "BUS-ABC" into "Registration Number"
And I type 6 into "Seat Belts"
And I click "Submit"
Then the "Registration Number" should be "BUS-ABC"
```

</section>

<section>

### Long-Running Specifications

```gherkin
Scenario: Updating bus attributes
Given I log in as an administrator
When I update the attributes for bus "BUS-ABC"
Then the updated attributes for bus "BUS-ABC" should
     be available when viewing bus information
```

</section>

<section>

### Aimless Requirements

```gherkin
Feature: Display customer details

As a user
I want to view the customer's profile details
So that I can see the personal information on the user
```

Would you put that into the documentation of your system?

</section>

<section>

### Aimless Requirements

```gherkin
Feature: Locate a customer

In order to propose more relevant services to a customer
As a financial advisor
I want to access relevant customer's profile details
```

</section>

<section>

### A Pattern

```gherkin
Feature: Locate a customer

<Real business goal> In order to propose more relevant services to a customer
<Target audience of the feature> As a financial advisor
<What capability will help me achieve this> I want to access relevant customer's profile details
```

</section>

<section>

### Boring Scenarios

```gherkin
Scenario Outline: User tries to log in with
                  invalid credentials

Given I am a registered user
When I log in using <username> and <password>
Then I should not be allowed to log in
And I see an error message <message>

Examples:
| username | password | message                  |
| scott    |          | Enter password           |
|          | tiger    | Enter name               |
| scott    | wrong    | Invalid user or password |
```

</section>

<section>

### Scenario Overload

```gherkin
Scenario: Account gets 4% interest when balance is
          >= 1000 EUR
Given/When/Then...

Scenario: Account gets 2% interest when balance is
          less than 1000 EUR

Scenario: Account gets 4% interest when balance is
          >= 1000 EUR and no more than 100 EUR
          have been withdrawn

Scenario: Account gets 2% interest when balance is
          >= 1000 EUR and more than 100 EUR have
          been withdrawn
```

</section>

<section>

### Scenario Overload

```gherkin
Scenario Outline: Account interest rate
Given/When/Then...

Examples:
| balance | previous | rate |
| 1200    | 1200     | 4    |
| 900     | 900      | 2    |
| 1200    | 1300     | 4    |
| 1200    | 1400     | 2    |
```

Sometimes tables are more expressive.
</section>

<section>

### Scenario Overload

```gherkin
Scenario Outline: Account interest rate
Given/When/Then...

Examples:
| balance | previous | rate |
| 1001    | 1001     | 4    |
| 1000    | 1000     | 4    |
| 999     | 999      | 2    |
| 1000    | 1100     | 4    |
| 1000    | 1101     | 2    |
```

Sometimes tables are *less* expressive.
</section>

<section>

[An example](https://specflow.org/bdd/a-bdd-journey-with-specflow/)

</section>
