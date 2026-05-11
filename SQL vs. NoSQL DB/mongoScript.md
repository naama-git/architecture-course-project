``` bash
// Database: ChineseAuctionDB

// 1. Users Collection
db.users.insertMany([
  {
    "firstName": "Devora",
    "lastName": "Vexler",
    "email": "dv@gmail.com",
    "password": "$2a$11$NY0FJirHAAW86u0mqwHGeeuucl9qVuJAcDI5coctbwppYCGpdw/La",
    "phoneNumber": "0548467564",
    "role": "user"
  },
  {
    "firstName": "Naama",
    "lastName": "Stern",
    "email": "naanas344@gmail.com",
    "password": "$2a$11$yMc6dKqn//RHzRrJks.wSeOp0HaaQZXBXO86W13BmaBeXu9jf4G3u",
    "phoneNumber": "0556748344",
    "role": "admin"
  },
  {
    "firstName": "Michal",
    "lastName": "Stern",
    "email": "ms@gmail.com",
    "password": "$2a$11$smFhGh1l9Zk8IxpinUJyK.jJGWJb6e.FCEQO1l7DaM18JYNRyVD/G",
    "phoneNumber": "055677249",
    "role": "user"
  }
]);

// 2. Categories Collection
db.categories.insertMany([
  { "categoryName": "Electronic" },
  { "categoryName": "Kitchen" },
  { "categoryName": "Home Styling" },
  { "categoryName": "The Big Money" }
]);

// 3. Donors Collection
db.donors.insertMany([
  {
    "name": "Master Chef Kitchens",
    "company": "MasterChef",
    "email": "contact@masterchef.com",
    "phoneNumber": "555-01012",
    "address": "122 Industrial Way, NY",
    "prizes": []
  },
  {
    "name": "Jonathan Silverwood",
    "company": "Silverwood Music Group",
    "email": "j.silverwood@silverwoodmusic.com",
    "phoneNumber": "0548745632",
    "address": "42 Symphony Lane, Nashville, TN",
    "prizes": []
  }
]);

// 4. Prizes Collection
// Note: In MongoDB we embed donor and category details as per your request
db.prizes.insertMany([
  {
    "name": "Elegant Upright Piano",
    "description": "A high-quality upright piano featuring rich sound and a classic finish.",
    "imageUrl": "images/piano.webp",
    "quantity": 1,
    "donator": {
      "name": "Jonathan Silverwood",
      "company": "Silverwood Music Group"
    },
    "category": {
      "categoryName": "music"
    }
  },
  {
    "name": "Professional Cookware Set",
    "description": "A premium 10-piece stainless steel cookware collection.",
    "imageUrl": "images/cookware.webp",
    "quantity": 1,
    "donator": {
      "name": "Master Chef Kitchens",
      "company": "MasterChef"
    },
    "category": {
      "categoryName": "Kitchen"
    }
  }
]);

// 5. Packages Collection
db.packages.insertMany([
  { "packageName": "Silver", "numberOfTickets": 50, "price": 300 },
  { "packageName": "Classic", "numberOfTickets": 5, "price": 40 },
  { "packageName": "One", "numberOfTickets": 1, "price": 10 }
]);

// 6. Orders Collection
db.orders.insertOne({
  "user": {
    "firstName": "Racheli",
    "lastName": "Stern",
    "email": "rs@gmail.com",
    "phoneNumber": "025378456"
  },
  "prize": [
    { "name": "Elegant Upright Piano", "description": "...", "imageUrl": "..." }
  ],
  "packages": [
    { "packageName": "Silver", "quantity": 1 }
  ],
  "date": new Date("2026-02-15T19:57:28Z"),
  "totalPrice": 680
});

// 7. Winners Collection
db.winners.insertOne({
  "user": {
    "firstName": "Hello",
    "lastName": "World",
    "email": "hw@gmail.com",
    "phoneNumber": "0556748344"
  },
  "prize": {
    "name": "Luxury Family Retreat",
    "description": "Enjoy a relaxing weekend stay",
    "imageUrl": "images/retreat.webp"
  }
});

// 8. Carts Collection
db.carts.insertOne({
  "userId": "User_Object_Id_Here",
  "cartItems": [
    {
      "prize": {
        "name": "Professional Digital Camera",
        "description": "Advanced DSLR camera",
        "imageUrl": "images/camera.webp"
      },
      "qty": 2
    }
  ]
});
```