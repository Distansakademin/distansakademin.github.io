# Python generate data

## Random customer data

```python
import csv
import random

NUMBER_OF_ROWS = 1000

first_names = ["Linus", "Bill", "Steve", "Mark", "Elon",
               "Jeff", "Larry", "Sergey", "Sundar", "Satya"]
last_names = ["Torvalds", "Gates", "Jobs", "Zuckerberg", "Musk",
              "Bezos", "Page", "Brin", "Pichai", "Nadella"]


def random_email(first_name, last_name):
    email = first_name.lower() + "." + last_name.lower() + "@example.com"

    email = "invalid_email" if random.randint(0, 5) == 0 else email

    return email


def random_age():
    age = random.randint(0, 100)

    if random.randint(0, 5) == 0:
        age = None

    return age


def random_person(customer_id):
    first_name = random.choice(first_names)
    last_name = random.choice(last_names)
    name = first_name + " " + last_name
    email = random_email(first_name, last_name)
    age = random_age()
    purchase_frequency = random.choice(["high", "medium", "low"])
    phone = f"07{random.randint(10,99)}-{random.randint(100000,999999)}"

    return {
        "customer_id": customer_id,
        "name": name,
        "email": email,
        "age": age,
        "purchase_frequency": purchase_frequency,
        "phone": phone
    }


with open("customer_data.csv", "w", newline="") as csvfile:
    fieldnames = ["customer_id", "name", "email", "age", "purchase_frequency", "phone"]

    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

    writer.writeheader()

    customer_id = 0
    for i in range(NUMBER_OF_ROWS):
        customer_id += 1
        row = random_person(customer_id)
        writer.writerow(row)
```

## Random product data

```python
import csv
import random

NUMBER_OF_ROWS = 1000

product_property = ["Blue", "Large", "Slim", "Magnificent", "Fantastic",
                    "Awesome", "Incredible", "Amazing", "Stunning", "Beautiful", "Slimy"]
product_name = ["Shirt", "Pants", "Shoes", "Hat", "Gloves",
                "Socks", "Jacket", "Coat", "Scarf", "Tie"]


def random_price():
    price = random.randint(10, 99)
    price = f"{price}9"

    if random.randint(0, 10) == 0:
        price = None

    return price


def random_product_name():
    name = random.choice(product_property) + " " + \
        random.choice(product_property) + " " + random.choice(product_name)
    return name


def random_size():
    size = random.choice(["XS", "S", "M", "L", "XL"])
    return size


def random_color():
    color = random.choice(["Red", "Blue", "Green", "Yellow", "Black", "White"])
    return color


product_id = 0

with open("product_data.csv", "w", newline="") as csvfile:
    fieldnames = ["product_id", "product_name", "price", "size", "color"]

    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

    writer.writeheader()

    for i in range(NUMBER_OF_ROWS):
        product_id += 1

        row = {
            "product_id": product_id,
            "product_name": random_product_name(),
            "price": random_price(),
            "size": random_size(),
            "color": random_color()
        }

        writer.writerow(row)
```
