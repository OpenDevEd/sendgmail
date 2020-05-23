# sendgmail
Send gmail form the commandline

Basic options: to/from/cc/bcc/subject:
```
python3 sendgmail.py --to "..." --from "..." --cc "..." --bcc "..." --subject "..." --message "..."
```

Message options:
```
python3 sendgmail.py --message "..." 
python3 sendgmail.py --file message.txt
cat message.txt | python3 sendgmail.py
```
If all three options are present, they are processed in the way shown above.

Attachments:
```
python3 sendgmail.py --attach file.pdf [file.pdf] 
```

# Configuration

Saved configuration: Can be included (1) on the command line
```
python3 sendgmail.py --configuration config.json
```
or (2) be in a file config.json in the current directory.

If those are not the case, but `--sender ABC@DEF` is specified then (3)
```
$HOME/.config/sendgmail/ABC@DEF/config.json
```
is checked. Finally, (4)
```
$HOME/.config/sendgmail/config.json
```
is checked.

The config file looks like
```
{
"to": "...",
"from": "...",
"cc": "...",
"bcc": "...",
"subject": "...",
"attach": [ "...pdf", "...jpg", ...],
"message": "some text",
"file": "textfile.txt",
"credentials": "credentials.json",
"token": "token.pickle"
}
```
Note that all credentials and token files are relative to the config file, unless you use `./` or '/', i.e.,
```
{
"credentials": "./credentials.json",
"token": "./token.pickle"
}
```
or
```
{
"credentials": "/home/user/somewhere/credentials.json",
"token": "/home/user/somewhere/token.pickle"
}
```

#Credentials / token

Most (1) either be included on the command line:
```
python3 sendgmail.py --credentials credentials.json --token token.pickle
```
or (2) must be in files credentials.json/token.pickle in the current directory or (3) must be specified in the config file (see above).

If none of these, then if `--sender ABC@DEF`, then (4)
```
$HOME/.config/sendgmail/ABC@DEF/credentials.json
$HOME/.config/sendgmail/ABC@DEF/token.pickle
```
is checked and finally (5)
```
$HOME/.config/sendgmail/credentials.json
$HOME/.config/sendgmail/token.pickle
```
is checked. I.e., command line takes highest precedence, `$HOME/.config/sendgmail` takes lowest precedence.
