# Axios and Express

## Body vs Params vs Query

Send POST request with body:

```js
// axios
axios.post("url", { data: "the actual JSON data" });

// express
app.post("url", (req, res)=>{
  const data = req.body;
  res.status(201).json({data});
})
```

Send params in the URL and pass in actual payload as body:

```js
// axios
axios.post("url/123", { data: "the actual JSON data" });

// express
app.post("url/:id", (req, res)=>{
  const userId = req.params.id;
  const data = req.body;
  res.status(201).json({
    userId,
    data
  });
})
```

Send query string in URL:

```js
axios.get("url", { params: { userId: "123", userName: "admin" } });

app.get("url", (req, res)=>{
  const userId = req.query.userId;
  const userName = req.query["userName"];
  res.json({userId, userName})
})
```
