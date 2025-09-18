![[Pasted image 20240907135640.png]]
#### Docker 

```bash
┌──(root💀gobots)-[07Sep2024 18:03:06]-[/home/…/CSAW/charlies_Angels/challenge/node]
└─# docker build -t charlies_angels_node .         
Sending build context to Docker daemon   51.2kB
Step 1/11 : FROM node                             
latest: Pulling from library/node
8cd46d290033: Pull complete 
2e6afa3f266c: Pull complete 
2e66a70da0be: Pull complete 
1c8ff076d818: Pull complete 
45000ff9cd9c: Pull complete 
4326bccabba6: Pull complete 
3156cb54c99e: Pull complete 
b3d4302e0b06: Pull complete 
Digest: sha256:bd00c03095f7586432805dbf7989be10361d27987f93de904b1fc003949a4794
Status: Downloaded newer image for node:latest
 ---> dd6ce0f28c3c                                
Step 2/11 : WORKDIR /usr/src/app
 ---> Running in af49510a6ac1
Removing intermediate container af49510a6ac1
 ---> 732a12a99657                                
Step 3/11 : RUN mkdir -p sessions
 ---> Running in dafbd014bc14
Removing intermediate container dafbd014bc14
 ---> 6083540ee5e2                                
Step 4/11 : COPY package*.json ./
 ---> 981e083faf0d                                
Step 5/11 : RUN npm install
 ---> Running in cdc6566f5402

added 90 packages, and audited 91 packages in 3s

12 packages are looking for funding
  run `npm fund` for details
  Removing intermediate container cdc6566f5402
 ---> 1f4e09da9c21                                
Step 6/11 : COPY . .                              
 ---> a022cbd8e638                                
Step 7/11 : EXPOSE 1337                           
 ---> Running in 85bedd1e53c0
Removing intermediate container 85bedd1e53c0
 ---> 65272dc4f8df                                
Step 8/11 : RUN chmod -R 1777 /usr/src/app/sessions
 ---> Running in 7a658a1622b8
Removing intermediate container 7a658a1622b8
 ---> 738e4997b5f1                                
Step 9/11 : RUN useradd ctf
 ---> Running in 4274c4ccd3fc
Removing intermediate container 4274c4ccd3fc
 ---> cdb05fd598c9                                
Step 10/11 : USER ctf                             
 ---> Running in ebb8be62e76b
Removing intermediate container ebb8be62e76b
 ---> 22c835052c72                                
Step 11/11 : CMD [ "node", "index.js"]
 ---> Running in 69f6093fb189
Removing intermediate container 69f6093fb189
 ---> faee47ea626e                                
Successfully built faee47ea626e
Successfully tagged charlies_angels_node:latest
```
run
```bash
┌──(root💀gobots)-[07Sep2024 18:10:45]-[/home/…/CSAW/charlies_Angels/challenge/node]
└─# docker run -d -p 1337:1337 --name charlies_angels_node_container charlies_angels_node
f85bc94f70fefef4a9cd19749d687205f3a0868990080d410f699f1b0559b232
```
docker ps
```bash
┌──(root💀gobots)-[07Sep2024 18:11:24]-[/home/…/CSAW/charlies_Angels/challenge/node]
└─# docker ps                                                                            
Device "veth8db2871@if37" does not exist.
Device "veth8db2871@if37" does not exist.
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                                       NAMES
f85bc94f70fe   charlies_angels_node   "docker-entrypoint.s…"   6 seconds ago   Up 4 seconds   0.0.0.0:1337->1337/tcp, :::1337->1337/tcp   charlies_angels_node_container

```
#### Web Page - 1338 - node
Once docker is setup brose to `0.0.0.0:1337`, browse to `UR ANGEL`
![[Pasted image 20240907143743.png]]
In the `REPEATER` request, we can see an `id` and angel assigning with `talents`
![[Pasted image 20240907144123.png]]
Browsing to `RESTORE AN ANGEL` `REPEATER` request
![[Pasted image 20240907144442.png]]
Entering shell and listing .js, going to open on `VSCODE` for source code review
```bash
┌──(root💀gobots)-[07Sep2024 18:46:14]-[/home/kali]                                                                                                        
└─# docker exec -it charlies_angels_node_container /bin/bash                                                                                                                                               
Device "veth8db2871@if37" does not exist.                                                                                                                   
Device "veth8db2871@if37" does not exist.                                                                                                                                                                  
ctf@f85bc94f70fe:/usr/src/app$ ls                                                                                                                           
Dockerfile  angels.js  index.js  node_modules  package-lock.json  package.json  public  sessions   
```
#### Setting up Docker networking to run both node and app.py
```bash
┌──(root💀gobots)-[07Sep2024 19:40:30]-[/home/…/CSAW/charlies_Angels/challenge/py]
└─# docker network create my-network        
Device "veth8db2871@if37" does not exist.
Device "veth8db2871@if37" does not exist.
2d137962fc477837fb086b88442f4b7b33ed597a2da103e81096965e99557c9e
```
#### Web Source


