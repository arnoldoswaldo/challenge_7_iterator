# challenge_7_iterator
Ejercicio poo para incluir iteradores a ejercicio realizado anteriormente en el reto 3  de cuenta

```
class MenuItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def total(self, quantity):
        return self.price * quantity


class Beverage(MenuItem):
    def __init__(self, name, price, size):
        super().__init__(name, price)
        self.size = size


class Appetizer(MenuItem):
    pass


class MainCourse(MenuItem):
    pass

# OrderIterator class permite iterar sobre los items de la orden 
class OrderIterator:
    def __init__(self, items):
        self._items = items
        self._index = 0
    # __iter__ y __next__ son los metodos  que permiten iterar sobre un objeto
    def __iter__(self):
        return self

    def __next__(self):
        if self._index < len(self._items):
            item = self._items[self._index]
            self._index += 1
            return item
        else:
           # StopIteration es una excepcion que se lanza cuando se intenta acceder a un elemento que no existe
            raise StopIteration


class Order:
    def __init__(self):
        self.items = []

    def add_item(self, item, quantity):
        if quantity <= 0:
            raise ValueError("Cantidad debe ser un valor posito.")
        self.items.append((item, quantity))

    def bill(self):
        return sum(item.total(quantity) for item, quantity in self.items)

    def print_order(self):
        print("Order:")
        for item, quantity in self.items:
            print(f"{item.name} x {quantity}")

    def __iter__(self):
        return OrderIterator(self.items)


# Menu and Example Usage
menu = {
    "Vino": Beverage("Vino", 65000, "botella"),
    "Agua": Beverage("Agua", 3000, "botella"),
    "Cerveza": Beverage("Cerveza", 10000, "botella"),
    "Papas": Appetizer("Papas", 13000),
    "Alitas": Appetizer("Alitas", 25000),
    "Pan": Appetizer("Pan", 2000),
    "Churazco": MainCourse("Churazco", 45000),
    "Reve eye": MainCourse("Reve eye", 65000),
    "Salmon": MainCourse("Salmon", 55000),
    "Pasta Carbonara": MainCourse("Pasta Carbonara", 35000),
    "Pasta Bolognesa": MainCourse("Pasta Bolognesa", 35000),
}

order = Order()
order.add_item(menu["Vino"], 2)
order.add_item(menu["Pan"], 3)
order.add_item(menu["Salmon"], 1)

# Iterating through order items
for item, quantity in order:
    print(f"{item.name} (x{quantity}) - Total: {item.total(quantity)}")
print("Total a pagar:", order.bill())
```
