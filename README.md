# Apache Log Analyser

A Python program that helps a web server administrator check Apache log
files. You pick what to look at from a simple menu in the terminal.

**Author:** Melanie Chu
**Course:** OPS435 Assignment 1
**Status:** Part 1 (menus) and Part 2 (log parsing) are done.

## What it does

The program reads one or more Apache log files, then answers these questions:

**Successful requests**
- How many requests had status code 200?
- How many came from Seneca (IP addresses starting with 142.204)?
- How many were for OPS435_Lab?

**Failed requests**
- How many requests had status code 404 ("Not Found")?
- How many of those 404 requests had "hidebots" in the URL?
- Which IP addresses caused a 404? (each one is listed only once)

## How it works

1. The log files given on the command line are read, and every line is stored
   in one list called `all_log_lines`.
2. Each line is split into its parts (IP address, request, status code) using
   a regular expression.
3. Each report goes through the lines, counts or collects what it needs, and
   prints the result.
4. For the 404 IP list, the IPs are stored as keys in a dictionary, because a
   dictionary cannot hold the same key twice. This removes duplicates.

## How to run it

You need Python 3. Type the script name followed by one or more log files:

```
./check_apache_log_ckhna.py wiki-access_log*
```

If you get "permission denied", run this once:

```
chmod +x check_apache_log_ckhna.py
```

### Skip the menu

Add `-d` (or `--default`) before the file names. The program loads the files,
prints the total number of requests with code 200, and exits:

```
./check_apache_log_ckhna.py -d wiki-access_log*
```

### What happens if I type it wrong?

| What you type | Result |
|---|---|
| Nothing after the script name | Shows an error and stops |
| `-d` with no file names | Shows an error and stops |
| `-d` and file names | Loads the files, shows the Code 200 total, stops |
| File names only | Loads the files, shows the main menu |

## Using the menus

- Type the number of the option you want and press Enter.
- Type `q` to go back to the previous menu. In the main menu, `q` quits.
- If you type something that is not on the menu, the program asks you to try
  again.

## Test logs

The log files used for testing are not included in this repository. They can be
downloaded here: <http://ops345.ca/ops445/wiki_access_logs.tar.bz2>

## References

- Assignment instructions: [OPS445 Assignment 1 Part 2](http://wiki.littlesvr.ca/wiki/OPS445_Assignment_1_Part_2),
  Littlesvr Wiki (content by Andrew Smith)
- Sample log files: <http://ops345.ca/ops445/wiki_access_logs.tar.bz2>