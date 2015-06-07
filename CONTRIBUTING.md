#Contributing Guidelines

##Issues

###Be at the least, mildly civil
Issue reports that start out by rudely throwing blame around are subject to closure.

###Be clear and concise.
State what the issue is from a "whats wrong" prospective.
Bug reports should clearly allow maintainers to understand whats wrong and how to test/reproduce.

##PRs

###Hide something, get rejected.
Your PR should clearly state what it does. Adding unrelated things then never mentioning them will not fool us. In the rare circumstance it does, your PR may still be reverted wholesale once we notice and you will be required to resubmit it without the related thing.
Breaking this rule too many times will lead to a block.
Breaking this rule to attempt to add something that compromises the security of this application will lead to a block and report to github and/or the proper authorities.

###Test it, or risk closure.
PRs with obvious bugs that indicate the user never tested them will be closed unless marked as not yet tested in the body of the PR.

##Style and Code Requirements

###Tabs not spaces
And 1 block level equals 1 tab, no more, no less.
(You may use spaces to align something if you insist, but you must tab to the block level first)

###No duplicated code.
Genericize it into a proc that can be called from multiple places

This makes it easier to change it later, since you have one central place.

###No overriding byond type safety checks.
The use of the : operator to override type safety checks is strongly discouraged.
Exceptions are only made when used in loops that require the performance boast.

###Type paths must began with a /
eg: `/datum/thing` not `datum/thing`

###Datum type paths must began with "datum"
In byond this is optional, but omitting it makes finding object definitions harder.

###All Byond paths must contain the full path.
(ie: absolute pathing)

Byond will allow you nest almost any type keyword into a block, such as:

````
datum
	datum1
		var
			varname1 = 1
			varname2
			static
				varname3
				varname4
		proc
			proc1()
				code
			proc2()
				code
		
		datum2
			varname1 = 0
			proc
				proc3()
					code
			proc2()
				..()
				code
````

The use of this is not allowed in this project as it makes finding definitions via full text searching next to impossible. The only exception is the variables of an object may be nested to the object, but must not nest further.

The previous code made complaint:

````
/datum/datum1
		var/varname1
		var/varname2
		var/static/varname3
		var/static/varname4

/datum/datum1/proc/proc1()
	code
/datum/datum1/proc/proc2()
	code
/datum/datum1/datum2
	varname1 = 0
/datum/datum1/datum2/proc/proc3()
	code
/datum/datum1/datum2/proc2()
	..()
	code
````

###Operators and spaces:
* Operators that should be separated by spaces
	* Boolean and logic operators like &&, || <, >, ==, etc (but not !)
	* Argument separator operators like , (and ; when used in a forloop)
	* Assignment operators like = or += or the like (this can be ignored in forloops)
* Operators that should not be separated by spaces
	* Math operators like + or -
	* Bitwise operators like & or |
	* Access operators like . and :
	* Parentheses ()
	* logical not !
(this is not strictly enforced, but more a guideline for readability's sake)
	
###Control statements:
(if,while,for,etc)

* All control statements must have a space before the expression (eg: `if (blah)` not `if(blah)`)
* All control statements must not contain code on the same line as the statement (`if (blah) return`)
* All control statements that mix the use of && and || must use nested parentheses to make it clear to the reader the order it is parsed.
* for loops should use ; not , to separate expressions (eg: `for (var/i=1; i < 10; i++)` not `for (var/i=1,i < 10,i++)`)
* All control statements comparing a variable to a number should use the formula of `thing` `operator` `number`, not the reverse (eg: `if (count <= 10)` not `if (10 >= count)`)

###Use early return.
Do not enclose a proc in an if block when returning on a condition is feasible
This is bad:
````
/datum/datum1/proc/proc1()
	if (thing1)
		if (!thing2)
			if (thing3 == 30)
				do stuff
````
This is good:
````
/datum/datum1/proc/proc1()
	if (!thing1)
		return
	if (thing2)
		return
	if (thing3 != 30)
		return
	do stuff
````
This prevents nesting levels from getting deeper then they need to be.

###When adding new tcl commands, attempt to have it reuse any already existing tcl command in its internals.
For example, If you were implementing the if command, you would have it send the conditional expression to the expr tcl command, rather then try code the code to evaluate it yourself or sending it to the same internal proc that expr uses.


--More to come--
