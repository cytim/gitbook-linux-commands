# SSH


### Generate A New SSH Key-pair

> Reference: [GitHub Help](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

```sh
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**Example Output**

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/cytim/.ssh/id_rsa): /home/cytim/.ssh/id_rsa
Created directory '/home/cytim/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/cytim/.ssh/id_rsa.
Your public key has been saved in /home/cytim/.ssh/id_rsa.pub.
```

