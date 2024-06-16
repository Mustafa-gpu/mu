Feature: Manage Cucumber Consumption

  Scenario: Eat some cucumbers
    Given I have a belly
    When I eat 5 cucumbers
    Then my belly should contain 5 cucumbers

  Scenario: Eat more cucumbers
    Given I have a belly
    When I eat 7 cucumbers
    Then my belly should contain 7 cucumbers

  Scenario: Eat negative cucumbers (Edge case handling)
    Given I have a belly
    When I eat -3 cucumbers
    Then the system should show an error message

  Scenario Outline: Eat cucumbers with various amounts
    Given I have a belly
    When I eat <amount> cucumbers
    Then my belly should contain <expected>

    Examples:
      | amount | expected |
      | 0      | 0        |
      | 10     | 10       |
      | 1      | 1        |
      | 3      | 3        |
      | 6      | 6        |

  Scenario: Eat cucumbers over time
    Given I have a belly
    When I eat 2 cucumbers every day for 5 days
    Then my belly should contain 10 cucumbers

  Scenario: Eat cucumbers with different types (Feature variety)
    Given I have a belly
    When I eat 2 cucumbers of type "normal" and 3 cucumbers of type "organic"
    Then my belly should contain 5 cucumbers

  Scenario: Eat cucumbers with delays (Performance scenario)
    Given I have a belly
    When I eat 10 cucumbers with a 2-second delay between each cucumber
    Then my belly should contain 10 cucumbers

  Scenario: Eat cucumbers with errors (Error handling scenario)
    Given I have a belly
    When I eat cucumbers but the belly is full
    Then an error should be displayed
