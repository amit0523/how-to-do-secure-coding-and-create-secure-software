
**How to do secure coding and create secure software.**
----

I can do secure coding and no one can hack my code unless the language/OS have
some issues. You can challenge me on this.

Ultimately, all software boil down to functions/methods. If functions/methods
are secure then the whole software is secure.

Now, in the following text, the word function will mean both function and
method.

I am listing the four main points of secure coding below. These points are
applicable to almost all languages.

1. The first point is that all the arguments to your function should be checked
always whether they are in the allowed range or not, even if your function is
called from other trusted functions and even if your function is
private/protected or static. The value of a function argument should not be
unbounded, it should be within a bounded range. For example, you can specify
that the string argument accepts at most 1024 characters. And then you have to
check whether the length of the string is less than or equal to 1024 or not
(for this, you will have to write your own strlen() function, you can't depend
on the strlen() function of any library because the library's version will keep
counting until it finds '\0' character and by then your program may crash).
If you are using C language then you can use strnlen() function. The code will
be "len = strnlen(str, 1025); if (len >= 1025) { return error; }". Similarly,
your 'int' arguments, 'float' arguments, etc. should also have a bounded range.
Also, always check a pointer argument whether it is NULL or not.

Now, a counterpoint can be that checking all the function arguments will
take more time but actually because of very fast processors available these
days, it will not take noticeable time. On a 1 GHz processor, you can execute
1 Gig (2^30 or 10^9 for simplicity) instructions per second. So, if you are
checking a pointer for NULL then it will be around 5 instructions. So, this
will take only 5 nanoseconds (5 * 10^-9 seconds). So, time consumed in checking
arguments is not a big issue. Checking the length of a string may take some more
time but it will also be not noticeable. Assuming 5 instructions for checking
for NULL character ('\0') and 1 instruction for incrementing the len variable
and another 5 instructions for comparing the len variable to the MAX string len,
then we have 11 instructions per character. If the length we want to check is
1000 then it will be 11,000 instructions and it will take only 11 microseconds
(11 * 10^-6 seconds). So, this time is also not noticeable.

2. Avoid using global variables. In object oriented languages avoid using public
variables as much as possible. In C language also you should avoid global
variables, but in case you need to use some, then make them 'static' so that
they are not visible outside the file.

3. Don't expose all functions to the user. Expose only those functions that the
user will actually need, rest of the functions should be private/protected in
object oriented languages and static in C language.

4. Initialize all variables (global/local/private/protected/public) to proper
values (in C/C++ uninitialized global and static variables are automatically
initialized to 0).

In my opinion, if you follow these points then your functions/software will be
secure. I follow these points and my functions/software are fully secure, they
can't be hacked.

----
