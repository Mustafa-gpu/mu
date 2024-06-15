import static org.mockito.Mockito.*;
import org.junit.Test;

public class CoffeeMakerTest {

    // Mocking the RecipeBook interface
    RecipeBook recipeBook = mock(RecipeBook.class);

    @Test
    public void testPurchaseBeverage_SufficientIngredients() {
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

        // Optionally verify other interactions like checking ingredient amounts
        verify(recipeBook).getAmtChocolate(); // Verify getAmtChocolate() is called once
        verify(recipeBook).getAmtCoffee(); // Verify getAmtCoffee() is called once
        verify(recipeBook).getAmtMilk(); // Verify getAmtMilk() is called once
        verify(recipeBook).getPrice(); // Verify getPrice() is called once
    }

    // Additional test cases can be added for insufficient ingredients, incorrect recipe id, etc.
}
