# 🐝Team Bee

A word game based off of NYT's Spelling Bee. This repo includes the game UI. The backend API lives in [github.com/lokesh/team-bee-api](https://github.com/lokesh/team-bee-api).

## 🛠 To-do

**Next**
- [x] Admin for puzzle lists and generation.
- [ ] Fix, date in UI one day off.
- [ ] Save puzzles from admin. Check when saving to make sure combo of letters has not been prev used.
- [x] Auto-gen puzzles from admin
- [ ] Use socket.io to relay word additions between players
- [ ] Add simple token based security for puzzle crud

- [ ] Load latest puzzle by date

**UI**
- [ ] Fix name tags rounded corners
- [ ] Fix ios tap delay
- [ ] Reduce tap transition time
- [ ] Add feedback when delete, shuffle, and enter are pressed with kbd

**Real-time**
- [ ] Design distinct notifications for real-time.

**Gameplay**
- [ ] Once answers revealed, disable submitting new words for that puzzle for that user?

**User mgmt and security**
- [ ] Think about token for teams. Requiring a token to see user list on login.
- [ ] User sign up form
- [ ] API authentication


**Before sharing**
- [ ] Find a domain and final name
- [ ] Update design to prevent any confusion with the original NYT game.
- [ ] Give credit where credits are due for game design.


## 👨‍💻 Local development

### Quick reference

```
npm run serve // Compiles and hot-reloads for development
npm run build // Compiles and minifies for production
npm run lint
npm run deploy // FTPs files to lokeshdhakar.com/project/team-bee
```

### Set up

When the node env is set to `development`, the app will look for the API on localhost. You'll need to spin up the team-bee-api Node Express server for this.

The production API server hosted on Heroku has limited CORS domain origins to https://lokeshdhakar.com.

## 🚀 Deploy

This project is hosted on a shared static server alongside my other content for lokeshdhakar.com. The files are sent up via ftp. 🐌

## 👷‍♀️ Architecture

### API

```
GET    /users
GET    /users/:id
GET    /puzzles
POST   /puzzles
GET    /puzzles/:id
GET    /puzzles/:id/users
GET    /puzzles/:id/users/:userId
POST   /puzzles/:id/users/:userId
PUT    /puzzles/:id/users/:userId
```

### Data init and bootstrapping

- **User**: We store the current user in localStorage and store it on app start up. If we don't find it, we have a router guard that will route them to Login screen.
- **Users**: Loaded on app creation.
- **Puzzles**: Loaded on app creation.


App.js - created...

- Load user list
- Load puzzle list

users: [id, name]
puzzles: [id, name, date]

- Set current puzzle as puzzle who has latest date that is not in future

puzzle: id, name, date, config, userProgress

### Data CRUD

#### Puzzles

Manually enter in DB.

#### Users

Manually enter in DB.


### For next time

- **PostgreSQL**: I spent way to much time fighting postgres. It was challenging to figure out things that should have been easy such as picking out the right data types and setting proper defaults (e.g. '{}'::character varying[] to set a default empty varchar array). The docs are bad.
- User mgmt
- API auth
- Polling for DB writes?


_Scratchpad_

It took a couple tries, but I'm happy with the db schema and the Vuex store organization. Write down some of the issues I ran into in the two prev iterations.


1. Prefer initializing your store's initial state with all desired fields upfront.
2. When adding new properties to an Object, you should either:
* Use Vue.set(obj, 'newProp', 123), or
* Replace that Object with a fresh one. For example, using the object spread syntax
 we can write it like this:
state.obj = { ...state.obj, newProp: 123 }


