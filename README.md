package skeleton;
import cucumber.api.java.en.When;

public class Stepdefs {
    // NOTE: because the regular expressions are within 
    // Java strings, we have to make all backslashes double backslashes
    // for them to work correctly.  So, to find a decimal character,
    // rather than writing \d, you must write \\d. 

    // NOTE 2: to explicitly force a pattern to start with the 
    // beginning of the input string, start with ^.  To force it to 
    // end at the end of the input string, use $.  For example:
    // @When("test_foo \\d") will match:
    //     test_foo 5
    // but will also match:
    //     some test_foo 5 dollars
    //     bugga bugga test_foo 1 
    // 
    // On the other hand:
    // @When("^test_foo \\d$")
    // will only match: test_foo 5
    // 
    
    // NOTE 3: to not 'capture' a pattern as an argument to the 
    // Java method, use (?:<pattern>)
    // For example: 
    //    @When("^match_four ((in|out)(foo|bar))$") 
    // will match the words:
    //   infoo, inbar, outfoo, and outbar.  
    // However, the associated Java function will require three 
    // parameters: one for the 'in/out' value, one for the 
    // 'foo/bar' value, and one for their concatenation.  To 
    // only capture the concatenated value, use: 
    //   @When("^match_four ((?:in|out)(?:foo|bar))$")
    // 
    // You will probably need this to do the IP address example :)
    
    
    // Regular expression matcher for positive integers
    // Should match the string: test_posint followed by an sequence of 
    // digits of arbitrary length 
    @When("^test_posint\\s*(\\d+)$")
    public void test_posint(int number) throws Throwable {
        System.out.println("test_posint true for: " + number);
    }
    
    // Regular expression matcher for integers
    // Should match the string: test_int followed by an optional
    // minus sign followed by a sequence of 
    // digits of arbitrary length 
    //
    // I give you this one as a freebie!
    @When("^test_int\\s*(-?\\d+)$")
    public void test_int(int arg1) throws Throwable {
        System.out.println("test_int true for: " + arg1);
    }

    // Regular expression matcher for floats
    // Should match the string: test_float followed by an optional
    // minus sign followed by a sequence of 
    // digits of arbitrary length followed by a period followed by
    // a second sequence of digits of arbitrary length.
    @When("^test_float\\s*-?(\\d+\\.+\\d+$)")
    public void test_float(float arg1) throws Throwable {
        System.out.println("test_int true for: " + arg1);
    }
    
    // Regular expression matcher for IP addresses (though inexact).
    // It should accept four digit sequences separated by periods
    // where a digit sequence is defined as follows:
    //    Any single digit
    //    Any two digit characters if the first character is non-zero
    //    A one followed by a zero, one, or two followed by any digit
    
    // SEE NOTE 3 :)
    @When("^test_ip_address\\s*((?:(?:(?:\\d)|(?:1[0-2]\\d)|(?:[1-9]\\d))\\.){3}(?:(?:\\d)|(?:[1-9]\\d)|(?:1[0-2]\\d)))$")
    public void test_ip_address(String arg1) throws Throwable {
        System.out.println("test_ip_address true for: " + arg1);
    }

    
    // Pattern distinguisher.  
    // Should match the string starting with: test_splitter arg
    // Where <arg> should match the following positive examples
    // and not the negative examples.  Note: any string not in the 
    // positive or negative examples can be accepted or rejected.
    // 
    // Positive:        Negative:
    // =========        =========
    // spill            si
    // Sponge           egregious
    // tap              Foul
    // rebuild          Test
    //                  top
    //                  ta
    @When("^test_splitter\\s*(?=.*?\\bspill|Sponge|tap|rebuild\\b)((?!si|egregious|Foul|Test|ta).)*$")
    public void test_splitter(String match) throws Throwable {
        System.out.println("test_splitter true for: " + match);
    }
    
    
    // Pattern distinguisher 2.  
    // Should match the string starting with: test_splitter2 arg
    // Where <arg> should match the following positive examples
    // and not the negative examples.  Note: any string not in the
    // positive or negative examples can be accepted or rejected.
    // 
    // Positive:        Negative:
    // =========        =========
    // spill            spall
    // Sponge           egregious
    // tap              foul
    // rebuild          test
    //                  top
    //                  tapper
    @When("^test_splitter2\\s*(?=.*?\\bspill|Sponge|tap|rebuild\\b)((?!spall|egregious|foul|Test|top|tapper).)*$")
    public void test_splitter2(String match) throws Throwable {
        System.out.println("test_splitter2 true for: " + match);
    }
}

testfeature

Scenario: test regular expressions that should pass
    When test_posint 12345
    When test_posint 9
    When test_posint 77777777
    When test_int -1
    When test_int 1435
    When test_float 12345.543
    When test_float -13.56
    When test_ip_address 123.34.76.109
    When test_ip_address 123.34.76.109
    When test_ip_address 105.22.33.44
    When test_ip_address 1.2.3.4
    When test_splitter spill
    When test_splitter Sponge
    When test_splitter tap
    When test_splitter rebuild
    When test_splitter2 spill
    When test_splitter2 Sponge
    When test_splitter2 tap
    When test_splitter2 rebuild
  
  Scenario: fail 1
    When test_int 5y6
  Scenario: fail 2
    When test_int 56k
  Scenario: fail 3
    When test_int 57.45
  Scenario: fail 4
    When test_float 1235
  Scenario: fail 5
    When test_int 46 and more
  Scenario: fail 6
    When test_float 3.45 and more
  Scenario: fail 7
    When test_ip_address 123.45.47
  Scenario: fail 8
    When test_ip_address four score and 123.34.76.109
  Scenario: fail 9
    When test_ip_address 123.34.76.109 and more
