# txt2h5p-generator
This repository contains a Python script for generating [H5P](https://h5p.org) [Question-Set](https://h5p.org/question-set) files from a .txt input file. The script deals with the parsing of [Multiple Choice Questions](https://h5p.org/multichoice) with tips and right/wrong answer feedbacks and [Fill in the Blanks Questions](https://h5p.org/fill-in-the-blanks). 

### Notice
The script was adapted and inspired by [Justine Leon A. Uro's](https://github.com/justineuro) work, from the [ h5p-mcq-maker-fb repository](https://github.com/justineuro/h5p-mcq-maker-fb?tab=License-1-ov-file), which is licensed under the Creative Commons Attribution 4.0 International License. The original Bash script was translated into Python, with additional features and customizations built upon the original code foundation.

## Getting Started 
To get a local copy up and running, follow these simple steps.

### Prerequisites
* **Linux Terminal/Command Prompt:** Access is necessary to run the Python script.
* **Python 3.x:** Required for the script to run and can be downloaded from the [official website](https://www.python.org/downloads/).
* **Lumi (Broswer):** It's recommended to create an account on Lumi and use the [browser version](https://lumi.education/en/) to upload and test the generated H5P file. 

### Input File Structure
The plain-text input file contains Multiple Choice and Fill in the Blanks Questions as well as their corresponding answers. In order to understand the structure of this file we can examine the following example. 
```
MCQ: 1. Who of the following is a director? 
Rafael Nadal TIP: Grand Slam. YSEL: Rafael Nadal is a famous tennis player. NSEL: Rafael Nadal is indeed not a director.
Cristiano Ronaldo TIP: UEFA Champions League. YSEL: Cristiano Ronaldo is a famous soccer player. NSEL: Cristiano Ronaldo is indeed not a director.
William Shakespeare TIP: Hamlet, Romeo and Juliet and Macbeth. YSEL: William Shakespeare was a playwright. NSEL: William Shakespeare was not a film director.
*Quentin Tarantino TIP: Pulp Fiction and Kill Bill. YSEL: Correct! Quentin Tarantino is a famous film director. NSEL: Quentin Tarantino is a well-known director.

MCQ: 2. Which of the following is a letter?
*A
2
345
21

FIB: 3. *Paris* is the capital of France. 
```
As you can see, the following characteristics apply: 
1. **MCQ/FIB:** Each questions begins with an abreviation of the question type. MCQ denotes Multiple Choice Questions and FIB denotes Fill in the Blanks Questions. 
2. **Asterisk:** Answers preceded by an asterisk (*) are the correct answers to a Multiple Choice Question. Wrong answers are not indicated by an asterisk. 
3. **TIP/YSEL/NSEL:** TIP provides a hint to quide the user towards to the answer before any MC answer has been selected. YSEL is the feedback for a selected answer option and NSEL is the feedback for a non-selected answer option. These fields are optional and can be used in various combinations, e.g. only TIP, only YSEL, only YSEL and NSEL, all three, none of the three etc. In the second, an example question may look as follows.
```
MCQ: 2. Which of the following is a letter?
*A TIP: YSEL: Correct! NSEL: 
2 TIP: YSEL: This was wrongly selected. NSEL: 
345 TIP: YSEL: This is a number. NSEL: 
21 TIP: YSEL: This is wrong. NSEL: 
```
4. **Double Asterisks:** For Fill in the Blanks Questions, the correct answer within the sentence is surrounded by double asterisks. 

### The Control File
The plain-text control file is already present in the repository and is necessary for configuring the H5P file generation process. It includes some specific parameters and is of the following format. 
```
NAME_H5P: MY-INPUT.h5p
TITLE: "THIS IS THE TITLE"
AUTHOR: "chryysmad"
LICENSE: "ODC PDDL"
INTRODUCTION: "Example of an H5P Question Set."
PASS_PERCENTAGE: 50
DISABLE_BACKWARDS_NAVIGATION: false
RANDOM_QUESTIONS: true
POOL_SIZE: 3
N_QUESTIONS: 3
```
Each parameter has a specific meaning: 
1. **NAME_H5P:** Name of the output H5P file. 
2. **TITLE:** Title of the H5P content to be displayed to the user when they access the H5P file.
3. **AUTHOR:** Name of the author.
4. **LICENSE:** H5P content distribution license.
5. **INTRODUCTION:** Introduction/description of the H5P content.
6. **PASS_PERCENTAGE:** Percentage of correct answers required to pass the quiz.
7. **DISABLE_BACKWARDS_NAVIGATION:** Boolean that indicates whether backward navigation is disabled during the quiz.
8. **RANDOM_QUESTIONS:** Boolean that indicates whether questions are presented in a random order.
9. **POOL_SIZE:** Number of questions to be randomly selected from the pool for the quiz.
10. **N_QUESTIONS:** Total number of questions to be included in the quiz.

### Setting up 
1. Clone the repository.
```
git clone https://github.com/chryysmad/txt2h5p-generator.git
```
2. Create a plain-text file `MY-INPUT.txt` which contains your MCQs and Fill in the Blanks Questions and answers written in the required format (see [Input File Structure](#input-file-structure) section for additional information).
3. Save the input file under the `txt2h5p-generator` directory that you just cloned.
4. Edit the already existing `control.txt` file to set the necessary parameters for your new H5P (see [The Control File](#the-control-file) section for a description of these parameters).

### Running the Script
1. Enter the directory in which the cloned repository is located from your terminal.
```
cd txt2h5p-generator
``` 
2. Run the command.
```
python3 h5p-parser.py control.txt MY-INPUT.txt 
```
where `MY-INPUT.txt` is the input file you created that contains your MCQ and Fill in the Blanks questions and answers.

The newly created H5P file will be found in the `txt2h5p-generator` directory.
