# W01 Assignment Notes – CSE 325

## 1. Pizza Seed Data Evidence

The PizzaService seed data contains the following pizzas:

| ID  | Pizza Name      | Gluten Free |
| --- | --------------- | ----------- |
| 1   | Classic Italian | No          |
| 2   | Veggie          | Yes         |
| 3   | Pepperoni       | No          |
| 4   | Hawaiian        | No          |

The additional pizza I added to the original seed data is **Hawaiian**.

GET `/api/Pizzas` returned all four pizzas successfully with status code **200 OK**.

## 2. API Request and Response Evidence

### GET – Retrieve all pizzas

**Request:**
`GET http://localhost:5192/api/Pizzas`

**Response status:** 200 OK

**Response body:**

```json
[
  { "id": 1, "name": "Classic Italian", "isGlutenFree": false },
  { "id": 2, "name": "Veggie", "isGlutenFree": true },
  { "id": 3, "name": "Pepperoni", "isGlutenFree": false },
  { "id": 4, "name": "Hawaiian", "isGlutenFree": false }
]
```

### POST – Add a pizza

**Request:**
`POST http://localhost:5192/api/Pizzas`

**Request body:**

```json
{
  "id": 0,
  "name": "Hawaiian",
  "isGlutenFree": false
}
```

**Response status:** 201 Created

**Response body:**

```json
{
  "id": 4,
  "name": "Hawaiian",
  "isGlutenFree": false
}
```

### PUT – Update a pizza

**Request:**
`PUT http://localhost:5192/api/Pizzas/4`

**Request body:**

```json
{
  "id": 4,
  "name": "Hawaiian Supreme",
  "isGlutenFree": true
}
```

**Response status:** 204 No Content

### DELETE – Delete a pizza

**Request:**
`DELETE http://localhost:5192/api/Pizzas/4`

**Response status:** 204 No Content

## 3. Sales Summary Function

The following function reads the sales JSON files, calculates the total sales amount, and returns the grand total.

```csharp
double CalculateSalesTotal(IEnumerable<string> salesFiles)
{
    double salesTotal = 0;

    foreach (var file in salesFiles)
    {
        string salesJson = File.ReadAllText(file);

        SalesData? data = JsonConvert.DeserializeObject<SalesData?>(salesJson);

        salesTotal += data?.Total ?? 0;
    }

    return salesTotal;
}

record SalesData(double Total);
```