##### Index.html

<html lang="en">
   <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap" rel="stylesheet">
      <link href="https://fonts.googleapis.com/css2?family=Anek+Bangla:wght@100..800&display=swap" rel="stylesheet">
      <title>CHARLIE'S ANGELS</title>
      <style>
        * {
            text-align: center;
            font-family: "Anek Bangla";
         }
         @font-face {
         font-family: "Abril Fatface", serif;
         font-weight: 400;
         font-style: normal;
         src: url(abril-fatface-regular.woff2) format('woff2');
         }
         @font-face {
         font-family: "Anek Bangla", sans-serif;
         font-optical-sizing: auto;
         font-weight: 350;
         font-style: normal;
         src: url(anek-bangla.woff2) format('woff2');
         font-variation-settings:
            "wdth" 100;
         }
         H1 {
            font-family: "Abril Fatface";
         }

      </style>
   </head>
   <body>
      <img src="https://i.pinimg.com/originals/8f/68/2d/8f682d9e6cca66bee6aa1e1835cc161f.gif"></img>
      <h1>WELCOME TO THE CHARLES TOWNSEND DETECTIVE AGENCY</h1>
      <a href="/angel">UR ANGEL</a>
      <a href="/restore">RESTORE AN ANGEL</a>
      <br>
   </body>
###### Code
```html
<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap" rel="stylesheet">
      <link href="https://fonts.googleapis.com/css2?family=Anek+Bangla:wght@100..800&display=swap" rel="stylesheet">
      <title>CHARLIE'S ANGELS</title>
      <style>
        * {
            text-align: center;
            font-family: "Anek Bangla";
         }
         @font-face {
         font-family: "Abril Fatface", serif;
         font-weight: 400;
         font-style: normal;
         src: url(abril-fatface-regular.woff2) format('woff2');
         }
         @font-face {
         font-family: "Anek Bangla", sans-serif;
         font-optical-sizing: auto;
         font-weight: 350;
         font-style: normal;
         src: url(anek-bangla.woff2) format('woff2');
         font-variation-settings:
            "wdth" 100;
         }
         H1 {
            font-family: "Abril Fatface";
         }

      </style>
   </head>
   <body>
      <img src="https://i.pinimg.com/originals/8f/68/2d/8f682d9e6cca66bee6aa1e1835cc161f.gif"></img>
      <h1>WELCOME TO THE CHARLES TOWNSEND DETECTIVE AGENCY</h1>
      <a href="/angel">UR ANGEL</a>
      <a href="/restore">RESTORE AN ANGEL</a>
      <br>
   </body>
</html>
```

##### error.html
<html lang="en">
   <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <title>CHARLIE'S ANGELS</title>
      <style>
        * {
            text-align: center;
        }
      </style>
   </head>
   <body>
    <h1>ERROR!</h1>
    <p>CHARLES TOWNSEND DETECTIVE AGENCY</p>
   </body>
