# linux-labs
Where I'll put stuff about learning linux administration
______________________________________________________________
1) Base Linux commands :
pwd : where am I
cd : change directory
ls : list directories // options : -a (all) -l (details) -r (reverse order)
touch : change time stamps or create an empty file // if used on a existing file, it will update its time stamp. (touch myfile.txt) // touch -r : matches timestamp from one file to another / touch -d : sets a specific date ( touch -d "2023-01-01 12:30:00" mysuperduperfile )
file : gives you a description of a given file contents
cat : concatenate : displays the content of a file in the terminal // can combine , concatenate multiple files and display their combined output : ex cat file1.txt file2.txt / options : -n numbers the lines -b numbers only the non empty lines
less : displays text in a paged format allowing navigation : usefull for long text to display in the terminal : options, page up page down / up down to navigate, g to go to start G to go to end h for help /search_term to search in the text n for next occurence q to quit
history : displays a history of commands previously entered in the shell // delete a specific entry : -d #line
clear : clears the shell
cp (copy) copies a file : ex cp myfile /home/user/Documents/myfile_backup // -r for recursive copiying (a whole dir for example) or using wildcards * or ? to match a character to select multiple files to copy -i for interactive copy to prevent file overwriting -p to preserve attributes
mv (move) moves a file : mv file2 /home/user/Documents // to specify targer directory first : mv -t /somedirectory file_1 file_2 // to rename a file mv oldfile newfile // -i for interactive -b for backup -v for verbose
mkdir : creates a directory, you can also use mkdir -p books/hemmingway/favorites to create nested directories
rm (remove) : removes a file (rm file1) // -r for recursive, -f for forced this command can be dangerous (famous rm -rf (recursive+forced deletion) - safety mesures : -i // use rmdir for empty directories
find : used to find a file find /home -name puppies.jpg you can also specify the name and type : find /home -type d -name MyFolder
help : displays help about a command ex "help echo" or "ls --help" for executable programs
man : displays the manual for a command : man ls
whatis : displays a quick explanation for a command usage (ex whatis cat)
alias : to create a shortcut for a command (ex cl for clear) : alias cl='clear' but this info will be lost once logged out. To make the shortcut permanant, you need to write the command in the .bashrc file found at the root of the system
exit : to exit the terminal

2) User management & permissions :
chmod : modifies permissions for a file :
> Symbolic (Granular modification) : u=user(owner) g=group o=others a=all // for example, to add execute permission for a user on a file : chmod u+x myfile // to remove chmod u-x myfile // you can also bulk it : user + group writing permission exemple : chmod ug+w myfile
> Numerical change : 4=Read 2=Write 1=Execute / Then you use and add these number to fill the three u'g'o' slots : for example, for the rwx for the user (owner of the file) permission (4+2+1 =7) so you would write 7 at the user slot
for example : chmod 755 myfile : user gets rwx, group read and execute, user read and execute. // Always apply the principle of least privilege, to prevent giving full access to everyone.

chown : modifies ownership permissions on files :
>sudo chown gandalf myfile : changes the owner of the file to user gandalf.
>sudo chgrp wizards myfile : changes the group ownership of the file
>sudo chown gandalf:wizard myfile : changes the ownership of both the user and group

umask : modify the default permissions of created files :
Defines the default set of permissions of created files, by creating a mask. So it will be used like the numerical change of chmod but in reverse :
for example, for a file with a permission of 777, umask022 will get the permission of 755 which is more secure.

Setuid : allows a user to run a program as the owner of the program file rather than as themselves
Symbolic : sudo chmod u+s myfile
Numerical : sudo chmod 4755 myfile  - SUID is a 4 that is placed before the permission set

Setgid : same principle as the Setuid for groups :
Symbolic : sudo chmod g+s myfile
Numerical : sudo chmod 2555 myfile. - SGID is a 2 placed before the permission set

Stickybit : Permissions applied to a directory to ensure that files in that directory can only be deleted or renamed by their owners. Very usefull for shared directories / working spaces.
Symbolic : chmod +t my_shared_dir
Numerical : chmod 1755 my_shared_dir - Stickybit is a 1 placed before the permission set



