---
title: Chinese Chess Conclusion
date: 2021-01-02 23:41:28
tags:
- Project Conclusion
categories:
- [Project Conclusion]
---

1.Alpha-Beta Search

Understand this algorithm in this way

First is a question --- how computer know the best move?

Answer: This algorithm will evaluate the score, which represent the chance the computer will win

So the best move is the move that make the highest score

Second question --- how computer know to protect it's King?

Answer: This algorithm will simulate the move for both red and black

and it will simulate at least 2 depth, the algorithm will do the things follow:

evaluate the current score then start to search (simulate)

Simulate① -- computer legal move "A"

Keep on simulate② -- people legal move "B"

When reach the depth, start to evaluate the score again

If Simulate② make the score reduce,

Which means that the computer's Simulate① move "A" makes computer be in dangerous

And computer will avoid this kind of move

That's why computer knows to protect it's King

If it's King is killed, it's score will be super low

Then the algorithm will tell the computer do not move in that way

So that avoid the King be killed

I learn the implement of the algorithm from this [github project](https://github.com/dengl11/ChineseChessAI)

---

2.Object Oriented is a very idea

It's the project will be pretty clear when you encapsulate the relative functions in a .py file as a class

---

3.Cooperation 

The most important thing is responsibility

Then is the ability to solve the problem

---

4.Refactor

If you always think implement first and refactor in the end

The refactor will be pretty pretty hard

The best solution is do the refactor job when you are coding

And remember, don't straightly coding

Think more about efficiency, readability, maintainability

---

5.Record

It's a good habit to record the bug when you meet with it

 And you can create two files

"Bugs" record the bug waiting for solving

"Solved Bugs" record the bug and the solution

Maybe you can record other things more than bug

Whatever, it's a good habit

---

6.Rest

Do not keep coding for a long time

It's will make you brain numb

And the efficiency will be lower

---

7.Intresting Experience

When the .txt file is big enough

It will cost a long time to open the file

You will think "Wow ! My computer can't even deal with a txt file"

And when you trying to modify some contents

It also cost a long time ! Haha

---

8.Debug

With a long time apart with C and C++

I almost forget the efficient way to find a bug --- "Debug"

 Step by step, checking the variable to find the bug