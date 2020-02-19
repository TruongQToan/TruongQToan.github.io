---
layout: post
title: Questions to always keep in mind when you are programming  
tags: [software_engineer, brief_code]
comments: true
---

Asking questions is a very important skill. If you want to get better at everything, you have to ask a lot of questions. For a guideline of how to ask the right questions, check out the excellent book ``What smart students know`` by *Adam Robinson*. Programmers are not exceptions. They need to ask multiple questions when they write code, design a system or when they need to follow a tutorial... But what are the questions to ask? In my opinion, there are two questions (in general form) that stand out as the most important questions every programmer has to keep in mind when they are doing a technical work. What are they?  
1. **What if?**  
2. **What to do to make this better?**  
The *What if?* question is related to the edge cases. The difference between great and mediocre programmers is that great programmers care about edge cases. For example, whenever you write a function that receives parameters, you should consider the special cases of the function. For example, in `Go`, `C`, `C++`, sometimes you need to pass a pointer to a function. So in those cases, you must ask `What if the pointer is a null pointer?`. Or when you write a function that works with natural numbers, you must ask `What if the user pass a negative integer?`. A special case of `What if?` is `What if this change?`. Never assume that the specification will stay the same. You should think far in the future and consider all the changes that may happen. However, if the change is too big and not very important now, it may be not need to add to the code now. The point is, you should think about the changes in the future and that question is the trigger to start thinking about that.  
The other question is about the performance and the beauty of your code. After finishing a coding task, don't just stop there. Think about how to make the code more elegant or run faster. Try to spot the `pain-point` in your code and research the ways to get rid of them. Google it, or just ask your senior teammates. Remember to aim for higher bar and do not complacent.