</html>
###### Code
```html
<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <title>CHARLIE'S ANGELS</title>
      <style>
        * {
            text-align: center;
        }
      </style>
   </head>
   <body>
    <h1>ERROR!</h1>
    <p>CHARLES TOWNSEND DETECTIVE AGENCY</p>
   </body>
</html>
```
##### angels.js
- Shows a List of angels
```bash
const angels = [
    {
        name: "Jill Munroe",
        actress: "Farrah Fawcett-Majors",
        movie: "OG Charlie's Angels TV Series",
        talents: {
            "0": "Racecar Driving",
            "1": "Gun Wielding",
            "2": "Baking"
        }
    },
    {
        name: "Sabrina Duncan",
        actress: "Kate Jackson",
        movie: "OG Charlie's Angels TV Series",
        talents: {
            "0": "Intuition",
            "1": "Skiing",
            "2": "Gun Wielding"
        }
    },
    {
        name: "Kelly Garett",
        actress: "Jaclyn Smith",
        movie: "OG Charlie's Angels TV Series",
        talents: {
            "0": "Unarmed Combat",
            "1": "Gun Wielding",
            "2": "Roller Skating",
            "3": "Leadership"
        }
    },
    {
        name: "Kris Munroe",
        actress: "Cheryl Ladd",
        movie: "OG Charlie's Angels TV Series",
        talents: {
            "0": "Scuba Diving",
            "1": "Unarmed Combat",
            "2": "Bushcraft",
            "3": "Chemistry",
            "4": "Surfing",
            "5": "Roller Skating"
        }
    },
    {
        name: "Tiffany Welles",
        actress: "Shelley Hack",
        movie: "OG Charlie's Angels TV Series",
        talents: {
            "0": "Knot-tying",
            "1": "Latin",
            "2": "Truck-driving",
            "3": "Biology"
        }
    },
    {
        name: "Julie Rogers",
        actress: "Tanya Rogers",
        movie: "OG Charlie's Angels TV Series",
        talents: {
            "0": "Driving",
            "1": "Scuba Diving",
            "2": "Modelling"
        }
    },
    {
        name: "Natalie Cook",
        actress: "Cameron Diaz",
        movie: "Charlies Angels: Full Throttle",
        talents: {
            "0": "Unarmed Combat",
            "1": "Driving",
            "2": "Helicopter Piloting",
            "3": "Disguise"
        }
    },
    {
        name: "Dylan Sanders",
        actress: "Drew Barrymore",
        movie: "Charlies Angels: Full Throttle",
        talents: {
            "0": "Unarmed Combat",
            "1": "Disguise",
            "2": "Wrestling",
            "3": "Mongolian",
            "4": "Spanish"
        }
    },
    {
        name: "Alex Munday",
        actress: "Lucy Liu",
        movie: "Charlies Angels: Full Throttle",
        talents: {
            "0": "Unarmed Combat",
            "1": "Strategist",
            "2": "Safe Cracking",
            "3": "Bomb Defusal",
            "4": "Aerospace Engineering",
            "5": "Chess",
            "6": "Gymnastics",
            "7":"Archery",
            "8": "Horseriding"
        }
    },
    {
        name: "Sabina Wilson",
        actress: "Kristen Stewart",
        movie: "Charlie's Angels (2019)",
        talents: {
            "0": "Unarmed Combat",
            "1": "Acrobatics",
            "2": "Gun Wielding",
            "3": "Horseriding"
        }
    },
    {
        name: "Jane Kano",
        actress: "Ella Balinska",
        movie: "Charlie's Angels (2019)",
        talents: {
            "0": "Unarmed Combat",
            "1": "Gun Wielding",
            "2": "Tactics"
        }
    },
    {
        name: "Elena Houghlin",
        actress: "Naomi Scott",
        movie: "Charlie's Angels (2019)",
        talents: {
           "0":  "Hacking"
        }
    }

];

module.exports.randomAngel = () => {
    return angels[Math.floor(Math.random() * angels.length)];
};;
```
##### index.js
```js
const express = require('express');
const app = express();
const YAML = require('yaml');
const crypto = require("crypto");
const session = require('express-session');
var FileStore = require('session-file-store')(session);
const needle = require("needle");

const angels = require('./angels');
const BACKUP = process.env.backup || "http://localhost:1338";
app.use(express.json());
app.use(express.static('public'))
app.use(session({
    store: new FileStore({
        fileExtension: ".yaml",
        encoder: YAML.stringify,
        decoder: YAML.parse
    }),
    secret: crypto.randomBytes(30).toString('hex'),
    cookie: { secure: false },
    saveUninitialized: true,
    resave: false
}));

app.get('/', (req, res) => {                                      /// when a get request goes to `/` directory, displays index.html
    res.sendFile('public/html/index.html', {root: __dirname});
});

app.get('/angel', async (req, res) => {                           /// when navigating to /angel directory spits out a random angel pulled from angels.js
    if (!req.session.angel) {
        req.session.angel = angels.randomAngel();
    }
    const data = {
        id: req.sessionID,                                        /// returns SessionID and angel data in json format
        angel: req.session.angel                                
    }
    res.set('Content-Type', 'application/json');
    return res.status(200).send(JSON.stringify(data));
});

app.post('/angel', (req, res) => {                                /// post request to /angel directory enables a request and response
    for (const [k,v] of Object.entries(req.body.angel)) {         /// if the request contains angel the method returns an objects key, value pairs - 
        if (k != "talents" && typeof v != 'string') {             /// if key != talents and valueds isnt a string send ERROR
            return res.status(500).send("ERROR!");
        }
    }
    req.session.angel = {                                         /// submitting name / actress/ movie fields
        name: req.body.angel.name,
        actress: req.body.angel.actress,
        movie: req.body.angel.movie,
        talents: req.body.angel.talents
    };
    const data = {
        id: req.sessionID,
        angel: req.session.angel
    };
    const boundary = Math.random().toString(36).slice(2) + Math.random().toString(36).slice(2);
    needle.post(BACKUP + '/backup', data, {multipart: true, boundary: boundary},  (error, response) => {
        if (error){
            console.log(error);
            return res.status(500).sendFile('public/html/error.html', {root: __dirname});
        }
    });
    return res.status(200).send(req.sessionID);

});

const authn = (req, res, next) => {
    if (!req.session.angel) return res.status(403).sendFile('public/html/error.html', {root: __dirname});
    next();
}

app.get('/restore', authn, (req, res) => {  
    let restoreURL = BACKUP + `/restore?id=${req.sessionID}`;
    console.log(restoreURL);
    needle.get(restoreURL, (error, response) => {
        try {
            if (error) throw new Error(error);
            if (response.body == "ERROR") throw new Error("HTTP Client error");
            return res.send(response.body);
        } catch (e) {
            if (e.message != "HTTP Client error") {
                console.log(e);
            }
            return res.status(500).sendFile('public/html/error.html', {root: __dirname});
        }
    });
});

app.all('*', (req, res) => {
    return res.status(404).sendFile('public/html/error.html', {root: __dirname});
});

const PORT = 1337;
app.listen(PORT, () => {
    console.log(`[${new Date(Date.now())}]: Listening on port ${PORT}`);
});
```






