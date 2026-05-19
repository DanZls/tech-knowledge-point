# Entry

## Q1: How to unit test an object with database queries?

Unit testing objects that interact directly with a database should be avoided because true unit tests are meant to isolate the logic being tested, not the external dependencies. Instead, you should abstract the database interaction behind an interface or a repository pattern, and then use mocking frameworks such as Moq to replace the actual database with a mock object during testing. This allows you to verify the logic of your object, such as how it interacts with the repository, without hitting a real database. If your code accesses the database directly, consider refactoring it to improve testability. For integration tests, you may use in-memory databases like SQLite or EF Core’s InMemory provider to simulate real database behavior in a controlled test setup.

```csharp
public interface IUserRepository
{
    User GetUser(int id);
}

public class UserService
{
    private readonly IUserRepository _repository;

    public UserService(IUserRepository repository)
    {
        _repository = repository;
    }

    public string GetUserName(int id)
    {
        var user = _repository.GetUser(id);
        return user?.Name;
    }
}

// In a test:
var mockRepo = new Mock<IUserRepository>();
mockRepo.Setup(r => r.GetUser(1)).Returns(new User { Id = 1, Name = "TestUser" });
var service = new UserService(mockRepo.Object);
var name = service.GetUserName(1);
Assert.AreEqual("TestUser", name);
```
---

## Q2: What is the difference between Unit Tests and Functional Tests?

Unit tests check individual components or functions in isolation, ensuring that each part works as expected independently of the rest of the system. They usually mock dependencies and focus on small code units like classes or methods. Functional tests, on the other hand, validate the behavior of a system from the user’s perspective, often testing entire workflows or use cases with minimal mocking, covering more layers (e.g., API and database). Functional tests may be slower and involve integration points, while unit tests are fast and isolated. Unit tests help catch regressions in local logic, whereas functional tests detect issues with the overall design and integration.

```csharp
// Unit test:
[Test]
public void Add_TwoNumbers_ReturnsSum()
{
    var result = Calculator.Add(2, 3);
    Assert.AreEqual(5, result);
}

// Functional test (pseudo-code, may hit HTTP endpoint etc.)
[Test]
public void CreateUser_ShouldReturn200OK()
{
    var response = client.Post("/users", new { Name = "John" });
    Assert.AreEqual(HttpStatusCode.OK, response.StatusCode);
}
```
---

## Q3: What is Mocking?

Mocking is a technique in unit testing where you replace a dependency or collaborator of the unit under test with a controlled implementation that simulates specific behavior. This allows you to test code in isolation by setting expected calls, return values, or exceptions, and verifying how your code interacts with its dependencies. Mocking is commonly used for services like databases, web APIs, or file systems. C# provides mocking frameworks like Moq or NSubstitute for this purpose.

```csharp
var mockLogger = new Mock<ILogger>();
mockLogger.Setup(l => l.Log(It.IsAny<string>()));

var service = new OrderService(mockLogger.Object);
service.ProcessOrder(order);

mockLogger.Verify(l => l.Log("Order processed"), Times.Once);
```
---

# Junior

## Q4: Should unit tests be written for Getter and Setters?

Typically, you do not need to write unit tests for simple getters and setters, especially if they have no logic beyond getting or setting the value. Testing auto-properties provides little value since there’s no custom behavior to validate. However, if getters or setters contain non-trivial logic (e.g., validation, business rules, side effects), you should write unit tests for those cases. The goal is to test code that could possibly break, not code provided by the compiler or with trivial functionality.

```csharp
// No need to test:
public int Age { get; set; }

// Should test:
private int _age;
public int Age
{
    get { return _age; }
    set
    {
        if (value < 0) throw new ArgumentException();
        _age = value;
    }
}
```
---

## Q5: What’s the difference between Mock an object or Spy on it?

Mocking involves creating a fake object that you can control completely, both inputs and outputs, often used to set expectations and verify interactions. A "spy" is a special kind of mock that also records interactions like calls and arguments, but it might call real methods unless specifically overridden (partial mocking). In C#, the term "spy" is less common but can be achieved with frameworks that support partial mocks or by using external libraries. Mocks are usually for testing interactions and behavior, while spies are for recording and verifying those interactions, often in code bases with more complex dependencies.

```csharp
// Mock:
var mock = new Mock<IService>();
mock.Setup(s => s.Get()).Returns(42);
Assert.AreEqual(42, mock.Object.Get());

// "Spy":
var mock = new Mock<IService>();
int callCount = 0;
mock.Setup(s => s.Get()).Callback(() => callCount++);
mock.Object.Get();
Assert.AreEqual(1, callCount);
```
---

# Mid

