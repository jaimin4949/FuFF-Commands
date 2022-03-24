### Ignore Comments of wordlist

`ffuf -u https://example.com/FUZZ/ -w ~/wordlist.txt -ic`

### Color

`ffuf -u https://example.com/FUZZ/ -w ~/wordlist.txt -c`

### Some Matching

- `ml` match lines
- `mw` match words
- `ms` match response size
- `mr` match response like what we want to grep in page
- `fl` filter lines
- `fs` filter response size
- `fw` filter words
- `fr` filter response

### Error Function

- `se` parameter where it will stop our attack when our request is not real.

### Recursion:

If say we have admin then it will repeat that wordlist on same directory

`ffuf -u https://example.com/FUZZ/ -w ~/wordlist.txt -recursion`

We can add deapth on recursion also!

### Recursion with file extension [ Directory + Files ]:

`ffuf -u https://example.com/FUZZ -w ~/wordlist.txt -recursion -e .bak`

### Silent Mode:

`ffuf -u https://example.com/FUZZ -w ~/wordlist.txt -s`

### Output in Proper Fromat:

`ffuf -u https://example.com/FUZZ -w ~/wordlist.txt -of html -o ~/result`

Available file format: ***`json, ejson, html, md, csv, ecsv`***

### Matching or Filter

- mc [Match particular response code]

### Authentication

Cookies base authentication

`ffuf -u https://example.com/FUZZ -w ~/wordlist.txt -b "NAME1=VALUE1; NAME2=VALUE2"`

Header base authentication

`ffuf -u https://example.com/FUZZ -w ~/wordlist.txt -H "NAME1=VALUE1; NAME2=VALUE2"`

### Authentication via BURP

Burp > Proxy > Options

Add new port and host

### Multiple domains for fuzzing

`ffuf -u https://W2.io/W1 -w ~/wordlist:W1 -w ~/domains:W2`

- [ ]  Main use of this method is to fuzz multiple domains via same wordlist in one go

### Capture request in burp. Save Request in file. Add FUZZ keyword in that file where we want to fuzz

`ffuf -request ~/request.txt -w ~/wordlist.txt`

### Pitch Fork Method

```
Username.txt     Password.txt
Admin            Password
Sam              Okay
```

Here Pitch Fork method will automatically match 1st line with 1st line

### Delay or Limited Request

Delay: `-p 0.1-2` It will send request one by one after specific time

Limited Request: `-rate 2` send new request after 2 seconds

Thread: `-t 3` Change thread level from 40 to 3

### Filter the response/status code using regex

`ffuf -u https://www.example.com/FUZZ -w ~/wordlist.txt -reply-proxy http://127.0.0.1:8080 -fc "Some error with 200 OK Response but with empty body"`

It will filter that successful request from ffuf

### Send Post data

We can use this method to change the parameters of body [ For Test]

`ffuf -u https://www.example.com/login -w ~/wordlist.txt -d "email=test@mail.com&password=FUZZ"`

### Send PUT Request

`ffuf -u https://www.test.com/user -w ~/wordlist.txt -X "PUT" -H "Content-Type: application/json" -d "{'FUZZ':'User Data'}"`

### Reply Proxy

`ffuf -u https://www.example.com/FUZZ -w ~/wordlist.txt -reply-proxy http://127.0.0.1:8080`

Send all the successful request to Burp
