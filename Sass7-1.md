# Organising style sheets

Sass allows for the splitting of CSS into many files through partials and snippets.  
This means there are many ways to organise those many files into the directory.  
7-1 is a method of arborescence dividing those files into **7 folders and 1 file**.


## 1.Abstracts
equ utils, contains no style but functions

## 2.Vendors
3rd party style sheets. external libs and frameworks

## 3.Base
global boilerplate

## 4.Layout
headers, footers, navbars.... Layout elements

## 5.Components
buttons, form styles, pfps, .... 

## 6.Pages
any page specific style element

## 7.Themes
styles for each 'theme'

## main.scss
the main file retrieving and combinating every sub-file from the different folders. **only file that doesnt start with an _**  
In main.scss, the files are imported one by one, in the order of the folders as defined above. For clarity, imports from different folders should be separated by a newline, and the leading underscores as well as the file extensions should be omitted.  
**ex:**
```
@import ./3.layout/header  
@import ./3.layout/footer

@import ./4.components/button
```
