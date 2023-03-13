# Lab Report 5
By: Emmett Pangan

## The `bash` Grading Script

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

### Explanation
```
CPATH='.;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar'
```
We assign the class path for JUnit testing to a variable called `CPATH`. We will use this variable to compile and run our tests.

```
rm -rf student-submission
git clone -q $1 student-submission
```
First, we remove any existing `student-submission` folder and its contents so that we can create a new one. Using the `git clone` command, we take in the command line argument
