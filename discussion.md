# Discussion and Reflection


The bulk of this project consists of a collection of five
questions. You are to answer these questions after spending some
amount of time looking over the code together to gather answers for
your questions. Try to seriously dig into the project together--it is
of course understood that you may not grasp every detail, but put
forth serious effort to spend several hours reading and discussing the
code, along with anything you have taken from it.

Questions will largely be graded on completion and maturity, but the
instructors do reserve the right to take off for technical
inaccuracies (i.e., if you say something factually wrong).

Each of these (six, five main followed by last) questions should take
roughly at least a paragraph or two. Try to aim for between 1-500
words per question. You may divide up the work, but each of you should
collectively read and agree to each other's answers.

[ Question 1 ] 

For this task, you will three new .irv programs. These are
`ir-virtual?` programs in a pseudo-assembly format. Try to compile the
program. Here, you should briefly explain the purpose of ir-virtual,
especially how it is different than x86: what are the pros and cons of
using ir-virtual as a representation? You can get the compiler to to
compile ir-virtual files like so: 

racket compiler.rkt -v test-programs/sum1.irv 

(Also pass in -m for Mac)

Answer: The ir-virtual is a representation of assembly code in a simplified form, making it easier for compilation. It provides a clearer, structured view of the program, making it easier to understand, optimize and transform code. On the other hand, the x86 assembly specifies on specific processor architectures, meanwhile the IR-Virtual is more generic and doesn't require hardware-specific optimizations. A con is that its too simple, and does not provide all the data that might be necessary. You could miss a mov since they are not all visible.

[ Question 2 ] 

For this task, you will write three new .ifa programs. Your programs
must be correct, in the sense that they are valid. There are a set of
starter programs in the test-programs directory now. Your job is to
create three new `.ifa` programs and compile and run each of them. It
is very much possible that the compiler will be broken: part of your
exercise is identifying if you can find any possible bugs in the
compiler.

For each of your exercises, write here what the input and output was
from the compiler. Read through each of the phases, by passing in the
`-v` flag to the compiler. For at least one of the programs, explain
carefully the relevance of each of the intermediate representations.

For this question, please add your `.ifa` programs either (a) here or
(b) to the repo and write where they are in this file.

I created three different .ifa test programs, each testing different math statements. Each one ran smoothly, without any errors.

1)
input: (* (+ 1 2) (+ 3 4))
output: 21
Initially, the equation got simplified in IfArithTiny. Next, it created instructions in Administrative Normal Form (ANF), converted it to a virtual computer code in irv, and lastly compiled into a NASM file that the computer can execute.
2)
input:101
output:101
The input gets goes to ifarith-tiny, turning into a simple argument from, getting sent to ir-virtual which turns it into an assembly.
3)
input: (if 1 
  (print (+ 1 1)) 
  (print (+ 2 2)))
output:#t 
The test example files are placed in the test-program folder: arithExample1.ifa, example2.ifa, example3.ifa

[ Question 3 ] 
Describe each of the passes of the compiler in a slight degree of
detail, using specific examples to discuss what each pass does. The
compiler is designed in series of layers, with each higher-level IR
desugaring to a lower-level IR until ultimately arriving at x86-64
assembler. Do you think there are any redundant passes? Do you think
there could be more?
In answering this question, you must use specific examples that you
got from running the compiler and generating an output.

Input: 101 
Stage 1: Recognizes that the input is 101, which gets imputed into the second stage.
Stage 2: Transforms input into ANF, the output will be (let ([v1 101])
Stage 3: A virtual register is assigned: 'mov-lit v1, 101';
Stage4: Converts virtual registers into x86 registers. 
Step6: Converts x86 into NASM assembly, which leads to the output of 101.

[ Question 4 ] 

This is a larger project, compared to our previous projects. This
project uses a large combination of idioms: tail recursion, folds,
etc.. Discuss a few programming idioms that you can identify in the
project that we discussed in class this semester. There is no specific
definition of what an idiom is: think carefully about whether you see
any pattern in this code that resonates with you from earlier in the
semester.

I noticed various idioms that we learned in class. Firstly, I noticed fold, which is found in one of the last sections of compiler.rkt. Pattern matching also appeared, and it reminded me to the church encoding assigment we did before, where we went case by case to complete different definitions. I also managed to find Lambda calculus being used for  ifarith and ifarith-tiny

[ Question 5 ] 
In this question, you will play the role of bug finder. I would like
you to be creative, adversarial, and exploratory. Spend an hour or two
looking throughout the code and try to break it. Try to see if you can
identify a buggy program: a program that should work, but does
not. This could either be that the compiler crashes, or it could be
that it produces code which will not assemble. Last, even if the code
assembles and links, its behavior could be incorrect.
To answer this question, I want you to summarize your discussion,
experiences, and findings by adversarily breaking the compiler. If
there is something you think should work (but does not), feel free to
ask me.
Your team will receive a small bonus for being the first team to
report a unique bug (unique determined by me).

The bug I found was in the let* function. It displayed a bad syntax error: (not an identifier and expression for a binding), meaning it was a was an unfixed bug. In order to fix it you needed to change the let by adding quasi-quoting. 
Also the compiler.rkt seemed to not support any math signs, such as greater than, less than.

[ High Level Reflection ] 

In roughly 100-500 words, write a summary of your findings in working
on this project: what did you learn, what did you find interesting,
what did you find challenging? As you progress in your career, it will
be increasingly important to have technical conversations about the
nuts and bolts of code, try to use this experience as a way to think
about how you would approach doing group code critique. What would you
do differently next time, what did you learn?

By completing this project, we looked at various topics. We learned the difference between IRV and x86. This is mostly interesting since we get to see a new assembly code which we normally dont interact much, and we haven't interacted at all before. Its a new and interesting way of seeing what is happening behind the scenes from a program. Something else I saw was creating the three practice examples with ifa and running them. We then discovered what they compiled to, either meeting my prediction or completely giving a different result. Something that was a bit confusing initially was the concept of how code is translated in order to make things easier for the computer. I ran into questions, thinking something might get misinterpreted and lead to unpredictable errors. A challenge I found was finishing the coding part of this assignment. I havent used github before, so making sure everything worked accurately was confusing, but I managed to make it work.