## Q6: What do I lose by adopting TDD? What are the disadvantages of Test Driven Development?

Adopting Test Driven Development (TDD) means spending more time upfront writing tests before you write production code, which can lead to slower initial development, especially for new teams or complex designs. It may also be less efficient for rapidly prototyped features or experiments. TDD can result in many small, trivial tests that require ongoing maintenance. Overly focusing on tests might lead to excessive coupling between tests and implementation, making refactoring harder. Edge cases, user interface, or integration-heavy code are also less suited for pure TDD, and design constraints may limit creativity.

```csharp
// TDD: Write this test first
[Test]
public void Sum_ReturnsCorrectSum()
{
    Assert.AreEqual(5, MathUtils.Sum(2, 3));
}

// Then, implement:
public static int Sum(int a, int b)
{
    return a + b;
}
```
---

## Q7: Should I Unit Test private methods or only public ones?

Generally, unit tests should target public methods because they define the contract of your class. Private methods are implementation details, and testing them directly couples tests to internal structure, making refactoring harder. If critical logic is hidden in private methods, consider refactoring to move it into separate classes or make it protected/internal and testable. However, if absolutely needed, you can use reflection or InternalsVisibleTo, but this is discouraged unless justified.

```csharp
// Unit test public method, which calls private methods internally:
[Test]
public void Calculate_ShouldReturnExpectedResult()
{
    var calc = new Calculator();
    Assert.AreEqual(10, calc.Calculate(5, 5));
}
```
---

## Q8: What is the fundamental value of Unit Tests vs Integration Tests?

Unit tests validate that small, isolated components of your codebase work as intended, catching regressions early and facilitating refactoring. They are fast, usually running in milliseconds, and do not require dependencies like databases. Integration tests, on the other hand, verify that multiple components or the entire system work together correctly. They help detect issues arising from misconfigured dependencies or broken workflows. Unit tests give you confidence in your local logic, while integration tests provide confidence in overall system behavior.

```csharp
// Unit test:
Assert.AreEqual(4, MathUtils.Multiply(2, 2));

// Integration test:
var result = controller.CreateOrder(orderDto); // hits DB, services etc.
Assert.IsTrue(result.Success);
```
---

## Q9: What’s the difference between Unit Tests and Integration Tests?

Unit tests check individual components in isolation, usually with mocks for any dependencies, and aim for speed and repeatability. They are best for verifying small pieces of logic and fail if the code under test is broken. Integration tests focus on verifying the interaction between several components or external services, such as databases or APIs. They check if these interconnected parts work as intended when combined. Integration tests are typically slower, more fragile, and harder to maintain, but they provide deeper confidence that components integrate correctly.

```csharp
// Unit test:
var mockRepo = new Mock<IOrderRepo>();
mockRepo.Setup(r => r.Save(It.IsAny<Order>())).Returns(true);

// Integration test:
var order = repository.GetOrderFromDb(42); // Real DB call
Assert.IsNotNull(order);
```
---

## Q10: Name some Unit Testing benefits for devs that you personally experienced

Unit testing helps catch bugs early, making debugging faster and cheaper. It also provides safety when refactoring code, since tests will quickly reveal unintended behavior changes. Unit tests document intended behavior, making onboarding for new developers easier. They improve code quality by encouraging decoupled, maintainable design. Finally, unit tests foster a culture of reliability, as changes can be validated instantly with quick feedback, increasing development speed in the long term.

```csharp
[Test]
public void Division_ByZero_Throws()
{
    Assert.Throws<DivideByZeroException>(() => Calculator.Divide(1, 0));
}

// Documents edge case, prevents silent failures.
```
---

## Q11: When and where should I use Mocking?

Use mocking when you want to test code in isolation from its dependencies, such as databases, services, or external APIs. Mocking is essential when the dependency is slow, unreliable, hard to configure, or non-deterministic in tests. Mocks should be used for interfaces and abstractions, not internal business logic. Avoid using mocks for value objects or core business rules that don’t cross system boundaries. Use mocking in both unit tests and sometimes in integration tests (test doubles for services).

```csharp
var mockNotifier = new Mock<INotificationService>();
mockNotifier.Setup(n => n.Send(It.IsAny<string>())).Returns(true);

var manager = new UserManager(mockNotifier.Object);
Assert.IsTrue(manager.Register("test@example.com"));
```
---

## Q12: How would you unit test private methods?

Directly testing private methods is not recommended. Instead, test public methods that call them, ensuring the private logic is adequately covered indirectly. If private methods are complex or reusable, refactor them into separate classes or services with public interfaces that can be tested directly. If you must access private methods (not encouraged), you can use reflection or declare them as internal (and use the `InternalsVisibleTo` attribute).

