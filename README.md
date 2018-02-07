#ctlogger
 Log tool can help you see log more efficirently, by colors, prefix with time, show line number and so on.


##Effects
####BG_COLORS
    BG_BLACK, BG_RED, BG_GREEN, BG_YELLOW, BG_BLUE, BG_MAGENTA, BG_CYAN, BG_WHITE
####EFFECTS
    RESET, BOLD, FAINT, ITALIC, UNDERLINE
####COLORS
    BLACK, RED, GREEN, YELLOW, BLUE, MAGENTA, CYAN, WHITE

##Usages
###Time prefix
Set your environment variable ENABLE_TIME_PREFIX=1, each log from logger will contians time prefix with format [%m-%d %H:%M:%S]
###color(arg1, arg2, ...)
Usage is just like print(), but the log will with color which you specified.
```python
logger.cyan('this', 'is', 'a', 'cyan', 'log')
logger.red(1, 2, 3)
```
##bgColor(arg1, arg2, ...)
Simalar to color(), this funciton is for background color and the font-color will be complementary color.
```python
logger.bgBlue('this', 'log', 'is', 'blue', 'and with background color yellow')
```
###log(optList, arg1, arg2, ...)
print log with options(possible options are shown above) and option is case-insensitive.
```python
logger.log(['red','Bg_Yellow'], 3,4,5) #print 3,4,5 (with font-color:red, backgroud is yellow)
logger.log(['blue', 'Bold'], 'this', 'is', 'a', 'blue-Bold', 'log')
logger.log(['BG_BLUE', 'YELLOW'], 'this', 'is', 'as', 'same', 'as', 'logger.bgBlue')
```
###start(*opts), end()
You can set optsm and then below log from print will apply this opts util end() be called.
```python
logger.start('yellow','bold')
print('this is yellow and bold')
logger.end()
print('this is normal log')
```

###byCodes(codeList, arg1, arg2, ...)
If you know the code of SGR (Select Graphic Rendition) parameters, you can pass it directly(string list).
```python
logger.byCodes(['31','4'], "this is equl to logger.log(['red','underline'], ...)")
```

###showOpts()
Once you forgot which option can be use, you can call this function to see all options.
```python
logger.showOpts()
```

###debug()
This log will be print only if the env variable VERBOSE been set.
```python
logger.debug('shows only when', 'VERBOSE', 'been', 'set')
```

###printLineInfo(arg1, arg2...) printStack()
```python
def test():
    printLineInfo('1','2') # <YOUR_FILE_NAME>:12/test 1 2 
    printStack() 
    #<YOUR_FILE_NAME>:13/test logger.printStack()
    #<YOUR_FILE_NAME>:18/a test()
    #<YOUR_FILE_NAME>:19/<module> a()
    #...
def a():
    test()
a()
```