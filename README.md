# Server-Sent Events (SSE)

> If you doesn't need a complex real time feature
> SSE is a technology base on HTTP ( limited to UTF-8)

## swamp-events

```Shell
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

```Shell
npx create-react-app swamp-stats && cd ./swamp-stats
```

__App.js__
```JSX
import React, { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [ nests, setNests ] = useState([]);
  const [ listening, setListening ] = useState(false);

  useEffect( () => {
    if (!listening) {
      const events = new EventSource('http://localhost:4000/events');
      events.onmessage = (event) => {
        const parsedData = JSON.parse(event.data);

        setNests((nests) => nests.concat(parsedData));
      };

      setListening(true);
    }
  }, [listening, nests]);
  
  return (
    <table className="stats-table">
      <thead>
        <tr>
          <th>Momma</th>
          <th>Eggs</th>
          <th>Temperature</th>
        </tr>
      </thead>
      <tbody>
        {
          nests.map((nest, i) =>
            <tr key={i}>
              <td>{nest.momma}</td>
              <td>{nest.eggs}</td>
              <td>{nest.temperature} ℃</td>
            </tr>
          )
        }
      </tbody>
    </table>
  );
}

export default App;
```

__App.css__
```CSS
body {
  color: #555;
  margin: 0 auto;
  max-width: 50em;
  font-size: 25px;
  line-height: 1.5;
  padding: 4em 1em;
}

.stats-table {
  width: 100%;
  text-align: center;
  border-collapse: collapse;
}

tbody tr:hover {
  background-color: #f5f5f5;
}
```

```Shell
npm install && npm run start
```