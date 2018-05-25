# User Admin

Add new user bacon:
```
sudo adduser bacon
```
Enter password twice.
Enter full name. `bacon`
Press enter on other prompts.

Add sudo privilege:
```
sudo usermod -aG sudo bacon
```

See which groups user belongs to:
```
groups bacon
```
