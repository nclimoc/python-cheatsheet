Comprehensive Python Cheatsheet
===============================

### Arguments
```python
import argparse

p = argparse.ArgumentParser()

p.add_argument("positional", type=str)
p.add_argument("--non_positional", type=str)

args = p.parse_args()

print(args.positional)
print(args.non_positional)
```

### Read Text from File
```python
def read_file(filename):
    with open(filename, encoding='utf-8') as file:
        return file.readlines()
```

### Write Text to File
```python
def write_to_file(filename, text):
    with open(filename, 'w', encoding='utf-8') as file:
        file.write(text)
```

### Parse Directory
```python
import os

for (root,dirs,files) in os.walk('C:/W3school/',topdown=True):
    print("Directory path: %s"%root)
    print("Directory Names array: %s"%dirs)

    # first dir full path:
    os.path.join(root, dirs[0])

    print("Files Names array: %s"%files)

for thing in os.listdir(root_path):
    if os.path.isfile(os.path.join(root_path, thing)):
        files.append(os.path.join(root_path, thing))
```

### Parse Wildcards, do file checks
```python
<list> = glob.glob('<pattern>')

<bool> = os.path.exists(<path>)     # Or: <Path>.exists()
<bool> = os.path.isfile(<path>)     # Or: <DirEntry/Path>.is_file()
<bool> = os.path.isdir(<path>)      # Or: <DirEntry/Path>.is_dir()

<str>  = os.path.basename(<path>)   # Returns final component of the path.
<str>  = os.path.dirname(<path>)    # Returns path without the final component.
<tup.> = os.path.splitext(<path>)   # Splits on last period of the final component.
```

### String Stuff
```python
"".join(["str1", "str2", "str3"])   # Concatenate strings in a list
"string".count("substring")         # Count occurences of substring in string
```

### OS Commands
```python
import os, shutil, subprocess
os.chdir(<path>)                    # Changes the current working directory.
os.mkdir(<path>, mode=0o777)        # Creates a directory. Permissions are in octal.
os.makedirs(<path>, mode=0o777)     # Creates all path's dirs. Also `exist_ok=False`.

shutil.copy(from, to)               # Copies the file. 'to' can exist or be a dir.
shutil.copy2(from, to)              # Also copies creation and modification time.
shutil.copytree(from, to)           # Copies the directory. 'to' must not exist.

os.rename(from, to)                 # Renames/moves the file or directory.
os.replace(from, to)                # Same, but overwrites file 'to' even on Windows.
shutil.move(from, to)               # Rename() that moves into 'to' if it's a dir.

os.remove(<path>)                   # Deletes the file.
os.rmdir(<path>)                    # Deletes the empty directory.
shutil.rmtree(<path>)               # Deletes the directory.

<pipe> = os.popen('<commands>')     # Executes commands in sh/cmd. Returns combined stdout.
<str>  = <pipe>.read(size=-1)       # Reads 'size' chars or until EOF. Also readline/s().
<int>  = <pipe>.close()             # Returns None if last command exited with returncode 0.
```

### Symlink Stuff
```python
os.readlink('path')   # Get Link target

os.symlink(target, tmpLink)
os.rename(tmpLink, linkName)   # Change Link target
```

### Hashing
```python
from hashlib import sha256
print(sha256("string".encode('utf-8')).hexdigest())
```

