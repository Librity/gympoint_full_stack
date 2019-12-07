# Rocketseat Bootcamp Cerification Challenge

<h1 align="center">
  <img alt="Gympoint" title="Gympoint" src=".github/logo.png" width="200px" />
</h1>

<h3 align="center">
  Gympoint Full Stack
</h3>

## 🚀 About the challenge

This is my submission for the Bootcamp's final challenge: a full-stack application
that lets administrators manage daily gym functions and lets students post questions
about workouts and healthy habits.

I put a lot of hard work in this entire process, even lost
a girlfriend. I hope ya'll like my work and see the passion behind each line of code.
It's been crazy these last few months. I'm stocked this is finally done.

### 🤖 Running the back-end

To boot, we need to create three Docker containers to handle the applications
various jobs and databases. Assuming you have
[Docker installed](https://docs.docker.com/install/), run these:

```
docker run --name postgres -e POSTGRES_PASSWORD=docker -p 5432:5432 -d -t postgres
docker run --name mongo -p 27017:27017 -d -t mongo
docker run --name redis -p 6379:6379 -d -t redis:alpine
```

and wait for the machines to boot. We then navigate into to the project's
directory, create a .env file

```
cd gympoint_back_end
```

and fill it in with the relevant info.

```
APP_URL=http://YOU.R00.000.0IP
NODE_ENV=development

# Auth

APP_SECRET=9d2b2e84e506a7af0fa6e2103366793e

# Database

DB_HOST=localhost
DB_USER=postgres
DB_PASS=docker
DB_NAME=gympoint

# Mongo

MONGO_URL=mongodb://localhost:27017/gympoint

# Redis

REDIS_HOST=127.0.0.1
REDIS_PORT=6379

# Mail

MAIL_HOST=
MAIL_PORT=
MAIL_USER=
MAIL_PASS=

# Sentry

SENTRY_DSN=
```

We then run the initial yarn and sequelize configuration,

```
yarn
yarn sequelize db:create
yarn sequelize db:migrate
yarn sequelize db:seed:all
```

after which we can finally run the backend:

```
yarn dev
```

With a mail service configured we can also run the jobs machine in another Screen

```
yarn queue
```

Also, check out the the insomnia workspaces inside `gympoint_back_end/insomnia_workspaces`.

### 🖥️ Running the web front-end

We then open a third screen, navigate into the project's directory and run yarn:

```
cd gympoint_front_end_web
yarn
```

and edit the api's url to match the back-end's

```
nano ./src/services/api.js
```

```
import axios from 'axios';

const api = axios.create({
  baseURL: 'http://YOU.R00.000.0IP:3333',
});

export default api;
```

We then start the development server, and the web app should pop right up:

```
yarn start
```

The deault admin user is `admin@gympoint.com`, password `123456`.

### 📱 Running the Android front-end

We then open a fourth screen, navigate into the project's directory and run yarn again:

```
cd gympoint_front_end_mobile
yarn
```

Also edit the api's url like in the step above:

```
nano ./src/services/api.js
```

If you do decide to run it on an Android phone, you'll first have to:

- Enable Developer Options;
- Enable USB Debugging;
- Go to your PHONE app (yeah, the one where you make phone calls in), dial
  `*#0808#` and enable `MTP + ADB`;
- Run:

```
adb devices
adb reverse tcp:9090 tcp:9090
react-native start
```

- And in a fifth screen:

```
react-native run-android
```

This takes a while, so grab yoursel a cold one. Now I'm not gonna get into whether
or not you should emulate this thing, but I recomend running it in a physical Android
device. I do not own or ever plan on owning a mac, and I plan to develop exclusively
for Android and hire some bloke with more money to squeeze it into Apple's crocodilian
mouth.

Hopefully by now you'll have the entire project working on both fronts and
consuming the API.

## 💖 Acknowledgements

I would like to thank everyone who's helped me in getting this certificate:
My parents, my brother, my colleagues [Thiago Durante](https://github.com/thdurante),
[Lucas Amaral](https://github.com/linkbolto) and [Nicolas Marçal](https://github.com/nicolasmarcal).

I would also like to thank the instructors and everyone in the discord community
that lent a hand when I needed one.

## 📝 License

This software comes with the hyper-permissive [MIT LICENSE](LICENSE.md).

---

Made with ♥ by [🕎 Luis Geniole](https://github.com/Librity) :wave:
