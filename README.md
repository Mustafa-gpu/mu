Feature: Login Feature

  Scenario: Successful login with valid credentials
    Given I am on the login page
    When I enter username "user1" and password "password123"
    And I click on the login button
    Then I should be logged into the system
import cucumber.api.java.en.Given;
import cucumber.api.java.en.When;
import cucumber.api.java.en.Then;

public class Stepdefs {

    @Given("^the user is on the login page$")
    public void navigateToLoginPage() {
        System.out.println("Navigating to the login page");
        // Add actual navigation code here if necessary
    }

    @When("^they enter \"([^\"]*)\" and \"([^\"]*)\"$")
    public void enterCredentials(String username, String password) {
        System.out.println("Entering credentials: " + username + " / " + password);
        // Add actual credential entering code here if necessary
    }

    @Then("^they should be logged in$")
    public void verifyLoggedIn() {
        System.out.println("Verifying user is logged in");
        // Add verification code here
    }
}
Explanation:
Given Step: @Given("^the user is on the login page$")

This method (navigateToLoginPage) will be called when the step "Given the user is on the login page" is matched. You can implement navigation logic or setup necessary conditions for the test here.
When Step: @When("^they enter \"([^\"]*)\" and \"([^\"]*)\"$")

This method (enterCredentials) will be called when the step "When they enter "username" and "password"" is matched. It uses regex with capture groups ("([^\"]*)"), allowing you to capture the username and password for use in the method.
Then Step: @Then("^they should be logged in$")

This method (verifyLoggedIn) will be called when the step "Then they should be logged in" is matched. Here you can implement assertions or verification logic to check if the user is successfully logged in.
Running the Scenario
Ensure your Cucumber setup is correct with dependencies like cucumber-java and cucumber-junit.
Run the scenario using Gradle (gradlew test) or your IDE's test runner.
The console output (System.out.println statements) will indicate if each step is being executed as expected.
Note:
Replace System.out.println statements with actual implementation logic (like Selenium WebDriver actions or API calls) as per your application's requirements.
Extend the Stepdefs.java file to cover more scenarios from Test.feature by adding additional methods annotated with @Given, @When, and @Then, each with corresponding regular expressions that match the steps in your scenarios.
