John Doe: john.doe@example.com, +1-800-555-5555, 12/15/2020
Jane Smith: jane.smith@website.org, (123) 456-7890, 2021-04-01
Foo Bar: foo.bar@foo.com, 987.654.3210, 15-05-2019
Emails found:
- john.doe@example.com
- jane.smith@website.org
- foo.bar@foo.com

Phone numbers found:
- +1-800-555-5555
- (123) 456-7890
- 987.654.3210

Dates found:
- 12/15/2020
- 2021-04-01
- 15-05-2019
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexExample {

    public static void main(String[] args) {
        String filePath = "input.txt"; // Path to the input file
        StringBuilder content = new StringBuilder();

        // Read the file content
        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = br.readLine()) != null) {
                content.append(line).append("\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        String text = content.toString();

        // Regular expressions for email, phone numbers, and dates
        String emailRegex = "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}";
        String phoneRegex = "\\+?[0-9.()\\-\\s]+";
        String dateRegex = "(\\d{2}/\\d{2}/\\d{4})|(\\d{4}-\\d{2}-\\d{2})|(\\d{2}-\\d{2}-\\d{4})";

        // Find and print all matches
        findAndPrintMatches("Emails found:", text, emailRegex);
        findAndPrintMatches("Phone numbers found:", text, phoneRegex);
        findAndPrintMatches("Dates found:", text, dateRegex);
    }

    private static void findAndPrintMatches(String header, String text, String regex) {
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(text);

        System.out.println(header);
        while (matcher.find()) {
            System.out.println("- " + matcher.group());
        }
        System.out.println();
    }
}
