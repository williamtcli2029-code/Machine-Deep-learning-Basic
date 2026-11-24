1. Variable no need to declare type. Interchangeable

2. Docstring, help()-\> return doctring “””DocString”””  
3. 

def mult\_by\_five(x):  
    return 5 \* x

def call(fn, arg):  
    *"""Call fn on arg"""*  
    return fn(arg)

def squared\_call(fn, arg):  
    *"""Call fn on the result of calling fn on arg"""*  
    return fn(fn(arg))

print(  
    call(mult\_by\_five, 1),  
    squared\_call(mult\_by\_five, 1),   
    sep\='**\\n**', *\# '\\n' is the newline character \- it starts a new line*)  
Allowed to directly refer to the name of the function in Python

4. Direct casts  
* **int()** — casts to a whole number: int("13") → 13  
* **float()** — casts to a decimal: float("13.5") → 13.5  
* **str()** — casts to text: str(13) → "13"  
* **bool()** — casts to True or False: bool(1) → True

5. a=3— Optional: default is 3, capable of changing it by daying tosmash(100,5)

def to\_smash(total\_candies,a=3):  
    """Return the number of leftover candies that must be smashed after distributing  
    the given number of candies evenly between 3 friends.  
      
    \>\>\> to\_smash(91)  
    1  
    """  
    return total\_candies % a

\# Check your answer  
q3.check()

6. Indentations are important  
     
7. A list can contain a mix of different types of variables: Function, string, int…

8. List can be accessed from behind:: \-1 is last one  
     
9. Slicing: planet(0:3) is p0,p1,p2, same as planet(:3)   
     
10. Slicing: list\[a:b\] including a but not b,  
      
11.      Lists are MUTABLE  
      
12. Good Stuffs for list: (slicing, min, max, sum, sort)  
      
13. X.y or X.y() like getting variables or getters in Java

14. Adding Items–Append or List.append(a)  
      
15. Deleting items from end: List,pop()

16. List.index(item)--Index

17. Bool returning function: item in list  
      
18. Tuples: created by () List: created by \[\]  
      
19. Tuples ARE NOT MUTABLE:(Immutable), often used as function return value  
      
20. a,b=x.y() as for (a,b)=x.y()  
21. For loops: for i in range, for item in list, for item in tuple  
      
22. IN supports all that can be iterated  
      
23.  

squares \= \[n\*\*2 for n **in** range(10)\]  
squares  
\==  
squares \= \[\]  
for n **in** range(10):  
    squares.append(n\*\*2)  
squares  
short\_planets \= \[planet for planet **in** planets if len(planet) \< 6\]  
short\_planets  
loud\_short\_planets \= \[planet.upper() \+ '\!' for planet **in** planets if len(planet) \< 6\]  
loud\_short\_planets

24. Strings are immutable  
      
25. String to Word list divided by spaces or by other stuff  
      
26. Start with, end with  
      
27. item.join(List)  
      
28. "**{}**, you'll always be the **{}**th planet to me.".format(planet, position)  
    Formatting. Inserting necessary stuff into the line

	  
*\# Referring to format() arguments by index, starting from 0*  
s \= """Pluto's a **{0}**.  
No, it's a **{1}**.  
**{0}**\!  
**{1}**\!""".format('planet', 'dwarf planet')  
print(s)  
	pluto\_mass \= 1.303 \* 10\*\*22  
earth\_mass \= 5.9722 \* 10\*\*24  
population \= 52910390  
*\#         2 decimal points   3 decimal points, format as percent     separate with commas*  
"**{}** weighs about **{:.2}** kilograms (**{:.3%}** of Earth's mass). It is home to **{:,}** Plutonians.".format(  
    planet, pluto\_mass, pluto\_mass / earth\_mass, population,  
)

29. String.format(item 1, item 2, item…….)  
      
30. DIctionary: Key and corresponding value  
      
31. One to one. Key automatically updates if defined 2 times

32.    
    for k **in** numbers:  
        print("**{}** \= **{}**".format(k, numbers\[k\]))

    one \= Pluto

    two \= 2

    three \= 3

eleven \= 11

33. Import A as B, From A import B,C or \*(if \*, then no need to do A.B)  
      
34. TO Avoid problem, only import what’s needed  
    

IMPORTANT SURVIVAL Guide  
\-**type()**  
**\-dir()**  
**\-help()**  
**\-**