```csharp
// Preferred:
[Test]
public void PublicMethod_CoversPrivateBehavior()
{
    var obj = new MyClass();
    var result = obj.PublicMethod();
    Assert.AreEqual("expected", result);
}
```
---

## Q13: How can I unit test a GUI?

Unit testing GUI is challenging due to its stateful, event-driven nature. The best approach is to separate logic from presentation (e.g., ViewModel in MVVM), enabling you to unit test business logic and behaviors separately from the UI. For true UI testing, use specialized frameworks like Selenium or WinAppDriver for automated acceptance tests, though these are not classic unit tests. Focus on validating input processing and actions in the ViewModel or controller layers.

```csharp
// ViewModel for testable GUI code
public class LoginViewModel
{
    public bool Login(string username, string password)
    {
        return username == "admin" && password == "secret";
    }
}

[Test]
public void Login_WithValidCredentials_ReturnsTrue()
{
    var vm = new LoginViewModel();
    Assert.IsTrue(vm.Login("admin", "secret"));
}
```
---

## Q14: Is writing Unit Tests worth it for already existing functionality?

Yes, writing unit tests for existing code (“legacy code”) is worthwhile, especially if you plan to refactor, fix bugs, or add features. Tests give you confidence that changes don’t break existing behavior. Start by writing regression tests for critical or complex components and gradually increase coverage. However, prioritize coverage for business-critical paths rather than trivial code.

```csharp
[Test]
public void Calculate_DiscountWorksAsExpected()
{
    var calc = new InvoiceCalculator();
    Assert.AreEqual(90, calc.ApplyDiscount(100, 10));
}
```
---

## Q15: What is a reasonable Code Coverage % for unit tests (and why)?

A reasonable code coverage target is typically between 60-80%. Coverage below 60% indicates many parts are untested, while chasing 100% often leads to diminishing returns, testing trivial auto-generated code, or artificially inflating numbers without improving quality. Aim for high coverage of critical business logic, error paths, and edge cases, but prioritize meaningful, maintainable tests over pure numbers.

```csharp
// Practical test increasing critical path coverage, not getters/setters.
[Test]
public void Withdraw_WithInsufficientFunds_Throws()
{
    var account = new BankAccount(50);
    Assert.Throws<InvalidOperationException>(() => account.Withdraw(100));
}
```
---

# Senior

## Q16: Can Unit Testing be successfully added into an existing production project? If so, how and is it worth it?

Yes, unit testing can be retrofitted into production codebases, though it may require effort. Start with new features or bug fixes, adding tests for the most critical or volatile areas first. Refactor code to separate logic from side effects, abstract dependencies via interfaces, and build up a test suite iteratively. Tools like code coverage reports can help identify key gaps. While initial setup may be costly, the long-term payoff in confidence, easier debugging, and safer refactoring is substantial.

```csharp
// Add test to existing code after introducing repository abstraction
[Test]
public void GetUserByEmail_ReturnsUser()
{
    var repo = new Mock<IUserRepository>();
    repo.Setup(r => r.FindByEmail("test@mail.com")).Returns(new User { Email = "test@mail.com" });
    var service = new UserService(repo.Object);

    var user = service.GetUserByEmail("test@mail.com");
    Assert.IsNotNull(user);
}
```
---

## Q17: Explain what is Arrange-Act-Assert pattern?

Arrange-Act-Assert (AAA) is a common unit test pattern for structuring test code. “Arrange” sets up objects and dependencies, “Act” performs the operation or invocation being tested, and “Assert” checks if the outcome matches expectations. This pattern makes tests clear, readable, and easy to maintain. Keeping these steps separate helps future readers understand the intention and logic behind each test.

```csharp
// Arrange
var calc = new Calculator();

// Act
var sum = calc.Add(2, 3);

// Assert
Assert.AreEqual(5, sum);
```
---

## Q18: What are best practices for Unit Testing methods that use cache heavily?

When unit testing cache-dependent methods, abstract cache access behind an interface and use dependency injection. Mock the cache for predictable outcomes and to isolate logic from the real cache’s behavior. Cover scenarios for both cache hits and misses, and ensure thread safety if relevant. Avoid using static or singleton caches in tests. Include tests that verify correct cache retrieval and updates.

```csharp
var mockCache = new Mock<ICache>();
mockCache.Setup(c => c.Get("item")).Returns("cached-result");
var service = new CachedService(mockCache.Object);
Assert.AreEqual("cached-result", service.GetItem("item"));
```
---

## Q19: What’s the best strategy for Unit-Testing database-driven applications?

