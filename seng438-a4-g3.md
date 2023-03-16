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

# Explain the use of assertions and checkpoints

# how did you test each functionaity with different test data

# Discuss advantages and disadvantages of Selenium vs. Sikulix

# How the team work/effort was divided and managed


# Difficulties encountered, challenges overcome, and lessons learned

# Comments/feedback on the lab itself
