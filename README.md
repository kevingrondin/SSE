# Server-Sent Events (SSE)

> If you doesn't need a complex real time feature
> SSE is a technology base on HTTP ( limited to UTF-8)

## swamp-events

```JS
npm install && npm run start
```

Listen on CLI

```Shell
curl -H Accept:text/event-stream http://localhost:4000/events
```

Post with CLI

```Shell
curl -X POST \
 -H "Content-Type: application/json" \
 -d '{"momma": "swamp_princess", "eggs": 40, "temperature": 31}'\
 -s http://localhost:4000/nest
```

## swamp-stats

```JS
npm install && npm run start
```