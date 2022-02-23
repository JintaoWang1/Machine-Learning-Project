**SENG 637 - Dependability and Reliability of Software Systems**

**Lab. Report \#2 – Requirements-Based Test Generation**

| Group \#:  28   |   |
|-----------------|---|
| Student Names:  |   |
| yuhua guo       |   |
| Pang-Cheng Chang               |   |
| Jintao Wang                 |   |
| Misagh Ishani                 |   |

# 1 Introduction

From chapter 3 and 4, we have learnt how to design and develop test cases using JUnit and JMock on a black-box SUT. Since all group members do not have previous experience with unit testing, this lab would be a good chance to:

To develop automated test code in JUnit and other XUnit testing frameworks such as NUnit, CSUnit, PHPUnit etc.
To utilize and work with mock objects in test-code development.

As being said, We will use Junit 4 and JMock for this testing assignment


# 2 Detailed description of unit test strategy
We will create tests cases to cover the all 5 methods in `org.jfree.data.DataUtilities` class and 5 out of 15 methods in `org.jfree.data.Range` class which including:

-shift(Range base, double delta, boolean allowZeroCrossing)

-isNaNRange()

-expandToInclude(Range range, double value)

-combineIgnoringNaN(Range range1, Range range2)

-intersects(double b0, double b1) 

For each SUT(method), we will use the following test-case design techniques to develop test cases: 
- Equivalence class testing(ECT)
- Boundary value analysis(BVT)
- Robustness testing
- Worst case testing(WCT)


## Input partitions - DataUtilities class
- `calculateColumnTotal(data: Values2D, column: int): double`

  |  | P1, invalid | P2, invalid | P3, valid | P4, invalid | P5, invalid | P6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | column index | -inf ~ Integer.MIN_VALUE - 1 | Integer.MIN_VALUE ~ -1 | 0 ~ data.getColumnCount() - 1  | data.getColumnCount() ~ Integer.MAX_VALUE | Integer.MAX_VALUE + 1 ~ +inf | NaN |

- `calculateRowTotal(data: Values2D, row: int): double`

  |  | P1, invalid | P2, invalid | P3, valid | P4, invalid | P5, invalid | P6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | row index | -inf ~ Integer.MIN_VALUE - 1 | Integer.MIN_VALUE ~ -1 | 0 ~ data.getColumnCount() - 1  | data.getColumnCount() ~ Integer.MAX_VALUE | Integer.MAX_VALUE + 1 ~ +inf | NaN |

- `createNumberArray(data: double[]): Number[]`

  |  | P1, invalid | P2, valid | P3, invalid | P4, invalid | P5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | element count in double[ ] | 0 | 1 ~ +inf  | (contain null) | (contain NaN) | (not double[] type) |

- `createNumberArray2D(data: double[][]): Number[][]`

  |  | P1, invalid | P2, valid | P3, invalid | P4, invalid | P5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | element count in double[ ][ ] | 0 | 1 ~ +inf  | (contain null) | (contain NaN) | (not double[] type) |

- `getCumulativePercentages(data: KeyedValues): KeyedValues`

  |  | P1-1, invalid | P1-2, valid | P1-3, invalid | P1-4, invalid | P1-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | key | -inf ~ -1 | 0 ~ +inf  | (contain null) | (contain NaN) | (key count does not match value count) |

  |  | P2-1, valid | P2-2, invalid | P2-3, invalid | P2-4, invalid | P2-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | value | -inf ~ +inf | (contain blank)  | (contain null) | (contain NaN) | (key count does not match value count) |

## Input partitions - Range class
- `combine(range1: Range, range2: Range): Range`

  |  | P1-1, invalid | P1-2, valid | P1-3, invalid | P1-4, invalid | P1-5, valid | P1-6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | range1 | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | (contain null) | null | (contain NaN) |

  |  | P2-1, invalid | P2-2, valid | P2-3, invalid | P2-4, invalid | P2-5, valid | P2-6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | range2 | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | (contain null) | null | (contain NaN) |
- `expandToInclude(range: Range, value: double): Range`

  |  | P1-1, invalid | P1-2, valid | P1-3, invalid | P1-4, invalid | P1-5, valid | P1-6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | base | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | (contain null) | null | (contain NaN) |

  |  | P2-1, invalid | P2-2, valid | P2-3, invalid | P2-4, invalid | P2-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | delta | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | null |  NaN |

- `IsNanRange(lowerbounnd: double, upperbound: double): Boolean`

   |  | P1-1, invalid | P1-2, valid | P1-3, invalid | P1-4, invalid | P1-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | lowerbounnd | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | null |  NaN |

    |  | P2-1, invalid | P2-2, valid | P2-3, invalid | P2-4, invalid | P2-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | upperbound | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | null |  NaN |


- `shift(base: Range, delta: double): Range`

  |  | P1-1, invalid | P1-2, valid | P1-3, invalid | P1-4, invalid | P1-5, valid | P1-6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | base | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | (contain null) | null | (contain NaN) |

  |  | P2-1, invalid | P2-2, valid | P2-3, invalid | P2-4, invalid | P2-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | delta | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | null |  NaN |
