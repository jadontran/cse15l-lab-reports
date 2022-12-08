# Week 9 Lab Report

## Grading Script

```
rm -rf stderr.txt
rm -rf student-submission
git clone $1 student-submission
cd student-submission

CPATH=".:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar"

echo

if  ! [[ -e ListExamples.java ]]

	then
		echo "ListExamples.java is not found!"
		exit 1

	else
        echo "ListExamples.java is found!"
        cp ListExamples.java ./../
		cd ..
		javac -cp $CPATH *.java 2> stderr.txt
fi

echo

[ -s stderr.txt ]

if ! [[ $? -eq 0 ]]

then
	echo "Compile error!"
	exit 1

else
	echo "Compile success!"
fi

javac -cp $CPATH *.java
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > stdout.txt

FILTERTESTS=$(grep -c ".filter(" TestListExamples.java)
MERGETESTS=$(grep -c ".merge(" TestListExamples.java)

FILTER=$(grep -c "testFilter" stdout.txt)
MERGE=$(grep -c "testMerge" stdout.txt) 
FILTERPASSED=$(($FILTERTESTS-$FILTER/2))
MERGEPASSED=$(($MERGETESTS-$MERGE/2))

echo
echo "Score: $FILTERPASSED out of $FILTERTESTS tests passed for filter() method!"
echo
echo "Score: $MERGEPASSED out of $MERGETESTS tests passed for merge() method!"
exit
```

## Student Submission Examples

### List Methods Corrected
![Image](CorrectStudentSubmission.png)

This submission has the proper methods, therefore it will return a perfect score.

### List Methods Compile Error
![Image](CompileError.png)

This submission has a syntax error of missing a semicolon in a line, therefore it will simply return a "Compile error!" statement.

### List Methods Filename
![Image](FileNotFound.png)

This submission has the correct file with the wrong name, therefore it is not found and will return a "ListExamples.java is not found!" statement.

## Tracing Student Submission (Filename)

* Line 3 : 
    stdout = N/A
    stderr = N/A
    return code = 0
* Line 4 : 
    stdout = N/A
    stderr = N/A
    return code = 0
* Line 5 : 
    stdout = N/A
    stderr = Cloning into ‘student-submission' . . .
    return code = 0
* Line 6 : 
    stdout = N/A
    stderr = N/A
    return code = 0
* Line 12 : The condition was false because the submission gave the file the wrong name. Thus, no "ListExamples.java" file was found.
* Line 15 :  
    stdout = ListExamples.java is not found!
    stderr = N/A
    return code = 0
* Line 16 :
    stdout = N/A
    stderr = N/A
    return code = 1
* Lines 17-54 : These lines will not run because there is an early exit on Line 16 after it fails to detect a ListExamples.java file.