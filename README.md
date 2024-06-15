public interface RecipeBook {
    Recipe getRecipe(int recipeId);
    int getAmtChocolate();
    int getAmtCoffee();
    int getAmtMilk();
    double getPrice();
}
public class CoffeeMaker {
    private RecipeBook recipeBook;

    public CoffeeMaker(RecipeBook recipeBook) {
        this.recipeBook = recipeBook;
    }

    public void selectRecipe(int recipeId) {
        // Logic to select a recipe
    }

    public void depositMoney(double amount) {
        // Logic to handle money deposit
    }

    public void purchaseBeverage() {
        // Logic to purchase beverage
        int chocolate = recipeBook.getAmtChocolate();
        int coffee = recipeBook.getAmtCoffee();
        int milk = recipeBook.getAmtMilk();
        double price = recipeBook.getPrice();

        // Additional logic to check ingredients, money, dispense beverage, return change
    }
}
import static org.mockito.Mockito.*;
import org.junit.Test;

public class CoffeeMakerTest {

    // Mocking the RecipeBook interface
    RecipeBook recipeBook = mock(RecipeBook.class);

    @Test
    public void testPurchaseBeverage_SufficientIngredientsAndMoney() {
        // Stubbing RecipeBook methods
        Recipe selectedRecipe = new Recipe("Latte", 2, 1, 1, 2.50); // Example recipe
        when(recipeBook.getRecipe(1)).thenReturn(selectedRecipe); // Assuming recipe id 1 is selected

        // Assuming a CoffeeMaker instance that uses RecipeBook
        CoffeeMaker coffeeMaker = new CoffeeMaker(recipeBook);

        // Simulating the purchase flow
        coffeeMaker.selectRecipe(1); // User selects recipe with id 1
        coffeeMaker.depositMoney(3.00); // User deposits enough money

        coffeeMaker.purchaseBeverage();

        // Verify interactions with RecipeBook for the selected recipe
        verify(recipeBook).getRecipe(1); // Verify getRecipe(1) is called once
        verify(recipeBook, times(0)).getRecipe(anyInt()); // Verify getRecipe called zero times for other recipes

        verify(recipeBook).getAmtChocolate(); // Verify getAmtChocolate() is called once
        verify(recipeBook).getAmtCoffee(); // Verify getAmtCoffee() is called once
        verify(recipeBook).getAmtMilk(); // Verify getAmtMilk() is called once
        verify(recipeBook).getPrice(); // Verify getPrice() is called once
    }

    // Additional test cases can be added for insufficient ingredients, incorrect recipe id, etc.
}