Contents
--------
**&nbsp;&nbsp;&nbsp;** **1. Collections:** **&nbsp;** **[`List`](#list)**__,__ **[`Dictionary`](#dictionary)**__,__ **[`Tuple`](#tuple)**__,__ **[`Range`](#range)**__,__ **[`Enumerate`](#enumerate)**__.__
**&nbsp;&nbsp;&nbsp;** **2. Types:** **&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**  **[`Type`](#type)**__,__ **[`String`](#string)**__,__ **[`Regular_Exp`](#regex)**__,__ **[`Datetime`](#datetime)**__.__  
**&nbsp;&nbsp;&nbsp;** **3. System:** **&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**  **[`Exit`](#exit)**__,__ **[`Print`](#print)**__,__ **[`Input`](#input)**__,__ **[`Command_Line_Arguments`](#command-line-arguments)**__,__ **[`Open`](#open)**__,__ **[`Path`](#paths)**__,__ **[`OS_Commands`](#os-commands)**__.__  
**&nbsp;&nbsp;&nbsp;** **4. Data:** **&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**  **[`JSON`](#json)**__,__ **[`Pickle`](#pickle)**__,__ **[`CSV`](#csv)**__,__ **[`SQLite`](#sqlite)**__,__ **[`Bytes`](#bytes)**__.__
**&nbsp;&nbsp;&nbsp;**
**&nbsp;&nbsp;&nbsp;** **5. Multimedia:** **&nbsp;&nbsp;**  **[`NumPy`](#numpy)**__,__ **[`Image`](#image)**__.__ 


Main
----
```python
if __name__ == '__main__':      # Skips next line if file was imported.
    main()                      # Runs `def main(): ...` function.
```


List
----
```python
<list> = [<el_1>, <el_2>, ...]  # Creates new list. Also list(<collection>).
```

```python
<el>   = <list>[index]          # First index is 0. Last -1. Allows assignments.
<list> = <list>[<slice>]        # Also <list>[from_inclusive : to_exclusive : ±step].
```

```python
<list>.append(<el>)             # Appends element to the end. Also <list> += [<el>].
<list>.extend(<collection>)     # Appends elements to the end. Also <list> += <coll>.
```

```python
<list>.sort()                   # Sorts elements in ascending order.
<list>.reverse()                # Reverses the list in-place.
<list> = sorted(<collection>)   # Returns new list with sorted elements.
<iter> = reversed(<list>)       # Returns reversed iterator of elements.
```

```python
<el>  = max(<collection>)       # Returns largest element. Also min(<el_1>, ...).
<num> = sum(<collection>)       # Returns sum of elements. Also math.prod(<coll>).
```

```python
elementwise_sum  = [sum(pair) for pair in zip(list_a, list_b)]
sorted_by_second = sorted(<collection>, key=lambda el: el[1])
sorted_by_both   = sorted(<collection>, key=lambda el: (el[1], el[0]))
flatter_list     = list(itertools.chain.from_iterable(<list>))
```
* **For details about sort(), sorted(), min() and max() see [Sortable](#sortable).**
* **Module [operator](#operator) has function itemgetter() that can replace listed [lambdas](#lambda).**
* **This text uses the term collection instead of iterable. For rationale see [Collection](#collection).**

```python
<int> = len(<list>)             # Returns number of items. Also works on dict, set and string.
<int> = <list>.count(<el>)      # Returns number of occurrences. Also `if <el> in <coll>: ...`.
<int> = <list>.index(<el>)      # Returns index of the first occurrence or raises ValueError.
<el>  = <list>.pop()            # Removes and returns item from the end or at index if passed.
<list>.insert(<int>, <el>)      # Inserts item at index and moves the rest to the right.
<list>.remove(<el>)             # Removes first occurrence of the item or raises ValueError.
<list>.clear()                  # Removes all items. Also works on dictionary and set.
```


Dictionary
----------
```python
<dict> = {key_1: val_1, key_2: val_2, ...}      # Use `<dict>[key]` to get or set the value.
```

```python
<view> = <dict>.keys()                          # Collection of keys that reflects changes.
<view> = <dict>.values()                        # Collection of values that reflects changes.
<view> = <dict>.items()                         # Coll. of key-value tuples that reflects chgs.
```

```python
value  = <dict>.get(key, default=None)          # Returns default if key is missing.
value  = <dict>.setdefault(key, default=None)   # Returns and writes default if key is missing.
<dict> = collections.defaultdict(<type>)        # Returns a dict with default value `<type>()`.
<dict> = collections.defaultdict(lambda: 1)     # Returns a dict with default value 1.
```

```python
<dict> = dict(<collection>)                     # Creates a dict from coll. of key-value pairs.
<dict> = dict(zip(keys, values))                # Creates a dict from two collections.
<dict> = dict.fromkeys(keys [, value])          # Creates a dict from collection of keys.
```

```python
<dict>.update(<dict>)                           # Adds items. Replaces ones with matching keys.
value = <dict>.pop(key)                         # Removes item or raises KeyError if missing.
{k for k, v in <dict>.items() if v == value}    # Returns set of keys that point to the value.
{k: v for k, v in <dict>.items() if k in keys}  # Filters the dictionary by keys.
```

Tuple
-----
**Tuple is an immutable and hashable list.**
```python
<tuple> = ()                               # Empty tuple.
<tuple> = (<el>,)                          # Or: <el>,
<tuple> = (<el_1>, <el_2> [, ...])         # Or: <el_1>, <el_2> [, ...]
```

### Named Tuple
**Tuple's subclass with named elements.**
```python
>>> from collections import namedtuple
>>> Point = namedtuple('Point', 'x y')
>>> p = Point(1, y=2)
>>> print(p)
Point(x=1, y=2)
>>> p[0], p.x
(1, 1)
```


Range
-----
**Immutable and hashable sequence of integers.**
```python
<range> = range(stop)                      # I.e. range(to_exclusive).
<range> = range(start, stop)               # I.e. range(from_inclusive, to_exclusive).
<range> = range(start, stop, ±step)        # I.e. range(from_inclusive, to_exclusive, ±step).
```

```python
>>> [i for i in range(3)]
[0, 1, 2]
```


Enumerate
---------
```python
for i, el in enumerate(<coll>, start=0):   # Returns next element and its index on each pass.
    ...
```


String
------
**Immutable sequence of characters.**

```python
<str>  = <str>.strip()                       # Strips all whitespace characters from both ends.
<str>  = <str>.strip('<chars>')              # Strips passed characters. Also lstrip/rstrip().
```

```python
<list> = <str>.split()                       # Splits on one or more whitespace characters.
<list> = <str>.split(sep=None, maxsplit=-1)  # Splits on 'sep' str at most 'maxsplit' times.
<list> = <str>.splitlines(keepends=False)    # On [\n\r\f\v\x1c-\x1e\x85\u2028\u2029] and \r\n.
<str>  = <str>.join(<coll_of_strings>)       # Joins elements using string as a separator.
```

```python
<bool> = <sub_str> in <str>                  # Checks if string contains the substring.
<bool> = <str>.startswith(<sub_str>)         # Pass tuple of strings for multiple options.
<int>  = <str>.find(<sub_str>)               # Returns start index of the first match or -1.
<int>  = <str>.index(<sub_str>)              # Same, but raises ValueError if there's no match.
```

```python
<str>  = <str>.lower()                       # Changes the case. Also upper/capitalize/title().
<str>  = <str>.replace(old, new [, count])   # Replaces 'old' with 'new' at most 'count' times.
<str>  = <str>.translate(<table>)            # Use `str.maketrans(<dict>)` to generate table.
```

```python
<str>  = chr(<int>)                          # Converts int to Unicode character.
<int>  = ord(<str>)                          # Converts Unicode character to int.
```
* **Use `'unicodedata.normalize("NFC", <str>)'` on strings like `'Motörhead'` before comparing them to other strings, because `'ö'` can be stored as one or two characters.**
* **`'NFC'` converts such characters to a single character, while `'NFD'` converts them to two.**

### Property Methods
```python
<bool> = <str>.isdecimal()                   # Checks for [0-9]. Also [०-९] and [٠-٩].
<bool> = <str>.isdigit()                     # Checks for [²³¹…] and isdecimal().
<bool> = <str>.isnumeric()                   # Checks for [¼½¾…], [零〇一…] and isdigit().
<bool> = <str>.isalnum()                     # Checks for [a-zA-Z…] and isnumeric().
<bool> = <str>.isprintable()                 # Checks for [ !#$%…] and isalnum().
<bool> = <str>.isspace()                     # Checks for [ \t\n\r\f\v\x1c-\x1f\x85\xa0…].
```


Regex
-----
**Functions for regular expression matching.**

```python
import re
<str>   = re.sub(r'<regex>', new, text, count=0)  # Substitutes all occurrences with 'new'.
<list>  = re.findall(r'<regex>', text)            # Returns all occurrences as strings.
<list>  = re.split(r'<regex>', text, maxsplit=0)  # Add brackets around regex to keep matches.
<Match> = re.search(r'<regex>', text)             # First occurrence of the pattern or None.
<Match> = re.match(r'<regex>', text)              # Searches only at the beginning of the text.
<iter>  = re.finditer(r'<regex>', text)           # Returns all occurrences as Match objects.
```

* **Raw string literals do not interpret escape sequences, thus enabling us to use regex-specific escape sequences that cause SyntaxWarning in normal string literals (since 3.12).**
* **Argument 'new' of re.sub() can be a function that accepts Match object and returns a str.**
* **Argument `'flags=re.IGNORECASE'` can be used with all functions.**
* **Argument `'flags=re.MULTILINE'` makes `'^'` and `'$'` match the start/end of each line.**
* **Argument `'flags=re.DOTALL'` makes `'.'` also accept the `'\n'`.**
* **`'re.compile(<regex>)'` returns a Pattern object with methods sub(), findall(), etc.**

### Match Object
```python
<str>   = <Match>.group()                         # Returns the whole match. Also group(0).
<str>   = <Match>.group(1)                        # Returns part inside the first brackets.
<tuple> = <Match>.groups()                        # Returns all bracketed parts.
<int>   = <Match>.start()                         # Returns start index of the match.
<int>   = <Match>.end()                           # Returns exclusive end index of the match.
```

### Special Sequences
```python
'\d' == '[0-9]'                                   # Also [०-९…]. Matches a decimal character.
'\w' == '[a-zA-Z0-9_]'                            # Also [ª²³…]. Matches an alphanumeric or _.
'\s' == '[ \t\n\r\f\v]'                           # Also [\x1c-\x1f…]. Matches a whitespace.
```
* **By default, decimal characters and alphanumerics from all alphabets are matched unless `'flags=re.ASCII'` is used. It restricts special sequence matches to the first 128 Unicode characters and also prevents `'\s'` from accepting `'\x1c'`, `'\x1d'`, `'\x1e'` and `'\x1f'` (non-printable characters that divide text into files, tables, rows and fields, respectively).**
* **Use a capital letter for negation (all non-ASCII characters will be matched when used in combination with ASCII flag).**


Format
------
```perl
<str> = f'{<el_1>}, {<el_2>}'            # Curly brackets can also contain expressions.
<str> = '{}, {}'.format(<el_1>, <el_2>)  # Or: '{0}, {a}'.format(<el_1>, a=<el_2>)
<str> = '%s, %s' % (<el_1>, <el_2>)      # Redundant and inferior C-style formatting.
```

### Example
```python
>>> Person = collections.namedtuple('Person', 'name height')
>>> person = Person('Jean-Luc', 187)
>>> f'{person.name} is {person.height / 100} meters tall.'
'Jean-Luc is 1.87 meters tall.'
```

### General Options
```python
{<el>:<10}                               # '<el>      '
{<el>:^10}                               # '   <el>   '
{<el>:>10}                               # '      <el>'
{<el>:.<10}                              # '<el>......'
{<el>:0}                                 # '<el>'
```
* **Objects are rendered using `'format(<el>, "<options>")'`.**
* **Options can be generated dynamically: `f'{<el>:{<str/int>}[…]}'`.**
* **Adding `'='` to the expression prepends it to the output: `f'{1+1=}'` returns `'1+1=2'`.**
* **Adding `'!r'` to the expression converts object to string by calling its [repr()](#class) method.**

### Strings
```python
{'abcde':10}                             # 'abcde     '
{'abcde':10.3}                           # 'abc       '
{'abcde':.3}                             # 'abc'
{'abcde'!r:10}                           # "'abcde'   "
```

### Numbers
```python
{123456:10}                              # '    123456'
{123456:10,}                             # '   123,456'
{123456:10_}                             # '   123_456'
{123456:+10}                             # '   +123456'
{123456:=+10}                            # '+   123456'
{123456: }                               # ' 123456'
{-123456: }                              # '-123456'
```

### Floats
```python
{1.23456:10.3}                           # '      1.23'
{1.23456:10.3f}                          # '     1.235'
{1.23456:10.3e}                          # ' 1.235e+00'
{1.23456:10.3%}                          # '  123.456%'
```

#### Comparison of presentation types:
```text
+--------------+----------------+----------------+----------------+----------------+
|              |    {<float>}   |   {<float>:f}  |   {<float>:e}  |   {<float>:%}  |
+--------------+----------------+----------------+----------------+----------------+
|  0.000056789 |   '5.6789e-05' |    '0.000057'  | '5.678900e-05' |    '0.005679%' |
|  0.00056789  |   '0.00056789' |    '0.000568'  | '5.678900e-04' |    '0.056789%' |
|  0.0056789   |   '0.0056789'  |    '0.005679'  | '5.678900e-03' |    '0.567890%' |
|  0.056789    |   '0.056789'   |    '0.056789'  | '5.678900e-02' |    '5.678900%' |
|  0.56789     |   '0.56789'    |    '0.567890'  | '5.678900e-01' |   '56.789000%' |
|  5.6789      |   '5.6789'     |    '5.678900'  | '5.678900e+00' |  '567.890000%' |
| 56.789       |  '56.789'      |   '56.789000'  | '5.678900e+01' | '5678.900000%' |
+--------------+----------------+----------------+----------------+----------------+
```

```text
+--------------+----------------+----------------+----------------+----------------+
|              |  {<float>:.2}  |  {<float>:.2f} |  {<float>:.2e} |  {<float>:.2%} |
+--------------+----------------+----------------+----------------+----------------+
|  0.000056789 |    '5.7e-05'   |      '0.00'    |   '5.68e-05'   |      '0.01%'   |
|  0.00056789  |    '0.00057'   |      '0.00'    |   '5.68e-04'   |      '0.06%'   |
|  0.0056789   |    '0.0057'    |      '0.01'    |   '5.68e-03'   |      '0.57%'   |
|  0.056789    |    '0.057'     |      '0.06'    |   '5.68e-02'   |      '5.68%'   |
|  0.56789     |    '0.57'      |      '0.57'    |   '5.68e-01'   |     '56.79%'   |
|  5.6789      |    '5.7'       |      '5.68'    |   '5.68e+00'   |    '567.89%'   |
| 56.789       |    '5.7e+01'   |     '56.79'    |   '5.68e+01'   |   '5678.90%'   |
+--------------+----------------+----------------+----------------+----------------+
```
* **`'{<float>:g}'` is `'{<float>:.6}'` with stripped zeros, exponent starting at `'1e+06'`.**
* **When both rounding up and rounding down are possible, the one that returns result with even last digit is chosen. That makes `'{6.5:.0f}'` a `'6'` and `'{7.5:.0f}'` an `'8'`.**
* **This rule only effects numbers that can be represented exactly by a float (`.5`, `.25`, …).**

### Ints
```python
{90:c}                                   # 'Z'. Unicode character with value 90.
{90:b}                                   # '1011010'. Binary representation of the int.
{90:X}                                   # '5A'. Hexadecimal with upper-case letters.
```


Datetime
--------
**Provides 'date', 'time', 'datetime' and 'timedelta' classes. All are immutable and hashable.**

```python
# $ pip3 install python-dateutil
from datetime import date, time, datetime, timedelta, timezone
import zoneinfo, dateutil.tz
```

```python
<D>  = date(year, month, day)               # Only accepts valid dates from 1 to 9999 AD.
<T>  = time(hour=0, minute=0, second=0)     # Also: `microsecond=0, tzinfo=None, fold=0`.
<DT> = datetime(year, month, day, hour=0)   # Also: `minute=0, second=0, microsecond=0, …`.
<TD> = timedelta(weeks=0, days=0, hours=0)  # Also: `minutes=0, seconds=0, microseconds=0`.
```
* **Times and datetimes that have defined timezone are called aware and ones that don't, naive. If object is naive, it is presumed to be in the system's timezone!**
* **`'fold=1'` means the second pass in case of time jumping back for one hour.**
* **Timedelta normalizes arguments to ±days, seconds (< 86 400) and microseconds (< 1M). Its str() method returns `'[±D, ]H:MM:SS[.…]'` and total_seconds() a float of all seconds.**
* **Use `'<D/DT>.weekday()'` to get the day of the week as an int, with Monday being 0.**

### Now
```python
<D/DTn> = D/DT.today()                      # Current local date or naive DT. Also DT.now().
<DTa>   = DT.now(<tzinfo>)                  # Aware DT from current time in passed timezone.
```
* **To extract time use `'<DTn>.time()'`, `'<DTa>.time()'` or `'<DTa>.timetz()'`.**

### Timezone
```python
<tzinfo> = timezone.utc                     # London without daylight saving time (DST).
<tzinfo> = timezone(<timedelta>)            # Timezone with fixed offset from UTC.
<tzinfo> = dateutil.tz.tzlocal()            # Local timezone with dynamic offset from UTC.
<tzinfo> = zoneinfo.ZoneInfo('<iana_key>')  # 'Continent/City_Name' zone with dynamic offset.
<DTa>    = <DT>.astimezone([<tzinfo>])      # Converts DT to the passed or local fixed zone.
<Ta/DTa> = <T/DT>.replace(tzinfo=<tzinfo>)  # Changes object's timezone without conversion.
```
* **Timezones returned by tzlocal(), ZoneInfo() and implicit local timezone of naive objects have offsets that vary through time due to DST and historical changes of the base offset.**
* **To get ZoneInfo() to work on Windows run `'> pip3 install tzdata'`.**

### Encode
```python
<D/T/DT> = D/T/DT.fromisoformat(<str>)      # Object from ISO string. Raises ValueError.
<DT>     = DT.strptime(<str>, '<format>')   # Datetime from custom string. See Format.
<D/DTn>  = D/DT.fromordinal(<int>)          # D/DT from days since the Gregorian NYE 1.
<DTn>    = DT.fromtimestamp(<float>)        # Local naive DT from seconds since the Epoch.
<DTa>    = DT.fromtimestamp(<float>, <tz>)  # Aware datetime from seconds since the Epoch.
```
* **ISO strings come in following forms: `'YYYY-MM-DD'`, `'HH:MM:SS.mmmuuu[±HH:MM]'`, or both separated by an arbitrary character. All parts following the hours are optional.**
* **Python uses the Unix Epoch: `'1970-01-01 00:00 UTC'`, `'1970-01-01 01:00 CET'`, ...**

### Decode
```python
<str>    = <D/T/DT>.isoformat(sep='T')      # Also `timespec='auto/hours/minutes/seconds/…'`.
<str>    = <D/T/DT>.strftime('<format>')    # Custom string representation of the object.
<int>    = <D/DT>.toordinal()               # Days since Gregorian NYE 1, ignoring time and tz.
<float>  = <DTn>.timestamp()                # Seconds since the Epoch, from local naive DT.
<float>  = <DTa>.timestamp()                # Seconds since the Epoch, from aware datetime.
```

### Format
```python
>>> dt = datetime.strptime('2025-08-14 23:39:00.00 +0200', '%Y-%m-%d %H:%M:%S.%f %z')
>>> dt.strftime("%dth of %B '%y (%a), %I:%M %p %Z")
"14th of August '25 (Thu), 11:39 PM UTC+02:00"
```
* **`'%z'` accepts `'±HH[:]MM'` and returns `'±HHMM'` or empty string if object is naive.**
* **`'%Z'` accepts `'UTC/GMT'` and local timezone's code and returns timezone's name, `'UTC[±HH:MM]'` if timezone is nameless, or an empty string if object is naive.**

### Arithmetics
```python
<bool>   = <D/T/DTn> > <D/T/DTn>            # Ignores time jumps (fold attribute). Also ==.
<bool>   = <DTa>     > <DTa>                # Ignores time jumps if they share tzinfo object.
<TD>     = <D/DTn>   - <D/DTn>              # Ignores jumps. Convert to UTC for actual delta.
<TD>     = <DTa>     - <DTa>                # Ignores jumps if they share tzinfo object.
<D/DT>   = <D/DT>    ± <TD>                 # Returned datetime can fall into missing hour.
<TD>     = <TD>      * <float>              # Also `<TD> = abs(<TD>)`, `<TD> = <TD> ± <TD>`.
<float>  = <TD>      / <TD>                 # Also `(<int>, <TD>) = divmod(<TD>, <TD>)`.
```


Print
-----
```python
print(<el_1>, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
```
* **Use `'file=sys.stderr'` for messages about errors.**
* **Stdout and stderr streams hold output in a buffer until they receive a string containing '\n' or '\r', buffer reaches 4096 characters, `'flush=True'` is used, or program exits.**

### Pretty Print
```python
from pprint import pprint
pprint(<collection>, width=80, depth=None, compact=False, sort_dicts=True)
```
* **Each item is printed on its own line if collection exceeds 'width' characters.**
* **Nested collections that are 'depth' levels deep get printed as '...'.**


Input
-----
```python
<str> = input()
```
* **Reads a line from the user input or pipe if present (trailing newline gets stripped).**
* **If argument is passed, it gets printed to the standard output before input is read.**
* **EOFError is raised if user hits EOF (ctrl-d/ctrl-z⏎) or input stream gets exhausted.**


Command Line Arguments
----------------------
```python
import sys
scripts_path = sys.argv[0]
arguments    = sys.argv[1:]
```

### Argument Parser
```python
from argparse import ArgumentParser, FileType
p = ArgumentParser(description=<str>)                             # Returns a parser.
p.add_argument('-<short_name>', '--<name>', action='store_true')  # Flag (defaults to False).
p.add_argument('-<short_name>', '--<name>', type=<type>)          # Option (defaults to None).
p.add_argument('<name>', type=<type>, nargs=1)                    # Mandatory first argument.
p.add_argument('<name>', type=<type>, nargs='+')                  # Mandatory remaining args.
p.add_argument('<name>', type=<type>, nargs='?/*')                # Optional argument/s.
args  = p.parse_args()                                            # Exits on parsing error.
<obj> = args.<name>                                               # Returns `<type>(<arg>)`.
```

* **Use `'help=<str>'` to set argument description that will be displayed in help message.**
* **Use `'default=<obj>'` to set option's or optional argument's default value.**
* **Use `'type=FileType(<mode>)'` for files. Accepts 'encoding', but 'newline' is None.**


Open
----
**Opens a file and returns the corresponding file object.**

```python
<file> = open(<path>, mode='r', encoding=None, newline=None)
```
* **`'encoding=None'` means that the default encoding is used, which is platform dependent. Best practice is to use `'encoding="utf-8"'` whenever possible.**
* **`'newline=None'` means all different end of line combinations are converted to '\n' on read, while on write all '\n' characters are converted to system's default line separator.**
* **`'newline=""'` means no conversions take place, but input is still broken into chunks by readline() and readlines() on every '\n', '\r' and '\r\n'.**

### Modes
* **`'r'`  - Read. Used by default.**
* **`'w'`  - Write. Deletes existing contents.**
* **`'x'`  - Write or fail if the file already exists.**
* **`'a'`  - Append. Creates new file if it doesn't exist.**
* **`'w+'` - Read and write. Deletes existing contents.**
* **`'r+'` - Read and write from the start.**
* **`'a+'` - Read and write from the end.**
* **`'b'`  - Binary mode (`'rb'`, `'wb'`, `'xb'`, …).**

### Exceptions
* **`'FileNotFoundError'` can be raised when reading with `'r'` or `'r+'`.**
* **`'FileExistsError'` can be raised when writing with `'x'`.**
* **`'IsADirectoryError'` and `'PermissionError'` can be raised by any.**
* **`'OSError'` is the parent class of all listed exceptions.**

### File Object
```python
<file>.seek(0)                      # Moves to the start of the file.
<file>.seek(offset)                 # Moves 'offset' chars/bytes from the start.
<file>.seek(0, 2)                   # Moves to the end of the file.
<bin_file>.seek(±offset, origin)    # Origin: 0 start, 1 current position, 2 end.
```

```python
<str/bytes> = <file>.read(size=-1)  # Reads 'size' chars/bytes or until EOF.
<str/bytes> = <file>.readline()     # Returns a line or empty string/bytes on EOF.
<list>      = <file>.readlines()    # Returns a list of remaining lines.
<str/bytes> = next(<file>)          # Returns a line using buffer. Do not mix.
```

```python
<file>.write(<str/bytes>)           # Writes a string or bytes object.
<file>.writelines(<collection>)     # Writes a coll. of strings or bytes objects.
<file>.flush()                      # Flushes write buffer. Runs every 4096/8192 B.
<file>.close()                      # Closes the file after flushing write buffer.
```
* **Methods do not add or strip trailing newlines, not even writelines().**

### Read Text from File
```python
def read_file(filename):
    with open(filename, encoding='utf-8') as file:
        return file.readlines()
```

### Write Text to File
```python
def write_to_file(filename, text):
    with open(filename, 'w', encoding='utf-8') as file:
        file.write(text)
```


Paths
-----
```python
import os, glob
from pathlib import Path
```

```python
<str>  = os.getcwd()                # Returns working dir. Starts as shell's $PWD.
<str>  = os.path.join(<path>, ...)  # Joins two or more pathname components.
<str>  = os.path.realpath(<path>)   # Resolves symlinks and calls path.abspath().
```

```python
<str>  = os.path.basename(<path>)   # Returns final component of the path.
<str>  = os.path.dirname(<path>)    # Returns path without the final component.
<tup.> = os.path.splitext(<path>)   # Splits on last period of the final component.
```

```python
<list> = os.listdir(path='.')       # Returns filenames located at the path.
<list> = glob.glob('<pattern>')     # Returns paths matching the wildcard pattern.
```

```python
<bool> = os.path.exists(<path>)     # Or: <Path>.exists()
<bool> = os.path.isfile(<path>)     # Or: <DirEntry/Path>.is_file()
<bool> = os.path.isdir(<path>)      # Or: <DirEntry/Path>.is_dir()
```

```python
<stat> = os.stat(<path>)            # Or: <DirEntry/Path>.stat()
<num>  = <stat>.st_mtime/st_size/…  # Modification time, size in bytes, etc.
```

### DirEntry
**Unlike listdir(), scandir() returns DirEntry objects that cache isfile, isdir, and on Windows also stat information, thus significantly increasing the performance of code that requires it.**

```python
<iter> = os.scandir(path='.')       # Returns DirEntry objects located at the path.
<str>  = <DirEntry>.path            # Returns the whole path as a string.
<str>  = <DirEntry>.name            # Returns final component as a string.
<file> = open(<DirEntry>)           # Opens the file and returns a file object.
```

### Path Object
```python
<Path> = Path(<path> [, ...])       # Accepts strings, Paths, and DirEntry objects.
<Path> = <path> / <path> [/ ...]    # First or second path must be a Path object.
<Path> = <Path>.resolve()           # Returns absolute path with resolved symlinks.
```

```python
<Path> = Path()                     # Returns relative CWD. Also Path('.').
<Path> = Path.cwd()                 # Returns absolute CWD. Also Path().resolve().
<Path> = Path.home()                # Returns user's home directory (absolute).
<Path> = Path(__file__).resolve()   # Returns module's path if CWD wasn't changed.
```

```python
<Path> = <Path>.parent              # Returns Path without the final component.
<str>  = <Path>.name                # Returns final component as a string.
<str>  = <Path>.stem                # Returns final component w/o last extension.
<str>  = <Path>.suffix              # Returns last extension prepended with a dot.
<tup.> = <Path>.parts               # Returns all path's components as strings.
```

```python
<iter> = <Path>.iterdir()           # Returns directory contents as Path objects.
<iter> = <Path>.glob('<pattern>')   # Returns Paths matching the wildcard pattern.
```

```python
<str>  = str(<Path>)                # Returns path as a string.
<file> = open(<Path>)               # Also <Path>.read/write_text/bytes(<args>).
```


OS Commands
-----------
```python
import os, shutil, subprocess
```

```python
os.chdir(<path>)                    # Changes the current working directory.
os.mkdir(<path>, mode=0o777)        # Creates a directory. Permissions are in octal.
os.makedirs(<path>, mode=0o777)     # Creates all path's dirs. Also `exist_ok=False`.
```

```python
shutil.copy(from, to)               # Copies the file. 'to' can exist or be a dir.
shutil.copy2(from, to)              # Also copies creation and modification time.
shutil.copytree(from, to)           # Copies the directory. 'to' must not exist.
```

```python
os.rename(from, to)                 # Renames/moves the file or directory.
os.replace(from, to)                # Same, but overwrites file 'to' even on Windows.
shutil.move(from, to)               # Rename() that moves into 'to' if it's a dir.
```

```python
os.remove(<path>)                   # Deletes the file.
os.rmdir(<path>)                    # Deletes the empty directory.
shutil.rmtree(<path>)               # Deletes the directory.
```
* **Paths can be either strings, Path objects, or DirEntry objects.**
* **Functions report OS related errors by raising OSError or one of its [subclasses](#exceptions-1).**

### Shell Commands
```python
<pipe> = os.popen('<commands>')     # Executes commands in sh/cmd. Returns combined stdout.
<str>  = <pipe>.read(size=-1)       # Reads 'size' chars or until EOF. Also readline/s().
<int>  = <pipe>.close()             # Returns None if last command exited with returncode 0.
```

#### Sends '1 + 1' to the basic calculator and captures its output:
```python
>>> subprocess.run('bc', input='1 + 1\n', capture_output=True, text=True)
CompletedProcess(args='bc', returncode=0, stdout='2\n', stderr='')
```

#### Sends test.in to the basic calculator running in standard mode and saves its output to test.out:
```python
>>> from shlex import split
>>> os.popen('echo 1 + 1 > test.in')
>>> subprocess.run(split('bc -s'), stdin=open('test.in'), stdout=open('test.out', 'w'))
CompletedProcess(args=['bc', '-s'], returncode=0)
>>> open('test.out').read()
'2\n'
```


JSON
----
**Text file format for storing collections of strings and numbers.**

```python
import json
<str>  = json.dumps(<list/dict>)    # Converts collection to JSON string.
<coll> = json.loads(<str>)          # Converts JSON string to collection.
```

### Read Collection from JSON File
```python
def read_json_file(filename):
    with open(filename, encoding='utf-8') as file:
        return json.load(file)
```

### Write Collection to JSON File
```python
def write_to_json_file(filename, collection):
    with open(filename, 'w', encoding='utf-8') as file:
        json.dump(collection, file, ensure_ascii=False, indent=2)
```


Pickle
------
**Binary file format for storing Python objects.**

```python
import pickle
<bytes>  = pickle.dumps(<object>)   # Converts object to bytes object.
<object> = pickle.loads(<bytes>)    # Converts bytes object to object.
```

### Read Object from Pickle File
```python
def read_pickle_file(filename):
    with open(filename, 'rb') as file:
        return pickle.load(file)
```

### Write Object to Pickle File
```python
def write_to_pickle_file(filename, an_object):
    with open(filename, 'wb') as file:
        pickle.dump(an_object, file)
```


CSV
---
**Text file format for storing spreadsheets.**

```python
import csv
```

### Read
```python
<reader> = csv.reader(<file>)       # Also: `dialect='excel', delimiter=','`.
<list>   = next(<reader>)           # Returns next row as a list of strings.
<list>   = list(<reader>)           # Returns a list of remaining rows.
```
* **File must be opened with a `'newline=""'` argument, or newlines embedded inside quoted fields will not be interpreted correctly!**
* **To print the spreadsheet to the console use [Tabulate](#table) library.**
* **For XML and binary Excel files (xlsx, xlsm and xlsb) use [Pandas](#dataframe-plot-encode-decode) library.**
* **Reader accepts any iterator of strings, not just files.**

### Write
```python
<writer> = csv.writer(<file>)       # Also: `dialect='excel', delimiter=','`.
<writer>.writerow(<collection>)     # Encodes objects using `str(<el>)`.
<writer>.writerows(<coll_of_coll>)  # Appends multiple rows.
```
* **File must be opened with a `'newline=""'` argument, or '\r' will be added in front of every '\n' on platforms that use '\r\n' line endings!**
* **Open existing file with `'mode="a"'` to append to it or `'mode="w"'` to overwrite it.**

### Parameters
* **`'dialect'` - Master parameter that sets the default values. String or a 'csv.Dialect' object.**
* **`'delimiter'` - A one-character string used to separate fields.**
* **`'lineterminator'` - How writer terminates rows. Reader looks for '\n', '\r' and '\r\n'.**
* **`'quotechar'` - Character for quoting fields containing delimiters, quotechars, '\n' or '\r'.**
* **`'escapechar'` - Character for escaping quotechars.**
* **`'doublequote'` - Whether quotechars inside fields are/get doubled or escaped.**
* **`'quoting'` - 0: As necessary, 1: All, 2: All but numbers which are read as floats, 3: None.**
* **`'skipinitialspace'` - Is space character at the start of the field stripped by the reader.**

### Dialects
```text
+------------------+--------------+--------------+--------------+
|                  |     excel    |   excel-tab  |     unix     |
+------------------+--------------+--------------+--------------+
| delimiter        |       ','    |      '\t'    |       ','    |
| lineterminator   |    '\r\n'    |    '\r\n'    |      '\n'    |
| quotechar        |       '"'    |       '"'    |       '"'    |
| escapechar       |      None    |      None    |      None    |
| doublequote      |      True    |      True    |      True    |
| quoting          |         0    |         0    |         1    |
| skipinitialspace |     False    |     False    |     False    |
+------------------+--------------+--------------+--------------+
```

### Read Rows from CSV File
```python
def read_csv_file(filename, **csv_params):
    with open(filename, encoding='utf-8', newline='') as file:
        return list(csv.reader(file, **csv_params))
```

### Write Rows to CSV File
```python
def write_to_csv_file(filename, rows, mode='w', **csv_params):
    with open(filename, mode, encoding='utf-8', newline='') as file:
        writer = csv.writer(file, **csv_params)
        writer.writerows(rows)
```


SQLite
------
**A server-less database engine that stores each database into its own file.**

```python
import sqlite3
<conn> = sqlite3.connect(<path>)               # Opens existing or new file. Also ':memory:'.
<conn>.close()                                 # Closes connection. Discards uncommitted data.
```

### Read
```python
<cursor> = <conn>.execute('<query>')           # Can raise a subclass of sqlite3.Error.
<tuple>  = <cursor>.fetchone()                 # Returns next row. Also next(<cursor>).
<list>   = <cursor>.fetchall()                 # Returns remaining rows. Also list(<cursor>).
```

### Write
```python
<conn>.execute('<query>')                      # Can raise a subclass of sqlite3.Error.
<conn>.commit()                                # Saves all changes since the last commit.
<conn>.rollback()                              # Discards all changes since the last commit.
```

#### Or:
```python
with <conn>:                                   # Exits the block with commit() or rollback(),
    <conn>.execute('<query>')                  # depending on whether any exception occurred.
```

### Placeholders
```python
<conn>.execute('<query>', <list/tuple>)        # Replaces '?'s in query with values.
<conn>.execute('<query>', <dict/namedtuple>)   # Replaces ':<key>'s with values.
<conn>.executemany('<query>', <coll_of_coll>)  # Runs execute() multiple times.
```
* **Passed values can be of type str, int, float, bytes, None, or bool (stored as 1 or 0).**

### Example
**Values are not actually saved in this example because `'conn.commit()'` is omitted!**
```python
>>> conn = sqlite3.connect('test.db')
>>> conn.execute('CREATE TABLE person (person_id INTEGER PRIMARY KEY, name, height)')
>>> conn.execute('INSERT INTO person VALUES (NULL, ?, ?)', ('Jean-Luc', 187)).lastrowid
1
>>> conn.execute('SELECT * FROM person').fetchall()
[(1, 'Jean-Luc', 187)]
```

### SQLAlchemy
**Library for interacting with various DB systems via SQL, method chaining, or ORM.**
```python
# $ pip3 install sqlalchemy
from sqlalchemy import create_engine, text
<engine> = create_engine('<url>')              # Url: 'dialect://user:password@host/dbname'.
<conn>   = <engine>.connect()                  # Creates a connection. Also <conn>.close().
<cursor> = <conn>.execute(text('<query>'), …)  # `<dict>`. Replaces ':<key>'s with values.
with <conn>.begin(): ...                       # Exits the block with commit or rollback.
```

```text
+-----------------+--------------+----------------------------------+
| Dialect         | pip3 install |           Dependencies           |
+-----------------+--------------+----------------------------------+
| mysql           | mysqlclient  | www.pypi.org/project/mysqlclient |
| postgresql      | psycopg2     | www.pypi.org/project/psycopg2    |
| mssql           | pyodbc       | www.pypi.org/project/pyodbc      |
| oracle+oracledb | oracledb     | www.pypi.org/project/oracledb    |
+-----------------+--------------+----------------------------------+
```


Bytes
-----
**A bytes object is an immutable sequence of single bytes. Mutable version is called bytearray.**

```python
<bytes> = b'<str>'                       # Only accepts ASCII characters and \x00-\xff.
<int>   = <bytes>[index]                 # Returns an int in range from 0 to 255.
<bytes> = <bytes>[<slice>]               # Returns bytes even if it has only one element.
<bytes> = <bytes>.join(<coll_of_bytes>)  # Joins elements using bytes as a separator.
```

### Encode
```python
<bytes> = bytes(<coll_of_ints>)          # Ints must be in range from 0 to 255.
<bytes> = bytes(<str>, 'utf-8')          # Encodes the string. Also <str>.encode().
<bytes> = bytes.fromhex('<hex>')         # Hex pairs can be separated by whitespaces.
<bytes> = <int>.to_bytes(n_bytes, …)     # `byteorder='big/little', signed=False`.
```

### Decode
```python
<list>  = list(<bytes>)                  # Returns ints in range from 0 to 255.
<str>   = str(<bytes>, 'utf-8')          # Returns a string. Also <bytes>.decode().
<str>   = <bytes>.hex()                  # Returns hex pairs. Accepts `sep=<str>`.
<int>   = int.from_bytes(<bytes>, …)     # `byteorder='big/little', signed=False`.
```

### Read Bytes from File
```python
def read_bytes(filename):
    with open(filename, 'rb') as file:
        return file.read()
```

### Write Bytes to File
```python
def write_bytes(filename, bytes_obj):
    with open(filename, 'wb') as file:
        file.write(bytes_obj)
```




NumPy
-----
**Array manipulation mini-language. It can run up to one hundred times faster than the equivalent Python code. An even faster alternative that runs on a GPU is called CuPy.**

```python
# $ pip3 install numpy
import numpy as np
```

```python
<array> = np.array(<list/list_of_lists/…>)              # Returns a 1d/2d/… NumPy array.
<array> = np.zeros/ones/empty(<shape>)                  # Also np.full(<shape>, <el>).
<array> = np.arange(from_inc, to_exc, ±step)            # Also np.linspace(start, stop, len).
<array> = np.random.randint(from_inc, to_exc, <shape>)  # Also np.random.random(<shape>).
```

```python
<view>  = <array>.reshape(<shape>)                      # Also `<array>.shape = <shape>`.
<array> = <array>.flatten()                             # Also `<view> = <array>.ravel()`.
<view>  = <array>.transpose()                           # Or: <array>.T
```

```python
<array> = np.copy/abs/sqrt/log/int64(<array>)           # Returns new array of the same shape.
<array> = <array>.sum/max/mean/argmax/all(axis)         # Aggregates specified dimension.
<array> = np.apply_along_axis(<func>, axis, <array>)    # Func can return a scalar or array.
```

```python
<array> = np.concatenate(<list_of_arrays>, axis=0)      # Links arrays along first axis (rows).
<array> = np.vstack/column_stack(<list_of_arrays>)      # Treats 1d arrays as rows or columns.
<array> = np.tile/repeat(<array>, <int/list> [, axis])  # Tiles array or repeats its elements.
```
* **Shape is a tuple of dimension sizes. A 100x50 RGB image has shape (50, 100, 3).**
* **Axis is an index of a dimension. Leftmost dimension has index 0. Summing the RGB image along axis 2 will return a greyscale image with shape (50, 100).**

### Indexing
```perl
<el>       = <2d>[row_index, col_index]                 # Or: <3d>[<int>, <int>, <int>]
<1d_view>  = <2d>[row_index]                            # Or: <3d>[<int>, <int>, <slice>]
<1d_view>  = <2d>[:, col_index]                         # Or: <3d>[<int>, <slice>, <int>]
<2d_view>  = <2d>[from:to_row_i, from:to_col_i]         # Or: <3d>[<int>, <slice>, <slice>]
```

```perl
<1d_array> = <2d>[row_indices, col_indices]             # Or: <3d>[<int/1d>, <1d>, <1d>]
<2d_array> = <2d>[row_indices]                          # Or: <3d>[<int/1d>, <1d>, <slice>]
<2d_array> = <2d>[:, col_indices]                       # Or: <3d>[<int/1d>, <slice>, <1d>]
<2d_array> = <2d>[np.ix_(row_indices, col_indices)]     # Or: <3d>[<int/1d/2d>, <2d>, <2d>]
```

```perl
<2d_bools> = <2d> > <el/1d/2d>                          # 1d object must have size of a row.
<1/2d_arr> = <2d>[<2d/1d_bools>]                        # 1d_bools must have size of a column.
```
* **`':'` returns a slice of all dimension's indices. Omitted dimensions default to `':'`.**
* **Python converts `'obj[i, j]'` to `'obj[(i, j)]'`. This makes `'<2d>[row_i, col_i]'` and `'<2d>[row_indices]'` indistinguishable to NumPy if tuple of two indices is passed!**
* **`'ix_([1, 2], [3, 4])'` returns `'[[1], [2]]'` and `'[[3, 4]]'`. Due to broadcasting rules, this is the same as using `'[[1, 1], [2, 2]]'` and `'[[3, 4], [3, 4]]'`.**
* **Any value that is broadcastable to the indexed shape can be assigned to the selection.**

### Broadcasting
**A set of rules by which NumPy functions operate on arrays of different shapes.**
```python
left  = np.array([0.1,  0.6,  0.8])                     # `left.shape  == (3,)`
right = np.array([[0.1], [0.6], [0.8]])                 # `right.shape == (3, 1)`
```

#### 1. If array shapes differ in length, left-pad the shorter shape with ones:
```python
left  = np.array([[0.1,  0.6,  0.8]])                   # `left.shape  == (1, 3)`
right = np.array([[0.1], [0.6], [0.8]])                 # `right.shape == (3, 1)`
```

#### 2. If any dimensions differ in size, expand the ones that have size 1 by duplicating their elements:
```python
left  = np.array([[0.1,  0.6,  0.8],                    # `left.shape  == (3, 3)`
                  [0.1,  0.6,  0.8],
                  [0.1,  0.6,  0.8]])

right = np.array([[0.1,  0.1,  0.1],                    # `right.shape == (3, 3)`
                  [0.6,  0.6,  0.6],
                  [0.8,  0.8,  0.8]])
```

### Example
#### For each point returns index of its nearest point (`[0.1, 0.6, 0.8] => [1, 2, 1]`):

```python
>>> print(points := np.array([0.1, 0.6, 0.8]))
[0.1  0.6  0.8]
>>> print(wrapped_points := points.reshape(3, 1))
[[0.1]
 [0.6]
 [0.8]]
>>> print(deltas := points - wrapped_points)
[[ 0.   0.5  0.7]
 [-0.5  0.   0.2]
 [-0.7 -0.2  0. ]]
>>> deltas[range(3), range(3)] = np.inf
>>> print(distances := np.abs(deltas))
[[inf  0.5  0.7]
 [0.5  inf  0.2]
 [0.7  0.2  inf]]
>>> print(distances.argmin(axis=1))
[1 2 1]
```


Image
-----
```python
# $ pip3 install pillow
from PIL import Image
```

```python
<Image> = Image.new('<mode>', (width, height))  # Creates new image. Also `color=<int/tuple>`.
<Image> = Image.open(<path>)                    # Identifies format based on file's contents.
<Image> = <Image>.convert('<mode>')             # Converts image to the new mode (see Modes).
<Image>.save(<path>)                            # Selects format based on extension (PNG/JPG…).
<Image>.show()                                  # Displays image in default preview app.
```

```python
<int/tup> = <Image>.getpixel((x, y))            # Returns pixel's value (its color).
<ImgCore> = <Image>.getdata()                   # Returns a flattened view of pixel values.
<Image>.putpixel((x, y), <int/tuple>)           # Updates pixel's value. Clips passed int/s.
<Image>.putdata(<list/ImgCore>)                 # Updates pixels with a copy of the sequence.
<Image>.paste(<Image>, (x, y))                  # Draws passed image at the specified location.
```

```python
<Image> = <Image>.filter(<Filter>)              # Use ImageFilter.<name>(<args>) for Filter.
<Image> = <Enhance>.enhance(<float>)            # Use ImageEnhance.<name>(<Image>) for Enhance.
```

```python
<array> = np.array(<Image>)                     # Creates a 2d/3d NumPy array from the image.
<Image> = Image.fromarray(np.uint8(<array>))    # Use <array>.clip(0, 255) to clip the values.
```

### Modes
* **`'L'` - Lightness (greyscale image). Each pixel is an int between 0 and 255.**
* **`'RGB'` - Red, green, blue (true color image). Each pixel is a tuple of three ints.**
* **`'RGBA'` - RGB with alpha. Low alpha (i.e. forth int) makes pixel more transparent.**
* **`'HSV'` - Hue, saturation, value. Three ints representing color in HSV color space.**


### Examples
#### Creates a PNG image of a rainbow gradient:
```python
WIDTH, HEIGHT = 100, 100
n_pixels = WIDTH * HEIGHT
hues = (255 * i/n_pixels for i in range(n_pixels))
img = Image.new('HSV', (WIDTH, HEIGHT))
img.putdata([(int(h), 255, 255) for h in hues])
img.convert('RGB').save('test.png')
```

#### Adds noise to the PNG image and displays it:
```python
from random import randint
add_noise = lambda value: max(0, min(255, value + randint(-20, 20)))
img = Image.open('test.png').convert('HSV')
img.putdata([(add_noise(h), s, v) for h, s, v in img.getdata()])
img.show()
```

### Image Draw
```python
from PIL import ImageDraw
<Draw> = ImageDraw.Draw(<Image>)                # Object for adding 2D graphics to the image.
<Draw>.point((x, y))                            # Draws a point. Also `fill=<int/tuple/str>`.
<Draw>.line((x1, y1, x2, y2 [, ...]))           # For anti-aliasing use <Image>.resize((w, h)).
<Draw>.arc((x1, y1, x2, y2), deg1, deg2)        # Draws in clockwise dir. Also pieslice().
<Draw>.rectangle((x1, y1, x2, y2))              # Also rounded_rectangle(), regular_polygon().
<Draw>.polygon((x1, y1, x2, y2, ...))           # Last point gets connected to the first one.
<Draw>.ellipse((x1, y1, x2, y2))                # To rotate use <Image>.rotate(anticlock_deg).
<Draw>.text((x, y), <str>, font=<Font>)         # `<Font> = ImageFont.truetype(<path>, size)`.
```
* **Use `'fill=<color>'` to set the primary color.**
* **Use `'width=<int>'` to set the width of lines or contours.**
* **Use `'outline=<color>'` to set the color of the contours.**
* **Color can be an int, tuple, `'#rrggbb[aa]'` or a color name.**