- `constrain(value: double): double`

  |  | P1-1, invalid | P1-2, valid | P1-3, invalid | P1-4, invalid | P1-5, valid | P1-6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | this | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | (contain null) | null | (contain NaN) |

  |  | P2-1, invalid | P2-2, valid | P2-3, invalid | P2-4, invalid | P2-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | value | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | null |  NaN |
- `contains(value: double): boolean`

  |  | P1-1, invalid | P1-2, valid | P1-3, invalid | P1-4, invalid | P1-5, valid | P1-6, invalid |
  | --- | --- | --- | --- | --- | --- | --- |
  | this | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | (contain null) | null | (contain NaN) |

  |  | P2-1, invalid | P2-2, valid | P2-3, invalid | P2-4, invalid | P2-5, invalid |
  | --- | --- | --- | --- | --- | --- |
  | value | -inf ~ Double.MIN_VALUE | Double.MIN_VALUE ~ Double.MAX_VALUE  | Double.MAX_VALUE ~ +inf | null |  NaN |
# 3 Test cases developed
Each test case will cover one or more test-case design techniques, which are denoted with:

Test cases impelemented are to test the functionality of the methods in normal usage conditions. The test cases listed below are the full test casses that could be performed for a more thorough testing of the funciton. Most would not be necessary due to the method class parameters would throw an error if an invalid input is used. 

## Test cases - DataUtilities class
- `calculateColumnTotal(data: Values2D, column: int): double`
  
  | Case | Input of `column` variable | Partitions covered | Techniques covered|
  | --- | --- | --- | --- |
  | C1 | Integer.MIN_VALUE - 1 | P1 | BLB, Weak-robust ECT |
  | C2 | -1 | P2 | BLB, Weak-robust ECT |
  | C3 | 0 | P3 | LB, Weak-robust ECT |
  | C4 | data.getColumnCount() % 2 | P3 | Weak-robust ECT |
  | C5 | data.getColumnCount() - 1 | P3 | UB, Weak-robust ECT |
  | C6 | data.getColumnCount() | P4 | AUB, Weak-robust ECT |
  | C7 | Integer.MAX_VALUE + 1 | P4, P5 | AUB, Weak-robust ECT |
  | C8 | 'a' | P6 | Weak-robust ECT |

- `calculateRowTotal(data: Values2D, row: int): double`

  | Case | Input of `row` variable | Partitions covered | Techniques covered|
  | --- | --- | --- | --- |
  | C1 | Integer.MIN_VALUE - 1 | P1 | BLB, Weak-robust ECT |
  | C2 | -1 | P2 | BLB, Weak-robust ECT |
  | C3 | 0 | P3 | LB, Weak-robust ECT |
  | C4 | data.getColumnCount() % 2 | P3 | Weak-robust ECT |
  | C5 | data.getColumnCount() - 1 | P3 | UB, Weak-robust ECT |
  | C6 | data.getColumnCount() | P4 | AUB, Weak-robust ECT |
  | C7 | Integer.MAX_VALUE + 1 | P4, P5 | AUB, Weak-robust ECT |
  | C8 | 'a' | P6 | AUB, Weak-robust ECT |
  
- `createNumberArray(data: double[]): Number[]`
  
  | Case | Input of `data` variable | Partitions covered | Techniques covered|
  | --- | --- | --- | --- |
  | C1 | [] | P1 | LB, Weak-robust ECT |
  | C2 | [1, 2, 3] | P2 | Weak-robust ECT |
  | C3 | [1, 2, null] | P3 | Weak-robust ECT |
  | C4 | [1, 2, a] | P4 | Weak-robust ECT |
  | C5 | 1 | P5 | Weak-robust ECT |
  
- `createNumberArray2D(data: double[][]): Number[][]`
  
  | Case | Input of `data` variable | Partitions covered | Techniques covered|
  | --- | --- | --- | --- |
  | C1 | [] | P1 | LB, Weak-robust ECT |
  | C2 | [[1, 2, 3], [4, 5, 6], [7, 8, 9]] | P2 | Weak-robust ECT |
  | C3 | [[1, 2, null], [4, 5, 6], [7, 8, 9]] | P3 | Weak-robust ECT |
  | C4 | [[1, 2, a], [4, 5, 6], [7, 8, 9]] | P4 | Weak-robust ECT |
  | C5 | 1 | P5 | Weak-robust ECT |

