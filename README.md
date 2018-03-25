# ctlogger
Log tool can help you see log more efficiently, by colors, prefix with time, show line number and so on.

# How to use
Install by pip
```
pip install ctlogger
pip install --upgrade ctlogger
```
Use
```
from ctlogger import logger
logger.yellow('This is a yellow log')
```


## Effects
```
#BG_COLORS
BG_BLACK, BG_RED, BG_GREEN, BG_YELLOW, BG_BLUE, BG_MAGENTA, BG_CYAN, BG_WHITE
#EFFECTS
RESET, BOLD, FAINT, ITALIC, UNDERLINE
#COLORS
BLACK, RED, GREEN, YELLOW, BLUE, MAGENTA, CYAN, WHITE
```

## Usages

### Time prefix
Set your environment variable ENABLE_TIME_PREFIX=1, each log from logger will contians time prefix with format [%m-%d %H:%M:%S]

### color(arg1, arg2, ...)
Like print(), but the log is with color which you specified.
```python
logger.cyan('this', 'is', 'a', 'cyan', 'log')
logger.red(1, 2, 3)
```

## bg_color(arg1, arg2, ...)
Similar to color(), this function is for background color and the font-color will be complementary color.
```python
logger.bg_blue('this', 'background color blue, and font is yellow')
```

### log(optList, arg1, arg2, ...)
print log with options(possible options are shown above) and option is case-insensitive.
```python
logger.log(['red','Bg_Yellow'], 3,4,5) #print 3,4,5 (with font-color:red, backgroud is yellow)
logger.log(['blue', 'Bold'], 'this', 'is', 'a', 'blue-Bold', 'log')
logger.log(['BG_BLUE', 'YELLOW'], 'this', 'is', 'as', 'same', 'as', 'logger.bg_blue')
```

### start(*opts), end()
You can set opts and then below log from print will apply this opts until end() be called.
```python
logger.start('yellow','bold')
print('this is yellow and bold')
logger.end()
print('this is normal log')
```

### by_codes(codeList, arg1, arg2, ...)
You can pass other codes, and try it.
Find more codes: [ANSI ESCAPE CODE](https://en.wikipedia.org/wiki/ANSI_escape_code)
```python
logger.by_codes(['31','4'], "this is equl to logger.log(['red','underline'], ...)")
```

### show_opts()
Once you forgot which option can be use, you can call this function to see all options.
```python
logger.show_opts()
```

### debug()
This log will be print only if the env variable VERBOSE be set.
```python
logger.debug('shows only when', 'VERBOSE', 'been', 'set')
```

### print_line_info(arg1, arg2...) print_stack()
```python
def bar():
    print_line_info('1','2') # <YOUR_FILE_NAME>:12/bar 1 2
    print_stack()
    #<YOUR_FILE_NAME>:13/bar logger.printStack()
    #<YOUR_FILE_NAME>:18/foo bar()
    #<YOUR_FILE_NAME>:19/<module> foo()
    #...
def foo():
    bar()
foo()
```

### Notify
slack, sendgrid is supported
```
export SLACK_WEBHOOK_URL=https://hooks.slack.com/services/XXX/OOO/QQQ

export SENDGRID_API_KEY=SG.XXXXX.XXXX
export EMAIL_FROM=sender@example.com
export EMAIL_TO=receiver0@example.com,receiver1@example.com
```
```python
from ctlogger import slack, sendgrid
res = sendgrid.send('SG title', 'SG message')
assert res.status_code == 202
res = slack.send('Slack title', 'Slack message')
assert res.status_code == 200
```

