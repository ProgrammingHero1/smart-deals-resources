## Server Deployment steps

1. comment await commands outside api methods for solving gateway timeout error

```js
//comment following commands
await client.connect();
await client.db("admin").command({ ping: 1 });
```

2. create vercel.json file for configuring server

```json
{
  "version": 2,
  "builds": [
    {
      "src": "index.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "index.js",
      "methods": ["GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"]
    }
  ]
}
```

3. (for jwt using: httponly cookies) Add Your production domains to your cors configuration

```js
//Must remove "/" from your production URL
app.use(
  cors({
    origin: [
      "http://localhost:5173",
      "https://career-portal-ph.web.app",
      "https://career-portal-ph.firebaseapp.com",
    ],
    credentials: true,
  })
);
```

4. (for jwt using: httponly cookies) Let's create a cookie options for both production and local server for vercel

```js
const cookieOptions = {
  httpOnly: true,
  secure: process.env.NODE_ENV === "production",
  sameSite: process.env.NODE_ENV === "production" ? "none" : "strict",
};
//localhost:5000 and localhost:5173 are treated as same site.  so sameSite value must be strict in development server.  in production sameSite will be none
// in development server secure will false .  in production secure will be true
```

5. (for jwt using: httponly cookies) now we can use this object for cookie option to modify cookies

```js
//creating Token
app.post("/jwt", logger, async (req, res) => {
  const user = req.body;
  console.log("user for token", user);
  const token = jwt.sign(user, process.env.ACCESS_TOKEN_SECRET);

  res.cookie("token", token, cookieOptions).send({ success: true });
});

//clearing Token
app.post("/logout", async (req, res) => {
  const user = req.body;
  console.log("logging out", user);
  res
    .clearCookie("token", { ...cookieOptions, maxAge: 0 })
    .send({ success: true });
});
```

6. Deploy to Vercel

```bash
npm i -g vercel
vercel login
vercel
vercel --prod
- After completed the deployment . click on inspect link and copy the production domain
- setup your environment variables in vercel
- check your public API
```

<img src="https://i.ibb.co.com/dgH40d3/Screenshot-3.jpg"/>

7.Add Environment variable: Your project in Vercel > Settings > Environment Variables > add or upload .env file
8. Whitelisting the ip address or allow from anywhere ( Security > Database & Network Access > IP Access List > Add IP Address
9. Common issues: 
- not adding vercel.json
- not adding environment variable
- not whitelisting the ip address or allow all ( Security > Database & Network Access > IP Access List > Add IP Address
# Server Deployment on Vercel  Done
