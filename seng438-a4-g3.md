**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#4 – Mutation Testing and Web app testing**

| Group \#: 3    |
| -------------- |
| Aaron Frerichs |
| Avijot Gern    |
| Jesse Gerbrandt|
| Ethan Subasic  |

# Introduction

# Analysis of 10 Mutants of the Range class 

### **Mutant 1**<br/>
**Line:** 217 in ```combine()``` method <br/>
**Orignial Code:** ```if (range1 == null)```<br/>
**Mutated Code:** ```if (false)```<br/>
**Summary:** Mutant was <span style="color:green"><u>killed</u></span> by the test ```firstRangeNullShouldReturnRangeTwo()``` as we expected the returned range to be the same as the second input range but instead an unexpected value was recieved since the mutant code was using unexpected values for the max and min in lines 223 andd 224 which caused unexpected behaviour.<br/>

### **Mutant 2**<br/>
**Line:** 221 in ```combine()``` method <br/>
**Orignial Code:** ```return range1```<br/>
**Mutated Code:** ```return null```<br/>
**Summary:** Mutant was <span style="color:green"><u>killed</u> </span> by the test ```secondRangeNullShouldReturnRangeOne()``` as we expected the returned range to be the same as the first input range, since the second one from the test is null. The return value from the mutated code was null instead which was not expected from our test and was thus killed.<br/>

### **Mutant 3**<br/>
**Line:** 190 in ```constrain()``` method <br/>
**Orignial Code:** ```if (value > this.upper)```<br/>
**Mutated Code:** ```if (value >= this.upper)```<br/>
**Summary:** The mutant <span style="color:red"><u>survived</u></span>, this is because there are no tests in RangeTest that was used it check if the ```value``` argument is equal to the upper range value of the range its being used on.<br/>

### **Mutant 4**<br/>
**Line:** 132 in ```getCentralValue()``` method <br/>
**Orignial Code:** ```return this.lower / 2.0 + this.upper / 2.0```<br/>
**Mutated Code:** ```return this.lower / 1.0 + this.upper / 2.0```<br/>
**Summary:** The mutant was <span style="color:green"><u>killed</u></span>. Both of the tests made for this method, ```centerValueShouldBe0()``` and ```centerValueShouldBe0point5()``` were able to kill this mutation as the lower bound was no longer being haved so the center would have been offset from the expected center in both cases.<br/>

### **Mutant 5**<br/>
**Line:** 132 in ```getCentralValue()``` method <br/>
**Orignial Code:** ```return this.lower / 2.0 + this.upper / 2.0```<br/>
**Mutated Code:** ```return (this.lower)++ / 2.0 + this.upper / 2.0```<br/>
**Summary:** The mutant <span style="color:red"><u>survived</u></span>. This mutant was missed by the tests because it does not cause any damage. Since the incrementation succeeds the variable, it will only be applied once the variable is already used in the equation, and since the equation is done in the return line the lower will not cause any immediate damage in this method. However this could become an issue in the future if more opetations are enacted on the same range as now the lower field will have been altered.<br/>

### **Mutant 6**<br/>
**Line:** 157 in ```intersects()``` method <br/>
**Orignial Code:** ```if (b0 <= this.lower)```<br/>
**Mutated Code:** ```if (b0 < this.lower)```<br/>
**Summary:** The mutant <span style="color:red"><u>survived</u></span>. This mutant was able to survive since none of the tests working with this method tested arguments that were the same as ,in this case, the lower value of the range the method is being done on.<br/>

### **Mutant 7**<br/>
**Line:** 161 in ```intersects()``` method <br/>
**Orignial Code:** ```return (b0 < this.upper && b1 >= b0)```<br/>
**Mutated Code:** ```return (b0 <= this.upper && b1 >= b0)```<br/>
**Summary:** The mutant <span style="color:red"><u>survived</u></span>. Similar to mutation 6, this mutant code was not detected since none of the tests for the intersets method use arguments that are equivalent to the upper value of the range being used. <br/>

### **Mutant 8**<br/>
**Line:** 123 in ```getLength()``` method <br/>
**Orignial Code:** ```return this.upper - this.lower```<br/>
**Mutated Code:** ```return this.upper + this.lower```<br/>
**Summary:** The mutant was <span style="color:green"><u>killed</u></span>. The mutant was detected and killed by the test ```theLengthValueShouldBeTwo()``` since the original math of 1 - (-1) would have returned the expected value or 2, and the changed math 1 + (-1) returned an unexpected value 0.<br/>

