Feature: Eating cucumbers

  Scenario: Eating a few cucumbers
    Given there are 12 cucumbers
    When I eat 5 cucumbers
    Then I should have 7 cucumbers left

  Scenario: Eating too many cucumbers
    Given there are 5 cucumbers
    When I eat 6 cucumbers
    Then I should have 0 cucumbers left
    And I should see an error message "You can't eat more cucumbers than you have!"

  Scenario: Eating cucumbers with different phrases
    Given the cucumber count is "12"
    When I consume "5" cucumbers
    Then the remaining cucumber count should be "7"
package com.example.steps;

import io.cucumber.java.en.Given;
import io.cucumber.java.en.When;
import io.cucumber.java.en.Then;
import static org.junit.Assert.*;

public class Stepdefs {
    private int cucumbers;
    private String errorMessage;

    @Given("there are {int} cucumbers")
    public void there_are_cucumbers(int initialCount) {
        cucumbers = initialCount;
        errorMessage = null;
    }

    @When("I eat {int} cucumbers")
    public void i_eat_cucumbers(int count) {
        if (count > cucumbers) {
            errorMessage = "You can't eat more cucumbers than you have!";
            cucumbers = 0;
        } else {
            cucumbers -= count;
        }
    }

    @Then("I should have {int} cucumbers left")
    public void i_should_have_cucumbers_left(int expectedCount) {
        assertEquals(expectedCount, cucumbers);
    }

    @Then("I should see an error message {string}")
    public void i_should_see_an_error_message(String expectedMessage) {
        assertEquals(expectedMessage, errorMessage);
    }

    // New steps with different phrases using regex in Cucumber expressions
    @Given("^the cucumber count is \"(\\d+)\"$")
    public void the_cucumber_count_is(String initialCount) {
        cucumbers = Integer.parseInt(initialCount);
        errorMessage = null;
    }

    @When("^I consume \"(\\d+)\" cucumbers$")
    public void i_consume_cucumbers(String count) {
        int numCucumbers = Integer.parseInt(count);
        if (numCucumbers > cucumbers) {
            errorMessage = "You can't eat more cucumbers than you have!";
            cucumbers = 0;
        } else {
            cucumbers -= numCucumbers;
        }
    }

    @Then("^the remaining cucumber count should be \"(\\d+)\"$")
    public void the_remaining_cucumber_count_should_be(String expectedCount) {
        int expectedCucumbers = Integer.parseInt(expectedCount);
        assertEquals(expectedCucumbers, cucumbers);
    }
}
plugins {
    id 'java'
}

repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'io.cucumber:cucumber-java:7.0.0'
    testImplementation 'io.cucumber:cucumber-junit:7.0.0'
    testImplementation 'junit:junit:4.13.2'
}

test {
    useJUnitPlatform()
}