-------
#### Burp
Analyzing the original `/angel` and sending to repeater
![[Pasted image 20240907171536.png]]
after sending it to repeater and hitting send we get the angel `alex Munday`
![[Pasted image 20240907171642.png]]
copy and paste the response starting with `id` to `8` and have chat gpt reformat it into a `POST` request
```json
POST /angel HTTP/1.1
Host: 0.0.0.0:1337
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://0.0.0.0:1337/
Accept-Encoding: gzip, deflate, br
Cookie: pyramid=eyJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJST0xFIjoiY29tbW9uZXIiLCJDVVJSRU5UX0RBVEUiOiIwN18wOV8yMDI0X0FEIiwiZXhwIjo5NjMzMzcyOTYyMH0.D4HWEl77xlrA4_i7Qb0aoLxd7aU-yutN1xfdYy9YHj4cg8gIZEx1-8jG2zqxKBfwsoFg4PREH6rYj_bNpA8EAg; connect.sid=s%3AaLHN8XiUnJcO-A-yk7a_EAQ8EF5ZZryh.3t7xL0MJ2Cnt3XAJbr12EUhqYzDNSYAtFmlyFcUEZ1g
Connection: keep-alive
Content-Length: 400
Content-Type: application/json

{
  "id": "ynv2EzbIkpVtD05duHQXkn3ix7ewSjK6",
  "angel": {
    "name": "Alex Munday",
    "actress": "Lucy Liu",
    "movie": "Charlies Angels: Full Throttle",
    "talents": [
      "Unarmed Combat",
      "Strategist",
      "Safe Cracking",
      "Bomb Defusal",
      "Aerospace Engineering",
      "Chess",
      "Gymnastics",
      "Archery",
      "Horseriding"
    ]
  }
}
```
sending the `POST` request back spits out a random string of characters - going to look at the source code to see what is going on with it
![[Pasted image 20240907173823.png]]


Example boundary code
```
l8kj9ht3f3u5pf9d4mfr1z4u
```
Ours from the Response
```
M9mCJ6wFALkQwJ5pRcl-25abG1itwBG
```