### **Mutant 9**<br/>
**Line:** 425 in ```equals()``` method <br/>
**Orignial Code:** ```if (!(obj instanceof Range))```<br/>
**Mutated Code:** ```if (true)```<br/>
**Summary:** The mutant was <span style="color:green"><u>killed</u></span>. The test ```rangesAreEqual()``` detected and killed the mutation since a argument of type Range.class was sent to the equals method. In the regular code this resulted in a check to see if the argument's lower and upper bounds were equivalent to the 'this' range. For this test, the check should return true, but with the mutant code it would automatically always return false which is the unexpected behaviour that was detected.<br/>

### **Mutant 10**<br/>
**Line:** 448 in ```isNaNRange()``` method <br/>
**Orignial Code:** ```return Double.isNaN(this.lower) && Double.isNaN(this.upper)```<br/>
**Mutated Code:** ```return Double.isNaN(-(this.lower)) && Double.isNaN(this.upper)```<br/>
**Summary:** The mutant <span style="color:red"><u>survived</u></span>. None of the tests for the isNaNRange() method are able to detect this mutation since the negation does not affect the overall boolean being returned. If the value of this.lower is already NaN, the negation will result in a NaN value, so nothing changes. If the value of this.lower is instead a double, the negation will simply result in a different double. This means that in either case the Double.isNaN() method will result the same boolean even after the negation. This means the method isNaNRange() is still acting as expected.<br/>

# Report all the statistics and the mutation score for each test class

# Analysis drawn on the effectiveness of each of the test classes

# A discussion on the effect of equivalent mutants on mutation score accuracy

# A discussion of what could have been done to improve the mutation score of the test suites

# Why do we need mutation testing? Advantages and disadvantages of mutation testing

# Explain your SELENUIM test case design process
For our test case design process, we wanted to give each group member a chance to play with the Selenium IDE, so long as they tested 2 major functionalities of the website. We chose to test the IKEA website (https://www.ikea.com/) and some of the targeted functionality included Logging in, Adding to cart, adding to wishlist, and searching for products (alongside some others). Although each group member was allowed to explore the Selenium IDE freely, they were still tasked to functionality that would be utilized most by common users of the website. The follow table shows a list of the test cases as they appear on Selenium (in the submitted .SIDE files) alongside the group member who performed the respective tests. 

| Group Member | Test Case Name                            |
| ------------ | ----------------------------------------- |
| Ethan        | TC#1: Adding to and Viewing Wish List     |
| Ethan        | TC#2: Change Language to French           |
| Jesse        | TC#3: Adding Items to Cart                |
| Jesse        | TC#4: Category Browsing                   |
| Aaron        | TC#5: Login                               |
| Aaron        | TC#6: Search Item                         |
| Avijot       | TC#7: Creating/Adding to Custom Wish List |
| Avijot       | TC#8: Removing From Shopping Cart         |

# Explain the use of assertions and checkpoints
The purpose of using assertions and checkpoints during testing in SELENIUM IDE is to ensure we have an automated way to test the functionality. Assertions/Checkpoints can act as "Verification points" at which the IDE will test a specific condition, if the condition fails, the test will fail. Some points where we used assertions included checking whether or not a specific value existed on the page, or whether a text field was indeed editable. By using these features of the IDE, we were able to automate our testing further in that we could rely on the IDE to let us know when the test failed, and exactly what caused the failure. Checkpoints, like assertions, are essentially "true or false" checkers, however checkpoints are more specific in the fact that they compare specific values. For example, our "Change Language to French" test, we were able to comapre the "Select Store" button and see if it did indeed change to french ("Choisir un magasin"). These can prove to be especially useful when it comes to UI testing with SELENIUM as you can simple record the steps for a test, and add an asserrtion mid recording, this will now behave as an automated assertion or checkpoint whenever the test is re-run. 
# How did you test each functionaity with different test data

# Discuss advantages and disadvantages of Selenium vs. Sikulix

# How the team work/effort was divided and managed
In this lab, we yet again implemented pair programming in order to ensure that everyone got a chance to look through everything. Ethan and Avi were in a pair where Ethan took charge on the Mutation tests and Avi led on the SELENIUM tests. Jesse and Aaron were the other pair and in the same way, Jesse led on the Mutation tests whereas Aaron spearheaded the SELENIUM tests.

# Difficulties encountered, challenges overcome, and lessons learned
Selenium IDE is a powerful tool for automating web application testing, but it can also present some significant challenges. One of the biggest obstacles that we would often encounter was that the IDE would crash unexpectedly, causing frustration and delays in the testing process. One simple test case would take up to 2 hours since the program would crash the website with every run, this led to a lot of "debugging" (restarting the program) and a lot of unresolved issues still up tp the night before the demo. 
# Comments/feedback on the lab itself
Overall we felt that this lab was informative on the advantages and disadvantages of mutation testing, as well as getting to understand UI testing. The instructions in the lab could be a little bit better presented as setting up the project was quite difficult.