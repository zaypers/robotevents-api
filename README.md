# RobotEvents API Wrapper
<a href="https://www.npmjs.com/package/robotevents-api"><img src="https://img.shields.io/npm/v/robotevents-api"></a>
<a href="https://www.npmjs.com/package/robotevents-api"><img src="https://badgen.net/packagephobia/install/robotevents-api"></a>
<a href="https://github.com/zaypers/robotevents-api/blob/main/LICENSE"><img src="https://img.shields.io/github/license/zaypers/robotevents-api"></a>
<br>

This is a wrapper for the RobotEvents API:  
https://www.robotevents.com/api/v2

Currently it's in the Alpha phase supporting only /teams URLs.  

This includes  
\- /teams  
\- /teams/{id}  
\- /teams/{id}/events  
\- /teams/{id}/matches  
\- /teams/{id}/rankings  
\- /teams/{id}/skills  
\- /teams/{id}/awards  

## Installation

To start using this package, install it using ``npm`` and a ``terminal``. Enter this command into the terminal:
```
npm install robotevents-api
```

Also install the dotenv package:  
https://www.npmjs.com/package/dotenv  
```
npm install dotenv
```

In a .env file in the directory with your app.js file, add your RobotEvents token with the key of 'TOKEN'.  

<img src="https://github.com/zaypers/robotevents-api/raw/main/assets/source-dir.png" style="width: 14em"><br>  

Example (this is not a real token):  
<img src="https://github.com/zaypers/robotevents-api/raw/main/assets/dotenv-token.png">  

## Usage

In your ``app.js`` or ``index.js`` file, start by writing:  
```javascript
main();

async function main() {
  // start your code here
};
```  
This is required because all functions ran using this package are ``async``, meaning they run in the background. Whenever you call a method, you will have to use the keyword ``await`` before it.  

To fetch a ``Team``, use the method ``robotevents.teams.get(number, program)``. Replace ``number`` with the team number (ex. 392X or 23900B) and replace ``program`` with the program (ex. VRC or VIQC).
```javascript
const team = await robotevents.teams.get('392X', 'VRC');
```  
This will return a ``Team`` object. For more details on the data that a ``Team`` object contains, go to the file ``/src/api/teams.ts``.  

The ``Team`` object contains several methods, mostly mirrored with the URLs on https://www.robotevents.com/api/v2: ``.events()``, ``.matches()``, ``rankings()``, ``skills()``, ``awards()``.  

```javascript
const team = await robotevents.teams.get('392X', 'VRC');
const events = await team.events();
const matches = await team.matches();
const rankings = await team.rankings();
const skills = await team.skills();
const awards = await team.awards();
```  

``Team.events()`` has a few optional perameters, which you keep inside of an object and pass in as the first argument.  
Arguments include ``sku``, ``season``, and ``level``.

```javascript
const team = await robotevents.teams.get('23900B', 'VRC');
const events = await team.events({
  sku: 'RE-VRC-21-5434',
  season: '2021-2022',
  level: 'World'
});
```

``Team.matches()`` has a few optional perameters, which you keep inside of an object and pass in as the first argument.  
Arguments include ``eventId``, ``instance``, and ``matchnum``.

```javascript
const team = await robotevents.teams.get('23900B', 'VRC');
const matches = await team.matches({
  eventId: 45414,
  instance: 1,
  matchnum: 1
});
```

``Team.rankings()`` has a few optional perameters, which you keep inside of an object and pass in as the first argument.  
Arguments include ``eventId`` and ``rank``.

```javascript
const team = await robotevents.teams.get('23900B', 'VRC');
const rankings = await team.rankings({
  eventId: 46025,
  rank: 19
});
```

``Team.skills()`` has a few optional perameters, which you keep inside of an object and pass in as the first argument.  
Arguments include ``eventId`` and ``type``.

```javascript
const team = await robotevents.teams.get('23900B', 'VRC');
const skills = await team.skills({
  eventId: 47030,
  type: 'driver'
});
```

``Team.awards()`` has a few optional perameters, which you keep inside of an object and pass in as the first argument.  
Arguments include ``eventId``.

```javascript
const team = await robotevents.teams.get('315Y', 'VRC');
const awards = await team.awards({
  eventId: 47029
});
```