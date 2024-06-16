my-cucumber-project/
|-- build.gradle
|-- src/
|   |-- test/
|       |-- java/
|       |   |-- com/
|       |       |-- example/
|       |           |-- steps/
|       |               |-- EatingCucumbersSteps.java
|       |-- resources/
|           |-- features/
|               |-- eating_cucumbers.feature
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
package com.example.steps;

import io.cucumber.java.en.Given;
import io.cucumber.java.en.When;
import io.cucumber.java.en.Then;
import static org.junit.Assert.*;

public class EatingCucumbersSteps {
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
}
gradle build
gradle test
