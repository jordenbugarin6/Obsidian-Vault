###### Links:
[[2.2.1 - 2.2.7 Web Application Enumeration]]

------------
This script is utilized to generate multiple combinations of potential usernames by utilizing the names provided.
```python
names = [
    "Ernesto Freeman",
    "Jane Smith",
    "Alice Johnson",
    "joe sheer",
    "tom hudson",
    "tanya rivera",
    "matt smith",
    "mike carlow",
    "alan grofield",
    "roxanne jones",
    "ernesto freeman",
    # Add more names here
]

usernames = []

for name in names:
    first_name, last_name = name.split()
    first_initial = first_name[0].lower()
    last_initial = last_name[0].lower()
    
    usernames.extend([
        first_name.lower(),  # ernesto
        first_name.lower() + last_name.lower(),  # ernestofreeman
        first_initial + last_name.lower(),  # efreeman
        first_initial + '.' + last_name.lower(),  # e.freeman
        first_name.lower() + '_' + last_name.lower(),  # ernesto_freeman
        first_initial + '_' + last_name.lower(),  # e_freeman
        last_name.lower() + first_initial,  # freemane
        last_name.lower() + '.' + first_initial,  # freeman.e
        last_name.lower() + first_name.lower(),  # freemanernesto
        first_name.lower() + '.' + last_name.lower(),  # ernesto.freeman
        first_initial + last_initial,  # ef
        first_initial + '_' + last_initial,  # e_f
        first_name.lower() + last_initial,  # ernestof
        first_name.lower() + '.' + last_initial,  # ernesto.f
        first_name.lower() + '-' + last_name.lower(),  # ernesto-freeman
        first_initial + '-' + last_name.lower(),  # e-freeman
        last_name.lower() + '-' + first_initial,  # freeman-e
        last_name.lower() + '_' + first_initial,  # freeman_e
        first_name.lower() + last_name.lower()[0],  # ernestof
        first_name.lower() + '-' + last_initial,  # ernesto-f
        last_name.lower() + '.' + first_initial,  # freeman.e
        first_initial + last_initial + first_name.lower(),  # ef_ernesto
        first_initial + last_initial + '.' + first_name.lower(),  # ef.ernesto
        last_name.lower() + '_' + first_initial + last_initial,  # freeman_ef
        last_name.lower() + '.' + first_initial + last_initial,  # freeman.ef
        first_name.lower() + last_name.lower(),  # ernestofreeman
        first_initial + last_name.lower(),  # efreeman
        first_name.lower() + '.' + last_name.lower(),  # ernesto.freeman
        first_name.lower() + '-' + last_name.lower(),  # ernesto-freeman
        first_name.lower() + last_initial + '1',  # ernestof1
        first_name.lower() + last_name.lower() + '123',  # ernestofreeman123
    ])

with open("usernames.txt", "w") as f:
    for username in usernames:
        f.write(username + "\n")

```
This script spits the results out into the `usernames.txt` file
```bash
┌──(kali㉿gobots)-[17Jul2024 20:22:47]-[~/SUT/OSWA]
└─$ cat usernames.txt
ernesto
ernestofreeman
efreeman
e.freeman
```