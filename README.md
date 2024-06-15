// Suppose we have a class that interacts with an external service

public class DataService {
    private ExternalService service;

    public DataService(ExternalService service) {
        this.service = service;
    }

    public int processData(int input) {
        // Logic to process data using the external service
        return service.performOperation(input);
    }
}

// Interface for the external service
public interface ExternalService {
    int performOperation(int input);
}

// Test class using Mockito for mocking ExternalService
import static org.mockito.Mockito.*;

public class DataServiceTest {

    @Test
    public void testProcessData() {
        // Create a mock for ExternalService
        ExternalService mockService = mock(ExternalService.class);
        
        // Define stub behavior for the mock
        when(mockService.performOperation(5)).thenReturn(10);
        
        // Create DataService instance with the mock
        DataService dataService = new DataService(mockService);
        
        // Invoke the method under test
        int result = dataService.processData(5);
        
        // Verify the result
        assertEquals(10, result);
        
        // Verify interaction with mock (optional)
        verify(mockService).performOperation(5);
    }
}
