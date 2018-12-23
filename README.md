# mailecho
A small python script which receives an email on stdin, and then sends a reply to sender containing the full original email, including headers.

## Usage
To use this with Postfix:

### Install the script
* Install script somewhere, like /usr/local/bin/mailecho

* Add a line to master.cf to define the mailecho service:
```mailecho unix - n n - - pipe flags=F user=nobody:nobody argv=/usr/local/bin/mailecho```

### Configure Postfix
* Pick an email to use for the MailEcho service and add a transport entry so Postfix knows to send the mail to the mailecho service:

```echo@example.com mailecho:```

* Postfix might not accept mail for the address until you add a mailbox or alias:

```insert into virtual_alias_maps (localpart, domain, destination) values ('echo', 'example.com', 'echo@example.com');```

