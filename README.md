# Reto 4
## The Restaurant Revisted
* Add setters and getters to all subclasses for menu item.
* Override calculate_total_price() according to the order composition (e.g if the order includes a main course apply some disccount on beverages).
* Add the class Payment() following the class example.
```python
class MenuItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def get_name(self):
        return self.name
    
    def set_name(self, name):
        self.name = name

    def get_price(self):
        return self.price
    
    def set_price(self, price):
        self.price = price

    def calculate_total_price(self):
        return self.price
    
class Berevarage(MenuItem):
    def __init__(self, name, price, alcohol_content:bool):
        super().__init__(name, price)
        self.alcohol_content = alcohol_content

    def get_alcohol_content(self):
        return self.alcohol_content
    
    def set_alcohol_content(self, alcohol_content):
        self.alcohol_content = alcohol_content
    
    def calculate_total_price(self):
        return self.price
    
class Appetizer(MenuItem):
    def __init__(self, name, price, pieces):
        super().__init__(name, price)
        self.pieces = pieces
    
    def calculate_total_price(self):
        return self.price
    
    def get_pieces(self):
        return self.pieces
    
    def set_pieces(self, pieces):
        self.pieces = pieces
    
class MainCourse(MenuItem):
    def __init__(self, name, price):
        super().__init__(name, price)
    
    def calculate_total_price(self):
        return self.price
    
class Salad(MenuItem):
    def __init__(self, name, price, size):
        super().__init__(name, price)
        self.size = size

    def calculate_total_price(self):
        return self.price
    
    def get_size(self):
        return self.size
    
    def set_size(self, size):
        self.size = size
    
class Dessert(MenuItem):
    def __init__(self, name, price):
        super().__init__(name, price)
    
    def calculate_total_price(self):
        return self.price
    
class Sauces(MenuItem):
    def __init__(self, name, price, type):
        super().__init__(name, price)
        self.type = type

    def calculate_total_price(self):
        return self.price
    
    def get_type(self):
        return self.type

    def set_type(self, type):
        self.type = type

class Payment:
    def __init__(self):
        pass

    def pay(self, amount):
        raise NotImplementedError("Subclasses must implement pay()")

class CardPayment(Payment):
    def __init__(self, number, cvv):
        super().__init__()
        self.number = number
        self.cvv = cvv

    def pay(self, amount):
        print(f"Paying {amount} with card ending in {self.number[-4:]}")

class CashPayment(Payment):
    def __init__(self, amount_given):
        super().__init__()
        self.amount_given = amount_given

    def pay(self, amount):
        if self.amount_given >= amount:
            print(f"Payment successful in cash. Change: {self.amount_given - amount}")
        else:
            print(f"Insufficient funds. Missing {amount - self.amount_given} to complete the payment.")

class Order:
    def __init__(self):
        self.items = []
    
    def add_item(self, item):
        self.items.append(item)
    
    def calculate_total_price(self):
        total = 0
        has_main_course = False
        for item in self.items:
            if isinstance(item, Berevarage):
                total -= item.calculate_total_price()*0.1
        return total
    
menu_items = [
    Berevarage("Soda", 5000, False),
    Berevarage("Beer", 7000, True),
    Berevarage("Water", 3000, False),
    Appetizer("Empanadas", 3000, 3),
    Appetizer("Nachos", 4000, 5),
    Appetizer("Shrimp Rolls", 5000, 6),
    MainCourse("Meat", 25000),
    MainCourse("Fish", 23000),
    MainCourse("Chicken", 20000),
    Salad("Florentina", 6000, "Small"),
    Salad("Florentina", 9000, "Medium"),
    Salad("Florentina", 12000, "Large"),
    Salad("Mediterrenean", 9000, "Small"),
    Salad("Mediterrenean", 7000, "Medium"),
    Salad("Mediterrenean", 10000, "Large"),
    Salad("Mediterrenean", 13000, "Medium"),
    Salad("Mexican", 9000, "Large"),
    Salad("Mexican", 12000, "Large"),
    Salad("Mexican", 15000, "Large"),
    Dessert("Ice Cream", 5000),
    Dessert("Brownie", 6000),
    Dessert("Banan Split", 7000),
    Sauces("Ketchup", 1000, "8g"),
    Sauces("Mayo", 1000,"10g"),
    Sauces("Mustard", 1000,"9g")
]

order = Order()
order.add_item(menu_items[1])
order.add_item(menu_items[3])
order.add_item(menu_items[7])
order.add_item(menu_items[9])
order.add_item(menu_items[11])

for item in menu_items:
    order.add_item(item)

print(order.calculate_total_price())
```
