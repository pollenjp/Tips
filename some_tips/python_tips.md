# Python3 Tips

## Regular Expression
```
import re
match = re.match(r'.*_Shot(?P<shot_number>\d+)_(?P<date>\d+)_.*_', AAA)
print(match.group('shot_number', 'date'))
```


