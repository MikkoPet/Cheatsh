# Terminal

## move around
cd (dest)  
. is where we're at rn  
.. is prev folder  
.... is prev prev  
...... etc  

ls lists stuff in current loc  
pwd gives current path  

## create. and delete
mkdir (name) makes a dir  
rmdir (name) removes a dir. ONLY empty  
rm -rf (name) where -rf stands for "recursive folder" will delete a full folder and its contents.  

touch (name) makes any sort of changes to file(name), if there is no file(name) it will create it.  

## check and sort
find can find anything matching specified parametres  
cat (file) prints contents of file in term  

tr helps modifying output to decode, can be appended to cat (or echo or any other command that gets a text output)

        See-> Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi in data.txt

        running cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
        will give The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

        tr interprets a string in 'part1' through the parametres of the 'part2', here, A-Z and a-z indicate alphabetical strings, they are the the og input. N-ZA-M is the expected output of A-Z, meaning each character is moved 13 spots. same applies to a-z into n-za-m

mv (file)[destination] to move file  
cp -r (sourcepath) (destpath) to copy  
grep can find specified strings WITHIN files  
sort grabs the content of a file and orders it  

## Modify

### quick dirty modify
nano (file) will allow modifs of (file) content through terminal  
echo"message">(file) puts the content of "message" as content of (file) (chill for README.md)  

### serious.
code . opens the current dir into VScode  


## NODE & NPM

### npm

package manager  
creates a package.jason listing dependencies  

```
npm init
```

will have to specify
- proj name
- init version
- desc
- main file
- test command
- git repo
- tags
- license  
        will provide default sugg  

```
npm init --yes
```
quick creates the proj with all the default answer values   

#### npm install or npm i 
followed by a package name will install the package  

as standalone, installs all packages listed as dependencies in package.json in current dir  

- **--save**  
will also enscribe the installed pack into the package.json file to be indicated as dependency  

- **--global**  
will install module globally  