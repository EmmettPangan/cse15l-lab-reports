# Lab Report 5
By: Emmett Pangan

## The `bash` Autograder Script

```
CPATH='.;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar'

rm -rf student-submission
git clone -q $1 student-submission

if [[ ! -f student-submission/ListExamples.java ]]
then
    echo "ListExamples.java not found"
    echo "GRADE: 0.00%"
    exit 1
fi

cp TestListExamples.java student-submission
cd student-submission
javac ListExamples.java

if [[ $? != 0 ]]
then
    echo "ListExamples.java failed to compile"
    echo "GRADE: 0.00%"
    exit 1
fi

javac -cp $CPATH TestListExamples.java
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > results.txt
cat results.txt

if grep -qE "OK \([0-9]+ test[s]?\)" results.txt
then
    echo "GRADE: 100.00%"
    exit 1
fi

numTests=`grep -oE "Tests run: [0-9]+," results.txt | grep -oE "[0-9]+"`
numFailures=`grep -oE "Failures: [0-9]+" results.txt | grep -oE "[0-9]+"`
numSuccesses=`expr $numTests - $numFailures`

if [[ $numTests -eq 0 || $numSuccesses -eq 0 ]]
then
    echo "GRADE: 0.00"
    exit 1
else
    grade=`expr 10000 \* $numSuccesses`
    grade=`expr $grade / $numTests`
    len=`expr length $grade`
    decimalIndex=`expr $len - 2`
    grade=`expr $grade / 100`.`expr substr $grade $decimalIndex 2`%
    echo "GRADE: $grade"
    exit 1
fi
```

## Explanation of the Script
```
CPATH='.;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar'
```
We assign the class path for JUnit testing to a variable called `CPATH`. We will use this variable to compile and run our tests later.

---
```
rm -rf student-submission
git clone -q $1 student-submission
```
First, we remove any existing `student-submission` directory so that everything from previous runs of the autograder is cleared. With the `git clone` command, we take in a command line argument for a link to the student's respository and clone it to a directory called `student-submission`. The `-q` option suppresses the output from the `git clone` command since we don't need that for the autograder.

---
```
if [[ ! -f student-submission/ListExamples.java ]]
then
    echo "ListExamples.java not found"
    echo "GRADE: 0.00%"
    exit 1
fi
```
This block of code checks to make sure that the correct Java file, `ListExamples.java` exists in the `student-submission` directory. If `ListExamples.java` is not found in the `student-submission` directory, then the autograder will indicate that `ListExamples.java` is not found, assign a grade of 0 for the student, and exit. If `ListExamples.java` is found in the `student-submission` directory, then the autograder will proceed to the rest of the script.

---
```
cp TestListExamples.java student-submission
cd student-submission
javac ListExamples.java
```
Next, we copy our JUnit testing file, `TestListExamples.java` into the `student-submission` directory so that all of the relevant files are in one place. After that, we change our working directory to the `student-submission` directory, which now houses all of the files we need. Lastly, we compile the student's `ListExamples.java` file.

---
```
if [[ $? != 0 ]]
then
    echo "ListExamples.java failed to compile"
    echo "GRADE: 0.00%"
    exit 1
fi
```
This block of code checks whether the previous command returned an error (`$? != 0` will only be true if there was an error, since a status code of 0 means that the command executed properly). More specifically, since the previous command compiled the student's `ListExamples.java` file, we are checking for a compile error. If there was a compile error, then the autograder will indicate that there was a compile error, assign a grade of 0 for the student, and exit. If there was not a compile error, then the autograder will proceed to the rest of the script.

---
```
javac -cp $CPATH TestListExamples.java
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > results.txt
cat results.txt
```
The first line compiles our JUnit testing file. The second line executes our JUnit tests and stores the output in a text file called `results.txt`. Both of these lines use the `CPATH` variable that was created at the very beginning of the script to find the required files for compiling and running JUnit tests. The last line prints the contents of `results.txt`, which is useful for the student to see which tests they passed and failed.

---
```
if grep -qE "OK \([0-9]+ test[s]?\)" results.txt
then
    echo "GRADE: 100.00%"
    exit 1
fi
```
This block of code checks to see if the results from running the JUnit tests contain the regular expression `"OK \([0-9]+ test[s]?\)"`, which matches the JUnit output when all tests are passed. The `-q` option suppresses the output of this `grep` command since we are not interested in the location of the match. The `-E` option allows the `grep` command to process extended regular expressions, which are needed for proper matching. If all tests are passed (that is, the regular expression is matched), then the autograder will indicate a grade of 100 and exit. If not all tests were passed, then the autograder will proceed to the rest of the script.

---
```
numTests=`grep -oE "Tests run: [0-9]+," results.txt | grep -oE "[0-9]+"`
numFailures=`grep -oE "Failures: [0-9]+" results.txt | grep -oE "[0-9]+"`
numSuccesses=`expr $numTests - $numFailures`
```
The first line is used to extract the total number of JUnit tests that were run. The second line is used to extract the number of JUnit tests that failed. For both of these, we use chained `grep` commands with regular expressions to match and return the values that we are interested in from the `results.txt` file. The `-o` option in the `grep` command returns the matching string. The `-E` option allows the `grep` command to process extended regular expressions, which are needed for proper matching. Finally, the third line uses the `expr` command to calculate the number of JUnit tests that succeeded. All of these values are assigned to variables to be used for grade calculation.

---
```
if [[ $numTests -eq 0 || $numSuccesses -eq 0 ]]
then
    echo "GRADE: 0.00"
    exit 1
else
    grade=`expr 10000 \* $numSuccesses`
    grade=`expr $grade / $numTests`
    len=`expr length $grade`
    decimalIndex=`expr $len - 2`
    grade=`expr $grade / 100`.`expr substr $grade $decimalIndex 2`%
    echo "GRADE: $grade"
    exit 1
fi
```
This block of code first checks whether 0 tests were run or 0 tests were passed. In either case, the autograder assigns a grade of 0 and exits. Otherwise, we calculate the grade of the student's submission up to two decimal places. First, we multiply the number of successes by 10000 and divide it by the number of tests. This yields the percentage grade of the student times 100. To convert this value to the actual percentage grade to two decimal places, we use the `expr` command to find the proper index to split the number and insert a decimal point. Once this has been calculated, the autograder indicates the grade of the student and exits. 

## Examples of Running the Script
<img width="480" alt="image" src="https://user-images.githubusercontent.com/110417473/224874261-a246d8f7-6369-4b01-a6fa-97d821e02b17.png">

This submission had a faulty `merge` method and failed the corresponding tests.

---
<img width="410" alt="image" src="https://user-images.githubusercontent.com/110417473/224874689-ec491fd6-a3a0-45d9-9200-6f1e58c60a47.png">
This submission was correct and passed all tests.

---
<img width="432" alt="image" src="https://user-images.githubusercontent.com/110417473/224874931-48af4c08-4dc4-4c4e-8616-bdd6dbe6f71e.png">
This submission had a syntax error and did not compile.

---
<img width="610" alt="image" src="https://user-images.githubusercontent.com/110417473/224875115-c7c7856a-3617-4a09-9d58-77c0c7c8747e.png">

This submission used an incorrect order of arguments to its `filter` method and was not compatible with the tester.

---
<img width="401" alt="image" src="https://user-images.githubusercontent.com/110417473/224875259-9eb48ce0-b90c-4d56-b86d-ed329f02677a.png">
This submission had the correct implementation but saved under a different name than `ListExamples.java`.
