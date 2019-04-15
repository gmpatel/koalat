## Shell/CLI
1. What is happening in these Linux commands?  Describe as much as you know about what each symbol means and the effect it will have in the execution of the command, and the named programs.

   a) `(for i in {1..100}; do echo $i; done;) | grep 3 | grep -v 1 | paste -s -d+ - | bc`
   
   b) `[ ! -f /var/lock/myscript.lock ] && touch /var/lock/myscript.lock && (yum -y update >> /var/log/mylog.log 2>&1; ) && rm -f /var/lock/myscript.lock`


2. There is a directory, containing a large tree of subdirectories and files.  Scattered throughout these files are Australian phone numbers, and we want to harvest them – we want to end up with a simple list of the phone numbers.

   a) Write a regular expression to match Australian phone numbers.  The numbers will be in a mixture of the forms 02xxxxxxxx and +612xxxxxxxx, and there will also be the common usage of hyphens, spaces, and parentheses, so all of those common possibilities must be supported.

   b) Write an example phone number, for each specific phone number format that your regex would match.

   c) Imagine that the full path of the directory is
   > /var/www/site1/uploads/phnumbers/
   
   Can you write a single-line or simple command that you could run from the shell (ideally Linux), to apply this regular expression to the files in the directory tree, and result in the simple list of phone numbers?  Or describe basically the kind of command you would do, if you don’t know the exact syntax.


## Software development

1.	Write a function/method/subroutine to determine if a string starts with an upper-case letter A-Z.

   * Your choice of language
   * Be a bit weird with it - don't just use a "toUpper()" or "isUpper()" function provided by the language

2. Consider this statement:
   ```
   $a = implode(',',array_map(function($b,$c) {
     return str_replace(array('-','_',','), '', $b) . "x{$c}";
   },array_keys($d),$d));
   ```
   a) what language is it written in?
   
   b) at the point when this statement is executed, which (if any) pre-existing variable(s) does this statement use or rely on?
   
   c) after this statement has executed, which (if any) variable(s) have been initialised or modified by the statement?
   
   d) taking your answer from b), give simple example value(s) for each used/relied-upon variable.  There is not a single correct answer, rather you should make an educated guess based on your interpretation of what the statement is doing.
   
   e) what would be the output or effect of the statement, if you used your example value(s) from d) ?


3. Under what circumstances would an application require one or more databases as part of its architecture?

4. When might you use bitwise operations in an application?

5. Describe the main tenets of a microservice.

   a) how would you evaluate between using a monolithic vs microservices architecture?
   
6. Describe your favourite design pattern.

7. What do you modify an API without breaking backwards compatibility?