- `getCumulativePercentages(data: KeyedValues): KeyedValues`
  
  Since the KeyedValues object is to be mocked by JMock, there is no point to try all combinations of key and value pair
  to cover all partition combinations. We will use weak ECT and only implement a few combinations instead.

  | Case | Key-value pair in `data` | Partitions covered | Techniques covered|
  | --- | --- | --- | --- |
  | C1 | {-1: 1, 0: 10, 1: 100} | P1-1, P2-1 | BLB, Weak-robust ECT |
  | C2 | {} | P1-2, P2-1 | BLB, Weak-robust ECT |
  | C3 | {0: 1, 1: 10, 2: 100} | P1-2, P2-1 | LB, Weak-robust ECT |
  | C4 | {null: 1, 1: 10, 2: 100} | P1-3, P2-1 | Weak-robust ECT |
  | C5 | {a: 1, 1: 10, 2: 100} | P1-4, P2-1 | Weak-robust ECT |
  | C6 | {a: b, 1: 10, 2: 100} | P1-4, P2-4 | Weak-robust ECT, WCT |
  | C7 | {0: , 1: 10, 2: 100} | P1-2, P2-2 | Weak-robust ECT |
  | C8 | {0: null, 1: 10, 2: 100} | P1-2, P2-3 | Weak-robust ECT |
  | C9 | {0: a, 1: 10, 2: 100} | P1-2, P2-4 | Weak-robust ECT |


## Test cases - Range class

- `combine(range1: Range, range2: Range): Range`



- `IsNanRange(lowerbounnd: double, upperbound: double): Boolean`
  | Case | lowerbounnd | upperbound | Partitions covered | Techniques covered|
  | --- | --- | --- | --- |  --- |
  | C1 |  Double.MIN_VALUE | 1.5 | P1-1 , P2-2 | LB, Weak-robust ECT |
  | C2 | 1.5 | 1.5 | P1-2, P2-2| Weak-robust ECT |
   | C3 | -1.5 | -1.5 | P1-2, P2-2| Weak-robust ECT |
  | C4 | Double.MAX_VALUE| 1.5  | P1-3, P2-2 |UB, Weak-robust ECT |
  | C5 |  1.5 | Double.Min_value | P1-2 , P2-1 |LB, Weak-robust ECT |
  | C6 | 1.5 | null  | P1-2, P2-4 | ,Weak-robust ECT |
  | C7 |  Double.NaN |  Double.NaN  | P1-6, P2-6 | Weak-robust ECT |


  
- `expandToInclude(range: Range, value: double): Range`

  | Case | range | value | Partitions covered | Techniques covered|
  | --- | --- | --- | --- |  --- |
  | C1 |  Range(1,5 ) | 6.0 | P1-2 , P2-2 | Weak-robust ECT |
  | C2 | Range(1,5)| 0.5 | P1-2, P2-1 |  Weak-robust ECT |
  | C3 | Range(Double.MAX_VALUE , Double.MAX_VALUE)| Double.MAX_VALUE | P1-3, P2-2 |UB, Weak-robust ECT |
  | C4 | Range(Double.MIN_VALUE , Double.MIN_VALUE)| Double.MIN_VALUE | P1-1, P2-1 |LB, Weak-robust ECT |
    | C5 | Range(Double.MAX_VALUE , Double.MAX_VALUE)| 0.5 | P1-3, P2-2 |AUB, Weak-robust ECT |
    | C6 | Range(Double.MIN_VALUE , Double.MIN_VALUE)| -0.5 | P1-1, P2-2 |BLB, Weak-robust ECT |

- `shift(base: Range, delta: double): Range`

  | Case | base | delta | Partitions covered | Techniques covered|
  | --- | --- | --- | --- | --- |
  | C1 |  Range(Double.MIN_VALUE , Double.MIN_VALUE) | 1.5 | P1-1 , P2-2 | LB, Weak-robust ECT |
  | C2 | Range(1,5)| 1.5 | P1-2, P2-2| Weak-robust ECT |
   | C2 | Range(1,5)| -1.5 | P1-2, P2-2| Weak-robust ECT |
  | C3 | Range(Double.MAX_VALUE , Double.MAX_VALUE)| 1.5  | P1-3, P2-2 |UB, Weak-robust ECT |
  | C4 |  Range(1,5) | Double.Min_value | P1-2 , P2-1 |LB, Weak-robust ECT |
  | C6 | Range(1,5)| null  | P1-2, P2-4 | ,Weak-robust ECT |
  | C6 | Range(1,5)| 'b'  | P1-2, P2-5 | Weak-robust ECT |

- `constrain(value: double): double`


  


- `contains(value: double): boolean`



# 4 How the team work/effort was divided and managed

In the stage of developing test cases, we discussed and analyzed the SUT and discussed and assign the test cases to each individuals.

In the stage of writing test scripts for those test cases, we divided the methods in two parts and implemented the script individually. Before combining scripts, we had a meeting to go through all scripts and made necessary adjustments. The test results of all cases impelemetned was also reviewed as a group. 

# 5 Difficulties encountered, challenges overcome, and lessons learned

In this lab, we had diffculties with setting up the test cases. They are hard to design to a level therefore all method functionalities can be fully tested. The lesson that we learned is that the input partitions can really help the process and determining the right tests to run.

It is also really challenging to run the test and check whether all scenerarios are being tested. A simple method with two parameters could have many different test scenarios. The process of impelementing these test scenarios is espically diffcult when classes requires Mocking to be tested thoroughly. 



# 6 Comments/feedback on the lab itself

The detailed descirption of the assignment 2, especially the part 2.1.3, is of greate help to us start on writing test cases using JUnit.