The best strategy is to decouple business logic from database access using repositories or service abstractions. Unit tests should target the logic by mocking out database dependencies. Only for integration tests should you use in-memory or test databases. Avoid database hits in unit tests due to slowness and side effects. Focus unit tests on logic, validations, and correct query invocations.

```csharp
// Unit test for logic, not DB
var mockRepo = new Mock<IProductRepository>();
mockRepo.Setup(r => r.GetPrice(1)).Returns(100);

var service = new ProductService(mockRepo.Object);
Assert.AreEqual(100, service.GetPrice(1));
```
---

## Q20: What is Unit test, Integration Test, Smoke test, Regression Test and what are the differences between them?

- Unit test: Validate individual components/methods in isolation, with mocks for dependencies.
- Integration Test: Check that multiple components work together, typically using real or simulated dependencies.
- Smoke Test: Quick, coarse tests to verify that basic application functionality works after a build (sanity check).
- Regression Test: Tests designed to catch bugs that have reappeared after previously being fixed.

Each type serves a unique purpose: unit tests catch bugs early and fast, integration tests confirm correct component integration, smoke tests ensure system health post-deployment, and regression tests prevent bug reintroduction.

```csharp
// Unit test
Assert.AreEqual(5, MyMath.Add(2, 3));

// Integration test
Assert.IsNotNull(controller.GetUser(42)); // hits multiple layers

// Smoke test
[Test]
public void HomePage_ShouldLoadWithoutError()
{
    var resp = client.Get("/");
    Assert.AreEqual(HttpStatusCode.OK, resp.StatusCode);
}

// Regression test
[Test]
public void PreviouslyFixedBug_ShouldNotReoccur()
{
    Assert.AreEqual(expected, buggyFunction(input));
}
```
---

## Q21: What is the best way to unit test a method that doesn't return anything (void)?

Unit test void methods by verifying their side effects, such as changes in state, calls to collaborators, or raised events. Use mocks to assert that dependent methods were called with correct arguments, or inspect updated fields or collections. Exceptions thrown should also be asserted as expected.

```csharp
[Test]
public void Logger_Log_ShouldCallWrite()
{
    var mockWriter = new Mock<IWriter>();
    var logger = new Logger(mockWriter.Object);

    logger.Log("message");

    mockWriter.Verify(w => w.Write("message"), Times.Once);
}
```
---

# Expert

## Q22: How do I test a private function or a class that has private methods, fields or inner classes?

Prefer indirect testing via public methods, which should cover all internal logic. For large or reusable private methods, extract them into new classes or make them internal with [InternalsVisibleTo] for the test project. If you must, reflection can invoke private methods, but this couples tests to implementation and is generally discouraged. Testing should be focused on behavior rather than implementation details.

```csharp
// Indirectly tested:
public class Calculator
{
    public int AddAndDouble(int a, int b)
    {
        return Double(Add(a, b));
    }

    private int Add(int x, int y) => x + y;
    private int Double(int z) => z * 2;
}

[Test]
public void AddAndDouble_CorrectResult()
{
    var calc = new Calculator();
    Assert.AreEqual(10, calc.AddAndDouble(2, 3));
}
```
---

## Q23: Is Unit Testing worth the effort?

Unit testing requires effort to set up and maintain, but the long-term benefits outweigh the costs for almost all production code. Tests prevent regressions, clarify intended behavior, make code safer to refactor, and improve developer confidence and productivity. They are especially valuable in large or long-lived codebases, mission-critical systems, or rapid development contexts. The upfront cost pays back through faster debugging, easier onboarding, and fewer production bugs.

```csharp
[Test]
public void Calculator_AddsCorrectly()
{
    var result = Calculator.Add(1, 3);
    Assert.AreEqual(4, result);
}
```
---

# Mid: Code

## Q1: Can you provide an example of a common Mocking scenario?

A typical example is testing a service that sends emails. Instead of really sending emails, mock the email service to verify that your code attempts to send the right message under proper conditions.

```csharp
public interface IEmailSender
{
    void Send(string address, string message);
}

public class NotificationService
{
    private readonly IEmailSender _emailSender;

    public NotificationService(IEmailSender sender)
    {
        _emailSender = sender;
    }

    public void NotifyUser(string userEmail)
    {
        _emailSender.Send(userEmail, "You have a new notification!");
    }
}

// Unit test:
[Test]
public void NotifyUser_ShouldCallSendWithCorrectParameters()
{
    var mockEmailSender = new Mock<IEmailSender>();
    var service = new NotificationService(mockEmailSender.Object);

    service.NotifyUser("test@example.com");

    mockEmailSender.Verify(s => s.Send("test@example.com", "You have a new notification!"), Times.Once);
}
```
---
