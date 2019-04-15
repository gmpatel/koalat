## Shell/CLI
1. What is happening in these Linux commands?  Describe as much as you know about what each symbol means and the effect it will have in the execution of the command, and the named programs.

   a) `(for i in {1..100}; do echo $i; done;) | grep 3 | grep -v 1 | paste -s -d+ - | bc`

        From the collection of number from `1 to 100`, `take all` the `numbers having 3` in it and then `remove` the `numbers having 1` in it, then paste all those numbers in line with sign `+` in between and then calculate the equation created.

   b) `[ ! -f /var/lock/myscript.lock ] && touch /var/lock/myscript.lock && (yum -y update >> /var/log/mylog.log 2>&1; ) && rm -f /var/lock/myscript.lock`
        
        If the file `/var/lock/myscript.lock` does not exists, create the file `/var/lock/myscript.lock` and the run the command `yum -y update` and append the output to the log file `/var/log/mylog.log` and then remove the file `/var/lock/myscript.lock`.

        `2>&1` is actually be interpreted as `redirect stderr to a file named 1`. & indicates that what follows is a file descriptor and not a filename. So the construct becomes: 2>&1.

2. There is a directory, containing a large tree of subdirectories and files.  Scattered throughout these files are Australian phone numbers, and we want to harvest them – we want to end up with a simple list of the phone numbers.

   a) Write a regular expression to match Australian phone numbers.  The numbers will be in a mixture of the forms 02xxxxxxxx and +612xxxxxxxx, and there will also be the common usage of hyphens, spaces, and parentheses, so all of those common possibilities must be supported.

    `(?:\+?(61))? ?(?:\((?=.*\)))?(0?[2-57-8])\)? ?(\d\d(?:[- ](?=\d{3})|(?!\d\d[- ]?\d[- ]))\d\d[- ]?\d[- ]?\d{3})`

   b) Write an example phone number, for each specific phone number format that your regex would match.

    ```
    +61(02)89876544
    +61 2 8986 6544
    02 8986 6544
    +61289876544
    0414 570776 
    0414570776
    0414 570 776
    +61 414 570776
    414 570776
    ```

   c) Imagine that the full path of the directory is
   > /var/www/site1/uploads/phnumbers/
   
   Can you write a single-line or simple command that you could run from the shell (ideally Linux), to apply this regular expression to the files in the directory tree, and result in the simple list of phone numbers?  Or describe basically the kind of command you would do, if you don’t know the exact syntax.

    ```
    grep -Eo '^{{expression}}$' /var/www/site1/uploads/phnumbers/
    ```

## Software development

1.	Write a function/method/subroutine to determine if a string starts with an upper-case letter A-Z.

   * Your choice of language
   * Be a bit weird with it - don't just use a "toUpper()" or "isUpper()" function provided by the language

    // C#
    public static class Extensions
    {
        public static bool IsStartsWithUpperCase(this string value)
        {
            if (value != null && value.Length > 0) 
            {
                var firstLetterAscii = (int)value.ToCharArray().First();
                
                if (firstLetterAscii >= 65 && firstLetterAscii <= 90)
                {
                    return true;
                }
            }

            return false;
        }
    }

2. Consider this statement:
   ```
   $a = implode(',',array_map(function($b,$c) {
     return str_replace(array('-','_',','), '', $b) . "x{$c}";
   },array_keys($d),$d));
   ```
    NOTE: Not sure about the answers below as I never worked on PHP so far, just trying to give anwers with instinct.

   a) what language is it written in?

    PHP
   
   b) at the point when this statement is executed, which (if any) pre-existing variable(s) does this statement use or rely on?

    variable `d`

   c) after this statement has executed, which (if any) variable(s) have been initialised or modified by the statement?
   
    variable `a`

   d) taking your answer from b), give simple example value(s) for each used/relied-upon variable.  There is not a single correct answer, rather you should make an educated guess based on your interpretation of what the statement is doing.

    ...

   e) what would be the output or effect of the statement, if you used your example value(s) from d) ?

    It will replace the `-`, `_` and `,` from the given string to `` blank. 

3. Under what circumstances would an application require one or more databases as part of its architecture?

    If the question here is looking/asking for the one ore more instances of the same database, we need more clusters of the same database when we are experiencing the slow system overall and looks like the DB Server is the bottle neck. In this circumstances the good approace is to make load balanced DB Server clusters. These clusters sync with each other when any data changes happens. There is also a possibility of creating more than one read replicas of the DB Server if the high propotion of the queries are select queries.

    If the question here is looking/asking for more than one different databases, there can be many anwers. But the most common answer these days is when we are creating microservices architecture. Microservices should not share common database and they should have their own DB for the business function it is responsible for.

4. When might you use bitwise operations in an application?

5. Describe the main tenets of a microservice.

    * Modular 
    * Event driven or REST
    * Decentralized
    * Independent (No dependency on other services and business functions)
    * Do one thing well (Single business function responsibility)
    * Black box

   a) how would you evaluate between using a monolithic vs microservices architecture?

    You should start converting to microservcies from the outer layer of the monolithic service and continue breaking down the variaous business functions to seperate microservices. This is how you evaluate to microservices architecure from monolithic.
   
6. Describe your favourite design pattern.

**Dependency Injection**

DI is a way of writing a code where all the dependent components of the working class has been injected to the class using constructor and not created within the class itself.

As per the SOLID practices the task for building dependencies for the given class should not be done by that class but should be done by the caller of the given class and the caller should be responsible for constructing the dependencies for the given glass and pass them in to the given class through constructor injection when creating the instance of the given class. DI can be performed at property level as well but the constructor injection is the most common scenario.

DI is most widely used design pattern as it help us lot in making the code more clean, readable and testable.

7. What do you modify an API without breaking backwards compatibility?

Versioning is the best way to modify API without breaking backward compatibility. There are several ways/approaches of applying versioning and several ways/approaches of hitting the different vesions of the same API.