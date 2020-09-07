# Rest API
## URI convention

- `GET  /orders          <---> orders`
- `POST /orders          <---> orders.push(data)`
- `GET  /orders/1        <---> orders[1]`
- `PUT  /orders/1        <---> orders[1] = data`
- `GET  /orders/1/lines  <---> orders[1].lines`
- `POST /orders/1/lines  <---> orders[1].lines.push(data)`